# Regulatory Discovery

- **Trigger/precondition:** Scheduled/forced scan; approval source active.
- **Primary flow:** Source scan → candidate → security validation → evidence → extraction → advisory classification → Compliance queue.
- **Exceptions:** Duplicate, quarantine, unsupported document, source failure, extraction failure.
- **Screens:** SCR-001, SCR-003, SCR-004, SCR-016, SCR-017

## Transition requirements
Every transition is server-authorized, version-aware, auditable and idempotent for repeated integration delivery. The detailed state/action matrix must be represented in application tests and Azure DevOps Test Plans.
