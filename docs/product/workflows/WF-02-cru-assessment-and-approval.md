# CRU Assessment and Approval

- **Trigger/precondition:** Validated regulatory candidate.
- **Primary flow:** Compliance validation → Risk Champion → Compliance Head → BU Head → Approved/Published.
- **Exceptions:** Return, reject, withdraw, reassign, material edit, concurrency conflict.
- **Screens:** SCR-002, SCR-004, SCR-006, SCR-007, SCR-008, SCR-009

## Transition requirements
Every transition is server-authorized, version-aware, auditable and idempotent for repeated integration delivery. The detailed state/action matrix must be represented in application tests and Azure DevOps Test Plans.
