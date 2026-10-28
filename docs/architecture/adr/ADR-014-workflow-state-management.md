# ADR-014: Product Workflow State Management

- **Status:** Proposed
- **Date:** 2026-10-28

## Decision
Azure SQL is authoritative for workflow state. ASP.NET Core application services validate transitions and authorization. Azure Logic Apps Standard orchestrates asynchronous integration, notifications, reminders and escalation, but Logic App run history is not the business-state ledger.

Persist WorkflowDefinition, WorkflowInstance, WorkflowState, WorkflowTransition and Decision. Each transition records entity/version, actor, role, UTC time, reason where required, correlation ID and audit event. Material state update and audit event are transactional wherever practical; repeated delivery is idempotent.

## Workflows
Regulatory discovery, CRU approval, CRMP/remediation, amendment reassessment, remediation closure, reassignment/delegation and exception handling.
