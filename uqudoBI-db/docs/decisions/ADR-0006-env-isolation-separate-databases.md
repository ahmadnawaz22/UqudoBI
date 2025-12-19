# ADR-0006: Environment isolation via separate databases

## Context
We require separate Dev and Prod environments to reduce risk while iterating quickly.
The system will be multiuser and will evolve with schema changes and data imports.

## Decision
Use a single PostgreSQL instance with separate databases:
- revops_dev
- revops_prod

Schemas will not be used to separate environments in v1.

## Consequences
- Reduced risk of accidentally modifying production data
- Simpler permissions and operational workflow
- Backups/restores are straightforward per environment
