# Production slot rollback

- **Trigger:** Post-swap critical failure
- **Initial severity:** Assign using enterprise incident matrix and regulatory processing impact.
- **Triage and recovery:** Assess DB compatibility, reverse swap if safe, validate health/authentication, monitor, communicate and reconcile
- **Escalation/constraint:** Slot rollback does not reverse database schema/data.

## Validation and closure
Confirm platform health, business-state consistency, audit/evidence integrity, notification status and any missed regulatory-processing window. Link alert, incident/change, actions, owner and timestamps. Conduct problem review for repeated or high-severity incidents.
