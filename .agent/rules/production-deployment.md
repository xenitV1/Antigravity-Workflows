# Production Deployment Rule

## Activation
- **Mode:** Model Decision
- **Description:** Safe production deployment methodology. Activate for: CI/CD setup, deployment strategy, rollback planning, monitoring setup, and release management.

---

## Deployment Principles

| Principle | Description |
|-----------|-------------|
| Automate Everything | Manual step = Error risk |
| Shift-Left Security | Security from the start |
| Progressive Delivery | Gradual rollout |
| Immutable Infrastructure | Replace, don't modify |
| Everything as Code | Config, infra, policy = Code |
| Fail Fast, Rollback Faster | Quick detection, quick recovery |

---

## Pre-Deployment Checklist

### Code Quality
- [ ] All tests passing (unit, integration, e2e)
- [ ] Test coverage >= 80%
- [ ] Lint errors: 0
- [ ] TypeScript errors: 0
- [ ] Build successful

### Security
- [ ] Dependency audit done (npm audit)
- [ ] SAST (Static Analysis) passed
- [ ] No hardcoded secrets
- [ ] OWASP Top 10 checked

### Code Review
- [ ] At least 1 approval
- [ ] All comments addressed
- [ ] No merge conflicts

### Documentation
- [ ] Breaking changes documented
- [ ] API changes updated
- [ ] Changelog updated

---

## CI/CD Pipeline

```yaml
# Key stages
1. Test & Lint
2. Security Scan (Snyk, Trivy)
3. Build & Artifact
4. Deploy (with approval)
5. Health Check
6. Rollback (if failed)
```

### Secret Management
```yaml
# Use GitHub Secrets
env:
  DATABASE_URL: ${{ secrets.DATABASE_URL }}

# NEVER hardcode
env:
  API_KEY: "sk-12345..."  # NEVER!
```

---

## Deployment Strategies

### Blue-Green
```
Load Balancer
      |
+-----+-----+
|           |
BLUE       GREEN
(Current)  (New)

1. Deploy to Green
2. Test Green
3. Switch traffic to Green
4. Keep Blue for rollback
```

### Canary
```
Load Balancer
      |
+-----+-----+
|           |
STABLE     CANARY
95%        5%

1. Deploy to Canary (5%)
2. Monitor metrics
3. If OK: 10% -> 25% -> 50% -> 100%
4. If not: rollback
```

### Feature Flags
```typescript
if (await featureFlags.isEnabled('new-payment-flow')) {
  return newPaymentFlow(order);
}
return legacyPaymentFlow(order);
```

---

## Monitoring & Observability

### Health Checks
```typescript
app.get('/health', (req, res) => {
  res.json({ status: 'healthy', version: process.env.APP_VERSION });
});

app.get('/ready', async (req, res) => {
  await prisma.$queryRaw`SELECT 1`;
  res.json({ status: 'ready' });
});
```

### Key Metrics
- Error rate (< 1%)
- P95 latency
- Request throughput
- CPU/Memory usage

### Alerting Rules
- High error rate (> 5% for 5min)
- High latency (P95 > 2s for 5min)
- Service down

---

## Rollback Strategy

### Automated Rollback
```yaml
- name: Health check
  run: curl -s https://api.example.com/health

- name: Rollback on failure
  if: failure()
  run: ./rollback.sh
```

### Manual Rollback
```bash
# Kubernetes
kubectl rollout undo deployment/app-name

# Docker
docker service update --rollback app-name

# Vercel
vercel rollback
```

---

## Deployment Checklist

### Pre-Deployment
- [ ] All tests pass
- [ ] Security scan clean
- [ ] Code review approved
- [ ] Changelog updated
- [ ] Rollback plan ready

### During Deployment
- [ ] Maintenance window (if needed)
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

## Don't List

- Deploy on Friday
- Deploy untested code
- Large changes at once
- Deploy without rollback plan
- Deploy without monitoring
- Deploy off-hours (no on-call)
- Mix database migration with app deploy

---

## Must Do List

- Automated testing
- Security scanning
- Progressive rollout (canary)
- Feature flags
- Health check endpoints
- Monitoring & alerting
- Rollback plan
- Post-deployment verification
- Incident response plan

---

**Version:** 2.0 (Antigravity Rule)
