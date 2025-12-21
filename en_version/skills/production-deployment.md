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

## 🎯 Deployment Principles

| Principle | Description |
|---------|----------|
| **Automate Everything** | Manual steps = Risk of error |
| **Shift-Left Security** | Security from the very beginning |
| **Progressive Delivery** | Gradual rollout (canary) |
| **Immutable Infrastructure** | Do not modify, replace |
| **Everything as Code** | Config, infra, policy = Code |
| **Fail Fast, Rollback Faster** | Detect fast, revert faster |

---

## 🔒 Pre-Deployment Checklist

### Code Quality
- [ ] All tests pass (unit, integration, e2e)
- [ ] Test coverage threshold met (>80%)
- [ ] No lint or TypeScript errors
- [ ] Build is successful

### Security
- [ ] Dependency audit performed (npm audit)
- [ ] SAST (Static Analysis) passed
- [ ] No hardcoded secrets
- [ ] OSWAP Top 10 checked

### Database Migrations
- [ ] Migration is backward compatible
- [ ] Rollback script is ready
- [ ] Performance impact evaluated

---

## 🚀 Deployment Strategies

### 1. Blue-Green Deployment
1. Deploy to Green (New version).
2. Test Green.
3. Switch traffic from Blue to Green.
4. Keep Blue on standby for rollback.

### 2. Canary Deployment
1. Deploy to Canary (5% traffic).
2. Monitor metrics.
3. Increase traffic gradually if no issues occur.
4. Revert immediately if issues are detected.

### 3. Feature Flags
Use feature flags to decouple deployment from release, allowing features to be toggled on/off without fresh deployments.

---

## 📊 Monitoring & Observability

### Health Checks
- **Health**: General status and version.
- **Readiness**: Can the app handle traffic? (DB/Redis check).
- **Liveness**: Is the app alive?

### Metrics
Monitor HTTP request durations, error rates, and total request counts. Use alerting rules to notify on high error rates or latency.

---

## 🔙 Rollback Strategy

### Automated Rollback
Integrate health checks into the CI/CD pipeline. If post-deployment checks fail, trigger an automated rollback script.

### Emergency Rollback Procedure
1. Detect and confirm the issue.
2. Assess severity.
3. Execute rollback (e.g., `kubectl rollout undo`).
4. Verify previous version and communicate with stakeholders.

---

## ✅ Checklist

### Pre-Deployment
- [ ] All tests and security scans pass
- [ ] Rollback plan is ready
- [ ] Changelog updated

### Post-Deployment
- [ ] Health and smoke tests pass
- [ ] Metrics are normal
- [ ] Stakeholders notified

---

## 🔴 Don't List

❌ Do not deploy on Fridays
❌ Do not deploy untested code
❌ Do not deploy without a monitoring system
❌ Do not make large changes at once
❌ Do not skip the rollback plan

---

## ✅ Must Do List

✅ Automated testing and scanning
✅ Progressive rollout (canary/blue-green)
✅ Use feature flags
✅ Monitor health and metrics
✅ Post-deployment verification
✅ Incident response plan

---

**Last Update:** December 2025
**Version:** 1.0
