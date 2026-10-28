# Regulatory Compliance Management Platform

Azure-native platform for proactive regulatory-source monitoring and controlled management of the Compliance Regulatory Universe (CRU) and Compliance Risk Management Plan (CRMP).

## Target architecture

- Azure App Service: React web application and ASP.NET Core API
- Azure Logic Apps Standard: source monitoring, workflow orchestration, notifications and SLA escalation
- Azure AI Document Intelligence: factual extraction from regulatory publications
- Azure OpenAI: optional advisory classification/summarization only
- Azure SQL Database: authoritative CRU/CRMP, workflow and business-audit system of record
- Azure Blob Storage: original publications, versions and evidence
- Microsoft Entra ID: authentication and RBAC
- Azure Key Vault: secrets/certificates
- Application Insights, Log Analytics and Azure Monitor: operational observability

## Repository layout

```text
regulatory-compliance-platform/
├── README.md
├── AGENT.md
├── docs/                 # Architecture, requirements, security, operations and testing docs
├── src/                  # Web, API, domain, application and infrastructure application code
├── integrations/         # Logic Apps and regulator-source adapters
├── ai/                   # Document Intelligence, prompts/rules and AI evaluation assets
├── database/             # SQL schema, migrations, seed and operational SQL scripts
├── infrastructure/       # Bicep modules, environment definitions and Azure policies
├── tests/                # Unit through UAT/security/performance tests
├── devops/               # Azure DevOps pipelines, Boards and Test Plans artefacts
└── scripts/              # Developer, build, migration and support scripts
```

## Core business flow

1. Monitor approved regulatory sources.
2. Detect new or amended publications using metadata and content hashes.
3. Validate/quarantine the downloaded document and retain the original evidence.
4. Extract factual fields using Azure AI Document Intelligence.
5. Generate optional rules/AI-assisted classification suggestions.
6. Require Compliance human validation.
7. Route CRU review and approval.
8. Create/manage CRMP controls, gaps and remediation actions.
9. Track ownership, SLA, reminders, reassignment and escalation.
10. Retain end-to-end business audit and display management dashboards.

## Key architecture principles

- AI recommendations never constitute regulatory approval.
- Email is notification only; decisions occur in the authenticated web application.
- Azure SQL is authoritative for business state and business audit.
- Azure Monitor/Log Analytics are technical telemetry, not the compliance approval ledger.
- Original regulatory publications are versioned and preserved with integrity metadata.
- Material business-state changes and their audit events should be committed transactionally wherever practical.
- Sources, workflow stages, SLA rules and templates must be configuration-driven.
- Managed identities and private connectivity are preferred over stored credentials/public data-service access.

## Development prerequisites

Expected engineering tooling:

- .NET SDK version approved by enterprise engineering standards
- Node.js LTS and npm/pnpm as selected by the frontend team
- Azure CLI
- Bicep CLI
- SQL tooling
- Azure Functions/Logic Apps tooling where required
- Git

Do not pin final production versions here until the enterprise technology standards and target Azure subscriptions are confirmed.

## Getting started

1. Read `AGENT.md` and `docs/architecture/`.
2. Review `docs/requirements/` and the Azure Boards backlog before coding.
3. Provision a developer environment from `infrastructure/bicep/environments/dev/`.
4. Apply database migrations from `database/migrations/`.
5. Configure local settings using non-secret examples only. Real secrets belong in Azure Key Vault or approved developer secret stores.
6. Run unit, integration and security checks before opening a pull request.

## Branch and pull-request expectations

- Use feature branches linked to an Azure Boards work item.
- Require peer review and successful CI before merge.
- Never commit credentials, production data, regulator credentials, certificates or access tokens.
- Database and API contract changes require migration/versioning artefacts in the same pull request.
- Architecture-impacting changes require an ADR update under `docs/architecture/adr/`.

## Testing

Test assets are organized under `tests/` and Azure Test Plans mapping artefacts under `devops/test-plans/`.

Release evidence should preserve traceability:

`Requirement → User Story → Test Case → Test Run → Evidence/Defect`

Critical production gates include business-audit verification, authorization testing, source-monitoring failure handling, backup/restore, DR, security testing and UAT.

## Environments

Recommended logical environments:

- `dev`
- `test`
- `uat`
- `prod`

Production and non-production should be isolated according to enterprise subscription/network/security standards. Live regulator polling should be deliberately enabled per environment to prevent accidental duplicate monitoring from test environments.

## Documentation

Start here:

- `docs/architecture/` – HLD, LLD, logical/network/security/data architecture and ADRs
- `docs/requirements/` – functional/NFR requirements and traceability
- `docs/security/` – threat model, RBAC and control evidence
- `docs/operations/` – support, monitoring, backup/DR and runbooks
- `docs/testing/` – test strategy and traceability
