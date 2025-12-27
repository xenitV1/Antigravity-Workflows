# Optimization Rule - System & Flow Performance

## Activation
- **Mode:** Model Decision
- **Description:** System and user flow optimization methodology. Activate for: performance issues, bottleneck identification, user experience optimization, and observability setup.

---

## Optimization Principles (2025)

| Principle | Description |
|-----------|-------------|
| Measurement Over Guessing | You can't optimize what you don't measure |
| 80/20 Rule (Pareto) | 80% of problems come from 20% of code |
| Don't Optimize Early | First make it work, then right, then fast |
| User-Centric Metrics | Perceived performance matters, not just speed |
| AI-Assisted Analysis | Use AI tools for complex data analysis |

---

## Bottleneck Identification

### Systematic Detection Steps

1. **Profiling:** Identify CPU/Memory consuming code
2. **Tracing:** Follow request journey across systems
3. **Log Analysis:** Find error and slowness patterns
4. **User Flow Analysis:** Detect where users struggle

### Bottleneck Indicators

| Indicator | Possible Cause |
|-----------|----------------|
| CPU Spikes | Heavy computation, infinite loops |
| Memory Leaks | Growing memory that never decreases |
| High Latency | Database queries, external APIs |
| Lock Contention | Concurrency resource waiting |

---

## AI-Driven Optimization (2025)

- **AI Profiling:** AI tools predict performance issues
- **Automated Refactoring:** AI suggests cleaner & faster code
- **Predictive Scaling:** Forecast future load, prepare infrastructure

---

## Modern Observability

### Three Pillars

| Pillar | Description |
|--------|-------------|
| Metrics | Time-based numerical data (RPS, latency) |
| Traces | Single request journey (distributed tracing) |
| Logs | Detailed event records |

### Tools

- **Prometheus & Grafana:** Metric visualization
- **Jaeger/Zipkin:** Distributed tracing
- **New Relic / Datadog:** Full-stack APM

---

## Frontend Optimization

### Core Web Vitals (2025)

| Metric | Description | Target |
|--------|-------------|--------|
| LCP | Largest Contentful Paint | < 2.5s |
| INP | Interaction to Next Paint | < 200ms |
| CLS | Cumulative Layout Shift | < 0.1 |

### Techniques

- **SSR/SSG:** Server-side rendering, static generation
- **Image Optimization:** WebP/AVIF, lazy loading
- **Bundle Splitting:** Tree shaking, code splitting
- **CDN:** Static asset delivery

---

## Backend Optimization

### Database Query Optimization

| Technique | Benefit |
|-----------|---------|
| Indexing | Can improve query speed 100x |
| N+1 Avoidance | Use joins/includes instead of loops |
| Query Caching | Cache frequently accessed data (Redis) |
| Connection Pooling | Reuse database connections |

### Async Processing

- Move time-consuming tasks to background jobs
- Use message queues (Redis, RabbitMQ)
- Implement proper job retry logic

---

## Systematic Improvement Cycle

```
Measure -> Analyze -> Optimize -> Verify -> Repeat
```

1. **Measure:** Establish baseline metrics
2. **Analyze:** Find bottleneck and root cause
3. **Optimize:** Make highest-impact change
4. **Verify:** Confirm improvement (no regression)

---

## Performance Budget

### Frontend
```
Total bundle: < 200KB (gzipped)
Initial load: < 3 seconds (3G)
Time to Interactive: < 5 seconds
```

### Backend
```
API response: P95 < 200ms
Database query: < 100ms
Memory per request: < 50MB
```

---

## Profiling Commands

### Node.js
```bash
# CPU profiling
node --prof app.js
node --prof-process isolate-*.log

# Memory
node --inspect app.js
# Use Chrome DevTools Memory tab
```

### Database
```sql
-- PostgreSQL
EXPLAIN ANALYZE SELECT * FROM users WHERE id = 1;

-- Index suggestions
SELECT * FROM pg_stat_user_indexes;
```

---

## Caching Strategy

### Cache Layers
```
Client Cache -> CDN -> App Cache (Redis) -> Database
```

### Cache Patterns
```typescript
// Cache-Aside
async function getUser(id: string) {
  let user = await cache.get(`user:${id}`);
  if (!user) {
    user = await db.user.findById(id);
    await cache.set(`user:${id}`, user, { ex: 3600 });
  }
  return user;
}
```

### Cache Invalidation
- TTL (Time-to-Live) based
- Event-based invalidation
- Write-through updates

---

## Checklist

- [ ] Bottleneck verified with metrics?
- [ ] No premature optimization?
- [ ] Rollback plan ready?
- [ ] Perceived performance measured?
- [ ] No new bottleneck created?
- [ ] Regression tests passed?

---

## Don't List

- Change code without measuring
- Decide based on benchmarks alone (need real user data)
- Optimize too many things at once
- Sacrifice readability for "faster" code
- Skip baseline measurement

---

## Must Do List

- Focus on 80/20 rule: optimize most-used flows
- Use OpenTelemetry standards for observability
- Leverage AI tools for pattern detection
- Address perceived slowness with user flow analysis
- Run regression tests after every optimization
- Document performance improvements

---

**Version:** 2.0 (Antigravity Rule)
