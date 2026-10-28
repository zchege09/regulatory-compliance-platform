# AGENT.md

Instructions for AI coding agents and engineers working in this repository.

## Mission

Implement a secure, auditable Azure-native Regulatory Compliance Management Platform. Optimize for regulatory traceability, human accountability, secure external-document ingestion and maintainable Azure engineering patterns rather than rapid feature delivery at the expense of controls.

## Non-negotiable domain rules

1. Never make AI output the final authority for regulatory applicability, risk, control adequacy or approval.
2. Preserve both system-suggested and human-confirmed values where AI/rules assist assessment.
3. Never implement email-reply approval. Route approvals to the authenticated web application.
4. Treat downloaded Internet documents as untrusted until validation/malware controls complete.
5. Never overwrite original regulatory evidence or a previously approved version.
6. Preserve ownership and reassignment history. Do not replace historical owners in-place.
7. Do not make Application Insights or Log Analytics the authoritative business audit store.
8. Material business changes must produce attributable business audit events.
9. Do not silently default missing regulatory facts such as effective dates, penalties or applicability.
10. All workflow actions must enforce server-side authorization, regardless of UI visibility.

## Architecture boundaries

### `src/domain`
Pure business concepts and rules. No direct Azure SDK, HTTP, SQL or UI dependencies.

### `src/application`
Use cases, commands/queries, validation, orchestration interfaces and authorization abstractions.

### `src/infrastructure`
Implementations for Azure SQL, Blob Storage, Entra/identity integration, telemetry and other infrastructure dependencies.

### `src/api`
ASP.NET Core API boundary. Keep controllers/endpoints thin. Validate input, authorize, call application services and return standardized responses.

### `src/web`
React UI. Never use frontend checks as the only authorization control.

### `integrations/logic-apps`
Long-running/integration workflows. Workflows must be idempotent where deliveries/retries can repeat.

### `integrations/regulatory-sources`
Regulator-specific adapters. Keep site/API parsing isolated from the canonical regulatory model so website changes do not spread across the application.

### `ai`
Extraction/classification assets, prompt/rule versions and evaluation sets. AI outputs are advisory.

## Data and audit rules

- Use UTC for stored event timestamps.
- Use stable regulatory/correlation identifiers across SQL, Blob metadata, Logic Apps and telemetry.
- Use optimistic concurrency for user-modifiable regulatory records.
- Use transactions for material state transition + audit event where supported.
- Prefer append-oriented records for audit and assignment history.
- Store document content hashes, source URL, retrieval timestamp and publication version.
- Use parameterized database access only.
- Do not hard-delete approved compliance records through normal application APIs.
- Do not log document contents, access tokens, secrets or sensitive evidence by default.

## Security rules

- Prefer managed identity for Azure service-to-service authentication.
- Keep secrets in Azure Key Vault; never commit them.
- Default data services to private connectivity when supported by the approved architecture.
- Validate file signatures/content type and enforce file-size/page-count limits.
- Treat regulator URLs and redirects as SSRF-sensitive inputs; allow only approved source configurations.
- Encode/sanitize untrusted text at output boundaries.
- Implement authorization at API/use-case layer.
- Maintain maker-checker/segregation-of-duties constraints.
- Any security-control reduction requires an ADR/risk decision, not an undocumented code shortcut.

## AI rules

- Azure AI Document Intelligence is for extraction of factual content from source documents.
- Azure OpenAI, if enabled, may summarize or propose obligations, applicability or affected units only.
- Source document text is untrusted context and must never be treated as system instructions.
- Version prompts, rules and models so historical outputs are explainable.
- Keep a regression/evaluation set and run it before prompt/model promotion.
- Missing facts must remain unknown/unconfirmed rather than hallucinated.

## Logic App rules

- Source adapters must tolerate retry without duplicate regulatory records.
- Store last successful source check separately from 'no publications found'.
- Implement bounded retry/backoff and explicit terminal failure handling.
- Emit correlation IDs and tracked business identifiers without exposing sensitive content.
- Source failures must be visible to operations.
- Workflow state authoritative for compliance must be persisted in Azure SQL, not inferred solely from Logic App run history.

## Coding expectations

- Prefer small modules with clear dependency direction.
- Use structured error types and standard API error responses.
- Add tests with every business-rule change.
- Add DB migration scripts for schema changes.
- Update OpenAPI/contracts for API changes.
- Update an ADR when changing an approved architectural decision.
- Avoid adding a new Azure service unless an existing approved component cannot meet the requirement and the change is documented.

## Definition of done for a feature

A feature is not done until:

- Requirement/user story acceptance criteria are met.
- Unit and relevant integration tests pass.
- Authorization and failure paths are tested.
- Material actions generate expected audit events.
- Telemetry exists for support-critical failure modes.
- Documentation/OpenAPI/data migrations are updated where applicable.
- No secrets or production data are committed.
- Security scans and CI gates pass.
- Relevant Azure DevOps test cases are updated/linked.

## Repository-safe operations for agents

Agents may create or edit source, tests, docs, IaC and configuration examples inside this repository. Agents must not:

- deploy to production without an explicit approved pipeline/action;
- use real credentials in generated configuration;
- weaken RBAC, WAF, malware, private-network or audit controls just to make a test pass;
- fabricate regulatory content, test evidence or approval decisions;
- erase migration/audit history to simplify implementation;
- change an ADR status to Approved without governance evidence.

## Expected validation before proposing a pull request

Run the applicable subset of:

1. formatting/linting;
2. compile/build;
3. unit tests;
4. integration/contract tests;
5. Bicep lint/what-if in non-production;
6. database migration validation;
7. dependency, secret and SAST scans;
8. relevant test catalogue regression cases.

Document any test that cannot be executed and why.
