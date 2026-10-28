# JRN-001: Regulatory discovery

- **Persona:** Compliance Officer
- **Trigger:** A scheduled scan finds a publication
- **Starting screen:** SCR-001
- **User journey:** Review candidate, open source, validate extraction, accept/correct fields, submit to CRU.
- **System responsibilities:** authorize actions; persist state/version; create audit events; manage assignment/SLA; send configured notifications.
- **Exceptions:** follow `EXCEPTION-CATALOGUE.md` and linked operational runbook.
- **End state:** Publication candidate ready for assessment.
- **Traceability:** map to applicable WF, requirement, user story, screen and tests before implementation.
