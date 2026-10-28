# Workflow Catalogue

## WF-01 Regulatory discovery
Scan → detect new/amended → security validation → evidence → extraction → advisory classification → Compliance queue. Exceptions: duplicate, quarantine, unsupported content, source failure and manual review.

## WF-02 CRU
New → Extracted → Compliance Validation → Risk Champion Review → Compliance Head Review → BU Head Approval → Approved → Published. Actions: return, reject, reassign, withdraw and resubmit.

## WF-03 CRMP
Applicable Obligation → Control Assessment → Adequate Control or Gap → Remediation → Owner/Target Date → Progress → Ready for Closure → Validation → Closed.

## WF-04 Amendment
Approved Publication → Amendment → New Version → Impact Review → affected CRU/CRMP → reassessment → required reapproval.

## WF-05 Closure
Owner supplies evidence → Ready for Closure → Compliance/Risk validates control/evidence → residual risk reassessed → approve or return.

## WF-06 Ownership
Controlled reassignment/delegation with reason → notify new owner → preserve history → continue/recalculate SLA per policy.

All transitions use server authorization, version binding, required comments and idempotent processing.
