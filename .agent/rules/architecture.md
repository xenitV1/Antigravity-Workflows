# Architecture Rule - System Design

## Activation
- **Mode:** Model Decision
- **Description:** System design and architecture decision guide. Activate for: scalability planning, microservices design, API architecture, database selection, and infrastructure patterns.

---

## Architecture Decision Process

```
1. REQUIREMENTS -> Understand needs
        |
        v
2. CONSTRAINTS -> Identify limitations
        |
        v
3. OPTIONS -> List alternatives
        |
        v
4. TRADE-OFFS -> Analyze trade-offs
        |
        v
5. DECIDE -> Document (ADR)
        |
        v
6. VALIDATE -> Proof of concept
```

---

## Functional vs Non-Functional Requirements

### Functional (What)
- User stories and features
- Core business requirements

### Non-Functional (How)
- **Performance:** P99 latency, concurrent users
- **Availability:** Uptime SLA, RPO/RTO
- **Scalability:** Traffic spikes, horizontal scaling
- **Security:** Compliance (GDPR, PCI-DSS)

---

## Architecture Patterns

### Monolith vs Microservices

| Aspect | Monolith | Microservices |
|--------|----------|---------------|
| Complexity | Low | High |
| Deployment | Single unit | Independent |
| Scaling | Entire app | Per-service |
| Team Size | Small (<10) | Large (>20) |
| Debugging | Easy | Complex |

### Decision Matrix

**Choose Monolith if:**
- Small team (<10 developers)
- MVP/Startup phase
- Domain not yet clear
- Fast iteration needed

**Choose Microservices if:**
- Large team (>20 developers)
- Different scaling needs
- Independent deployment critical
- Polyglot persistence needed

---

## Scalability Patterns

### Horizontal vs Vertical
- **Vertical:** Increase CPU/RAM (limited, simple)
- **Horizontal:** Add more instances (unlimited, requires stateless)

### Caching Strategy
```
CDN -> App Cache (Redis) -> Database
```

**Patterns:**
- Cache-Aside (Lazy Loading)
- Write-Through
- Cache Invalidation

---

## Database Selection

| Criteria | SQL (PostgreSQL) | NoSQL (MongoDB) |
|----------|------------------|-----------------|
| Schema | Fixed | Flexible |
| Relations | Strong (JOIN) | Limited |
| ACID | Full support | Eventual consistency |
| Best For | Complex queries | High write throughput |

---

## Security Architecture

### Defense in Depth
```
WAF/CDN -> API Gateway -> Application -> Data Layer
```

### Zero Trust Principles
1. Never trust, always verify
2. Least privilege access
3. Assume breach

---

## Architecture Decision Record (ADR)

```markdown
# ADR-001: [Title]

## Status
[Proposed/Accepted/Deprecated]

## Context
[Why this decision is needed]

## Decision
[What was decided]

## Consequences
### Positive
- [Benefit 1]

### Negative
- [Tradeoff 1]

### Mitigations
- [How to handle negatives]

## Alternatives Considered
- [Option A - why rejected]

## Date
[YYYY-MM-DD]
```

---

## Capacity Planning

```markdown
## Back-of-Envelope Estimation

### Assumptions
- DAU: 1M users
- Avg requests/user: 20/day
- Peak traffic: 3x average

### Calculations
- Daily requests = 1M x 20 = 20M/day
- RPS (avg) = 20M / 86400 = ~230 RPS
- RPS (peak) = 230 x 3 = ~700 RPS
```

---

## Checklist

- [ ] Requirements (functional & non-functional) documented
- [ ] Trade-offs analyzed
- [ ] Alternatives evaluated
- [ ] ADR written
- [ ] Capacity estimation done
- [ ] Security audit passed
- [ ] PoC/Prototype completed
- [ ] Team review obtained

---

## Don't List

- Over-engineering (YAGNI)
- Premature optimization
- Resume-driven development
- Cargo cult architecture
- Big bang migration
- Single point of failure
- Undocumented decisions

---

**Version:** 2.0 (Antigravity Rule)
