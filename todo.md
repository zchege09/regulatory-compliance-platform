# Regulatory Compliance Management Platform - Implementation TODO

**Status:** Working implementation backlog  
**Architecture baseline:** ADR-013 through ADR-017  
**Product workflow baseline:** WF-01 through WF-06  
**Test baseline:** 163 mapped test cases  

## 1. Governance and architecture
- [ ] Obtain Design Authority approval for target architecture.
- [ ] Approve ADR-013 environment/deployment strategy.
- [ ] Approve ADR-014 workflow state management.
- [ ] Approve ADR-015 approval, version binding and segregation of duties.
- [ ] Approve ADR-016 regulatory source processing and amendment handling.
- [ ] Approve ADR-017 audit and evidence model.
- [ ] Confirm Azure landing-zone subscriptions, regions, naming and network standards.
- [ ] Confirm DEV, TEST, UAT and PROD isolation model.
- [ ] Confirm PROD staging-slot release pattern and rollback runbook.
- [ ] Maintain architecture decision and RAID logs.

## 2. Product design sign-off
- [ ] Approve PRODUCT-SPECIFICATION.md.
- [ ] Approve SCR-001 through SCR-020 in SCREEN-CATALOGUE.md.
- [ ] Approve WF-01 through WF-06 in WORKFLOW-CATALOGUE.md.
- [ ] Approve ROLE-PERMISSION-MATRIX.md with Compliance and Security.
- [ ] Approve NOTIFICATION-CATALOGUE.md.
- [ ] Approve SLA-ESCALATION-MATRIX.md and business calendar.
- [ ] Define material versus non-material changes.
- [ ] Confirm CRU maker-checker constraints.
- [ ] Confirm remediation closure evidence and independent validation rules.
- [ ] Confirm amendment impact/reapproval rules.

## 3. Requirements and Azure DevOps traceability
- [ ] Import/create workflow requirements REQ-WF-001 through REQ-WF-006.
- [ ] Import/create cross-cutting requirement REQ-XCUT-001.
- [ ] Import/create US-WF-001 through US-WF-006 and US-XCUT-001.
- [ ] Create Epic → Feature → Requirement/PBI → User Story hierarchy.
- [ ] Import the 163-case Azure DevOps Test Plans catalogue.
- [ ] Link test cases to applicable requirements and user stories.
- [ ] Create requirement-based suites for WF-01 through WF-06.
- [ ] Create Critical Release, Security Regression, POC Regression and Full Regression suites.
- [ ] Replace catalogue cross-reference IDs with generated Azure DevOps IDs while retaining REQ/US/TC IDs in tags/titles.
- [ ] Establish Requirement → Story → Test → Run → Evidence/Defect traceability reporting.

## 4. Regulatory source catalogue and feasibility
- [ ] Agree approved regulator/source list with Compliance and Legal.
- [ ] Select 2-3 POC sources.
- [ ] Capture URL/endpoint, publication categories, source type, monitoring frequency, criticality and owner.
- [ ] Prefer official API/feed, then document repository, then controlled HTML monitoring.
- [ ] Validate automated-access terms and anti-bot restrictions.
- [ ] Test Azure connectivity and controlled outbound path.
- [ ] Test publication listing and PDF retrieval.
- [ ] Test new/amended/duplicate detection.
- [ ] Test source layout/API change failure detection.
- [ ] Define manual/fallback monitoring where automation is unavailable.
- [ ] Approve source-feasibility matrix.

## 5. Azure environments and infrastructure as code
- [ ] Create reusable Bicep modules.
- [ ] Provision isolated DEV environment.
- [ ] Provision isolated TEST environment.
- [ ] Provision isolated UAT environment.
- [ ] Provision isolated PROD environment.
- [ ] Configure PROD App Service staging slot.
- [ ] Configure App Service VNet integration.
- [ ] Configure Logic Apps Standard VNet integration.
- [ ] Configure Azure SQL private connectivity.
- [ ] Configure Blob Storage private connectivity.
- [ ] Configure Key Vault private connectivity.
- [ ] Configure Private DNS and routing.
- [ ] Configure approved enterprise ingress/WAF.
- [ ] Configure controlled outbound access to regulator sources.
- [ ] Configure managed identities and RBAC.
- [ ] Configure resource tags, budgets and cost alerts.
- [ ] Ensure production monitoring is disabled in PROD staging slot.

## 6. Configuration and secrets
- [ ] Create browser-safe frontend configuration templates.
- [ ] Create backend/runtime environment configuration templates.
- [ ] Create Logic App parameter templates.
- [ ] Create Bicep environment parameter templates.
- [ ] Store secrets/certificates in Azure Key Vault.
- [ ] Prohibit secrets in .env/source/IaC parameter files.
- [ ] Configure environment-specific managed identities.
- [ ] Define slot-specific settings for PROD staging/production.
- [ ] Verify non-production cannot access production SQL, Blob or Key Vault.

## 7. Azure SQL canonical data platform
- [ ] Implement RegulatorySource and SourceScan.
- [ ] Implement RegulatoryPublication and RegulatoryPublicationVersion.
- [ ] Implement RegulatoryObligation.
- [ ] Implement BusinessUnit/reference data.
- [ ] Implement ApplicabilityAssessment and RiskAssessment.
- [ ] Implement CRURecord and version model.
- [ ] Implement CRMPRecord.
- [ ] Implement Control and ControlAssessment.
- [ ] Implement Gap and RemediationAction.
- [ ] Implement Assignment and AssignmentHistory.
- [ ] Implement WorkflowDefinition, WorkflowInstance, WorkflowState and transitions.
- [ ] Implement Approval/ReviewDecision linked to exact versions.
- [ ] Implement Comment, Evidence and DocumentReference.
- [ ] Implement Notification and DeliveryAttempt.
- [ ] Implement append-oriented AuditEvent.
- [ ] Add optimistic concurrency.
- [ ] Add referential integrity, indexes and uniqueness rules.
- [ ] Prevent normal hard-delete of approved business/audit records.
- [ ] Create versioned migrations and rollback/forward-recovery procedures.

## 8. WF-01 Regulatory Discovery
- [ ] Implement Regulatory Source Registry administration.
- [ ] Implement scheduled Logic App source monitoring.
- [ ] Implement source-specific adapters.
- [ ] Retrieve and normalize publication metadata.
- [ ] Calculate SHA-256 content hash.
- [ ] Detect new, unchanged, duplicate and amended publications.
- [ ] Generate regulatory/correlation IDs.
- [ ] Download source document with bounded size/time controls.
- [ ] Validate MIME type/file signature.
- [ ] Implement malware scanning/quarantine pattern.
- [ ] Store original publication and version metadata in Blob Storage.
- [ ] Implement source health: last attempt, last success, duration and failure reason.
- [ ] Implement retry/backoff/throttling handling.
- [ ] Alert when source monitoring gap exceeds threshold.
- [ ] Trigger Azure AI Document Intelligence extraction.
- [ ] Extract regulator, title, reference, publication/effective dates, penalties and obligations.
- [ ] Display extraction confidence/quality where supported.
- [ ] Implement optional advisory classification.
- [ ] Protect AI processing from document prompt injection.
- [ ] Route candidate to Compliance work queue.
- [ ] Implement SCR-001, SCR-003, SCR-004, SCR-016 and SCR-017.

## 9. WF-02 CRU Assessment and Approval
- [ ] Implement CRU workflow states and allowed transitions.
- [ ] Implement Compliance Officer validation/submission.
- [ ] Implement Risk Champion review.
- [ ] Implement Compliance Head review.
- [ ] Implement Business Unit Head final approval.
- [ ] Implement rework, rejection, withdrawal and resubmission.
- [ ] Require comments for rework/rejection.
- [ ] Implement server-side maker-checker controls.
- [ ] Bind approvals to Assessment ID + Assessment Version + Publication Version.
- [ ] Capture exact approved snapshot/version.
- [ ] Create new assessment version for material edits.
- [ ] Reopen required approvals after material change.
- [ ] Audit non-material changes without unnecessary reapproval when configured.
- [ ] Prevent email replies from changing approval state.
- [ ] Implement SCR-002 and SCR-006 through SCR-009.

## 10. WF-03 CRMP Controls and Remediation
- [ ] Create CRMP assessment from applicable obligation.
- [ ] Capture required control and control owner.
- [ ] Capture control existence and adequacy.
- [ ] Create gap when control is missing/inadequate.
- [ ] Create remediation action with accountable owner and target date.
- [ ] Implement Not Started/In Progress/Blocked/Ready for Closure/Closed/Overdue states.
- [ ] Track target-date changes and reasons.
- [ ] Recalculate residual risk using approved methodology.
- [ ] Implement CRMP/remediation permissions.
- [ ] Implement SCR-010 and SCR-011.

## 11. WF-04 Amendment Reassessment
- [ ] Create new publication version when approved source content changes.
- [ ] Preserve previous source document and approvals.
- [ ] Identify CRU/CRMP records linked to amended publication/obligations.
- [ ] Present amendment for impact review.
- [ ] Allow reasoned 'no material impact' outcome with audit evidence.
- [ ] Trigger new assessment version where impact is material.
- [ ] Reopen applicable approval stages.
- [ ] Reassess changed effective dates and implementation deadlines.
- [ ] Update dashboards/work queues for pending amendment reassessment.

## 12. WF-05 Remediation Closure
- [ ] Implement Ready for Closure transition.
- [ ] Require configured closure evidence before submission.
- [ ] Route closure to approved Compliance/Risk validator.
- [ ] Implement return-to-owner with mandatory comments.
- [ ] Validate control effectiveness/adequacy at closure as required.
- [ ] Reassess residual risk.
- [ ] Implement closure approval.
- [ ] Preserve evidence, reviewer, timestamp and decision version.
- [ ] Prevent Action Owner from self-validating closure where SoD prohibits it.

## 13. WF-06 Reassignment and Delegation
- [ ] Implement initial assignment by role/business unit.
- [ ] Implement controlled reassignment with mandatory reason.
- [ ] Preserve old/new owner and assignment intervals.
- [ ] Notify new owner and relevant previous owner/manager according to policy.
- [ ] Implement temporary delegation start/end dates.
- [ ] Prevent action by expired delegate.
- [ ] Detect disabled/inactive owners.
- [ ] Provide orphaned-assignment report/work queue.
- [ ] Continue/recalculate SLA according to configuration without losing history.
- [ ] Audit all reassignment/delegation events.

## 14. Notifications, SLA and escalation
- [ ] Implement NTF-001 through NTF-009.
- [ ] Create centrally managed HTML email templates.
- [ ] Include secure deep links, regulatory ID and due-date context.
- [ ] Prevent sensitive evidence from being embedded unless approved.
- [ ] Implement configurable business-calendar due-date calculation.
- [ ] Implement reminder thresholds.
- [ ] Implement overdue detection.
- [ ] Implement escalation levels.
- [ ] Prevent duplicate delivery through idempotency.
- [ ] Record every notification and delivery attempt.
- [ ] Handle failed email delivery.

## 15. Business audit and evidence
- [ ] Generate AuditEvent for every defined material event.
- [ ] Capture actor Entra object ID, role and UTC timestamp.
- [ ] Capture entity/version, old/new values and comments where applicable.
- [ ] Propagate regulatory/correlation ID across app, SQL, Logic Apps and telemetry.
- [ ] Capture source URL, hash and retrieval timestamp.
- [ ] Capture Document Intelligence model/version.
- [ ] Prevent audit mutation through normal APIs.
- [ ] Implement evidence integrity verification.
- [ ] Define retention, immutability and legal hold with Records Management.
- [ ] Implement SCR-012, SCR-013 and SCR-014.

## 16. Dashboard and reporting
- [ ] Implement Regulatory Radar KPIs.
- [ ] Implement CRU workflow KPIs.
- [ ] Implement CRMP/gap/remediation KPIs.
- [ ] Implement high residual-risk views.
- [ ] Implement upcoming effective-date views.
- [ ] Implement source-health views.
- [ ] Implement extraction/manual-correction quality metrics.
- [ ] Implement role-scoped drill-down.
- [ ] Reconcile every KPI to authoritative Azure SQL query.
- [ ] Implement authorized Excel export.
- [ ] Implement authorized PDF/report export.
- [ ] Implement SCR-015 and SCR-020.

## 17. Identity, access and security
- [ ] Register Web/API application in Microsoft Entra ID.
- [ ] Create approved Entra groups/app roles.
- [ ] Implement API-level policies for each business role.
- [ ] Implement joiner/mover/leaver ownership process.
- [ ] Implement privileged access review/recertification.
- [ ] Enforce MFA/Conditional Access according to enterprise policy.
- [ ] Conduct STRIDE threat modelling.
- [ ] Cover malicious PDFs, prompt injection, source spoofing, SSRF, XSS, CSRF, SQL injection, IDOR, role escalation, audit tampering and data exfiltration.
- [ ] Configure WAF and secure HTTP headers.
- [ ] Configure TLS according to enterprise standard.
- [ ] Enable Defender/security recommendations as approved.
- [ ] Run SAST, dependency and secret scanning in CI.
- [ ] Run DAST and penetration testing before production.
- [ ] Resolve Critical/High findings or obtain formal risk acceptance.

## 18. Azure Web App implementation
- [ ] Implement React application shell and authenticated routing.
- [ ] Implement ASP.NET Core API and OpenAPI specification.
- [ ] Implement domain/application/infrastructure boundaries defined in AGENT.md.
- [ ] Implement SCR-001 through SCR-020 per catalogue.
- [ ] Implement standardized validation/error responses.
- [ ] Implement optimistic-concurrency conflict UX.
- [ ] Implement health/readiness endpoints.
- [ ] Implement accessible keyboard/focus/error behaviour.
- [ ] Validate responsive layout down to supported minimum viewport.

## 19. DevSecOps and deployment
- [ ] Configure repos, branches and code owners.
- [ ] Configure PR build, lint, unit test, SAST, dependency and secret scans.
- [ ] Build immutable/versioned deployment artifact.
- [ ] Promote the same artifact DEV → TEST → UAT → PROD staging.
- [ ] Configure environment approvals.
- [ ] Validate DB migrations before app promotion.
- [ ] Deploy production candidate to staging slot.
- [ ] Run staging health/authentication/smoke/DB compatibility checks.
- [ ] Execute production approval gate.
- [ ] Swap staging to production.
- [ ] Execute post-swap smoke/telemetry checks.
- [ ] Test reverse-slot swap.
- [ ] Use expand-contract database migration pattern so application rollback remains safe.

## 20. Testing and quality assurance
- [ ] Maintain 163-case workflow-aligned catalogue.
- [ ] Execute all Critical cases for relevant release scope.
- [ ] Automate suitable source-monitoring tests.
- [ ] Automate duplicate/amendment/hash tests.
- [ ] Automate API validation, authorization and concurrency tests.
- [ ] Automate workflow state-transition tests.
- [ ] Automate audit-event verification.
- [ ] Automate dashboard reconciliation where practical.
- [ ] Run extraction completeness and field-accuracy evaluation separately.
- [ ] Run AI prompt-injection/adversarial test set if Azure OpenAI is enabled.
- [ ] Run accessibility and browser-compatibility tests.
- [ ] Run load/performance tests against approved NFRs.
- [ ] Run resilience/failure-injection tests.
- [ ] Run backup/restore and DR tests.
- [ ] Execute UAT-E2E regulatory lifecycle scenarios.
- [ ] Require zero unresolved Critical security findings at release.
- [ ] Require zero unresolved High security findings unless formally risk accepted.

## 21. Legacy data migration
- [ ] Confirm historical migration scope and cutoff date.
- [ ] Profile all approved Excel workbooks.
- [ ] Map fields to canonical Azure SQL model.
- [ ] Normalize business units, statuses, owners and risk values.
- [ ] Detect duplicates and exceptions.
- [ ] Migrate required comments/evidence/approval history.
- [ ] Reconcile source/staging/target row counts.
- [ ] Perform field-level reconciliation.
- [ ] Obtain Compliance data-owner sign-off.
- [ ] Archive/freeze legacy workbooks according to records policy.

## 22. Operations, monitoring and DR
- [ ] Enable Application Insights and structured application telemetry.
- [ ] Enable Logic Apps diagnostics and Log Analytics integration.
- [ ] Configure source-monitoring alerts and runbooks.
- [ ] Configure extraction/workflow/notification failure alerts.
- [ ] Define L1/L2/L3 support responsibilities.
- [ ] Integrate critical alerts with approved ITSM process.
- [ ] Configure Azure SQL backup/PITR/LTR as required.
- [ ] Configure Blob redundancy/version recovery per RPO/RTO.
- [ ] Document application/Logic App redeployment from IaC.
- [ ] Test disaster recovery and record achieved RTO/RPO.
- [ ] Complete operational handover and support training.

## 23. POC gate
- [ ] Select one BU/corporate function and 2-3 regulator sources.
- [ ] Demonstrate source monitoring through human validation.
- [ ] Demonstrate CRU review and approval.
- [ ] Demonstrate CRMP control/gap/remediation.
- [ ] Demonstrate amendment reassessment.
- [ ] Demonstrate remediation closure.
- [ ] Demonstrate reassignment/delegation.
- [ ] Demonstrate business audit from source through action closure.
- [ ] Achieve 100% detection of controlled test publications.
- [ ] Achieve 100% controlled duplicate/version test detection.
- [ ] Target at least 95% completeness for agreed mandatory factual extracted fields after tuning; measure accuracy separately.
- [ ] Capture 100% of defined critical business audit events.
- [ ] Demonstrate source failure alerting.
- [ ] Complete POC security and performance assessment.
- [ ] Obtain go/no-go for MVP.

## 24. Production readiness and cutover
- [ ] Complete UAT and Compliance sign-off.
- [ ] Complete Design Authority closure/conditions.
- [ ] Complete Security sign-off and penetration remediation.
- [ ] Complete Privacy/Legal/Records Management approvals.
- [ ] Complete DR test and operations acceptance.
- [ ] Complete production capacity/FinOps review.
- [ ] Complete role provisioning/access review.
- [ ] Execute final migration and reconciliation.
- [ ] Validate PROD Regulatory Source Registry.
- [ ] Validate PROD staging-slot settings and source monitoring disabled there.
- [ ] Perform go-live readiness review.
- [ ] Enable approved production monitoring schedules.
- [ ] Validate first source scan, extraction, work queue, approval and audit chain.
- [ ] Enter hypercare.

## 25. Post-go-live
- [ ] Conduct 30-day review.
- [ ] Conduct 90-day review.
- [ ] Measure processing-time reduction versus baseline.
- [ ] Measure extraction correction rate.
- [ ] Measure SLA compliance and overdue items.
- [ ] Measure source-monitor reliability and false positives.
- [ ] Review workflow bottlenecks and reassignment trends.
- [ ] Tune models, prompts/rules and SLA configuration under change control.
- [ ] Retire legacy Excel/email process when formally approved.
- [ ] Plan additional regulators/business units/jurisdictions.

## Definition of Done
The product is production ready only after approved sources are reliably monitored, original evidence is preserved, human validation and version-bound approvals operate correctly, CRU/CRMP/remediation workflows pass UAT, amendment and closure paths are proven, role/SoD controls pass security testing, all required business audit events are traceable, dashboards reconcile to Azure SQL, migration is reconciled, DR is exercised, support accepts the service, and all release-blocking governance conditions are closed or formally accepted.
