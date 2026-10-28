# Regulatory Compliance Management Platform – Detailed Test Case Catalogue

**Purpose:** Implementation/UAT/security test catalogue for the proposed Azure-native regulatory compliance platform.  
**Traceability:** Each case should ultimately be linked to Requirement → Epic → Feature/User Story → Test Case → Execution Result → Evidence.  
**Assumption:** Final NFR values, source-specific details, retention rules and approval rules remain subject to business/security sign-off; provisional values are labelled as such.

## Test case template

Each executable test should capture: Test Case ID, Requirement ID, Epic/Feature, title, objective, preconditions, test data, steps, expected results, priority, automation candidate, environment, actual result, status, evidence link, defect ID, tester and execution date.

## Regulatory Source Monitoring

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-RSM-001 | Detect a new publication | Approved source is active; test publication not previously processed | Run scheduled/forced scan | One publication/version is created; source URL, retrieval time, hash and correlation ID recorded; downstream processing starts | Critical | Yes |
| TC-RSM-002 | Do not duplicate an unchanged publication | Publication already exists with same content hash | Rescan source | No new publication/version is created; scan outcome is recorded | Critical | Yes |
| TC-RSM-003 | Detect amended content at the same URL | Existing publication URL returns changed content | Rescan source | New publication version is created and linked to prior version | Critical | Yes |
| TC-RSM-004 | Recognize identical content under a different filename | Existing content is republished with another filename | Scan source | Duplicate is flagged and not treated as a new obligation without review | High | Yes |
| TC-RSM-005 | Handle source HTTP 429 throttling | Source returns 429 | Execute scan | Configured backoff/retry occurs; failure/recovery telemetry recorded | High | Yes |
| TC-RSM-006 | Handle temporary source outage | Source returns 5xx/timeout | Execute scan | Retries occur; no partial duplicate; operational failure is recorded | High | Yes |
| TC-RSM-007 | Alert when monitoring gap exceeds threshold | Last successful scan exceeds source threshold | Run monitoring health check | Alert is raised to configured operations owner | Critical | Yes |
| TC-RSM-008 | Disable a source | Administrator disables source | Run next scheduler cycle | Disabled source is not polled; configuration change is audited | High | Yes |
| TC-RSM-009 | Manual forced rescan | Authorized administrator requests rescan | Trigger manual rescan | Source is rescanned and action is audited | Medium | Yes |
| TC-RSM-010 | Detect malformed publication listing | Source response cannot be parsed | Execute scan | Adapter fails safely; source health degrades; no corrupt business record is created | High | Yes |

## Document Download and Security

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-DOC-001 | Accept valid PDF | Valid supported regulatory PDF | Download and validate file | File is accepted, hashed and moved to approved evidence storage | Critical | Yes |
| TC-DOC-002 | Reject executable renamed as PDF | Executable bytes with .pdf extension | Download file | Signature validation fails; file is quarantined/rejected | Critical | Yes |
| TC-DOC-003 | Quarantine malware test file | Approved harmless anti-malware test artefact | Process download | File is quarantined and no AI/business processing starts | Critical | Yes |
| TC-DOC-004 | Reject zero-byte file | 0-byte response | Process download | Document is rejected and source event is logged | High | Yes |
| TC-DOC-005 | Handle corrupted PDF | Corrupt PDF | Submit for processing | Failure is controlled; original retained/quarantined according to policy; operator can diagnose | High | Yes |
| TC-DOC-006 | Enforce maximum file size | Document exceeds configured size | Download file | Processing is blocked with explicit reason and audit/telemetry | High | Yes |
| TC-DOC-007 | Handle password-protected PDF | Encrypted PDF | Process file | Routed to configured exception/manual path; no silent processing | Medium | Yes |
| TC-DOC-008 | Reject unsupported content type | Unsupported file type | Process file | File rejected/routed according to policy | Medium | Yes |
| TC-DOC-009 | Verify SHA-256 integrity metadata | Valid document | Ingest file | Stored SHA-256 matches independently calculated hash | Critical | Yes |
| TC-DOC-010 | Preserve original document version | Amended regulatory PDF | Ingest change | Old and new evidence files remain retrievable and linked to publication versions | Critical | Yes |

## Document Intelligence Extraction

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-DI-001 | Extract regulator | Document names issuing regulator | Run extraction | Regulator field is populated with evidence/confidence where supported | High | Yes |
| TC-DI-002 | Extract publication title | Document contains title | Run extraction | Title is captured accurately | High | Yes |
| TC-DI-003 | Extract reference number | Document contains circular/gazette/reference number | Run extraction | Reference number captured | High | Yes |
| TC-DI-004 | Extract publication date | Document contains publication date | Run extraction | Publication date captured in canonical date format | Critical | Yes |
| TC-DI-005 | Extract effective date | Document contains explicit effective date | Run extraction | Effective date captured in canonical date format | Critical | Yes |
| TC-DI-006 | Handle missing effective date | No effective date present | Run extraction | Field remains unconfirmed/blank; system does not invent a date | Critical | Yes |
| TC-DI-007 | Extract penalties | Document contains penalties/sanctions | Run extraction | Penalty information is captured for human validation | High | Partial |
| TC-DI-008 | Extract multiple obligations | Document contains several obligations | Run extraction | Distinct candidate obligations are produced without losing source linkage | Critical | Partial |
| TC-DI-009 | Process scanned PDF using OCR | Image-only regulatory PDF | Run extraction | Readable fields extracted or explicitly marked low confidence | High | Yes |
| TC-DI-010 | Process multi-column layout | Multi-column regulatory publication | Run extraction | Reading order does not materially corrupt extracted obligations | High | Yes |
| TC-DI-011 | Expose low-confidence fields | Poor-quality field | Run extraction | Field is visibly identified for human attention | High | Yes |
| TC-DI-012 | Recover from Document Intelligence outage | AI service unavailable | Submit document | Retry/exception path works; document remains queued and no data is lost | Critical | Yes |

## AI and Classification

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-AI-001 | Suggest affected business unit | Clearly relevant banking requirement | Run classification | Candidate BU is presented as a suggestion, not approval | High | Partial |
| TC-AI-002 | Suggest applicability | Clearly relevant requirement | Run classification | Applicability recommendation and rationale displayed for human validation | High | Partial |
| TC-AI-003 | Handle ambiguous applicability | Ambiguous publication | Run classification | System requires human decision rather than auto-approving | Critical | Partial |
| TC-AI-004 | Support multiple affected units | Requirement spans several BUs | Run classification | Multiple candidate units can be proposed/confirmed | High | Partial |
| TC-AI-005 | Allow correction of AI suggestion | AI suggestion is deliberately incorrect | User edits result | Human-confirmed value is stored separately; correction is audited | Critical | Yes |
| TC-AI-006 | Operate when optional AI is unavailable | OpenAI endpoint unavailable | Open assessment | Manual assessment remains possible | Critical | Yes |
| TC-AI-007 | Resist prompt injection in source document | Document contains instructions aimed at model/system | Run classification | Document instructions do not override system policy/workflow; output remains advisory | Critical | Partial |
| TC-AI-008 | Do not invent unsupported fact | Document lacks a key fact | Run classification | Unsupported fact is not promoted to confirmed business data | Critical | Partial |
| TC-AI-009 | Record model/prompt version | Classification executed | Inspect audit/metadata | Model and prompt/rule version are traceable per policy | High | Yes |
| TC-AI-010 | Regression after model change | New model/prompt version deployed | Run golden test set | Results meet agreed regression thresholds before promotion | High | Yes |

## CRU Workflow

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-CRU-001 | CRU happy path approval | Valid assessment; all roles provisioned | Submit through Risk Champion, Compliance Head, BU Head | Correct states, timestamps, decisions, notifications and audit events recorded | Critical | Partial |
| TC-CRU-002 | Return for rework | Item at review stage | Reviewer returns with comment | State becomes Rework; comment mandatory; submitter notified | Critical | Yes |
| TC-CRU-003 | Reject assessment | Authorized reviewer; rejection allowed | Reject with reason | Rejected state and immutable decision evidence recorded | High | Yes |
| TC-CRU-004 | Resubmit corrected assessment | Item returned for rework | Correct and resubmit | New version/state is routed to appropriate reviewer; history preserved | Critical | Yes |
| TC-CRU-005 | Prevent submission with missing mandatory fields | Required field blank | Submit | Submission blocked with field-level validation | Critical | Yes |
| TC-CRU-006 | Prevent unauthorized approval | User lacks approval role | Call UI/API approval | Access denied; no state change; security event logged as appropriate | Critical | Yes |
| TC-CRU-007 | Enforce maker-checker | Submitter attempts prohibited approval | Attempt approval | Operation denied according to segregation rule | Critical | Yes |
| TC-CRU-008 | Invalidate/reopen approval after material change | Approved/reviewed item changed in material field | Save change | Prior approval is reopened/invalidated per policy and change audited | Critical | Yes |
| TC-CRU-009 | Handle concurrent edit | Two users edit same version | Both save | Optimistic concurrency prevents silent overwrite | High | Yes |
| TC-CRU-010 | Prevent normal edit of archived CRU | Archived record | Attempt edit | Edit denied except approved administrative process | High | Yes |
| TC-CRU-011 | Handle new publication version after approval | Approved CRU linked to publication that is amended | Ingest amended version | Change is surfaced and reassessment path is triggered according to rule | Critical | Partial |
| TC-CRU-012 | Capture approved snapshot | Item ready for approval | Approve | Exact data/version reviewed by approver is retrievable | Critical | Yes |

## CRMP Controls and Remediation

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-CRMP-001 | Existing adequate control | Applicable obligation with adequate control | Complete control assessment | No gap required; adequacy and evidence captured | High | Yes |
| TC-CRMP-002 | Existing inadequate control | Control exists but is inadequate | Complete assessment | Gap and remediation can be created | Critical | Yes |
| TC-CRMP-003 | No control exists | No mitigating control | Complete assessment | Gap creation is required according to methodology | Critical | Yes |
| TC-CRMP-004 | Create remediation action | Validated gap | Create action with owner/date | Action is linked to gap and obligation; audit created | Critical | Yes |
| TC-CRMP-005 | Block action without owner or due date | Required ownership/date absent | Save/submit action | Validation blocks active remediation state | High | Yes |
| TC-CRMP-006 | Update remediation progress | Open action | Change status/progress | History and audit event preserved | High | Yes |
| TC-CRMP-007 | Record target-date change | Existing target date | Change date with reason | Old/new dates and reason retained | Critical | Yes |
| TC-CRMP-008 | Mark action overdue | Open action passes due date | Run SLA job | Status/dashboard reflects overdue without losing original due date | High | Yes |
| TC-CRMP-009 | Require closure evidence | Action configured to require evidence | Attempt close without evidence | Closure blocked | Critical | Yes |
| TC-CRMP-010 | Close action with evidence | Required evidence attached | Submit closure/approval | Action closes and closure evidence/decision retained | Critical | Yes |
| TC-CRMP-011 | Recalculate residual risk | Control/remediation changes approved | Reassess risk | Residual risk recalculated using approved methodology | Critical | Yes |

## Assignment Reassignment and SLA

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-ASG-001 | Initial assignment | Item requires BU review | Assign to eligible user/role | Current owner and start time stored; owner notified | High | Yes |
| TC-ASG-002 | Manual reassignment requires reason | Assigned item | Reassign without reason then with reason | First attempt blocked; valid reassignment succeeds and history retained | High | Yes |
| TC-ASG-003 | Preserve previous owner | Assigned item reassigned | Inspect history | Old owner and assignment interval remain available | Critical | Yes |
| TC-ASG-004 | Handle disabled owner | Assigned Entra user disabled | Run ownership monitor/admin process | Item is flagged/orphaned and can be reassigned without losing history | Critical | Partial |
| TC-ASG-005 | Temporary delegation | Approved delegate and dates | Activate delegation | Delegate can act only within allowed scope/time; action attributed correctly | High | Partial |
| TC-ASG-006 | Delegation expiry | Delegation end time passes | Attempt action | Delegated authority is no longer valid | High | Yes |
| TC-ASG-007 | Reminder before due date | Action reaches configured reminder threshold | Run SLA workflow | One reminder is sent and delivery recorded | Medium | Yes |
| TC-ASG-008 | Prevent duplicate reminder | Same SLA job reruns | Run again | Idempotency prevents duplicate notification | High | Yes |
| TC-ASG-009 | Escalate overdue item | Action exceeds escalation threshold | Run SLA workflow | Configured escalation target notified and event recorded | High | Yes |
| TC-ASG-010 | Business-calendar calculation | Due date crosses weekend/approved holiday | Calculate due date | Due date follows configured business calendar | High | Yes |

## Audit and Evidence

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-AUD-001 | Audit material field update | Existing CRU field changed | Save change | Audit contains entity, field, old/new value, actor, role, UTC time and correlation ID | Critical | Yes |
| TC-AUD-002 | Audit approval | Authorized approver approves | Approve | Decision, actor, role, timestamp and approved version/snapshot reference recorded | Critical | Yes |
| TC-AUD-003 | Audit reassignment | Owner is changed | Reassign | Old/new owner, reason and actor recorded | Critical | Yes |
| TC-AUD-004 | Audit source discovery | New publication found | Process discovery | Source scan, URL, hash and regulatory ID traceable | Critical | Yes |
| TC-AUD-005 | Audit document model version | Document extracted | Inspect audit/metadata | Document Intelligence model/version traceable | High | Yes |
| TC-AUD-006 | Prevent audit mutation via application | Audit event exists | Attempt update/delete using UI/API | Operation is denied | Critical | Yes |
| TC-AUD-007 | Trace complete lifecycle | Completed regulatory record | Search by regulatory ID | Source → publication → extraction → CRU → CRMP → approval/remediation evidence can be reconstructed | Critical | Partial |
| TC-AUD-008 | Correlation ID propagation | Start source ingestion | Inspect app/integration telemetry and business records | Same correlation context links key processing stages | High | Yes |
| TC-AUD-009 | Evidence integrity check | Stored evidence exists | Recalculate hash | Hash matches stored integrity metadata | Critical | Yes |
| TC-AUD-010 | Auditor read-only export | Auditor role provisioned | View/export evidence history | Auditor can read/export permitted data but cannot modify it | High | Yes |

## Identity and Authorization

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-IAM-001 | Authenticate valid Entra user | Authorized active user | Sign in | User authenticated and mapped to application permissions | Critical | Yes |
| TC-IAM-002 | Reject unauthenticated API call | No token | Call protected API | 401/appropriate authentication response; no data disclosed | Critical | Yes |
| TC-IAM-003 | Reject expired token | Expired token | Call protected API | Request denied | Critical | Yes |
| TC-IAM-004 | Enforce role authorization at API | User lacks required role | Call privileged endpoint directly | 403/denied even if UI is bypassed | Critical | Yes |
| TC-IAM-005 | Disabled user loses access | Previously authorized Entra account disabled | Attempt sign-in/action | Access fails according to identity-control propagation expectations | Critical | Partial |
| TC-IAM-006 | Prevent IDOR | User can view record A but not record B | Manipulate record identifier | Unauthorized record remains inaccessible | Critical | Yes |
| TC-IAM-007 | Prevent role escalation | Normal user tampers with client claims/request | Call admin endpoint | Server-side authorization denies request | Critical | Yes |
| TC-IAM-008 | Administrator segregation | Application admin without approval role | Attempt compliance approval | Operation denied unless explicitly assigned approval role | High | Yes |
| TC-IAM-009 | Auditor is read-only | Auditor user | Attempt edit/approve | Read permitted; mutations denied | Critical | Yes |
| TC-IAM-010 | Managed identity least privilege | Service identity deployed | Attempt allowed and disallowed resource actions | Only required resource operations succeed | High | Partial |

## Notifications

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-NTF-001 | New assignment email | New task is assigned | Trigger notification | Configured recipient receives template with regulatory ID, due date and secure deep link | High | Partial |
| TC-NTF-002 | Approval request email | Assessment enters approval stage | Trigger workflow | Correct approver notified once | High | Partial |
| TC-NTF-003 | Reassignment email | Owner changes | Complete reassignment | New owner notified; prior owner notified if policy requires | Medium | Partial |
| TC-NTF-004 | Overdue escalation email | Action overdue | Run SLA workflow | Configured escalation template delivered and logged | High | Partial |
| TC-NTF-005 | Link requires authentication | Recipient opens deep link without session | Open link | User is authenticated before record is displayed | Critical | Yes |
| TC-NTF-006 | Email reply does not approve | Approval notification received | Reply to email | Business record remains unapproved | Critical | Partial |
| TC-NTF-007 | Failed email delivery | Mail service/recipient failure | Send notification | Failure recorded/retried/escalated according to configuration | High | Partial |
| TC-NTF-008 | Avoid sensitive email content | Sensitive evidence exists | Generate task email | Email contains only approved metadata and secure link | High | Yes |

## Dashboard and Reporting

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-RPT-001 | Reconcile new-regulation KPI | Known SQL dataset | Open dashboard | Displayed KPI equals authoritative SQL result | High | Yes |
| TC-RPT-002 | Reconcile overdue-action KPI | Known overdue dataset | Open dashboard | Displayed count equals authoritative SQL result | Critical | Yes |
| TC-RPT-003 | Drill down from KPI | Dashboard shows nonzero KPI | Select KPI | User sees exactly the records contributing to authorized count | High | Yes |
| TC-RPT-004 | Apply role-based reporting scope | Two users have different data scope | Open same dashboard | Each user sees only authorized records | Critical | Yes |
| TC-RPT-005 | Source-health dashboard | One source healthy, one failed | Open Regulatory Radar | Correct last-success/failure state shown | High | Yes |
| TC-RPT-006 | Excel export | Authorized filtered dataset | Export Excel | Export reproduces permitted filters/data accurately | Medium | Partial |
| TC-RPT-007 | PDF export | Authorized report | Export PDF | Readable report generated with correct scope and metadata | Medium | Partial |
| TC-RPT-008 | Large export control | Dataset exceeds configured export limit | Request export | Controlled asynchronous/limited behaviour occurs without app failure | Medium | Partial |

## API Data Integrity and Resilience

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-API-001 | Mandatory API validation | Request omits required field | POST/PUT request | 400 validation response; no partial record | High | Yes |
| TC-API-002 | Optimistic concurrency conflict | Stale row version | Submit update | Conflict response; no silent overwrite | High | Yes |
| TC-API-003 | Idempotent workflow callback | Same callback delivered twice | Replay callback | Single business transition/audit effect occurs | Critical | Yes |
| TC-API-004 | SQL transient failure | Inject transient DB failure | Execute operation | Retry where safe; transaction remains consistent | Critical | Partial |
| TC-API-005 | Blob transient failure | Inject storage failure | Upload evidence | Failure is surfaced/retried without orphaning approved business state | High | Partial |
| TC-API-006 | Key Vault unavailable | Secret/key dependency unavailable | Execute dependent operation | Failure is controlled and monitored; no fallback hard-coded secret | Critical | Partial |
| TC-API-007 | Invalid payload/XSS | Payload contains script markup | Submit field/comment | Stored/displayed content is safely encoded/sanitized | Critical | Yes |
| TC-API-008 | SQL injection attempt | Injection string in input | Call search/data API | Parameterized access prevents injection | Critical | Yes |

## Performance Accessibility and Compatibility

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-NFR-001 | Standard API response performance | Representative production-like data | Run load test | 95th percentile meets agreed NFR, provisional <3s for normal requests | High | Yes |
| TC-NFR-002 | Dashboard performance | Representative dataset | Load dashboard under target concurrency | 95th percentile meets agreed NFR, provisional <5s | High | Yes |
| TC-NFR-003 | Asynchronous long document processing | Large supported PDF | Submit document | Browser/API is not blocked for extraction duration; status can be tracked | High | Yes |
| TC-NFR-004 | Concurrent users | Target concurrent-user load | Execute mixed workload | Error/latency/resource targets met without data corruption | High | Yes |
| TC-NFR-005 | Keyboard accessibility | Web application | Navigate critical journeys keyboard-only | All critical controls usable with visible focus order | High | Partial |
| TC-NFR-006 | Screen-reader labels | Critical forms | Run accessibility scan/manual check | Inputs/buttons have meaningful accessible names and errors | High | Partial |
| TC-NFR-007 | Responsive layout | 320px to desktop viewport | Use core workflows | No page-level horizontal scrolling; critical controls remain usable | Medium | Partial |
| TC-NFR-008 | Supported browser coverage | Agreed Edge/Chrome versions | Run smoke suite | Critical workflows operate consistently | Medium | Yes |

## Migration

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-MIG-001 | Migrate valid CRU workbook records | Approved migration sample | Run migration | All expected records/fields arrive and reconcile | Critical | Yes |
| TC-MIG-002 | Normalize business-unit names | Source contains historical name variants | Transform/import | Values map to approved canonical reference data | High | Yes |
| TC-MIG-003 | Detect migration duplicates | Duplicate legacy rows | Run migration | Duplicates identified/handled by approved rule | Critical | Yes |
| TC-MIG-004 | Reject invalid mandatory data | Legacy record lacks mandatory target data | Run migration | Record goes to exception report; no silent default | High | Yes |
| TC-MIG-005 | Reconcile record counts | Known migration dataset | Compare source/staging/target | Counts reconcile with explained exceptions | Critical | Yes |
| TC-MIG-006 | Field-level reconciliation | Known sampled records | Compare source and target | Critical fields match approved mapping | Critical | Partial |
| TC-MIG-007 | Preserve migrated evidence linkage | Legacy evidence included | Migrate | Evidence is linked to correct regulatory/CRMP record | High | Partial |
| TC-MIG-008 | Repeat migration safely | Same migration batch rerun | Execute rerun | No unintended duplicates; batch is idempotent/reconcilable | High | Yes |

## Backup Disaster Recovery and Operations

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-DR-001 | Azure SQL point-in-time restore | Backup exists | Restore to alternate target | Database restored and validated within agreed RPO/RTO targets | Critical | Partial |
| TC-DR-002 | Evidence recovery/version retrieval | Evidence/version exists | Recover prior version | Document is retrievable with integrity intact | Critical | Partial |
| TC-DR-003 | Redeploy application from IaC | Clean approved environment target | Run IaC/deployment pipelines | Required platform/application components deploy reproducibly | Critical | Yes |
| TC-DR-004 | Recover Logic App workflows | Workflow definition unavailable/corrupt | Redeploy | Workflow restored from source-controlled artefact | High | Yes |
| TC-DR-005 | Operational alert routing | Simulated critical failure | Trigger alert | Correct support channel/persona receives actionable alert | High | Partial |
| TC-DR-006 | Runbook execution | Known source-monitor outage | Follow runbook | Support restores/diagnoses service using documented steps | High | Partial |
| TC-DR-007 | Health endpoint | Application healthy/unhealthy states | Call health endpoint | Endpoint correctly reflects dependency/readiness state without leaking secrets | High | Yes |
| TC-DR-008 | Post-recovery reconciliation | Service recovered after interruption | Reconcile queued/in-flight work | No silent record loss or duplicate approvals; exceptions identified | Critical | Partial |

## Security Verification

| ID | Test case | Preconditions | Steps | Expected result | Priority | Automation |
|---|---|---|---|---|---|---|
| TC-SEC-001 | WAF blocks common malicious request | Approved test payload | Send through ingress | Request blocked/logged according to WAF policy | High | Partial |
| TC-SEC-002 | CSRF protection for state-changing web action | Authenticated browser | Attempt cross-site forged request | Action denied/protected according to app pattern | Critical | Partial |
| TC-SEC-003 | SSRF resistance | User-controlled URL/input path | Attempt internal metadata/private target access | Application cannot be used to reach unauthorized internal endpoints | Critical | Partial |
| TC-SEC-004 | Secrets absent from source/logs | Application exercised | Scan repo/build/log sample | No production secrets exposed | Critical | Yes |
| TC-SEC-005 | TLS enforcement | Attempt legacy/insecure connection | Connect | Connection rejected per enterprise TLS policy | High | Partial |
| TC-SEC-006 | Public data-service access restricted | External/untrusted network | Attempt direct SQL/Blob/Key Vault access | Public path blocked according to approved network design | Critical | Partial |
| TC-SEC-007 | Penetration test critical findings | Release candidate | Execute independent penetration test | Zero unresolved Critical findings before go-live | Critical | No |
| TC-SEC-008 | Penetration test high findings | Release candidate | Execute independent penetration test | Zero unresolved High findings unless formally risk accepted | Critical | No |

## UAT end-to-end scenarios

### UAT-E2E-001 – New applicable regulation to CRMP closure

- **Scenario:** A new regulator publication is detected, contains multiple obligations, affects the selected POC business unit, one control is inadequate and a remediation action is required.
- **Flow:** Detect → download/security scan → version/hash → extract → classify → Compliance validation → CRU review/approval → CRMP → control/gap → remediation → evidence → closure → dashboard/audit.
- **Expected:** Every business decision is attributable; original evidence and versions remain available; final dashboard values reconcile to Azure SQL.

### UAT-E2E-002 – Amended regulation after prior approval

- **Scenario:** A previously approved regulatory publication changes at the same source URL.
- **Expected:** A new source version is preserved, the amendment is visible, impacted assessment is routed for reassessment per policy, and prior approval evidence is not overwritten.

### UAT-E2E-003 – Source outage and recovery

- **Scenario:** A critical regulator source becomes unreachable beyond the configured monitoring threshold and later recovers.
- **Expected:** retries, degraded source health, alerting, recovery status, audit/telemetry and no duplicate discovery after recovery.

### UAT-E2E-004 – Owner leaves during open remediation

- **Scenario:** An assigned action owner is disabled/transferred while an action remains open.
- **Expected:** item is flagged/reassigned using the approved ownership process; previous ownership and SLA history remain intact.

### UAT-E2E-005 – Rework and segregation of duties

- **Scenario:** A reviewer returns an assessment; the submitter corrects it and attempts a prohibited self-approval before routing it correctly.
- **Expected:** self-approval is denied; rework/resubmission history is retained; authorized approval succeeds.

## Entry criteria

- [ ] Requirements and acceptance criteria baselined for the scope under test.
- [ ] Test environment deployed from approved IaC and stable.
- [ ] Test identities/roles provisioned.
- [ ] Test regulator endpoints/fixtures and representative documents available.
- [ ] Required integrations, telemetry and audit logging enabled.
- [ ] Known blocking defects resolved or explicitly waived.

## Exit criteria

- [ ] 100% of Critical test cases executed.
- [ ] 100% of Critical test cases passed or have formal risk acceptance.
- [ ] No unresolved Critical security defects.
- [ ] No unresolved High security defects unless formally risk accepted.
- [ ] POC/MVP extraction quality meets agreed field-level completeness and accuracy thresholds.
- [ ] 100% of defined approval/reassignment/material-change audit events verified.
- [ ] Dashboard KPI reconciliation completed.
- [ ] UAT signed off by agreed Compliance/Risk stakeholders.
- [ ] DR/restore evidence completed before production go-live.

## Coverage summary

| Test suite | Cases |
|---|---:|
| Regulatory Source Monitoring | 10 |
| Document Download and Security | 10 |
| Document Intelligence Extraction | 12 |
| AI and Classification | 10 |
| CRU Workflow | 12 |
| CRMP Controls and Remediation | 11 |
| Assignment Reassignment and SLA | 10 |
| Audit and Evidence | 10 |
| Identity and Authorization | 10 |
| Notifications | 8 |
| Dashboard and Reporting | 8 |
| API Data Integrity and Resilience | 8 |
| Performance Accessibility and Compatibility | 8 |
| Migration | 8 |
| Backup Disaster Recovery and Operations | 8 |
| Security Verification | 8 |
| **Detailed catalogue total** | **151** |

> Note: the catalogue is intentionally implementation-oriented. Add Requirement IDs, owners, environment, execution status and evidence links when the requirements baseline and Azure DevOps/Jira project are established.
