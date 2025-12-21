---
name: production-deployment
description: Güvenli production deployment rehberi. DevSecOps, CI/CD, progressive delivery ve 2025 güvenlik standartları.
metadata:
  skillport:
    category: operations
    tags:
      - devops
      - ci-cd
      - deployment
      - security
      - monitoring
---

# Production Deployment Skill

> Güvenli ve güvenilir production deployment metodolojisi.
> DevSecOps, CI/CD pipeline güvenliği ve progressive delivery.

---

# 📋 İçindekiler

1. [Deployment Prensipleri](#1-deployment-prensipleri)
2. [Pre-Deployment Kontrol Listesi](#2-pre-deployment-checklist)
3. [CI/CD Pipeline](#3-cicd-pipeline)
4. [Deployment Stratejileri](#4-deployment-stratejileri-deployment-strategies)
    - [4.1 Blue-Green Deployment](#41-blue-green-deployment)
    - [4.2 Canary Deployment](#42-canary-deployment)
    - [4.3 Feature Flags](#43-feature-flags)
5. [Monitoring & Observability](#5-monitoring--observability)
6. [Rollback Stratejisi](#6-rollback-strategy)
7. [Deployment Kontrol Listesi](#7-deployment-kontrol-listesi)
8. [Mutlaka Yap Listesi](#8-mutlaka-yap-listesi)

---

# 1. Deployment Prensipleri

| Prensip | Açıklama |
|---------|----------|
| **Automate Everything** | Manuel adım = Hata riski |
| **Shift-Left Security** | Güvenlik en baştan |
| **Progressive Delivery** | Kademeli rollout |
| **Immutable Infrastructure** | Değiştir değil, değiştir |
| **Everything as Code** | Config, infra, policy = Code |
| **Fail Fast, Rollback Faster** | Hızlı tespit, hızlı geri al |

---

# 2. Pre-Deployment Checklist

## 2.1 Kod Kalitesi

```markdown
### Code Quality
- [ ] Tüm testler geçiyor (unit, integration, e2e)
- [ ] Test coverage threshold karşılanıyor (>80%)
- [ ] Lint hatası yok
- [ ] TypeScript type error yok
- [ ] Build başarılı

### Security
- [ ] Dependency audit yapıldı (npm audit)
- [ ] SAST (Static Analysis) geçti
- [ ] Secrets hardcoded değil
- [ ] OWASP Top 10 kontrol edildi

### Code Review
- [ ] En az 1 approval alındı
- [ ] Tüm review yorumları addressed
- [ ] Merge conflict yok

### Documentation
- [ ] Breaking changes belgelendi
- [ ] API changes update edildi
- [ ] Changelog güncellendi
```

## 2.2 Database Migrations

```markdown
### Database Migration Checklist

- [ ] Migration backward compatible
- [ ] Rollback script hazır
- [ ] Migration test ortamında çalıştırıldı
- [ ] Performance impact değerlendirildi
- [ ] Downtime gerekiyorsa planlandı
```

---

# 3. CI/CD Pipeline

## 3.1 GitHub Actions Örneği

```yaml
# .github/workflows/deploy.yml
name: Deploy to Production

on:
  push:
    branches: [main]

env:
  NODE_VERSION: '20'

jobs:
  # 1. Test & Build
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Lint
        run: npm run lint
      
      - name: Type check
        run: npm run type-check
      
      - name: Unit tests
        run: npm run test:unit -- --coverage
      
      - name: Integration tests
        run: npm run test:integration

  # 2. Security Scan
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Run Snyk to check for vulnerabilities
        uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      
      - name: Run Trivy vulnerability scanner
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: 'fs'
          severity: 'CRITICAL,HIGH'

  # 3. Build
  build:
    needs: [test, security]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Build
        run: npm run build
      
      - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: build
          path: dist/

  # 4. Deploy (with approval)
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment: production  # Requires approval
    steps:
      - name: Download artifact
        uses: actions/download-artifact@v4
        with:
          name: build
      
      - name: Deploy to production
        run: |
          # Deploy command here
          echo "Deploying to production..."
```

## 3.2 Pipeline Security

### Secret Management

```yaml
# ✅ DOĞRU: GitHub Secrets kullan
env:
  DATABASE_URL: ${{ secrets.DATABASE_URL }}
  API_KEY: ${{ secrets.API_KEY }}

# ❌ YANLIŞ: Hardcoded secrets
env:
  API_KEY: "sk-12345..."  # ASLA!
```

### OIDC Federation (Secretless)

```yaml
# AWS OIDC - No static credentials
jobs:
  deploy:
    permissions:
      id-token: write
      contents: read
    steps:
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: arn:aws:iam::123456789:role/GitHubActionsRole
          aws-region: eu-west-1
```

### Dependency Security

```yaml
# Automated dependency updates
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: npm
    directory: "/"
    schedule:
      interval: weekly
    open-pull-requests-limit: 10
    ignore:
      - dependency-name: "*"
        update-types: ["version-update:semver-major"]
```

---

# 4. Deployment Stratejileri (Deployment Strategies)

## 4.1 Blue-Green Deployment

```
                    Load Balancer
                         │
            ┌────────────┴────────────┐
            │                         │
     ┌──────▼──────┐          ┌───────▼─────┐
     │   BLUE      │          │   GREEN     │
     │  (Current)  │          │   (New)     │
     │   v1.0      │          │   v1.1      │
     └─────────────┘          └─────────────┘

1. Green'e deploy et
2. Green'i test et
3. Traffic'i Green'e yönlendir
4. Blue'yu standby tut (rollback için)
```

## 4.2 Canary Deployment

```
                    Load Balancer
                         │
              ┌──────────┴──────────┐
              │                     │
       ┌──────▼──────┐      ┌───────▼─────┐
       │   STABLE    │      │   CANARY    │
       │    95%      │      │     5%      │
       │   v1.0      │      │   v1.1      │
       └─────────────┘      └─────────────┘

1. Canary'ye deploy et (5% traffic)
2. Metrikleri izle
3. Sorun yoksa traffic'i artır (10%, 25%, 50%, 100%)
4. Sorun varsa geri al
```

## 4.3 Feature Flags

```typescript
// Feature flag implementation
import { featureFlags } from './lib/feature-flags';

async function processOrder(order: Order) {
  if (await featureFlags.isEnabled('new-payment-flow', { userId: order.userId })) {
    return newPaymentFlow(order);
  }
  return legacyPaymentFlow(order);
}

// LaunchDarkly / Unleash / custom implementation
const featureFlags = {
  async isEnabled(feature: string, context?: object): Promise<boolean> {
    // Check feature flag service
    return await flagService.evaluate(feature, context);
  }
};
```

---

# 5. Monitoring & Observability

## 5.1 Health Checks

```typescript
// Health check endpoint
app.get('/health', (req, res) => {
  res.json({
    status: 'healthy',
    timestamp: new Date().toISOString(),
    version: process.env.APP_VERSION,
    uptime: process.uptime(),
  });
});

// Readiness check (for K8s)
app.get('/ready', async (req, res) => {
  try {
    await prisma.$queryRaw`SELECT 1`;
    await redis.ping();
    res.json({ status: 'ready' });
  } catch (error) {
    res.status(503).json({ status: 'not ready', error: error.message });
  }
});

// Liveness check
app.get('/live', (req, res) => {
  res.json({ status: 'alive' });
});
```

## 5.2 Metrics & Alerting

```typescript
// Prometheus metrics
import { Counter, Histogram, register } from 'prom-client';

const httpRequestDuration = new Histogram({
  name: 'http_request_duration_seconds',
  help: 'Duration of HTTP requests in seconds',
  labelNames: ['method', 'route', 'status_code'],
  buckets: [0.1, 0.5, 1, 2, 5],
});

const httpRequestTotal = new Counter({
  name: 'http_requests_total',
  help: 'Total number of HTTP requests',
  labelNames: ['method', 'route', 'status_code'],
});

// Middleware
app.use((req, res, next) => {
  const end = httpRequestDuration.startTimer();
  res.on('finish', () => {
    const labels = {
      method: req.method,
      route: req.route?.path || 'unknown',
      status_code: res.statusCode,
    };
    end(labels);
    httpRequestTotal.inc(labels);
  });
  next();
});

// Metrics endpoint
app.get('/metrics', async (req, res) => {
  res.set('Content-Type', register.contentType);
  res.end(await register.metrics());
});
```

## 5.3 Alert Rules

```yaml
# Prometheus alerting rules
groups:
  - name: production-alerts
    rules:
      - alert: HighErrorRate
        expr: |
          sum(rate(http_requests_total{status_code=~"5.."}[5m])) 
          / sum(rate(http_requests_total[5m])) > 0.05
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: High error rate detected
          
      - alert: HighLatency
        expr: |
          histogram_quantile(0.95, 
            sum(rate(http_request_duration_seconds_bucket[5m])) by (le)
          ) > 2
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: P95 latency above 2 seconds
```

---

# 6. Rollback Strategy

## 6.1 Automated Rollback

```yaml
# GitHub Actions rollback
deploy:
  steps:
    - name: Deploy
      id: deploy
      run: ./deploy.sh
      
    - name: Health check
      id: health
      run: |
        for i in {1..10}; do
          if curl -s https://api.example.com/health | grep -q "healthy"; then
            echo "Health check passed"
            exit 0
          fi
          sleep 10
        done
        echo "Health check failed"
        exit 1
      
    - name: Rollback on failure
      if: failure()
      run: ./rollback.sh
```

## 6.2 Manual Rollback Procedure

```markdown
## Emergency Rollback Procedure

### 1. Detect Issue
- [ ] Alert received or user report
- [ ] Issue confirmed (not false positive)

### 2. Assess Severity
- Critical: Data loss, security breach → Immediate rollback
- High: Major feature broken → Rollback within 15 min
- Medium: Minor issue → Hotfix or scheduled rollback

### 3. Execute Rollback
```bash
# Kubernetes
kubectl rollout undo deployment/app-name

# Docker
docker service update --rollback app-name

# Vercel
vercel rollback
```

### 4. Verify
- [ ] Previous version running
- [ ] Health checks passing
- [ ] User-facing functionality restored

### 5. Communicate
- [ ] Stakeholders notified
- [ ] Status page updated
- [ ] Post-mortem scheduled
```

---

# 7. Deployment Kontrol Listesi

## 7.1 Pre-Deployment
- [ ] Tüm testler geçiyor
- [ ] Security scan temiz
- [ ] Code review approved
- [ ] Changelog güncel
- [ ] Rollback plan hazır

## 7.2 During Deployment
- [ ] Maintenance window (gerekiyorsa)
- [ ] Monitoring dashboard açık
- [ ] On-call engineer hazır
- [ ] Communication channel açık

## 7.3 Post-Deployment
- [ ] Health checks passing
- [ ] Smoke tests passing
- [ ] Metrics normal
- [ ] No error spike
- [ ] Stakeholders notified

---

# 8. Mutlaka Yap Listesi

## 🔴 Yapma
- ❌ Cuma günü deploy etme
- ❌ Test edilmemiş kodu deploy etme
- ❌ Tek seferde büyük değişiklik
- ❌ Rollback planı olmadan deploy
- ❌ Monitoring olmadan deploy
- ❌ Off-hours'da (nöbetçi yokken) deploy
- ❌ Database migration'ı app deploy ile birleştirme

## ✅ Mutlaka Yap
- ✅ Automated testing
- ✅ Security scanning
- ✅ Progressive rollout (canary)
- ✅ Feature flags kullan
- ✅ Health check endpoint'leri
- ✅ Monitoring & alerting
- ✅ Rollback plan hazırla
- ✅ Post-deployment verification
- ✅ Incident response plan

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 2.0
