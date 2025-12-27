# Deploy Workflow

## Description
Production deployment workflow with safety checks, progressive rollout, and rollback procedures. Ensures safe and reliable deployments.

---

## Invocation
```
/deploy [environment: staging|production]
```

---

## Steps

### Step 1: Pre-Deployment Checklist

```markdown
## Pre-Deployment Verification

### Code Quality
- [ ] All tests passing
- [ ] Coverage >= 80%
- [ ] No lint errors
- [ ] No TypeScript errors
- [ ] Build successful

### Security
- [ ] npm audit clean
- [ ] No hardcoded secrets
- [ ] OWASP Top 10 reviewed

### Review
- [ ] Code review approved
- [ ] All comments addressed

### Documentation
- [ ] CHANGELOG updated
- [ ] Breaking changes documented
- [ ] API changes noted
```

### Step 2: Database Migration Check

```markdown
## Migration Checklist

- [ ] Migration is backward compatible
- [ ] Rollback script prepared
- [ ] Migration tested on staging
- [ ] Performance impact evaluated
- [ ] Downtime planned (if needed)
```

### Step 3: Deployment Strategy Selection

```markdown
## Deployment Strategy

### For Low-Risk Changes
- [ ] Direct deployment with monitoring

### For Medium-Risk Changes
- [ ] Canary deployment (5% -> 25% -> 50% -> 100%)

### For High-Risk Changes
- [ ] Blue-Green deployment with quick rollback
- [ ] Feature flag with kill switch
```

### Step 4: Execute Deployment

```markdown
## Deployment Execution

### Pre-Deploy
- [ ] Notify team in communication channel
- [ ] Confirm on-call engineer available
- [ ] Open monitoring dashboard

### Deploy
- [ ] Trigger deployment pipeline
- [ ] Monitor logs for errors
- [ ] Watch metrics for anomalies

### Rollout (Canary)
- [ ] 5% traffic - observe 10 minutes
- [ ] 25% traffic - observe 10 minutes
- [ ] 50% traffic - observe 10 minutes
- [ ] 100% traffic - deployment complete
```

### Step 5: Post-Deployment Verification

```markdown
## Post-Deployment Checks

### Health
- [ ] Health endpoint responding
- [ ] All services healthy
- [ ] No increased error rate

### Functionality
- [ ] Smoke tests passing
- [ ] Critical paths working
- [ ] No user complaints

### Metrics
- [ ] Response times normal
- [ ] Error rate < 1%
- [ ] CPU/Memory stable
```

### Step 6: Rollback Procedure (If Needed)

```markdown
## Rollback Steps

### Trigger Conditions
- Error rate > 5%
- P95 latency > 2x normal
- Critical functionality broken

### Execute Rollback
```bash
# Kubernetes
kubectl rollout undo deployment/app-name

# Verify previous version
kubectl get pods
```

### Post-Rollback
- [ ] Verify rollback successful
- [ ] Investigate root cause
- [ ] Create incident report
```

---

## Communication Template

```markdown
## Deployment Notification

### Starting Deployment
:rocket: Deploying v[X.Y.Z] to [environment]
- Changes: [brief summary]
- Rollout: [strategy]
- ETA: [time]

### Deployment Complete
:white_check_mark: v[X.Y.Z] deployed successfully
- All health checks passing
- Metrics stable

### Rollback (if needed)
:warning: Rolling back v[X.Y.Z]
- Reason: [description]
- Investigating...
```

---

## Output

Successful deployment with:
- All pre-checks passed
- Progressive rollout completed
- Health verified
- Team notified
- Rollback plan ready

---

## Related Workflows
- `/test` - Ensure tests pass before deploy
- `/review` - Code review before deploy
