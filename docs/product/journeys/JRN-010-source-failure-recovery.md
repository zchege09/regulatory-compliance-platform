# JRN-010: Source failure recovery

- **Persona:** Support Operator
- **Trigger:** Source health alert
- **Starting screen:** SCR-016
- **User journey:** Triage adapter/connectivity, follow runbook, test rescan, reconcile missed window.
- **System responsibilities:** authorize actions; persist state/version; create audit events; manage assignment/SLA; send configured notifications.
- **Exceptions:** follow `EXCEPTION-CATALOGUE.md` and linked operational runbook.
- **End state:** Healthy source or manual workaround.
- **Traceability:** map to applicable WF, requirement, user story, screen and tests before implementation.
