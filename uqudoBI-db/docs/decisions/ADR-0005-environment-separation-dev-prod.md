# ADR-0005: Separate Dev and Prod environments

## Context
The system will be multiuser and will evolve over time.
Schema changes, data imports, and experiments must not risk production data.

## Decision
The system will maintain separate environments:
- Dev: for schema changes, testing, experiments, and dry runs
- Prod: for real data and operational use

Environments will be logically separated even when running on the same machine
(e.g., separate databases or schemas).

## Consequences
- Lower risk of accidental data corruption
- Slightly higher operational complexity
- Clear workflow for testing changes before production deployment
