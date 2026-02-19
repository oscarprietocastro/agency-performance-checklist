# 01 - Triage (30 min)

A fast first-pass to identify the most likely cause of a performance problem.

> If you don't have metrics, you don't have a performance problem — you have a feeling.
> First, measure. Then change one thing at a time.
> Do not flush caches until you understand what is happening.

## 1. Confirm the Symptom

- [ ] Is the site slow globally or only for certain URLs?
- [ ] Is it slow for all users or only some (logged-in vs anonymous, specific region)?
- [ ] **Anonymous vs authenticated?** In Drupal, these are completely different cache paths — isolate this first.
- [ ] When did it start? Was there a recent deploy, config change, or traffic spike?
- [ ] Is it a latency issue (slow TTFB) or a rendering issue (slow FCP/LCP)?

## 2. Isolate: CDN vs Origin (5 min)

This is the most important cut. It tells you whether the problem is in the cache layer or the application.

- [ ] Compare TTFB **via CDN** vs **direct to origin** (bypass with `curl -o /dev/null -s -w "%{time_starttransfer}\n"`)
- [ ] Check response headers for cache status: `Age`, `X-Cache`, `CF-Cache-Status`, `X-Varnish`, `HIT/MISS`
- [ ] Bypass the cache on one URL with a query string (`?nocache=1` or a `Cache-Control: no-cache` header) — is the origin itself slow?
- [ ] Segment by route type: Views listing vs node page vs search vs form — which route pattern is slow?

## 3. Check Server Health (5 min)

- [ ] CPU usage — is it spiking?
- [ ] Memory usage — is there pressure or swap in use?
- [ ] Disk I/O — any bottleneck on reads/writes?
- [ ] Active connections — are they at or near the limit?
- [ ] Error rate — are there 500s, 502s, or 504s in the logs?

## 4. Check Cache Hit Rate (5 min)

- [ ] Is the CDN/reverse proxy cache hit rate healthy (>80%)?
- [ ] Is the application-level cache (Redis, Memcached) responding?
- [ ] Has anything caused a full cache flush recently?
- [ ] Are cache headers correct? (`Cache-Control`, `Vary`, `Surrogate-Control`) — a misconfigured `Vary` can prevent caching entirely.

## 5. Check the Database (5 min)

- [ ] Are there long-running queries?
- [ ] Is the DB CPU or memory under pressure?
- [ ] Are connections close to max?

## 6. Identify the Bottleneck

- [ ] Slow TTFB from origin → backend, DB, or application cache problem
- [ ] Slow TTFB only at CDN → CDN misconfiguration, cache miss rate, or Vary header issue
- [ ] Slow after TTFB → frontend assets, render-blocking resources
- [ ] Intermittent slowness → possible memory leak, cron job, or queue buildup
- [ ] Slow only for logged-in users → session handling, personalized blocks, BigPipe not configured

## 7. Immediate Actions

- [ ] Note findings in the [Incident Report](../templates/incident-report.md) if this is an active incident
- [ ] Escalate to [Incident Runbook](08-incident-runbook.md) if the site is down or severely degraded
- [ ] Proceed to [02 - Audit](02-audit-2h.md) for a deeper investigation
