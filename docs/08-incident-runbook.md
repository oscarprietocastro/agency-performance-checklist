# 08 - Incident Runbook

Step-by-step guide for responding to a performance incident.

---

## Phase 1 — Detect & Declare (0–5 min)

1. Confirm the alert is real — check the monitoring dashboard, not just the alert.
2. Open the [Incident Report](../templates/incident-report.md) and start filling it in.
3. Declare the incident in the team channel: state what is happening, severity, and who is leading.
4. Assign roles:
   - **Incident Commander** — coordinates response, communicates status
   - **Technical Lead** — drives diagnosis and fixes
   - **Comms** — updates stakeholders and status page

---

## Phase 2 — Triage (5–15 min)

1. Work through [01 - Triage](01-triage-30min.md) quickly.
2. Answer:
   - Is the site completely down or degraded?
   - Is the problem affecting all users or a subset?
   - What changed recently? (deploys, config, traffic)
3. Identify the most likely cause and focus there first.

---

## Phase 3 — Mitigate (15–60 min)

Apply the fastest mitigation available, not the most correct one.

| Likely cause | Immediate mitigation |
|---|---|
| Bad deploy | Roll back to previous release |
| Cache poisoning | Purge CDN/reverse proxy cache |
| DB overload | Kill long-running queries; scale read replicas |
| Memory exhaustion | Restart app workers; increase memory limit |
| Traffic spike | Enable rate limiting; scale horizontally |
| Third-party outage | Disable or facade the third-party integration |

- [ ] Mitigation applied
- [ ] Impact confirmed reduced or resolved

---

## Phase 4 — Resolve (varies)

1. If mitigation is not a permanent fix, create a follow-up ticket immediately.
2. Apply a permanent fix or confirm the rollback is the correct state.
3. Monitor for 30 min after the fix to confirm stability.

- [ ] Site confirmed stable
- [ ] Follow-up ticket created (if needed)

---

## Phase 5 — Post-Incident (within 24h)

1. Complete the [Incident Report](../templates/incident-report.md).
2. Write a timeline of events.
3. Identify root cause (5 Whys).
4. Document action items to prevent recurrence.
5. Schedule a blameless post-mortem if severity warrants it.

- [ ] Incident report completed
- [ ] Action items assigned with owners and due dates
- [ ] Post-mortem scheduled (if needed)

---

## Severity Definitions

| Level | Definition | Response time |
|---|---|---|
| P1 — Critical | Site down or data loss | Immediate, 24/7 |
| P2 — High | Major feature broken, significant degradation | Within 1 hour |
| P3 — Medium | Degraded performance, workaround exists | Within 4 hours |
| P4 — Low | Minor issue, no user impact | Next business day |
