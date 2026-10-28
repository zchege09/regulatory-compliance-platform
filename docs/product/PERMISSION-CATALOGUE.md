# Permission Catalogue

| Permission | Purpose | Typical roles |
|---|---|---|
| regulatory.publication.read | View source publication/version | Authorized business roles, Auditor |
| regulatory.source.configure | Configure approved source adapters | Administrator |
| assessment.create | Create assessment | Compliance Officer |
| assessment.edit | Edit permitted assessment version | Compliance Officer, controlled Compliance Head |
| assessment.submit | Submit to review | Compliance Officer |
| assessment.reassign | Reassign with reason | Compliance Manager/Admin |
| cru.review.risk | Risk Champion decision | Risk Champion |
| cru.review.compliance | Compliance methodology decision | Compliance Head |
| cru.approve.businessunit | Final BU approval | BU Head |
| crmp.control.assess | Assess controls/adequacy | Compliance, Risk Champion |
| crmp.gap.create | Create gap/action | Compliance, Risk Champion |
| remediation.update | Update assigned action | Action Owner |
| remediation.submitClosure | Submit closure with evidence | Action Owner |
| remediation.approveClosure | Validate closure | Configured independent validator |
| audit.read | Read audit timeline | Authorized roles, Auditor |
| audit.export | Export audit evidence | Auditor/approved Compliance role |
| report.export | Export authorized reports | Approved roles |
| admin.workflow.configure | Configure workflow/SLA | Administrator |

Map Microsoft Entra groups to application roles, and roles to permissions. Code must authorize permissions, not hard-coded display-role names.
