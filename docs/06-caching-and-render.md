# 06 - Caching & Render

Checklist for cache layers and server-side/client-side rendering.

## HTTP Cache Headers

- [ ] `Cache-Control` set correctly for all response types
  - Static assets: `max-age=31536000, immutable`
  - HTML pages (anonymous): `max-age=300, s-maxage=3600`
  - Authenticated pages: `Cache-Control: private, no-store`
- [ ] `Vary` header is minimal and correct (avoid `Vary: *`)
- [ ] `ETag` or `Last-Modified` present for revalidation
- [ ] `Surrogate-Control` used for CDN-specific TTL where needed

## CDN

- [ ] CDN in front of origin for all public traffic
- [ ] CDN cache hit ratio > 80% for anonymous pages
- [ ] CDN edge nodes in regions matching user geography
- [ ] CDN purge/invalidation tested and working
- [ ] CDN not caching responses with `Set-Cookie` unless intentional
- [ ] CDN origin shield / tiered caching enabled

## Reverse Proxy (Varnish / Nginx)

- [ ] Reverse proxy deployed between CDN and application
- [ ] Cache hit ratio monitored per URL pattern
- [ ] Cache invalidation strategy defined (purge on publish, tag-based, TTL)
- [ ] Grace mode configured — serve stale while revalidating

## Application Cache (Redis / Memcached)

- [ ] Cache backend configured and connected
- [ ] Memory limit set appropriately — no silent eviction under normal load
- [ ] Key TTLs set — no infinite-TTL keys that grow unboundedly
- [ ] Cache stampede protection in place (locking, probabilistic expiry)
- [ ] Cache hit ratio monitored

## Full-Page Cache

- [ ] Full-page cache enabled for anonymous users
- [ ] Logged-in users bypass full-page cache
- [ ] Session cookies excluded or stripped before caching
- [ ] Cache warm-up after deployments

## Object / Fragment Cache

- [ ] Expensive computations cached at the object/fragment level
- [ ] Cache invalidation tied to content changes (tag-based or event-driven)
- [ ] No over-caching of user-specific data in shared caches

## Server-Side Rendering

- [ ] TTFB measured from origin (without CDN) — target < 200ms for cached, < 800ms for uncached
- [ ] Streaming SSR used where framework supports it
- [ ] Partial hydration / islands architecture considered for JS-heavy pages

## Client-Side Rendering

- [ ] First paint not blocked by data fetching
- [ ] Skeleton screens or loading states in place
- [ ] Stale-while-revalidate pattern used in client cache (SWR, React Query)
