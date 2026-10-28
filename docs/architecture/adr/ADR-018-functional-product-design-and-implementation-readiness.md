# ADR-018: Functional Product Design and Implementation Readiness

- **Status:** Proposed
- **Date:** 2026-10-28
- **Owners:** Solution Architecture, Compliance Product Owner, Engineering Lead

## Context
ADRs 013-017 define environment, workflow-state, approval, regulatory-source and audit/evidence architecture. They do not by themselves provide enough screen, field, permission, journey, exception and operational detail for deterministic implementation.

## Decision
Implementation shall be governed by a Functional Product Design Pack under `docs/product/` and operational runbooks under `docs/operations/`. A feature may enter implementation only when the following are defined and linked:

1. user journey and persona;
2. workflow state and transition;
3. screen and user interaction;
4. field definitions and validations;
5. role/permission and segregation-of-duties rule;
6. audit events and evidence;
7. notification/SLA behaviour;
8. exception handling and runbook;
9. user story and acceptance criteria;
10. test cases and Azure DevOps traceability.

## Authoritative artefacts
- `PRODUCT-SPECIFICATION.md`
- `DATA-FIELD-CATALOGUE.md`
- `APPROVAL-RULES.md`
- `PERMISSION-CATALOGUE.md`
- `EXCEPTION-CATALOGUE.md`
- `journeys/JRN-*.md`
- `screens/SCR-*.md`
- `workflows/WF-*.md`
- `operations/RELEASE-GOVERNANCE.md`
- `operations/runbooks/RB-*.md`

## Implementation gate
A Product Owner, architect, engineering lead, security representative and test lead must confirm that the applicable artefacts are sufficiently complete. Engineering must not invent unapproved transitions, permission grants, material-field classifications or exception outcomes in code.

## Consequences
This adds design effort before coding but reduces ambiguity, rework and unsafe implicit compliance decisions. Product documentation becomes controlled implementation input and must change with code, tests and ADRs.
