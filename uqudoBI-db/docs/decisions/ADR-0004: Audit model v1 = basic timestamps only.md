# ADR-0004: Audit model v1 = basic timestamps only

## Context
This system will be multiuser and data will be entered/changed through an application (no direct DB access). We need basic traceability without adding complexity in v1.

## Decision
For v1, we will not implement full audit history (change logs / event sourcing).
Instead, each key table will include:
- created_at
- updated_at
- created_by (nullable initially)
- updated_by (nullable initially)

## Consequences
- We can see when records were created/last updated (and later who did it).
- We cannot reconstruct historical values or field-by-field changes in v1.
- A full audit trail can be added later using an audit table/event log without breaking the core schema.
