# ADR-0009: Schema changes via SQL migrations only

## Context
The system will evolve over time with schema changes, new tables, and reporting views.
Dev and Prod environments must remain consistent and reproducible.

## Decision
All database schema changes will be performed using versioned SQL migration files.
Manual, ad-hoc changes to the database are not allowed.

Migrations will be:
- Numbered
- Stored in version control
- Applied in order to Dev and Prod

## Consequences
- Environments can be rebuilt from scratch reliably
- Dev and Prod remain in sync
- Slightly slower initial changes, but significantly lower long-term risk
