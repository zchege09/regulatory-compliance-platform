# Source layout/API change

- **Trigger:** Parser/schema errors or unexpected empty listing
- **Initial severity:** Assign using enterprise incident matrix and regulatory processing impact.
- **Triage and recovery:** Disable affected adapter if unsafe, capture response sample, update fixture/parser, regression test, controlled redeploy/rescan
- **Escalation/constraint:** Use approved manual monitoring until restored.

## Validation and closure
Confirm platform health, business-state consistency, audit/evidence integrity, notification status and any missed regulatory-processing window. Link alert, incident/change, actions, owner and timestamps. Conduct problem review for repeated or high-severity incidents.
