---
description: Production deployment workflow with pre-deployment checks and rollback procedures
---

# Deploy Workflow

## Description
Use this workflow for deploying code to staging or production. It covers pre-deployment checks, migration verification, progressive rollout, monitoring, and rollback procedures.

---

## Steps

1. **Run pre-deployment checks** - Verify all tests pass with coverage >= 80%, no lint errors, no TypeScript errors, build succeeds, npm audit is clean, code review is approved, and CHANGELOG is updated.

2. **Check database migrations** - Ensure migrations are backward compatible, rollback script is prepared, migrations are tested on staging, performance impact is evaluated, and downtime is planned if needed.

3. **Select deployment strategy** - Choose direct deployment for low-risk changes, canary deployment (5% → 25% → 50% → 100%) for medium-risk changes, or blue-green deployment with feature flags for high-risk changes.

4. **Notify team and prepare** - Send deployment notification to communication channel, confirm on-call engineer is available, and open monitoring dashboard.

5. **Execute deployment** - Trigger deployment pipeline, monitor logs for errors, and watch metrics for anomalies during rollout.

6. **Monitor progressive rollout** - For canary deployments: observe 10 minutes at 5% traffic, then 25%, then 50%, then 100%. Check health metrics at each stage.

7. **Verify post-deployment** - Confirm health endpoint is responding, all services are healthy, no increased error rate, smoke tests pass, critical paths work, and response times are normal.

8. **Rollback if needed** - Trigger rollback if error rate > 5%, P95 latency > 2x normal, or critical functionality is broken. Verify rollback successful and investigate root cause.

9. **Complete deployment** - Mark deployment as successful in tracking system, document any issues, and create incident report if rollback occurred.

---

## Related Workflows
- Call `/test` to ensure tests pass before deploy
- Call `/review` to complete code review before deploy
