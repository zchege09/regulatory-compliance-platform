# Approval Rules

| Current state | Role | Action | Next state | Comment | Main side effects |
|---|---|---|---|---|---|
| Draft/Validation | Compliance Officer | Submit | Risk Champion Review | Optional | Version saved, assignment/SLA/notification/audit |
| Risk Champion Review | Risk Champion | Confirm | Compliance Review | Optional | Decision and snapshot recorded |
| Risk Champion Review | Risk Champion | Return | Rework | Required | Owner notified, reason audited |
| Compliance Review | Compliance Head | Confirm | BU Approval | Optional | Approval task created |
| Compliance Review | Compliance Head | Return | Rework | Required | Prior review retained |
| BU Approval | BU Head | Approve | Approved | Optional | Version-bound approval recorded |
| BU Approval | BU Head | Reject/Return | Rework or Rejected | Required | No publication as approved |
| Ready for Closure | Closure Validator | Approve | Closed | Optional | Evidence/control/residual risk recorded |
| Ready for Closure | Closure Validator | Return | In Progress | Required | Action owner notified |

## Invariants
- Approval binds to assessment and publication versions.
- Prohibited preparation and final approval cannot be performed by the same identity.
- Email replies never transition workflow state.
- Material edits create a new version and reopen configured approvals.
- Non-material corrections are audited and follow the approved field classification.
- API authorization is authoritative; UI visibility is not a security control.
