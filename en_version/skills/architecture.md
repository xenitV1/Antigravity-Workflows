---
name: architecture
description: System design and architectural decisions guide. Scalability, microservices, API design and infrastructure patterns.
metadata:
  skillport:
    category: thinking
    tags:
      - system-design
      - architecture
      - scalability
      - microservices
---

# Architecture Skill - System Design

> Guide for designing scalable, maintainable and reliable systems.
> Trade-off analysis, pattern selection and architectural decisions.

---

## 🎯 Architectural Decision Process

```
1. REQUIREMENTS → Understand requirements
        │
        ▼
2. CONSTRAINTS → Determine constraints
        │
        ▼
3. OPTIONS → List alternatives
        │
        ▼
4. TRADE-OFFS → Analyze trade-offs
        │
        ▼
5. DECIDE → Document decision (ADR)
        │
        ▼
6. VALIDATE → Proof of concept
```

---

## 📏 Functional vs Non-Functional Requirements

### Functional Requirements (What)

```markdown
## Functional Requirements

### Core Features
- User must be able to register/login
- Product search and filtering
- Add product to cart
- Checkout process

### User Stories
- "As a user, I want to see my order history"
- "As an admin, I want to perform inventory management"
```

### Non-Functional Requirements (How)

```markdown
## Non-Functional Requirements

### Performance
- P99 latency < 200ms
- 10,000 concurrent users
- 1M daily active users

### Availability
- 99.9% uptime (8.76 hours downtime/year)
- RPO: 1 hour (max data loss)
- RTO: 4 hours (max recovery time)

### Scalability
- Handle 10x traffic spike
- Horizontal scaling capability

### Security
- GDPR compliance
- PCI-DSS for payments
- SOC 2 Type II
```

---

## 🏗️ Architecture Patterns

### 1. Monolith vs Microservices

| Aspect | Monolith | Microservices |
|--------|----------|---------------|
| **Complexity** | Low | High |
| **Deployment** | Single unit | Independent services |
| **Scaling** | Entire application | Service-based |
| **Team Size** | Small team | Large, distributed |
| **Initial Cost** | Low | High |
| **Debugging** | Easy | Hard (distributed) |

**Decision Matrix:**
```markdown
CHOOSE Monolith If:
- [ ] Small team (<10 developers)
- [ ] MVP/Startup stage
- [ ] Domain is not clear
- [ ] Rapid iteration required

CHOOSE Microservices If:
- [ ] Large team (>20 developers)
- [ ] Different scaling requirements
- [ ] Independent deployment is critical
- [ ] Polyglot persistence required
```

### 2. Layered Architecture

```
120: ┌─────────────────────────────────────┐
121: │         Presentation Layer          │ ← UI, API endpoints
122: ├─────────────────────────────────────┤
123: │          Application Layer          │ ← Business logic orchestration
124: ├─────────────────────────────────────┤
125: │           Domain Layer              │ ← Core business rules
126: ├─────────────────────────────────────┤
127: │        Infrastructure Layer         │ ← Database, external services
128: └─────────────────────────────────────┘
```

### 3. Event-Driven Architecture

```
134: ┌──────────┐     ┌──────────────┐     ┌────────────┐
135: │ Producer │────▶│ Event Broker │────▶│  Consumer  │
136: │ Service  │     │ (Kafka/SQS)  │     │  Service   │
137: └──────────┘     └──────────────┘     └────────────┘
138:                         │
139:                         ▼
140:               ┌─────────────────┐
141:               │ Event Store     │
142:               │ (Audit/Replay)  │
143:               └─────────────────┘
```

**Use Cases:**
- Async operations (email, notification)
- Audit logging
- System integration
- CQRS implementation

### 4. CQRS (Command Query Responsibility Segregation)

```
155:             ┌─────────────────────────────┐
156:             │         API Gateway         │
157:             └─────────────┬───────────────┘
158:                           │
159:          ┌────────────────┴────────────────┐
160:          │                                 │
161:     ┌────▼────┐                      ┌─────▼─────┐
162:     │ Command │                      │   Query   │
163:     │ Service │                      │  Service  │
164:     └────┬────┘                      └─────┬─────┘
165:          │                                 │
166:     ┌────▼────┐     Events           ┌─────▼─────┐
167:     │  Write  │─────────────────────▶│   Read    │
168:     │   DB    │                      │   DB      │
169:     └─────────┘                      └───────────┘
```

---

## 🔄 Scalability Patterns

### Horizontal vs Vertical Scaling

```markdown
## Vertical Scaling (Scale Up)
- Increasing CPU/RAM
- Single machine limit exists
- May require downtime
- Simple but expensive

## Horizontal Scaling (Scale Out)
- Increasing machine count
- Theoretically unlimited
- Stateless services required
- Load balancer required
```

### Load Balancing

```
195:            ┌───────────────┐
196:            │ Load Balancer │
197:            └───────┬───────┘
198:         ┌──────────┼──────────┐
199:         │          │          │
200:    ┌────▼───┐ ┌────▼───┐ ┌────▼───┐
201:    │ App 1  │ │ App 2  │ │ App 3  │
202:    └────────┘ └────────┘ └────────┘
```

**Algorithms:**
- Round Robin: Distribute in order
- Least Connections: To the one with least connections
- IP Hash: Based on Client IP (sticky)
- Weighted: Weighted distribution

### Caching Strategy

```
214:               ┌─────────┐
215:               │ Client  │
216:               └────┬────┘
217:                    │
218:               ┌────▼────┐
219:               │   CDN   │ ← Static assets
220:               └────┬────┘
221:                    │
222:               ┌────▼────┐
223:               │   App   │
224:               └────┬────┘
225:                    │
226:         ┌──────────┴──────────┐
227:         │                     │
228:    ┌────▼────┐          ┌─────▼────┐
229:    │  Redis  │          │ Database │
230:    │ (Cache) │          │          │
231:    └─────────┘          └──────────┘
```

**Cache Patterns:**
```typescript
// Cache-Aside (Lazy Loading)
async function getUser(id: string) {
  let user = await cache.get(`user:${id}`);
  if (!user) {
    user = await db.user.findById(id);
    await cache.set(`user:${id}`, user, { ex: 3600 });
  }
  return user;
}

// Write-Through
async function updateUser(id: string, data: UpdateUserDto) {
  const user = await db.user.update(id, data);
  await cache.set(`user:${id}`, user);
  return user;
}

// Cache Invalidation
async function deleteUser(id: string) {
  await db.user.delete(id);
  await cache.del(`user:${id}`);
}
```

---

## 🗄️ Database Selection

### SQL vs NoSQL

| Criteria | SQL (PostgreSQL) | NoSQL (MongoDB) |
|----------|------------------|-----------------|
| **Schema** | Fixed | Flexible |
| **Relationships** | Strong (JOIN) | Limited |
| **ACID** | Full support | Eventual consistency |
| **Scaling** | Vertical + Read replicas | Horizontal (sharding) |
| **Best For** | Complex queries, transactions | High write throughput, flexible schema |

**Decision Tree:**
```markdown
CHOOSE PostgreSQL If:
- [ ] Complex JOINs required
- [ ] ACID transactions critical
- [ ] Schema will not change
- [ ] Reporting/analytics

CHOOSE MongoDB If:
- [ ] Flexible schema required
- [ ] High write throughput
- [ ] Document-oriented data
- [ ] Rapid prototyping

CHOOSE Redis If (as cache):
- [ ] Session storage
- [ ] Real-time leaderboards
- [ ] Pub/sub messaging
- [ ] Rate limiting
```

---

## 🔐 Security Architecture

### Defense in Depth

```
302: ┌─────────────────────────────────────────────┐
303: │                 WAF/CDN                     │ ← DDoS, common attacks
304: ├─────────────────────────────────────────────┤
305: │              API Gateway                    │ ← Rate limiting, auth
306: ├─────────────────────────────────────────────┤
307: │          Application Layer                  │ ← Input validation
308: ├─────────────────────────────────────────────┤
309: │             Data Layer                      │ ← Encryption at rest
310: └─────────────────────────────────────────────┘
```

### Zero Trust Architecture

```markdown
## Zero Trust Principles

1. **Never trust, always verify**
   - Every request must be authenticated
   - Network location does not provide trust

2. **Least privilege access**
   - Minimum required authority
   - Just-in-time access

3. **Assume breach**
   - Segmentation
   - Monitoring & anomaly detection
```

---

## 📝 Architecture Decision Record (ADR)

```markdown
# ADR-001: Database Selection

## Status
Accepted

## Context
We need to select the main database for the e-commerce platform.
- 1M+ products
- Complex product-category relationships
- Transaction support for orders

## Decision
We will use PostgreSQL.

## Consequences

### Positive
- Strong relational model
- ACID compliance for orders
- Rich query capabilities
- Mature ecosystem

### Negative
- Horizontal scaling is harder
- Schema changes require migrations

### Mitigations
- Read replicas for scaling reads
- Redis cache for hot data
- Database-per-service if needed later

## Alternatives Considered

### MongoDB
- Rejected: Not suitable for complex JOINs
- Product-category relationships are difficult

### DynamoDB
- Rejected: Lack of query flexibility
- Vendor lock-in

## Date
2025-01-15

## Authors
- @john-doe
- @jane-smith
```

---

## 📊 Capacity Planning

### Back-of-envelope Estimation

```markdown
## Capacity Estimation Example

### Assumptions
- DAU: 1M users
- Avg requests per user: 20/day
- Peak traffic: 3x average

### Calculations
Daily requests = 1M × 20 = 20M requests/day
RPS (average) = 20M / 86400 = ~230 RPS
RPS (peak) = 230 × 3 = ~700 RPS

### Storage
- User data: 1KB × 1M = 1GB
- Products: 10KB × 100K = 1GB
- Orders: 5KB × 10M/year = 50GB/year

### Bandwidth
- Avg response: 10KB
- Daily bandwidth: 20M × 10KB = 200GB/day
```

---

## ✅ Checklist

In every architectural decision:

- [ ] Requirements (functional & non-functional) documented
- [ ] Trade-offs analyzed
- [ ] Alternatives evaluated
- [ ] ADR written
- [ ] Capacity estimation performed
- [ ] Security audit passed
- [ ] PoC/Prototype performed
- [ ] Received team review

---

## 🔴 Don't List

❌ Over-engineering (YAGNI)
❌ Premature optimization
❌ Resume-driven development
❌ Cargo cult architecture
❌ Big bang migration
❌ Single point of failure
❌ Undocumented decisions

---

## ✅ Must Do List

✅ Start simple, evolve
✅ Document decisions (ADR)
✅ Consider failure modes
✅ Plan for observability
✅ Security by design
✅ Test at scale
✅ Review with team
✅ Iterate based on feedback

---

**Last Update:** December 2025
**Version:** 1.0
