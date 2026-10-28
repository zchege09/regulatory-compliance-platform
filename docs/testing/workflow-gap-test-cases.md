# Workflow Gap Test Cases

These cases supplement the original 151-case catalogue and close explicit coverage gaps introduced by WF-04/WF-05 and version-bound approval rules.

## TC-WF04-001 – Approved publication amended at same URL
- **Workflow:** WF-04
- **Requirement:** REQ-WF-004
- **User Story:** US-WF-004
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Approved publication amended at same URL.
- **Expected:** New version is created and affected approved CRU/CRMP records enter impact review.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF04-002 – Amendment has no material impact
- **Workflow:** WF-04
- **Requirement:** REQ-WF-004
- **User Story:** US-WF-004
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Amendment has no material impact.
- **Expected:** Impact decision and rationale are audited; prior approvals remain valid according to policy.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF04-003 – Amendment changes an approved obligation
- **Workflow:** WF-04
- **Requirement:** REQ-WF-004
- **User Story:** US-WF-004
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Amendment changes an approved obligation.
- **Expected:** Affected assessment is versioned and required approvals reopen.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF04-004 – Amendment changes effective date
- **Workflow:** WF-04
- **Requirement:** REQ-WF-004
- **User Story:** US-WF-004
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Amendment changes effective date.
- **Expected:** New date is presented for validation; affected SLA/implementation dates are reassessed without overwriting history.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF05-001 – Action owner requests closure with required evidence
- **Workflow:** WF-05
- **Requirement:** REQ-WF-005
- **User Story:** US-WF-005
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Action owner requests closure with required evidence.
- **Expected:** State becomes Ready for Closure and routes to configured validator.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF05-002 – Closure attempted without mandatory evidence
- **Workflow:** WF-05
- **Requirement:** REQ-WF-005
- **User Story:** US-WF-005
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Closure attempted without mandatory evidence.
- **Expected:** Transition is rejected with validation message and audited failure/context.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF05-003 – Closure reviewer returns remediation
- **Workflow:** WF-05
- **Requirement:** REQ-WF-005
- **User Story:** US-WF-005
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Closure reviewer returns remediation.
- **Expected:** Action returns to In Progress/Rework with comment and owner notification.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF05-004 – Closure approval recalculates residual risk
- **Workflow:** WF-05
- **Requirement:** REQ-WF-005
- **User Story:** US-WF-005
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Closure approval recalculates residual risk.
- **Expected:** Approved control/evidence is reflected in residual-risk reassessment and closure audit.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF06-001 – Reassignment preserves active SLA
- **Workflow:** WF-06
- **Requirement:** REQ-WF-006
- **User Story:** US-WF-006
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Reassignment preserves active SLA.
- **Expected:** Ownership changes, history is retained and SLA follows configured policy.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF06-002 – Delegation expires during pending task
- **Workflow:** WF-06
- **Requirement:** REQ-WF-006
- **User Story:** US-WF-006
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Delegation expires during pending task.
- **Expected:** Expired delegate cannot act; current accountable owner remains identifiable.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF02-013 – Material edit after final approval
- **Workflow:** WF-02
- **Requirement:** REQ-WF-002
- **User Story:** US-WF-002
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Material edit after final approval.
- **Expected:** A new assessment version is created and applicable approvals are reopened.
- **Priority:** Critical
- **Automation candidate:** Yes

## TC-WF02-014 – Non-material correction after final approval
- **Workflow:** WF-02
- **Requirement:** REQ-WF-002
- **User Story:** US-WF-002
- **Preconditions:** Relevant workflow record exists in the required state.
- **Action:** Execute the scenario: Non-material correction after final approval.
- **Expected:** Correction is audited and approval remains valid when policy classifies the change as non-material.
- **Priority:** Critical
- **Automation candidate:** Yes
