---
name: architecture
description: Sistem tasarımı ve mimari kararlar rehberi. Scalability, microservices, API design ve infrastructure patterns.
metadata:
  skillport:
    category: thinking
    tags:
      - system-design
      - architecture
      - scalability
      - microservices
---

# Architecture Skill - Sistem Tasarımı

> Ölçeklenebilir, bakımı kolay ve güvenilir sistemler tasarlama rehberi.
> Trade-off analizi, pattern seçimi ve mimari kararlar.

---

# 📋 İçindekiler

1. [Mimari Karar Süreci](#1-mimari-karar-süreci)
2. [Functional vs Non-Functional Requirements](#2-functional-vs-non-functional-requirements)
3. [Architecture Patterns](#3-architecture-patterns)
4. [Scalability Patterns](#4-scalability-patterns)
5. [Database Selection](#5-database-selection)
6. [Security Architecture](#6-security-architecture)
7. [Architecture Decision Record (ADR)](#7-architecture-decision-record-adr)
8. [Capacity Planning](#8-capacity-planning)
9. [Kontrol Listesi](#9-kontrol-listesi)
10. [Yapma Listesi](#10-yapma-listesi)
11. [Mutlaka Yap Listesi](#11-mutlaka-yap-listesi)

---

# 1. Mimari Karar Süreci

```
1. REQUIREMENTS → Gereksinimleri anla
        │
        ▼
2. CONSTRAINTS → Kısıtları belirle
        │
        ▼
3. OPTIONS → Alternatifleri listele
        │
        ▼
4. TRADE-OFFS → Trade-off'ları analiz et
        │
        ▼
5. DECIDE → Kararı belgele (ADR)
        │
        ▼
6. VALIDATE → Proof of concept
```

---

# 2. Functional vs Non-Functional Requirements

## 2.1 Functional Requirements (What)

```markdown
## Functional Requirements

### Core Features
- Kullanıcı kayıt/giriş yapabilmeli
- Ürün arama ve filtreleme
- Sepete ürün ekleme
- Ödeme işlemi

### User Stories
- "Kullanıcı olarak sipariş geçmişimi görmek istiyorum"
- "Admin olarak stok yönetimi yapmak istiyorum"
```

## 2.2 Non-Functional Requirements (How)

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

# 3. Architecture Patterns

## 3.1 Monolith vs Microservices

| Aspect | Monolith | Microservices |
|--------|----------|---------------|
| **Complexity** | Düşük | Yüksek |
| **Deployment** | Tek unit | Bağımsız servisler |
| **Scaling** | Tüm uygulama | Service bazlı |
| **Team Size** | Küçük takım | Büyük, dağıtık |
| **Initial Cost** | Düşük | Yüksek |
| **Debugging** | Kolay | Zor (distributed) |

**Karar Matrisi:**
```markdown
Monolith SEÇSEN Eğer:
- [ ] Küçük takım (<10 developer)
- [ ] MVP/Startup aşaması
- [ ] Domain net değil
- [ ] Hızlı iteration gerekli

Microservices SEÇSEN Eğer:
- [ ] Büyük takım (>20 developer)
- [ ] Farklı scaling gereksinimleri
- [ ] Bağımsız deployment kritik
- [ ] Polyglot persistence gerekli
```

## 3.2 Layered Architecture

```
┌─────────────────────────────────────┐
│         Presentation Layer          │ ← UI, API endpoints
├─────────────────────────────────────┤
│          Application Layer          │ ← Business logic orchestration
├─────────────────────────────────────┤
│           Domain Layer              │ ← Core business rules
├─────────────────────────────────────┤
│        Infrastructure Layer         │ ← Database, external services
└─────────────────────────────────────┘
```

## 3.3 Event-Driven Architecture

```
┌──────────┐     ┌──────────────┐     ┌────────────┐
│ Producer │────▶│ Event Broker │────▶│  Consumer  │
│ Service  │     │ (Kafka/SQS)  │     │  Service   │
└──────────┘     └──────────────┘     └────────────┘
                        │
                        ▼
               ┌─────────────────┐
               │ Event Store     │
               │ (Audit/Replay)  │
               └─────────────────┘
```

**Kullanım Alanları:**
- Async işlemler (email, notification)
- Audit logging
- System integration
- CQRS implementation

## 3.4 CQRS (Command Query Responsibility Segregation)

```
            ┌─────────────────────────────┐
            │         API Gateway         │
            └─────────────┬───────────────┘
                          │
         ┌────────────────┴────────────────┐
         │                                 │
    ┌────▼────┐                      ┌─────▼─────┐
    │ Command │                      │   Query   │
    │ Service │                      │  Service  │
    └────┬────┘                      └─────┬─────┘
         │                                 │
    ┌────▼────┐     Events           ┌─────▼─────┐
    │  Write  │─────────────────────▶│   Read    │
    │   DB    │                      │   DB      │
    └─────────┘                      └───────────┘
```

---

# 4. Scalability Patterns

## 4.1 Horizontal vs Vertical Scaling

```markdown
## Vertical Scaling (Scale Up)
- CPU/RAM artırma
- Tek makine limiti var
- Downtime gerektirebilir
- Basit ama pahalı

## Horizontal Scaling (Scale Out)
- Makine sayısı artırma
- Teorik olarak sınırsız
- Stateless servisler gerekli
- Load balancer gerekli
```

## 4.2 Load Balancing

```
            ┌───────────────┐
            │ Load Balancer │
            └───────┬───────┘
         ┌──────────┼──────────┐
         │          │          │
    ┌────▼───┐ ┌────▼───┐ ┌────▼───┐
    │ App 1  │ │ App 2  │ │ App 3  │
    └────────┘ └────────┘ └────────┘
```

**Algorithms:**
- Round Robin: Sırayla dağıt
- Least Connections: En az bağlantılı olana
- IP Hash: Client IP'ye göre (sticky)
- Weighted: Ağırlıklı dağıtım

## 4.3 Caching Strategy

```
               ┌─────────┐
               │ Client  │
               └────┬────┘
                    │
               ┌────▼────┐
               │   CDN   │ ← Static assets
               └────┬────┘
                    │
               ┌────▼────┐
               │   App   │
               └────┬────┘
                    │
         ┌──────────┴──────────┐
         │                     │
    ┌────▼────┐          ┌─────▼────┐
    │  Redis  │          │ Database │
    │ (Cache) │          │          │
    └─────────┘          └──────────┘
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

# 5. Database Selection

## 5.1 SQL vs NoSQL

| Criteria | SQL (PostgreSQL) | NoSQL (MongoDB) |
|----------|------------------|-----------------|
| **Schema** | Fixed | Flexible |
| **Relationships** | Strong (JOIN) | Limited |
| **ACID** | Full support | Eventual consistency |
| **Scaling** | Vertical + Read replicas | Horizontal (sharding) |
| **Best For** | Complex queries, transactions | High write throughput, flexible schema |

**Karar Matrisi:**
```markdown
PostgreSQL SEÇSEN Eğer:
- [ ] Complex JOINs gerekli
- [ ] ACID transactions kritik
- [ ] Schema değişmeyecek
- [ ] Reporting/analytics

MongoDB SEÇSEN Eğer:
- [ ] Flexible schema gerekli
- [ ] High write throughput
- [ ] Document-oriented data
- [ ] Rapid prototyping

Redis SEÇSEN Eğer (cache olarak):
- [ ] Session storage
- [ ] Real-time leaderboards
- [ ] Pub/sub messaging
- [ ] Rate limiting
```

---

# 6. Security Architecture

## 6.1 Defense in Depth

```
┌─────────────────────────────────────────────┐
│                 WAF/CDN                     │ ← DDoS, common attacks
├─────────────────────────────────────────────┤
│              API Gateway                    │ ← Rate limiting, auth
├─────────────────────────────────────────────┤
│          Application Layer                  │ ← Input validation
├─────────────────────────────────────────────┤
│             Data Layer                      │ ← Encryption at rest
└─────────────────────────────────────────────┘
```

## 6.2 Zero Trust Architecture

```markdown
## Zero Trust Principles

1. **Never trust, always verify**
   - Her request authenticate edilmeli
   - Network location güven vermiyor

2. **Least privilege access**
   - Minimum gerekli yetki
   - Just-in-time access

3. **Assume breach**
   - Segmentation
   - Monitoring & anomaly detection
```

---

# 7. Architecture Decision Record (ADR)

```markdown
# ADR-001: Database Selection

## Status
Accepted

## Context
E-commerce platformu için ana veritabanı seçmemiz gerekiyor.
- 1M+ ürün
- Complex product-category relationships
- Transaction support for orders

## Decision
PostgreSQL kullanacağız.

## Consequences

### Positive
- Strong relational model
- ACID compliance for orders
- Rich query capabilities
- Mature ecosystem

### Negative
- Horizontal scaling daha zor
- Schema changes require migrations

### Mitigations
- Read replicas for scaling reads
- Redis cache for hot data
- Database-per-service if needed later

## Alternatives Considered

### MongoDB
- Rejected: Complex JOINs için uygun değil
- Product-category relationships zor

### DynamoDB
- Rejected: Query flexibility eksikliği
- Vendor lock-in

## Date
2025-01-15

## Authors
- @john-doe
- @jane-smith
```

---

# 8. Capacity Planning

## 8.1 Back-of-envelope Estimation

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

# 9. Kontrol Listesi

Her mimari kararda:

- [ ] Requirements (functional & non-functional) belgelendi
- [ ] Trade-off'lar analiz edildi
- [ ] Alternatifler değerlendirildi
- [ ] ADR yazıldı
- [ ] Capacity estimation yapıldı
- [ ] Security audit geçti
- [ ] PoC/Prototype yapıldı
- [ ] Team review aldı

---

# 10. Yapma Listesi

❌ Over-engineering (YAGNI)
❌ Premature optimization
❌ Resume-driven development
❌ Cargo cult architecture
❌ Big bang migration
❌ Single point of failure
❌ Undocumented decisions

---

# 11. Mutlaka Yap Listesi

✅ Start simple, evolve
✅ Document decisions (ADR)
✅ Consider failure modes
✅ Plan for observability
✅ Security by design
✅ Test at scale
✅ Review with team
✅ Iterate based on feedback

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 2.0
