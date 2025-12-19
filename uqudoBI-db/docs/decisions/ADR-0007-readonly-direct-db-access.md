# ADR-0007: Read-only users have direct PostgreSQL access

## Context
The system includes power users who need ad-hoc querying and live access.
In addition to application access, these users require direct read-only access
to the database for analysis and reporting.

## Decision
Read-only users will:
- Have application access (as defined by the app)
- Also have direct PostgreSQL access with read-only permissions

Admin users retain full database access.

## Constraints
- Read-only users must not be able to INSERT, UPDATE, or DELETE
- Access should be limited to reporting tables/views where possible
- Credentials are user-specific (not shared)

## Consequences
- Greater flexibility for advanced users
- Increased responsibility for access management and query discipline
- Requires careful permission design to avoid performance or data exposure issues
