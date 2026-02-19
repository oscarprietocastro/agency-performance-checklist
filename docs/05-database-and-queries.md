# 05 - Database & Queries

Checklist for diagnosing and optimizing database performance.

## Health Check

- [ ] CPU usage on the DB server is within normal range
- [ ] Memory usage — buffer pool (InnoDB) is sized to hold the working set
- [ ] Disk I/O — no persistent read/write bottleneck
- [ ] Active connections — not near `max_connections`
- [ ] Replication lag (if replica exists) — under 1 second

## Slow Query Analysis

- [ ] Slow query log enabled with `long_query_time = 1` (or lower)
- [ ] Top slow queries identified and reviewed
- [ ] `EXPLAIN` run on slow queries — no full table scans without justification
- [ ] `EXPLAIN ANALYZE` used where available (MySQL 8+, PostgreSQL)

## Indexes

- [ ] All foreign key columns are indexed
- [ ] Columns used in `WHERE`, `ORDER BY`, and `JOIN` conditions are indexed
- [ ] Composite indexes ordered by selectivity (most selective first)
- [ ] Unused indexes identified and removed (they slow down writes)
- [ ] Index statistics up to date (`ANALYZE TABLE`)

## Query Patterns

- [ ] No N+1 query patterns — batch loads used where possible
- [ ] No `SELECT *` in production queries — only needed columns selected
- [ ] Large result sets paginated, not loaded all at once
- [ ] Avoid `OFFSET` pagination on large tables — use keyset/cursor pagination
- [ ] Transactions kept short — no long-running open transactions

## Schema

- [ ] Appropriate data types used (avoid `TEXT` for short strings, `BIGINT` for small IDs)
- [ ] Tables that grow unboundedly have a retention/archival policy
- [ ] No excessive nullable columns where NOT NULL would suffice

## Connection Pooling

- [ ] Connection pooler in use (PgBouncer for PostgreSQL, ProxySQL for MySQL)
- [ ] Application not opening more connections than the pool allows
- [ ] Idle connection timeout configured

## Backups & Maintenance

- [ ] Backups verified and tested recently
- [ ] `OPTIMIZE TABLE` or `VACUUM` scheduled for high-churn tables
- [ ] Binary logs / WAL managed to prevent disk exhaustion
