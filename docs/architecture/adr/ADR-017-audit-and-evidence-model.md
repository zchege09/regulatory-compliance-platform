# ADR-017: Business Audit and Evidence Model

- **Status:** Proposed
- **Date:** 2026-10-28

Azure SQL stores the append-oriented authoritative business audit. Azure Blob Storage preserves publications/evidence with version and SHA-256 metadata. Application Insights and Log Analytics are operational telemetry only.

Minimum event: regulatory ID, entity/type/version, action, actor Entra ID, role, UTC timestamp, material old/new values, reason/comment, publication version, correlation ID and workflow run ID where relevant. Normal APIs cannot alter audit records or remove evidence from approved/closed records.
