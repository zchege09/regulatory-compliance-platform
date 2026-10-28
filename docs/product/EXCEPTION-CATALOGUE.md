# Exception Catalogue

| ID | Exception | Detection | Immediate treatment | Runbook |
|---|---|---|---|---|
| EX-001 | Regulatory site unavailable | Timeout/5xx/health gap | Retry/backoff; alert at threshold | RB-001 |
| EX-002 | Source layout/API changed | Parse/schema failure | Stop affected adapter; preserve evidence | RB-002 |
| EX-003 | Source throttling | HTTP 429 | Respect Retry-After/backoff | RB-001 |
| EX-004 | Publication unavailable | Broken document URL | Retry then manual handling | RB-001 |
| EX-005 | Malware detected | Scan result | Quarantine; no downstream processing | RB-003 |
| EX-006 | Unsupported/corrupt document | Signature/parser failure | Quarantine/manual review | RB-003 |
| EX-007 | Document Intelligence failure | Failed/timeout | Retry then manual extraction queue | RB-004 |
| EX-008 | AI classification failure | Failed/invalid response | Continue with manual assessment | RB-004 |
| EX-009 | Duplicate publication | Hash/metadata match | Link/suppress and audit | RB-002 |
| EX-010 | Ambiguous amendment impact | Human/system uncertainty | Route impact review | RB-005 |
| EX-011 | Assigned identity disabled | Directory/assignment check | Flag orphan; controlled reassignment | RB-007 |
| EX-012 | Approval SLA exceeded | SLA scheduler | Escalate and retain ownership history | RB-005 |
| EX-013 | Notification failure | Delivery status | Retry and operational alert | RB-006 |
| EX-014 | Workflow stuck/failed | State age/Logic App failure | Pause unsafe action; recover idempotently | RB-005 |
| EX-015 | Azure SQL unavailable | Health/exception | Fail closed for writes; recover/reconcile | RB-008 |
| EX-016 | Blob unavailable | Health/exception | Do not approve without evidence; recover | RB-009 |
| EX-017 | Key Vault unavailable | Health/exception | No hard-coded fallback secret | RB-010 |
| EX-018 | Production release failure | Smoke/health/telemetry | Stop/swap back if safe | RB-011/RB-012 |
