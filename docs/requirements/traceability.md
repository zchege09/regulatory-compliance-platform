# Requirements, User Stories and Test Case Traceability

This provisional baseline maps all 151 test cases to 16 implementation requirements and 16 user stories derived from the agreed architecture and test catalogue. Requirements/user stories should be reconciled with the formal BA requirements baseline before production governance sign-off.

| Requirement | Feature | User Story | Test Cases |
|---|---|---|---:|
| REQ-REG-001 | Regulatory Source Monitoring | US-REG-001 | 10 |
| REQ-DOC-001 | Secure Document Ingestion | US-DOC-001 | 10 |
| REQ-AI-001 | Document Intelligence | US-AI-001 | 12 |
| REQ-AI-002 | AI-assisted Classification | US-AI-002 | 10 |
| REQ-CRU-001 | CRU Workflow | US-CRU-001 | 12 |
| REQ-CRMP-001 | CRMP & Remediation | US-CRMP-001 | 11 |
| REQ-WFL-001 | Assignment, SLA & Escalation | US-WFL-001 | 10 |
| REQ-AUD-001 | Audit & Evidence | US-AUD-001 | 10 |
| REQ-IAM-001 | Identity & Authorization | US-IAM-001 | 10 |
| REQ-NTF-001 | Notifications | US-NTF-001 | 8 |
| REQ-RPT-001 | Dashboards & Reporting | US-RPT-001 | 8 |
| REQ-INT-001 | API Integrity & Resilience | US-INT-001 | 8 |
| REQ-NFR-001 | Performance & Accessibility | US-NFR-001 | 8 |
| REQ-MIG-001 | Migration | US-MIG-001 | 8 |
| REQ-OPS-001 | Operations & DR | US-OPS-001 | 8 |
| REQ-SEC-001 | Security Verification | US-SEC-001 | 8 |

## Azure DevOps linking recommendation

- Import/create the requirement/user-story backlog first and capture the generated Azure DevOps work item IDs.
- Link each User Story to its parent requirement/backlog item using the project process model.
- For requirements that need Azure Test Plans requirement coverage, create a requirement-based test suite from the applicable User Story/PBI and add/link the mapped Test Cases.
- Preserve the catalogue IDs (REQ-*, US-*, TC-*) in titles/tags so the generated Azure DevOps IDs can be cross-walked without losing the architecture traceability.
- Treat this mapping as the initial traceability baseline; future new test cases should include both Requirement ID and User Story ID.