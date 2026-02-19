# 00 - How to Use This Checklist

## Purpose

This checklist is designed for agency teams responding to performance problems on Drupal platforms — from the first alert to the post-incident sign-off.

> If you don't have metrics, you don't have a performance problem — you have a feeling.
> First, measure. Then change one thing at a time.

## When to Use Each Document

| Situation | Start here |
|-----------|-----------|
| Site is slow right now | [01 - Triage](01-triage-30min.md) |
| Scheduled performance audit | [02 - Audit](02-audit-2h.md) |
| Need fast improvements | [03 - Quick Wins](03-fixes-quick-wins.md) |
| Drupal-specific issues | [04 - Drupal Specific](04-drupal-specific.md) |
| Slow queries / DB load | [05 - Database & Queries](05-database-and-queries.md) |
| Cache misses / TTFB high | [06 - Caching & Render](06-caching-and-render.md) |
| Setting up monitoring | [07 - Ops & Observability](07-ops-and-observability.md) |
| Active incident | [08 - Incident Runbook](08-incident-runbook.md) |
| Pre-launch or sign-off | [09 - Acceptance & Metrics](09-acceptance-and-metrics.md) |

## How to Run an Audit

1. Clone or copy this repo into the project documentation.
2. Work through the relevant checklist sections top to bottom.
3. Mark items `[x]` as you complete or verify them.
4. Fill in the [Performance Audit Report](../templates/performance-audit-report.md) with findings.
5. Share the report with the client and team.

## Conventions

- `[ ]` — Not checked / not done
- `[x]` — Verified / completed
- `[~]` — Partially done or needs follow-up
- `[N/A]` — Not applicable to this project

## A note on process

Performance work goes wrong in predictable ways. The two most common:

1. **Changing things without measuring first.** You flush caches, restart PHP-FPM, bump memory limits — and the site feels better, but you don't know why or whether it will hold.
2. **Changing two things at once.** You can't attribute the improvement and you can't reproduce the fix reliably.

Work one hypothesis at a time. Record the baseline. Record the result. Then move on.

## Contributing

Found a missing check or a better approach? Open a PR or file an issue.
