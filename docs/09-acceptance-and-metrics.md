# 09 - Acceptance & Metrics

Sign-off criteria and performance KPIs for launch and ongoing health.

## Core Web Vitals Targets

| Metric | Good | Needs Improvement | Poor |
|--------|------|-------------------|------|
| LCP (Largest Contentful Paint) | ≤ 2.5s | 2.5s – 4.0s | > 4.0s |
| INP (Interaction to Next Paint) | ≤ 200ms | 200ms – 500ms | > 500ms |
| CLS (Cumulative Layout Shift) | ≤ 0.1 | 0.1 – 0.25 | > 0.25 |
| TTFB (Time to First Byte) | ≤ 800ms | 800ms – 1800ms | > 1800ms |
| FCP (First Contentful Paint) | ≤ 1.8s | 1.8s – 3.0s | > 3.0s |

**Target: all key pages in the "Good" range for the 75th percentile of real users.**

## Lighthouse Score Targets

| Category | Minimum | Target |
|----------|---------|--------|
| Performance | 70 | 90+ |
| Accessibility | 90 | 95+ |
| Best Practices | 90 | 95+ |
| SEO | 90 | 95+ |

## Backend Performance Targets

- [ ] TTFB from origin (uncached) < 800ms for 95th percentile
- [ ] TTFB from CDN (cached) < 200ms for 95th percentile
- [ ] No database query > 500ms in normal operation
- [ ] Error rate < 0.1% over a 24h period
- [ ] Uptime > 99.9% (< 8.7h downtime per year)

## Asset Budget

| Asset type | Maximum (per page) |
|---|---|
| Total page weight | 1.5MB |
| Images | 1MB |
| JavaScript (uncompressed) | 300KB |
| CSS (uncompressed) | 100KB |
| Web fonts | 100KB |

## Pre-Launch Acceptance Checklist

- [ ] All Core Web Vitals in "Good" range on mobile and desktop
- [ ] Lighthouse scores meet minimums on homepage and 3 representative pages
- [ ] Load test run at 2x expected peak traffic with no degradation
- [ ] Cache hit ratio > 80% for anonymous pages after warm-up
- [ ] Monitoring and alerting confirmed active
- [ ] Runbooks reviewed and updated
- [ ] Rollback plan documented and tested
- [ ] Client or product owner sign-off obtained

## Ongoing Monitoring KPIs

Review these monthly or after major releases:

- [ ] Core Web Vitals trend (CrUX data — real users)
- [ ] p50 / p75 / p95 server response time
- [ ] Cache hit ratios (CDN, reverse proxy, application)
- [ ] Error rate and top error types
- [ ] Slow query count and top offenders
- [ ] Page weight trend (regression check)
