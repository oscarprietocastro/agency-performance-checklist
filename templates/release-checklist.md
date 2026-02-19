# Release Checklist

**Project:** <!-- Project name -->
**Release version:** <!-- v1.2.3 -->
**Release date:** <!-- YYYY-MM-DD -->
**Release manager:** <!-- Name -->

---

## Pre-Release

### Code & Review

- [ ] All changes code-reviewed and approved
- [ ] No unresolved merge conflicts
- [ ] Feature flags set correctly for this release
- [ ] Migrations reviewed — are they reversible?
- [ ] No debug code, `console.log`, or development-only config committed

### Performance

- [ ] Lighthouse run on staging — scores within acceptable range
- [ ] Page weight compared to previous release — no unexpected regressions
- [ ] New or changed queries reviewed for performance
- [ ] Cache invalidation strategy confirmed for changed content types
- [ ] Asset aggregation/compilation run on staging

### Testing

- [ ] All automated tests passing (unit, integration, E2E)
- [ ] Manual smoke test of critical user flows on staging
- [ ] Tested on mobile and desktop
- [ ] Cross-browser check completed
- [ ] Accessibility checks passed

### Infrastructure

- [ ] Environment variables / config changes applied to production
- [ ] Database migrations tested on a production-size dataset
- [ ] Rollback plan documented (see below)
- [ ] Backup taken before release

---

## Release

- [ ] Deployment window communicated to stakeholders
- [ ] Maintenance mode enabled (if required)
- [ ] Deployment executed
- [ ] Database migrations run (if any)
- [ ] Cache cleared/warmed (if required)
- [ ] Maintenance mode disabled

---

## Post-Release Verification (first 30 min)

- [ ] Homepage loads without error
- [ ] Critical user flows tested manually in production
- [ ] Error rate normal — no spike in 5xx errors
- [ ] TTFB normal — no unexpected latency increase
- [ ] Logs checked — no new error patterns
- [ ] Monitoring dashboard checked — all metrics green
- [ ] Cache warming confirmed — hit ratio recovering

---

## Rollback Plan

**Trigger conditions:** <!-- Define when to roll back (e.g., error rate > 2%, TTFB > 3s) -->

**Rollback steps:**

1.
2.
3.

**Rollback owner:** <!-- Name -->
**Estimated rollback time:** <!-- e.g., 10 min -->

---

## Sign-off

| Role | Name | Time |
|------|------|------|
| Release manager | | |
| Tech lead | | |
| QA | | |
