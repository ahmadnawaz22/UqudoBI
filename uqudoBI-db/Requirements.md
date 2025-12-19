## Question 1 (this impacts multi-user security and database setup):
Will your users connect directly to PostgreSQL (e.g., using a DB client / scripts / connectors), or will they only access data through an application/UI (e.g., NocoDB now, your custom app later), with no direct DB access?
### Answer:  “DB reachable remotely, but only via strict network controls + SSL, with read-only accounts for connectors” while Admin can connect directly (for troubleshooting, imports, fixes).

>Cautions / controls you should adopt with DB reachable remotely \
1-Never expose Postgres openly to “the whole internet.” Remote access does not mean public access. it will be either: \
-IP allowlist (your office/home/VPN egress IPs), or \
-a VPN/tunnel (best), or \
-private networking only (cloud VPC) if you later host apps alongside it. \
>\
2-Enforce TLS (SSL) for remote connections. \
-No plain-text connections. This is mandatory once you go online \
>\
3-Separate roles: write vs read. \
-UI/app role: limited write permissions to specific tables. \  
-Connector/reporting role: read-only, ideally views-only. \
>\
4-Views-first reporting discipline. \
-Connectors should hit curated views, not raw transactional tables, to reduce: \
-accidental heavy queries \
-data leakage \
-schema churn breaking reports \
>\
5-Backups and restore drills (multiuser makes this non-optional). \
-Automated daily backups minimum (later) \
-Periodic restore test (monthly) so you know you can recover \
>\
6-Audit trail from day one. At minimum, columns like: \
-created_at, updated_at \
-optionally created_by, updated_by \
Even if you don’t populate user IDs initially, you will later.

## Question 3 — impacts schema design and audit model
Do you need a full change history (audit trail) for key tables (who changed what and when), or is it enough to store just: created_at, updated_at and the latest state:
- A) Full audit history (append-only log of changes).
- B) Basic timestamps only (latest state only).

### Answer: A

## Question 4 - Environment separation

Do we want separate environments to reduce risk?

Options:
- A) Separate Dev and Prod environments
- B) Single environment only

Impact:
- Backup strategy
- Migration workflow
- User access control
- Risk of data corruption

### Answer: B

## Question 5 - Environment isolation strategy

How should Dev and Prod be separated in PostgreSQL?

Options:
- A) Single PostgreSQL instance, separate databases (e.g., revops_dev, revops_prod)
- B) Single PostgreSQL instance, single database, separate schemas (e.g., dev.*, prod.*)

Impact:
- Access control
- Backup/restore safety
- Risk of cross-environment mistakes
- Operational simplicity

### Answer : A

## Question 6 (reframed): How will "read-only users" access data?

Choose ONE (this affects database roles, views, and what we build first):

A) Read-only users connect directly to PostgreSQL with their own read-only accounts
   - They can run queries (ideally against reporting views, not raw tables)

B) Read-only users do NOT connect to PostgreSQL
   - They only consume outputs: Google Sheets / Excel extracts / BI dataset / BigQuery
   - (They can still have app access for entry/requests)

### Answer: A

## Question 7: Read-only access scope

For read-only users with direct DB access, what should they be allowed to query?

Options:
- A) Reporting views only (recommended for control)
- B) Reporting views + selected base tables
- C) All tables (true read-only, no restrictions)

Impact:
- Data exposure risk
- Query performance
- Future ability to enforce row-level security

### A

## Question 8: Schema change workflow

How will database schema changes be made?

Options:
- A) SQL migrations only (every change is a numbered SQL file)
- B) Manual changes allowed in dev, then copied to prod
- C) Combination (migrations preferred, manual allowed occasionally)

Impact:
- Reproducibility
- Ability to rebuild environments
- Long-term maintainability

### Answer: A


