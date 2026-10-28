# ADR-016: Regulatory Source Processing and Amendment Handling

- **Status:** Proposed
- **Date:** 2026-10-28

Use configurable adapters in this preference order: official API/feed, official document repository, controlled HTML monitoring. Identify content using source metadata and SHA-256. Preserve originals and every version.

States: Detected → Downloaded → Security Validation → Stored → Extracted → Classified → Human Validation, with Quarantined, Failed and Manual Review exceptions.

An amendment creates a new publication version and triggers impact review/reassessment of affected approved CRU/CRMP records. No-new-publication is distinct from source failure; persist last attempt, last success, duration and failure reason.
