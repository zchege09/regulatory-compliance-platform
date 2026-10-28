# Release Governance

## Promotion path
DEV → TEST → UAT → PROD staging slot → production slot.

| Gate | Mandatory evidence |
|---|---|
| DEV to TEST | Successful build; unit tests; lint; SAST; secret/dependency scans |
| TEST to UAT | Integration/contract/regression tests; migration validation; relevant security tests |
| UAT to PROD staging | Business UAT sign-off; release version; approved change; production IaC/config validation |
| PROD staging to PROD | Health/authentication/DB compatibility; critical smoke tests; telemetry; release approval |
| Post swap | Health/synthetic checks; telemetry review; decision to accept or reverse swap |

## Failure policy
Stop promotion when a required gate fails. For production failure, assess data/schema compatibility before reverse swap. Slot swap is not a database rollback. Use expand-contract migrations and document forward recovery. Every release records approver, artifact version, migration version, test evidence, time, outcome and rollback decision.
