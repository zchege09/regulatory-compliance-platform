# Reassignment and Delegation

- **Trigger/precondition:** Ownership change, leave or administrative correction.
- **Primary flow:** Reasoned reassignment/delegation → permission validation → owner change → SLA policy → notifications/audit.
- **Exceptions:** Inactive owner, expired delegate, no eligible owner.
- **Screens:** SCR-002, SCR-018, SCR-019

## Transition requirements
Every transition is server-authorized, version-aware, auditable and idempotent for repeated integration delivery. The detailed state/action matrix must be represented in application tests and Azure DevOps Test Plans.
