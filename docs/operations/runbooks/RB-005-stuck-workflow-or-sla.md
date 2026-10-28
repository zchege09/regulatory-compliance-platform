# Stuck workflow or SLA

- **Trigger:** State-age/failed orchestration/escalation alert
- **Initial severity:** Assign using enterprise incident matrix and regulatory processing impact.
- **Triage and recovery:** Inspect authoritative SQL state and correlation ID, fix assignment/dependency, replay idempotently, verify audit/notification
- **Escalation/constraint:** Never directly mutate state without controlled support procedure.

## Validation and closure
Confirm platform health, business-state consistency, audit/evidence integrity, notification status and any missed regulatory-processing window. Link alert, incident/change, actions, owner and timestamps. Conduct problem review for repeated or high-severity incidents.
