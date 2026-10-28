# ADR-013: Azure Environment and App Service Deployment Strategy

- **Status:** Proposed
- **Date:** 2026-10-28
- **Decision owner:** Solution Architecture
- **Scope:** Regulatory Compliance Management Platform

## Context

The platform requires DEV, TEST, UAT and PROD environments for development, system/integration testing, business acceptance and production operation. Azure App Service also provides deployment slots, but deployment slots are release-management constructs within an App Service and do not provide complete isolation for the wider platform dependencies such as Azure SQL Database, Blob Storage, Logic Apps Standard, Key Vault, Document Intelligence, identities, networking and telemetry.

The platform handles regulatory evidence, controlled approvals, CRU/CRMP records and auditable compliance decisions. Environment isolation and predictable release promotion are therefore more important than minimizing the number of Azure resources.

## Decision

DEV, TEST, UAT and PROD shall be implemented as **logically isolated Azure environments**, not as App Service deployment slots.

Each environment shall have an environment-specific application deployment and isolated stateful/configuration dependencies appropriate to that environment.

Production Azure App Service shall additionally use a **staging deployment slot** for production release validation, warm-up, smoke testing, controlled swap and rapid rollback.

The React presentation layer and ASP.NET Core API remain logically separated in the codebase but are initially packaged and deployed together to the environment's Azure App Service.

## Environment model

```text
DEV
└── app-regcom-dev
    ├── React UI
    └── ASP.NET Core API

TEST
└── app-regcom-test
    ├── React UI
    └── ASP.NET Core API

UAT
└── app-regcom-uat
    ├── React UI
    └── ASP.NET Core API

PROD
└── app-regcom-prod
    ├── production slot
    │   ├── React UI
    │   └── ASP.NET Core API
    └── staging slot
        ├── React UI
        └── ASP.NET Core API
```

## Environment isolation

Each environment shall use isolated instances/configurations of the following where applicable:

- Azure App Service
- Azure SQL Database
- Azure Blob Storage
- Azure Logic Apps Standard
- Azure Key Vault
- Application Insights
- environment-specific configuration and identities
- regulatory-source monitoring configuration
- network controls/private endpoints as required by the approved landing-zone architecture

Azure AI Document Intelligence may be dedicated per environment or shared only where enterprise architecture, data classification, access isolation and cost controls explicitly permit it. Production processing must not expose production documents to non-production identities or applications.

## Resource organization

The target convention is:

```text
rg-regcom-dev
├── app-regcom-dev
├── sql-regcom-dev
├── st-regcom-dev
├── logic-regcom-dev
├── kv-regcom-dev
└── monitoring resources

rg-regcom-test
├── app-regcom-test
├── sql-regcom-test
├── st-regcom-test
├── logic-regcom-test
├── kv-regcom-test
└── monitoring resources

rg-regcom-uat
├── app-regcom-uat
├── sql-regcom-uat
├── st-regcom-uat
├── logic-regcom-uat
├── kv-regcom-uat
└── monitoring resources

rg-regcom-prod
├── app-regcom-prod
│   ├── production slot
│   └── staging slot
├── sql-regcom-prod
├── st-regcom-prod
├── logic-regcom-prod
├── kv-regcom-prod
└── monitoring resources
```

Actual names, subscriptions, regions and network placement remain subject to the enterprise Azure landing-zone naming and subscription standards.

## Release promotion model

The same immutable/versioned application artifact shall be promoted through environments rather than rebuilt differently for each environment.

```text
Source / Pull Request
        ↓
Build + Unit Tests + Security Scans
        ↓
DEV
        ↓
TEST
        ↓
Functional / Integration / Regression Tests
        ↓
UAT
        ↓
Business UAT Approval
        ↓
PROD Staging Slot
        ↓
Health + Smoke + Configuration/DB Compatibility Checks
        ↓
Production Approval Gate
        ↓
Slot Swap
        ↓
PROD Production Slot
```

Environment-specific settings are supplied at deployment/runtime and must not require rebuilding the application artifact.

## Production slot strategy

The production App Service shall have:

1. **Production slot** – serves live users.
2. **Staging slot** – receives the production candidate before release.

The staging slot shall be used to:

- deploy the release candidate;
- start/warm the application;
- validate application health endpoints;
- execute targeted smoke tests;
- validate Entra authentication;
- validate API startup and critical dependencies;
- validate database schema/application compatibility;
- confirm approved configuration;
- obtain production deployment approval;
- swap the validated candidate into production.

The previous production version remains available in the post-swap slot, supporting fast application rollback through a reverse swap when technically safe.

## Database deployment and rollback

App Service slot swap does **not** roll back Azure SQL schema changes. Database migrations must therefore follow backward-compatible deployment practices.

Preferred release sequence:

1. Deploy backward-compatible database migration.
2. Verify migration.
3. Deploy application candidate to production staging slot.
4. Run health/smoke/compatibility tests.
5. Swap staging to production.
6. Perform destructive schema cleanup only in a later release after the former application version no longer depends on the old schema.

A slot swap must not be considered a complete rollback plan when the release contains irreversible data/schema changes.

## Slot-specific configuration

Settings that must stay with a specific slot shall be marked as deployment-slot settings.

Examples include:

- `APP_ENVIRONMENT`
- Application Insights connection/configuration where slot-specific telemetry is required
- Key Vault/configuration references where the value must remain bound to the slot
- health/smoke-test configuration
- `REGULATORY_MONITORING_ENABLED`

The staging slot must not independently execute production regulatory-source monitoring or duplicate workflow schedulers.

Regulatory source monitoring remains primarily owned by Logic Apps Standard and is deployed/configured independently from the Web App production slot swap.

## Regulatory monitoring by environment

Recommended control:

```text
DEV   → disabled by default; use fixtures/synthetic sources
TEST  → disabled for live sources; use test fixtures/mock endpoints
UAT   → explicitly controlled; selected live-source read-only checks only when approved
PROD  → enabled for approved regulatory sources
PROD staging slot → disabled
```

This prevents duplicate ingestion, accidental regulatory records and duplicate notifications from non-production or staging instances.

## Configuration and secrets

- Non-secret environment configuration shall be parameterized through IaC/runtime application settings.
- Secrets shall not be committed to `.env`, Bicep parameter files or source control.
- Azure Key Vault and managed identities are the preferred secret/authentication pattern.
- Browser-visible React environment values must contain no secret material.
- Production and non-production identities must be separated according to the enterprise IAM model.

## Infrastructure as Code

Repository structure remains:

```text
infrastructure/bicep/environments/
├── dev/
├── test/
├── uat/
└── prod/
```

The PROD deployment definition shall additionally create/configure the App Service `staging` slot and its slot-specific settings.

Shared reusable resources belong under:

```text
infrastructure/bicep/modules/
```

Manual production drift is not the intended operating model. Environment and slot configuration should be reproducible from approved IaC and pipelines.

## Azure DevOps pipeline gates

The production pipeline shall, at minimum, enforce:

### Before TEST promotion
- successful build;
- unit tests;
- lint/static analysis;
- dependency and secret scanning.

### Before UAT promotion
- integration/contract tests;
- security checks;
- database migration validation;
- relevant automated regression suite.

### Before PROD staging
- UAT approval;
- release artifact/version identified;
- change/release approval as required by enterprise process;
- production configuration/IaC validation.

### Before production swap
- staging health check successful;
- critical smoke tests successful;
- authentication verified;
- production database compatibility verified;
- no unresolved release-blocking security/test defects;
- production approval completed.

### After swap
- production health check;
- critical synthetic/smoke test;
- telemetry validation;
- rollback decision window monitored.

## Availability and scaling

The deployed application shall be stateless at the App Service compute layer. Durable business state belongs in Azure SQL/Blob Storage and approved platform services.

Production capacity may scale horizontally to multiple App Service worker instances without changing the frontend/backend logical architecture.

DEV and TEST may use lower-cost sizing. UAT should be representative enough to validate production behaviour where required. Final production SKU, instance count, zone-redundancy requirements and autoscale thresholds are determined by the approved NFR/capacity exercise.

## Subscription boundary

Where the enterprise Azure landing-zone standard permits/requires it, PROD should reside in a separate subscription/security boundary from non-production environments. At minimum, production and non-production must have explicit IAM, networking, secrets and data separation.

## Alternatives considered

### Alternative A: DEV, TEST and UAT implemented as PROD App Service deployment slots

**Rejected.** This simplifies App Service allocation but does not provide equivalent isolation across SQL, Blob, Logic Apps, Key Vault, identities and monitoring. It also increases the risk that non-production activity interacts with production data/workflows.

### Alternative B: Separate frontend and backend App Services in every environment

**Deferred.** The React and ASP.NET Core components remain logically isolated in the repository and API boundary, but a single App Service deployment reduces initial operational complexity. Separate deployment remains possible if independent scaling, reusable API consumers, ownership boundaries or security-zone requirements justify it.

### Alternative C: No production staging slot; direct deployment to production

**Rejected.** It removes the production-like warm-up, smoke-test and rapid application rollback capabilities provided by the slot deployment pattern.

## Consequences

### Positive

- Stronger environment and data isolation.
- Reduced risk of DEV/TEST/UAT creating production compliance records.
- Independent environment lifecycle and configuration.
- Production candidate is validated before receiving live traffic.
- Slot swap supports low-disruption deployment and fast application rollback.
- Same artifact can be promoted through environments.
- Infrastructure remains reproducible through IaC.

### Negative / cost

- More Azure resources than a slot-only environment model.
- Higher non-production platform cost.
- More networking/private-endpoint/DNS configuration.
- Production slot strategy requires compatible database migration discipline.
- Configuration must be carefully classified between environment-specific and slot-specific values.

## Risks and controls

| Risk | Control |
|---|---|
| Staging processes production regulatory sources | Disable regulatory monitoring in staging; keep scheduled source ingestion in Logic Apps |
| Slot swap introduces incompatible application/database combination | Expand-contract/backward-compatible database migrations and compatibility gates |
| Environment configuration drift | Bicep/IaC and pipeline-controlled deployment |
| Non-production accesses production data | Separate identities, Key Vaults, databases/storage and network controls |
| Different binaries reach environments | Promote the same immutable/versioned application artifact |
| Swap succeeds but application is unhealthy | Pre-swap health/smoke checks plus post-swap monitoring and reverse-swap procedure |

## Validation / acceptance criteria

This ADR is implemented when:

- DEV, TEST, UAT and PROD are independently deployable through IaC.
- Each environment uses its intended SQL, storage, Key Vault and workflow configuration.
- PROD includes a staging App Service slot.
- Production staging cannot initiate duplicate regulatory monitoring.
- The pipeline promotes an identified application artifact without rebuilding environment-specific binaries.
- A controlled staging-to-production swap has been demonstrated.
- Reverse swap/application rollback has been tested.
- Database migration rollback/forward-recovery procedures are documented and tested.
- Production and non-production access boundaries pass security verification.

## Follow-up actions

- Update PROD Bicep to define the staging slot.
- Add slot-setting configuration to IaC.
- Add deployment/promotion stages and approvals to Azure Pipelines.
- Add production pre-swap and post-swap smoke tests.
- Add environment configuration templates without secrets.
- Update network/deployment diagrams to show isolated environments and the PROD staging slot.
- Add a release runbook covering slot swap and rollback.
- Confirm production/non-production subscription placement with the Azure landing-zone/platform team.
