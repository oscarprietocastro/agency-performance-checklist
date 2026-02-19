# 02 - Performance Audit (2h)

A structured deep-dive audit to be run during a scheduled performance review or after triage identifies a problem.

## 1. Baseline Metrics (15 min)

- [ ] Run Lighthouse (mobile + desktop) on the homepage and a key interior page
- [ ] Record: LCP, FID/INP, CLS, TTFB, FCP, TBT
- [ ] Run WebPageTest from a representative location with a representative connection
- [ ] Record waterfall and identify the critical path

## 2. Network & Asset Audit (20 min)

- [ ] Total page weight — is it above 1MB (mobile) or 2MB (desktop)?
- [ ] Images — are they properly sized, compressed, and in modern formats (WebP/AVIF)?
- [ ] Are render-blocking scripts and stylesheets deferred or async?
- [ ] Is the critical CSS inlined?
- [ ] Are web fonts optimized (font-display, preload, subsetting)?
- [ ] HTTP/2 or HTTP/3 enabled?
- [ ] Are all static assets served with long-lived cache headers?
- [ ] Is there unnecessary third-party script loading?

## 3. Backend & TTFB Audit (20 min)

- [ ] Measure TTFB for key pages — typical healthy range: ~200ms cached at edge, ~400–800ms uncached origin (varies by stack and geography; treat these as guidelines, not hard targets)
- [ ] Profile server-side response time with APM or Xhprof/Blackfire
- [ ] Check for N+1 query patterns
- [ ] Check for missing indexes on common query patterns
- [ ] Review slow query log

## 4. Cache Layer Audit (15 min)

- [ ] CDN cache hit ratio per URL group
- [ ] Reverse proxy (Varnish/Nginx) hit ratio
- [ ] Application cache (Redis/Memcached) hit ratio and memory usage
- [ ] Verify cache headers: `Cache-Control`, `Vary`, `Surrogate-Control`
- [ ] Check `Vary` header — a single unwanted entry (e.g., `Vary: Cookie` on public pages) can destroy cache efficiency

## 5. Frontend Runtime Audit (20 min)

- [ ] Check JavaScript bundle size — any chunks over 250KB (uncompressed)?
- [ ] Identify long tasks (>50ms) in Chrome DevTools Performance tab
- [ ] Check for layout thrashing or excessive reflows
- [ ] Are lazy loading and code splitting in use?

## 6. Infrastructure Audit (10 min)

- [ ] Is the server sized appropriately for current traffic?
- [ ] Are there auto-scaling rules or capacity limits that may be too tight?
- [ ] Is the database on the same network as the app server (low-latency connection)?

## 7. What Not To Do

Mistakes that waste time or make things worse during an audit:

- **Don't flush caches repeatedly** to test — one flush per hypothesis, then measure.
- **Don't enable Devel, Kint, or WebProfiler on production** — even briefly. They leak memory and slow every request.
- **Don't change two things at once** — you won't know what helped.
- **Don't trust Lighthouse on a localhost tunnel** (ngrok, etc.) — results are unreliable. Use staging with production-like infrastructure.
- **Don't optimize based on a single data point** — take at least 3 measurements and check real-user data (CrUX) alongside lab data.

## 8. Document Findings

- [ ] Fill in the [Performance Audit Report](../templates/performance-audit-report.md)
- [ ] Prioritize findings by impact vs. effort
- [ ] Refer to [03 - Quick Wins](03-fixes-quick-wins.md) for immediate improvements
