---
name: production-deployment
description: Safe production deployment guide. DevSecOps, CI/CD, progressive delivery, and 2025 security standards.
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

> Secure and reliable production deployment methodology.
> DevSecOps, CI/CD pipeline security, and progressive delivery.

---

# 📋 Contents

1. [Deployment Principles](#1-deployment-principles)
2. [Pre-Deployment Checklist](#2-pre-deployment-checklist)
3. [CI/CD Pipeline](#3-cicd-pipeline)
4. [Pipeline Security](#4-pipeline-security)
5. [Deployment Strategies](#5-deployment-strategies)
6. [Monitoring & Observability](#6-monitoring--observability)
7. [Rollback Strategy](#7-rollback-strategy)
8. [Checklist](#8-checklist)
9. [Don't List](#9-dont-list)
10. [Must Do List](#10-must-do-list)

---

# 1. Deployment Principles

| Principle | Description |
|---------|----------|
| **Automate Everything** | Manual steps = Risk of error |
| **Shift-Left Security** | Security from the very beginning |
| **Progressive Delivery** | Gradual rollout |
| **Immutable Infrastructure** | Do not modify, replace |
| **Everything as Code** | Config, infra, policy = Code |
| **Fail Fast, Rollback Faster** | Detect fast, revert faster |

---

# 2. Pre-Deployment Checklist

## 2.1 Code Quality

```markdown
## Pre-Deployment Checklist

### Code Quality
- [ ] All tests pass (unit, integration, e2e)
- [ ] Test coverage threshold met (>80%)
- [ ] No lint errors
- [ ] No TypeScript type errors
- [ ] Build is successful

### Security
- [ ] Dependency audit performed (npm audit)
- [ ] SAST (Static Analysis) passed
- [ ] No hardcoded secrets
- [ ] OWASP Top 10 checked

### Code Review
- [ ] At least 1 approval received
- [ ] All review comments addressed
- [ ] No merge conflicts

### Documentation
- [ ] Breaking changes documented
- [ ] API changes updated
- [ ] Changelog updated
```

## 2.2 Database Migrations

```markdown
## Database Migration Checklist

- [ ] Migration is backward compatible
- [ ] Rollback script is ready
- [ ] Migration tested in test environment
- [ ] Performance impact evaluated
- [ ] Downtime planned (if necessary)
```

---

# 3. CI/CD Pipeline

## 3.1 GitHub Actions Example

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

---

# 4. Pipeline Security

## 4.1 Secret Management

```yaml
# ✅ RIGHT: Use GitHub Secrets
env:
  DATABASE_URL: ${{ secrets.DATABASE_URL }}
  API_KEY: ${{ secrets.API_KEY }}

# ❌ WRONG: Hardcoded secrets
env:
  API_KEY: "sk-12345..."  # NEVER!
```

## 4.2 OIDC Federation (Secretless)

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

## 4.3 Dependency Security

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

# 5. Deployment Strategies

## 5.1 Blue-Green Deployment

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

1. Deploy to Green.
2. Test Green.
3. Divert traffic to Green.
4. Keep Blue on standby (for rollback).
```

## 5.2 Canary Deployment

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

1. Deploy to Canary (5% traffic).
2. Monitor metrics.
3. If no issues, increase traffic (10%, 25%, 50%, 100%).
4. Revert immediately if issues are detected.
```

## 5.3 Feature Flags

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

# 6. Monitoring & Observability

## 6.1 Health Checks

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

## 6.2 Metrics & Alerting

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

## 6.3 Alert Rules

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

# 7. Rollback Strategy

## 7.1 Automated Rollback

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

## 7.2 Manual Rollback Procedure

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

# 8. Checklist

### Pre-Deployment
- [ ] All tests pass
- [ ] Security scan clean
- [ ] Code review approved
- [ ] Changelog up to date
- [ ] Rollback plan ready

### During Deployment
- [ ] Maintenance window (if necessary)
- [ ] Monitoring dashboard open
- [ ] On-call engineer ready
- [ ] Communication channel open

### Post-Deployment
- [ ] Health checks passing
- [ ] Smoke tests passing
- [ ] Metrics normal
- [ ] No error spike
- [ ] Stakeholders notified

---

# 9. Don't List

❌ Do not deploy on Fridays
❌ Do not deploy untested code
❌ Do not make large changes at once
❌ Do not deploy without a rollback plan
❌ Do not deploy without monitoring
❌ Do not deploy during off-hours (no one on call)
❌ Do not combine database migration with app deploy

---

# 10. Must Do List

✅ Automated testing
✅ Security scanning
✅ Progressive rollout (canary)
✅ Use feature flags
✅ Health check endpoints
✅ Monitoring & alerting
✅ Prepare rollback plan
✅ Post-deployment verification
✅ Incident response plan

---

**Last Update:** December 2025
**Version:** 2.0
