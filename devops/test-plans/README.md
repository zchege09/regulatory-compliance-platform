# Azure DevOps Test Artefacts

- `azure-devops-test-cases-import.csv`: 163 test cases represented as 326 manual-step rows. IDs are blank because import creates new Azure DevOps work items.
- `azure-devops-traceability.csv`: Workflow → Requirement → User Story → Test Case cross-walk.

After import, retain the stable REQ/US/TC catalogue IDs in titles/tags and cross-reference generated Azure DevOps numeric IDs. `Automation Status` remains Not Automated until a real automated test is associated; `Automation-Yes` in Tags means candidate.
