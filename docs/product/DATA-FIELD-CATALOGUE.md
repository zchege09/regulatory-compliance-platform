# Data Field Catalogue

This is the initial field baseline. Add data type length, validation expression, database/API/UI names and reporting classification during detailed design.

| Field | Type | Required | Source | Editable roles | Material | Validation / notes |
|---|---|---:|---|---|---:|---|
| Regulatory ID | String | Yes | System | None | No | Unique immutable identifier |
| Regulator | Lookup | Yes | Extraction/Human | Compliance | Yes | Approved regulator list |
| Publication title | Text | Yes | Extraction/Human | Compliance | Yes | Required before submission |
| Source URL | URL | Yes | Source adapter | Admin only | Yes | Approved source allow-list |
| Publication date | Date | Yes | Extraction/Human | Compliance | Yes | Cannot be invalid calendar date |
| Effective date | Date | Conditional | Extraction/Human | Compliance | Yes | May remain Unconfirmed if absent |
| Publication version | Integer | Yes | System | None | Yes | Increment on detected amendment |
| Document hash | SHA-256 | Yes | System | None | Yes | Integrity and duplicate detection |
| Obligation | Long text | Yes | Extraction/AI/Human | Compliance | Yes | Must retain source reference |
| Applicability | Choice | Yes | Human | Compliance/Reviewer | Yes | Applicable/Not Applicable/Unclear |
| Affected business unit | Lookup | Conditional | AI/Human | Compliance/Reviewer | Yes | Required when applicable |
| Core/Ancillary | Choice | Conditional | Human | Compliance/Reviewer | Yes | Required when applicable |
| Applicability rationale | Long text | Yes | Human | Compliance/Reviewer | Yes | Mandatory for decision |
| Penalty | Long text | No | Extraction/Human | Compliance | Yes | Must not be invented when absent |
| Inherent risk | Choice/Score | Conditional | Calculated/Human | Controlled roles | Yes | Approved methodology |
| Control description | Long text | Conditional | Human | Compliance/Risk | Yes | Required for assessed control |
| Control adequacy | Choice | Conditional | Human | Compliance/Risk | Yes | Adequate/Inadequate/Not Present |
| Gap description | Long text | Conditional | Human | Compliance/Risk | Yes | Required if control inadequate |
| Remediation action | Long text | Conditional | Human | Compliance/Risk | Yes | Required for open gap |
| Action owner | User/Role | Conditional | Human/System | Controlled roles | Yes | Active authorized identity |
| Target date | Date | Conditional | Human/System | Controlled roles | Yes | History required on change |
| Residual risk | Choice/Score | Conditional | Calculated/Human | Controlled roles | Yes | Reassess at closure |
| Evidence reference | Document ref | Conditional | Human/System | Authorized roles | Yes | Hash, uploader, timestamp |
| Workflow state | Choice | Yes | System | Transition only | Yes | No direct update API |
| Assessment version | Integer | Yes | System | None | Yes | Approval binds to this version |
