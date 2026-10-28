# ADR-015: Approval, Version Binding and Segregation of Duties

- **Status:** Proposed
- **Date:** 2026-10-28

## Decision
Approvals bind to Assessment ID + Assessment Version + Publication Version. Server-side policy enforces maker-checker controls.

## Default chain
Compliance Officer → Risk Champion → Compliance Head → Business Unit Head → Compliance publication.

Rejection, rework and reassignment require comments. Material changes create a new version and reopen required approvals. Approval occurs only in the authenticated Web App. Initial material fields include applicability, affected unit, obligation, effective date, penalty, risk, control assessment, gap, remediation, owner and target date. Formatting-only changes may be non-material subject to Compliance approval.
