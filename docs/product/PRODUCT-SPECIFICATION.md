# Regulatory Compliance Management Platform - Product Specification

## 1. Purpose
The Regulatory Compliance Management Platform provides a centralized Azure-native capability for proactive regulatory monitoring, Compliance Regulatory Universe (CRU) management, Compliance Risk Management Plan (CRMP) management, controlled approvals, remediation tracking, evidence retention, auditability and management reporting.

## 2. Business problem
The current compliance operating model relies on approximately 40 Excel workbooks and email exchanges. This creates fragmented records, manual re-keying, inconsistent methodology enforcement, unclear ownership following staff changes, weak version control, email-based follow-up and limited evidence of who reviewed, changed or approved individual regulatory items.

## 3. Product objectives
- Proactively monitor approved regulatory sources rather than depend on manual website checking.
- Detect new and amended regulatory publications.
- Preserve original source documents and versions as regulatory evidence.
- Extract factual regulatory information using Azure AI Document Intelligence.
- Optionally provide advisory AI/rules-based summaries, obligation candidates, applicability suggestions and affected-business-unit suggestions.
- Keep human accountability for applicability, risk, control adequacy and approvals.
- Centralize CRU and CRMP records in Azure SQL.
- Replace email-driven approval with authenticated application workflow.
- Track controls, gaps, remediation actions, owners, target dates and closure evidence.
- Preserve an end-to-end business audit trail.
- Provide management dashboards and authorized exports without dependence on Power BI.

## 4. Scope
### 4.1 In scope
- Regulatory Source Registry and source-health monitoring.
- API/feed, document-repository and controlled HTML source adapters.
- New/amended/duplicate publication detection using metadata and SHA-256.
- Secure document ingestion and quarantine controls.
- Azure Blob Storage evidence/version management.
- Azure AI Document Intelligence extraction.
- Optional Azure OpenAI advisory classification/summarization.
- Human validation of extracted/suggested values.
- Obligation and applicability assessment.
- CRU workflow and version-bound approval.
- CRMP control assessment, gaps and remediation.
- Amendment reassessment.
- Reassignment/delegation.
- SLA reminders and escalation.
- Remediation closure validation.
- Business audit and evidence timeline.
- Management dashboards, drill-down and authorized Excel/PDF exports.
- Administrative configuration for sources, workflow/SLA and roles.

### 4.2 Out of scope unless separately approved
- Autonomous AI approval of regulatory applicability or risk.
- Approval by email reply.
- Replacement of Microsoft Entra ID as enterprise identity provider.
- Uncontrolled Internet-wide regulatory crawling.
- Unapproved automated legal interpretation.

## 5. Personas
| Persona | Primary responsibilities |
|---|---|
| Compliance Officer | Validate publications/extraction, assess applicability, prepare CRU, initiate processing |
| Risk Champion | Confirm business applicability, assess controls/gaps and review CRU/CRMP |
| Compliance Head | Review methodology, completeness, consistency and closure where configured |
| Business Unit Head | Final CRU approval for the accountable business unit |
| Remediation Action Owner | Execute assigned remediation, report progress and supply evidence |
| Internal Auditor | Read-only lifecycle, approval, evidence and audit review/export |
| Application Administrator | Configure approved sources, workflow/SLA and role mappings under change control |
| Support Operator | Monitor source/application health and execute approved operational runbooks |

## 6. Product modules
1. Regulatory Radar.
2. My Work Queue.
3. Publication and version management.
4. Regulatory extraction and assessment.
5. Obligation/applicability management.
6. CRU review and approval.
7. CRMP controls, gaps and remediation.
8. Amendment impact/reassessment.
9. Remediation closure.
10. Assignment, reassignment and delegation.
11. Evidence and regulatory timeline.
12. Business audit.
13. Management dashboard and reporting.
14. Source health and administration.
15. Workflow/SLA and role administration.

## 7. Core workflows
- **WF-01 Regulatory Discovery:** source scan to Compliance work queue.
- **WF-02 CRU Assessment and Approval:** Compliance Officer to Risk Champion to Compliance Head to Business Unit Head.
- **WF-03 CRMP Controls and Remediation:** obligation to control assessment, gap and accountable remediation.
- **WF-04 Amendment Reassessment:** amended publication to impact decision and required reapproval.
- **WF-05 Remediation Closure:** evidence submission to independent validation, residual-risk reassessment and closure.
- **WF-06 Reassignment and Delegation:** controlled ownership transfer while preserving SLA and history.

Detailed states and exceptions are maintained under `docs/product/workflows/`.

## 8. Core business rules
1. AI output is advisory and never constitutes final compliance approval.
2. System-suggested and human-confirmed values remain distinguishable.
3. Missing regulatory facts remain unknown/unconfirmed rather than being inferred as facts.
4. Original regulatory evidence and historic publication versions are never overwritten.
5. Azure SQL is authoritative for CRU/CRMP, workflow state and business audit.
6. Azure Monitor/Application Insights/Log Analytics are operational telemetry, not the compliance approval ledger.
7. Approvals bind to Assessment ID + Assessment Version + Publication Version.
8. Material changes create a new assessment version and reopen configured approvals.
9. Rework, rejection and reassignment require a reason/comment.
10. Maker-checker and segregation-of-duties controls are enforced server-side.
11. Approval occurs in the authenticated web application, not through an email reply.
12. Reassignment retains previous ownership history and the applicable SLA history.
13. Remediation cannot close without required evidence and configured validation.
14. Business audit events are append-oriented and unavailable for normal end-user modification.

## 9. User experience
The product is an Azure Web App with a React presentation layer and ASP.NET Core API initially deployed together per environment. The 20 defined screens are maintained under `docs/product/screens/`.

The Regulatory Assessment page uses a split-view approach: original publication/document context alongside extracted/system-suggested and human-confirmed fields. Workflow state, owner, due date and regulatory ID must remain visible for controlled work items.

## 10. Data and field governance
The canonical field definitions are maintained in `DATA-FIELD-CATALOGUE.md`. Each implementation field must ultimately define business name, API name, SQL mapping, type/length, required condition, validation, editable roles/states, materiality, sensitivity, audit treatment, search/report/export treatment and retention.

## 11. Approval and permissions
`APPROVAL-RULES.md`, `ROLE-PERMISSION-MATRIX.md` and `PERMISSION-CATALOGUE.md` are authoritative for product-level approval/permission design, subject to Compliance and Security sign-off. Microsoft Entra groups map to application roles, which map to explicit permissions. UI visibility never replaces API authorization.

## 12. Notifications and SLA
`NOTIFICATION-CATALOGUE.md` and `SLA-ESCALATION-MATRIX.md` define notification triggers, recipients, secure deep links, reminders and escalation. SLA calculation must use the approved business calendar. Duplicate notifications must be prevented and delivery attempts recorded.

## 13. Exception management
`EXCEPTION-CATALOGUE.md` defines known business/technical exceptions and links them to operational runbooks. Source failure is explicitly different from 'no new regulations found'. Manual fallback must be available for material regulatory processing when an optional AI component is unavailable.

## 14. Audit and evidence
The platform must be able to reconstruct:

Regulatory Source → Source Scan → Publication/Version → Original Document → Extraction → Human Validation → Obligation → CRU → Reviews/Approval → CRMP → Control/Gap → Remediation → Evidence → Closure.

Minimum audit context includes regulatory ID, entity/version, action, actor Entra object ID, actor role, UTC timestamp, material old/new values where applicable, reason/comment, publication version and correlation/workflow identifiers.

## 15. Reporting
The embedded Web App dashboard must support at least:
- new/amended regulatory publications;
- upcoming effective dates;
- high-risk obligations;
- business-unit impact;
- pending/overdue CRU reviews and approvals;
- controls and gaps;
- open/due/overdue remediation actions;
- residual-risk status;
- source health;
- extraction/manual-correction quality metrics;
- audit drill-down.

Dashboard values must reconcile to Azure SQL and honor role/data scope.

## 16. Environment and release model
DEV, TEST, UAT and PROD are isolated Azure environments. PROD additionally uses an App Service staging slot. The same immutable application artifact is promoted DEV → TEST → UAT → PROD staging → PROD. Slot swap is not a database rollback; database changes follow compatible expand-contract practices. See ADR-013 and `docs/operations/RELEASE-GOVERNANCE.md`.

## 17. Non-functional baseline
Final numerical NFRs require approval, but the product shall address availability, performance, asynchronous document processing, horizontal stateless App Service scaling, accessibility, security, privacy, retention, observability, backup/restore and disaster recovery. Provisional UI/API performance targets in the test catalogue are not contractual until NFR approval.

## 18. Traceability and testing
Implementation traceability is:

Business Requirement → Workflow Requirement → User Story → Journey → Screen → Permission/Data Rule → Test Case → Test Run → Evidence/Defect.

The current consolidated testing baseline contains 163 workflow-aligned cases. Azure DevOps import and traceability assets reside in `devops/`.

## 19. Implementation readiness
ADR-018 defines the readiness gate. A feature is Ready for Development only when applicable requirements, user story/acceptance criteria, journey, workflow, screen specification, field rules, permissions/SoD, audit events, notifications/SLA, exceptions/runbook, API contract, data model and tests are sufficiently defined and approved.

## 20. Open product decisions
- Final regulator/source list for POC and production.
- Final risk-rating methodology and calculation rules.
- Final material versus non-material field classification.
- Final CRU/CRMP field mapping from existing workbooks.
- Final approval/delegation/closure role combinations.
- Final business calendar and SLA periods.
- Final records-retention, immutability and legal-hold requirements.
- Final NFR targets including availability, RTO/RPO, performance and concurrency.
- Exact integration/export requirements for the existing internal portal or downstream GRC platforms.

## 21. Sign-off
Required before the specification is considered baselined:
- Compliance Product Owner
- Compliance Head/business sponsor
- Solution Architecture
- Cybersecurity
- Data/Records Management where applicable
- Engineering Lead
- Test/UAT Lead
