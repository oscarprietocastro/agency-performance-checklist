# 04 - Drupal Specific

Performance checks specific to Drupal 9/10/11 sites.

> The most common pattern: a View added "just for admins" becomes a public listing
> and takes the site down under traffic. Always check Views cache settings.

## Common Drupal Killers

These patterns account for the majority of performance issues seen on Drupal agency projects. Check these before anything else.

- **Views with relationships + DISTINCT + aggregation** — nearly always produces a slow query. Run `EXPLAIN` on the generated SQL. Add indexes or rewrite the query in a custom module.
- **Cache contexts exploding variation** — using `user`, `url`, or `languages` as cache contexts on high-traffic blocks means Drupal builds and stores a unique render for every combination. Audit cache contexts on every block and View display.
- **Entity loads in Twig or preprocess** — `node_load()` or `\Drupal::entityTypeManager()->getStorage()->load()` inside a template or `hook_preprocess_*` is N+1 in disguise. Load entities in bulk upstream or use lazy builders.
- **Webform with large submission tables** — if `webform_submission` has millions of rows without archival, queries against it slow down. Check table size and add a submission purge policy.
- **Paragraphs / Layout Builder with deep nesting** — 3+ levels of nested Paragraphs with per-paragraph entity loads can make a single node page fire 50+ queries. Profile with Blackfire or WebProfiler before launch.
- **dblog on production** — every 404, every slow query, every warning is written to the database. Switch to syslog + an external log aggregator. `dblog` is for development only.
- **Cron running on web requests** — if `automated_cron` module is enabled, cron runs inside normal page requests. Disable it and run `drush cron` externally.
- **migrate_* modules left installed** — they add hooks and overhead to every entity operation even when not actively migrating.

## Core Configuration

- [ ] Production mode enabled (`sites/default/settings.php`)
- [ ] `$config['system.performance']['css']['preprocess']` = TRUE
- [ ] `$config['system.performance']['js']['preprocess']` = TRUE
- [ ] Twig cache enabled and debug mode off
- [ ] Render cache enabled
- [ ] Dynamic Page Cache enabled
- [ ] Internal Page Cache enabled (for anonymous users)
- [ ] BigPipe enabled (for authenticated users)

## Cache

- [ ] Redis or Memcached configured as cache backend
- [ ] Cache tags invalidation working correctly (test: edit a node, confirm CDN/Varnish purges)
- [ ] Views cache configured per view — both **results** and **rendered output** TTLs set
- [ ] Block cache configured per block
- [ ] Cache contexts reviewed on every block — remove any context that isn't strictly necessary
- [ ] No development modules enabled on production (Devel, Kint, WebProfiler, etc.)

## Database

- [ ] Database queries profiled with Devel or WebProfiler (staging only, never production)
- [ ] No N+1 queries in entity loads — use `entity_load_multiple` and `loadMultiple`
- [ ] Views using aggregation where possible instead of loading full entities
- [ ] Custom modules using static caching (`drupal_static`) for repeated lookups
- [ ] Core database log (`dblog`) replaced with `syslog` or external logging

## Modules

- [ ] Unused modules uninstalled (not just disabled — uninstalled)
- [ ] Heavy contrib modules evaluated: Paragraphs nesting depth, Layout Builder complexity
- [ ] Search module replaced with Solr or Elasticsearch for content sets above ~5000 nodes
- [ ] Migrate modules uninstalled after migrations are complete
- [ ] `automated_cron` module disabled — external cron only

## Theme & Rendering

- [ ] Theme debug mode off on production
- [ ] Aggregated CSS/JS enabled
- [ ] Asset libraries reviewed — no global libraries loading on every page unnecessarily
- [ ] Lazy builders used for personalized or session-dependent blocks
- [ ] Image styles configured for all image fields (original-size images never served to end users)

## Cron & Queues

- [ ] Cron not running on web requests (`drush cron` or external scheduler)
- [ ] Queue workers configured and processing (advancedqueue or core queue)
- [ ] Scheduled cron jobs timed to off-peak hours

## Hosting

- [ ] PHP OPcache tuned for Drupal's file count (`opcache.max_accelerated_files` ≥ 20000)
- [ ] PHP-FPM pool sized appropriately
- [ ] Reverse proxy (Varnish/Nginx) aware of Drupal cache tags (purge module + purger configured)
- [ ] CDN configured to strip cookies for anonymous pages
