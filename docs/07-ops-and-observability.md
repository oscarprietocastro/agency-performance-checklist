# 07 - Ops & Observability

Checklist for monitoring, alerting, and operational readiness.

## Metrics Collection

- [ ] Server metrics collected (CPU, memory, disk, network) — Prometheus, Datadog, CloudWatch
- [ ] Application metrics collected (request rate, error rate, latency)
- [ ] Database metrics collected (queries/sec, slow queries, connections, replication lag)
- [ ] Cache metrics collected (hit ratio, memory usage, evictions)
- [ ] CDN metrics collected (hit ratio, bandwidth, error rate)

## Dashboards

- [ ] System health dashboard exists and is up to date
- [ ] Application performance dashboard (RPS, latency percentiles, error rate)
- [ ] Core Web Vitals dashboard (LCP, INP, CLS) — real user data preferred
- [ ] Business metrics dashboard (conversions, signups) correlated with performance

## Alerting

- [ ] Alert on high error rate (> 1% 5xx for > 2 min)
- [ ] Alert on high latency (p95 > threshold for > 2 min)
- [ ] Alert on low cache hit ratio
- [ ] Alert on DB connection saturation (> 80% of max)
- [ ] Alert on disk space (> 80% used)
- [ ] Alert on certificate expiry (> 30 days warning)
- [ ] Alerts routed to the correct on-call channel (PagerDuty, Slack, etc.)

## Logging

- [ ] Application logs centralized (ELK, Loki, Datadog Logs)
- [ ] Log levels appropriate for production (no DEBUG in production)
- [ ] Error logs include stack traces and request context
- [ ] Access logs include response time and cache status
- [ ] Log retention policy defined

## APM & Profiling

- [ ] APM agent installed (New Relic, Datadog APM, Elastic APM, Blackfire)
- [ ] Distributed tracing enabled across services
- [ ] Profiling data collected for slow transactions
- [ ] Synthetic monitoring in place for critical user flows

## Uptime & Availability

- [ ] External uptime monitoring active (Pingdom, UptimeRobot, Better Uptime)
- [ ] Monitoring from multiple geographic regions
- [ ] Status page available for stakeholders
- [ ] On-call rotation defined and documented

## Runbooks

- [ ] Runbook exists for each class of common incident
- [ ] Runbooks linked from alert notifications
- [ ] Runbooks reviewed and tested in the last 6 months
- [ ] See [08 - Incident Runbook](08-incident-runbook.md)
