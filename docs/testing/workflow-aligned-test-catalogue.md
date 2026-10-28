# Workflow-Aligned Test Catalogue

**Total:** 163 cases (151 original + 12 workflow-gap cases).

| Test Case | Workflow | Requirement | User Story | Title | Priority |
|---|---|---|---|---|---|
| TC-RSM-001 | WF-01 | REQ-WF-001 | US-WF-001 | Detect a new publication | Critical |
| TC-RSM-002 | WF-01 | REQ-WF-001 | US-WF-001 | Do not duplicate an unchanged publication | Critical |
| TC-RSM-003 | WF-01 | REQ-WF-001 | US-WF-001 | Detect amended content at the same URL | Critical |
| TC-RSM-004 | WF-01 | REQ-WF-001 | US-WF-001 | Recognize identical content under a different filename | Critical |
| TC-RSM-005 | WF-01 | REQ-WF-001 | US-WF-001 | Handle source HTTP 429 throttling | Critical |
| TC-RSM-006 | WF-01 | REQ-WF-001 | US-WF-001 | Handle temporary source outage | Critical |
| TC-RSM-007 | WF-01 | REQ-WF-001 | US-WF-001 | Alert when monitoring gap exceeds threshold | Critical |
| TC-RSM-008 | WF-01 | REQ-WF-001 | US-WF-001 | Disable a source | Critical |
| TC-RSM-009 | WF-01 | REQ-WF-001 | US-WF-001 | Manual forced rescan | Critical |
| TC-RSM-010 | WF-01 | REQ-WF-001 | US-WF-001 | Detect malformed publication listing | Critical |
| TC-DOC-001 | WF-01 | REQ-WF-001 | US-WF-001 | Accept valid PDF | Critical |
| TC-DOC-002 | WF-01 | REQ-WF-001 | US-WF-001 | Reject executable renamed as PDF | Critical |
| TC-DOC-003 | WF-01 | REQ-WF-001 | US-WF-001 | Quarantine malware test file | Critical |
| TC-DOC-004 | WF-01 | REQ-WF-001 | US-WF-001 | Reject zero-byte file | Critical |
| TC-DOC-005 | WF-01 | REQ-WF-001 | US-WF-001 | Handle corrupted PDF | Critical |
| TC-DOC-006 | WF-01 | REQ-WF-001 | US-WF-001 | Enforce maximum file size | Critical |
| TC-DOC-007 | WF-01 | REQ-WF-001 | US-WF-001 | Handle password-protected PDF | Critical |
| TC-DOC-008 | WF-01 | REQ-WF-001 | US-WF-001 | Reject unsupported content type | Critical |
| TC-DOC-009 | WF-01 | REQ-WF-001 | US-WF-001 | Verify SHA-256 integrity metadata | Critical |
| TC-DOC-010 | WF-01 | REQ-WF-001 | US-WF-001 | Preserve original document version | Critical |
| TC-DI-001 | WF-01 | REQ-WF-001 | US-WF-001 | Extract regulator | Critical |
| TC-DI-002 | WF-01 | REQ-WF-001 | US-WF-001 | Extract publication title | Critical |
| TC-DI-003 | WF-01 | REQ-WF-001 | US-WF-001 | Extract reference number | Critical |
| TC-DI-004 | WF-01 | REQ-WF-001 | US-WF-001 | Extract publication date | Critical |
| TC-DI-005 | WF-01 | REQ-WF-001 | US-WF-001 | Extract effective date | Critical |
| TC-DI-006 | WF-01 | REQ-WF-001 | US-WF-001 | Handle missing effective date | Critical |
| TC-DI-007 | WF-01 | REQ-WF-001 | US-WF-001 | Extract penalties | Critical |
| TC-DI-008 | WF-01 | REQ-WF-001 | US-WF-001 | Extract multiple obligations | Critical |
| TC-DI-009 | WF-01 | REQ-WF-001 | US-WF-001 | Process scanned PDF using OCR | Critical |
| TC-DI-010 | WF-01 | REQ-WF-001 | US-WF-001 | Process multi-column layout | Critical |
| TC-DI-011 | WF-01 | REQ-WF-001 | US-WF-001 | Expose low-confidence fields | Critical |
| TC-DI-012 | WF-01 | REQ-WF-001 | US-WF-001 | Recover from Document Intelligence outage | Critical |
| TC-AI-001 | WF-01 | REQ-WF-001 | US-WF-001 | Suggest affected business unit | Critical |
| TC-AI-002 | WF-01 | REQ-WF-001 | US-WF-001 | Suggest applicability | Critical |
| TC-AI-003 | WF-01 | REQ-WF-001 | US-WF-001 | Handle ambiguous applicability | Critical |
| TC-AI-004 | WF-01 | REQ-WF-001 | US-WF-001 | Support multiple affected units | Critical |
| TC-AI-005 | WF-01 | REQ-WF-001 | US-WF-001 | Allow correction of AI suggestion | Critical |
| TC-AI-006 | WF-01 | REQ-WF-001 | US-WF-001 | Operate when optional AI is unavailable | Critical |
| TC-AI-007 | WF-01 | REQ-WF-001 | US-WF-001 | Resist prompt injection in source document | Critical |
| TC-AI-008 | WF-01 | REQ-WF-001 | US-WF-001 | Do not invent unsupported fact | Critical |
| TC-AI-009 | WF-01 | REQ-WF-001 | US-WF-001 | Record model/prompt version | Critical |
| TC-AI-010 | WF-01 | REQ-WF-001 | US-WF-001 | Regression after model change | Critical |
| TC-CRU-001 | WF-02 | REQ-WF-002 | US-WF-002 | CRU happy path approval | Critical |
| TC-CRU-002 | WF-02 | REQ-WF-002 | US-WF-002 | Return for rework | Critical |
| TC-CRU-003 | WF-02 | REQ-WF-002 | US-WF-002 | Reject assessment | Critical |
| TC-CRU-004 | WF-02 | REQ-WF-002 | US-WF-002 | Resubmit corrected assessment | Critical |
| TC-CRU-005 | WF-02 | REQ-WF-002 | US-WF-002 | Prevent submission with missing mandatory fields | Critical |
| TC-CRU-006 | WF-02 | REQ-WF-002 | US-WF-002 | Prevent unauthorized approval | Critical |
| TC-CRU-007 | WF-02 | REQ-WF-002 | US-WF-002 | Enforce maker-checker | Critical |
| TC-CRU-008 | WF-02 | REQ-WF-002 | US-WF-002 | Invalidate/reopen approval after material change | Critical |
| TC-CRU-009 | WF-02 | REQ-WF-002 | US-WF-002 | Handle concurrent edit | Critical |
| TC-CRU-010 | WF-02 | REQ-WF-002 | US-WF-002 | Prevent normal edit of archived CRU | Critical |
| TC-CRU-011 | WF-04 | REQ-WF-004 | US-WF-004 | Handle new publication version after approval | Critical |
| TC-CRU-012 | WF-02 | REQ-WF-002 | US-WF-002 | Capture approved snapshot | Critical |
| TC-CRMP-001 | WF-03 | REQ-WF-003 | US-WF-003 | Existing adequate control | Critical |
| TC-CRMP-002 | WF-03 | REQ-WF-003 | US-WF-003 | Existing inadequate control | Critical |
| TC-CRMP-003 | WF-03 | REQ-WF-003 | US-WF-003 | No control exists | Critical |
| TC-CRMP-004 | WF-03 | REQ-WF-003 | US-WF-003 | Create remediation action | Critical |
| TC-CRMP-005 | WF-03 | REQ-WF-003 | US-WF-003 | Block action without owner or due date | Critical |
| TC-CRMP-006 | WF-03 | REQ-WF-003 | US-WF-003 | Update remediation progress | Critical |
| TC-CRMP-007 | WF-03 | REQ-WF-003 | US-WF-003 | Record target-date change | Critical |
| TC-CRMP-008 | WF-03 | REQ-WF-003 | US-WF-003 | Mark action overdue | Critical |
| TC-CRMP-009 | WF-05 | REQ-WF-005 | US-WF-005 | Require closure evidence | Critical |
| TC-CRMP-010 | WF-05 | REQ-WF-005 | US-WF-005 | Close action with evidence | Critical |
| TC-CRMP-011 | WF-03 | REQ-WF-003 | US-WF-003 | Recalculate residual risk | Critical |
| TC-ASG-001 | WF-06 | REQ-WF-006 | US-WF-006 | Initial assignment | High |
| TC-ASG-002 | WF-06 | REQ-WF-006 | US-WF-006 | Manual reassignment requires reason | High |
| TC-ASG-003 | WF-06 | REQ-WF-006 | US-WF-006 | Preserve previous owner | High |
| TC-ASG-004 | WF-06 | REQ-WF-006 | US-WF-006 | Handle disabled owner | High |
| TC-ASG-005 | WF-06 | REQ-WF-006 | US-WF-006 | Temporary delegation | High |
| TC-ASG-006 | WF-06 | REQ-WF-006 | US-WF-006 | Delegation expiry | High |
| TC-ASG-007 | WF-06 | REQ-WF-006 | US-WF-006 | Reminder before due date | High |
| TC-ASG-008 | WF-06 | REQ-WF-006 | US-WF-006 | Prevent duplicate reminder | High |
| TC-ASG-009 | WF-06 | REQ-WF-006 | US-WF-006 | Escalate overdue item | High |
| TC-ASG-010 | WF-06 | REQ-WF-006 | US-WF-006 | Business-calendar calculation | High |
| TC-AUD-001 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Audit material field update | Critical |
| TC-AUD-002 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Audit approval | Critical |
| TC-AUD-003 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Audit reassignment | Critical |
| TC-AUD-004 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Audit source discovery | Critical |
| TC-AUD-005 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Audit document model version | Critical |
| TC-AUD-006 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Prevent audit mutation via application | Critical |
| TC-AUD-007 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Trace complete lifecycle | Critical |
| TC-AUD-008 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Correlation ID propagation | Critical |
| TC-AUD-009 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Evidence integrity check | Critical |
| TC-AUD-010 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Auditor read-only export | Critical |
| TC-IAM-001 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Authenticate valid Entra user | Critical |
| TC-IAM-002 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Reject unauthenticated API call | Critical |
| TC-IAM-003 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Reject expired token | Critical |
| TC-IAM-004 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Enforce role authorization at API | Critical |
| TC-IAM-005 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Disabled user loses access | Critical |
| TC-IAM-006 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Prevent IDOR | Critical |
| TC-IAM-007 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Prevent role escalation | Critical |
| TC-IAM-008 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Administrator segregation | Critical |
| TC-IAM-009 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Auditor is read-only | Critical |
| TC-IAM-010 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Managed identity least privilege | Critical |
| TC-NTF-001 | CROSS | REQ-XCUT-001 | US-XCUT-001 | New assignment email | High |
| TC-NTF-002 | WF-02 | REQ-WF-002 | US-WF-002 | Approval request email | High |
| TC-NTF-003 | WF-06 | REQ-WF-006 | US-WF-006 | Reassignment email | High |
| TC-NTF-004 | WF-03 | REQ-WF-003 | US-WF-003 | Overdue escalation email | High |
| TC-NTF-005 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Link requires authentication | High |
| TC-NTF-006 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Email reply does not approve | High |
| TC-NTF-007 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Failed email delivery | High |
| TC-NTF-008 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Avoid sensitive email content | High |
| TC-RPT-001 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Reconcile new-regulation KPI | High |
| TC-RPT-002 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Reconcile overdue-action KPI | High |
| TC-RPT-003 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Drill down from KPI | High |
| TC-RPT-004 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Apply role-based reporting scope | High |
| TC-RPT-005 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Source-health dashboard | High |
| TC-RPT-006 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Excel export | High |
| TC-RPT-007 | CROSS | REQ-XCUT-001 | US-XCUT-001 | PDF export | High |
| TC-RPT-008 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Large export control | High |
| TC-API-001 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Mandatory API validation | High |
| TC-API-002 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Optimistic concurrency conflict | High |
| TC-API-003 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Idempotent workflow callback | High |
| TC-API-004 | CROSS | REQ-XCUT-001 | US-XCUT-001 | SQL transient failure | High |
| TC-API-005 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Blob transient failure | High |
| TC-API-006 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Key Vault unavailable | High |
| TC-API-007 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Invalid payload/XSS | High |
| TC-API-008 | CROSS | REQ-XCUT-001 | US-XCUT-001 | SQL injection attempt | High |
| TC-NFR-001 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Standard API response performance | High |
| TC-NFR-002 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Dashboard performance | High |
| TC-NFR-003 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Asynchronous long document processing | High |
| TC-NFR-004 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Concurrent users | High |
| TC-NFR-005 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Keyboard accessibility | High |
| TC-NFR-006 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Screen-reader labels | High |
| TC-NFR-007 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Responsive layout | High |
| TC-NFR-008 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Supported browser coverage | High |
| TC-MIG-001 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Migrate valid CRU workbook records | High |
| TC-MIG-002 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Normalize business-unit names | High |
| TC-MIG-003 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Detect migration duplicates | High |
| TC-MIG-004 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Reject invalid mandatory data | High |
| TC-MIG-005 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Reconcile record counts | High |
| TC-MIG-006 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Field-level reconciliation | High |
| TC-MIG-007 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Preserve migrated evidence linkage | High |
| TC-MIG-008 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Repeat migration safely | High |
| TC-DR-001 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Azure SQL point-in-time restore | High |
| TC-DR-002 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Evidence recovery/version retrieval | High |
| TC-DR-003 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Redeploy application from IaC | High |
| TC-DR-004 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Recover Logic App workflows | High |
| TC-DR-005 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Operational alert routing | High |
| TC-DR-006 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Runbook execution | High |
| TC-DR-007 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Health endpoint | High |
| TC-DR-008 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Post-recovery reconciliation | High |
| TC-SEC-001 | CROSS | REQ-XCUT-001 | US-XCUT-001 | WAF blocks common malicious request | Critical |
| TC-SEC-002 | CROSS | REQ-XCUT-001 | US-XCUT-001 | CSRF protection for state-changing web action | Critical |
| TC-SEC-003 | CROSS | REQ-XCUT-001 | US-XCUT-001 | SSRF resistance | Critical |
| TC-SEC-004 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Secrets absent from source/logs | Critical |
| TC-SEC-005 | CROSS | REQ-XCUT-001 | US-XCUT-001 | TLS enforcement | Critical |
| TC-SEC-006 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Public data-service access restricted | Critical |
| TC-SEC-007 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Penetration test critical findings | Critical |
| TC-SEC-008 | CROSS | REQ-XCUT-001 | US-XCUT-001 | Penetration test high findings | Critical |
| TC-WF04-001 | WF-04 | REQ-WF-004 | US-WF-004 | Approved publication amended at same URL | Critical |
| TC-WF04-002 | WF-04 | REQ-WF-004 | US-WF-004 | Amendment has no material impact | Critical |
| TC-WF04-003 | WF-04 | REQ-WF-004 | US-WF-004 | Amendment changes an approved obligation | Critical |
| TC-WF04-004 | WF-04 | REQ-WF-004 | US-WF-004 | Amendment changes effective date | Critical |
| TC-WF05-001 | WF-05 | REQ-WF-005 | US-WF-005 | Action owner requests closure with required evidence | Critical |
| TC-WF05-002 | WF-05 | REQ-WF-005 | US-WF-005 | Closure attempted without mandatory evidence | Critical |
| TC-WF05-003 | WF-05 | REQ-WF-005 | US-WF-005 | Closure reviewer returns remediation | Critical |
| TC-WF05-004 | WF-05 | REQ-WF-005 | US-WF-005 | Closure approval recalculates residual risk | Critical |
| TC-WF06-001 | WF-06 | REQ-WF-006 | US-WF-006 | Reassignment preserves active SLA | Critical |
| TC-WF06-002 | WF-06 | REQ-WF-006 | US-WF-006 | Delegation expires during pending task | Critical |
| TC-WF02-013 | WF-02 | REQ-WF-002 | US-WF-002 | Material edit after final approval | Critical |
| TC-WF02-014 | WF-02 | REQ-WF-002 | US-WF-002 | Non-material correction after final approval | Critical |
