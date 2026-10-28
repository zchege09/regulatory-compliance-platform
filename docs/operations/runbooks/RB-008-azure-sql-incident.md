# Azure SQL incident

- **Trigger:** Health check or write/read failure
- **Initial severity:** Assign using enterprise incident matrix and regulatory processing impact.
- **Triage and recovery:** Fail closed for writes, engage platform support, restore/fail over per DR plan, reconcile transactions/audit after recovery
- **Escalation/constraint:** Record achieved RPO/RTO and exceptions.

## Validation and closure
Confirm platform health, business-state consistency, audit/evidence integrity, notification status and any missed regulatory-processing window. Link alert, incident/change, actions, owner and timestamps. Conduct problem review for repeated or high-severity incidents.
