# ADR-0008: Read-only users access reporting views only

## Context
Read-only users are allowed direct PostgreSQL access for ad-hoc analysis.
To reduce risk, prevent misuse, and stabilize reporting, access must be controlled.

## Decision
Read-only users will be granted SELECT access to reporting views only.
They will not have access to base (raw) tables.

Base tables remain accessible only to admin users and application service accounts.

## Consequences
- Reduced risk of accidental heavy or unsafe queries
- Clear contract for reporting consumers
- Base schema can evolve without breaking users
- All analytical logic is centralized in views
