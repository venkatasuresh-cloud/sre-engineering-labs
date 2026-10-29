# Lesson 8 — Incident Response Basics

A typical workflow:

1. **Detect** — recognize actionable user/service impact.
2. **Assess** — confirm impact, scope, and severity per team policy.
3. **Coordinate** — acknowledge, involve owners, communicate facts and updates.
4. **Mitigate** — apply an evidence-based, authorized recovery action.
5. **Validate** — test user operations and watch error/latency metrics.
6. **Learn** — investigate contributing factors and track improvements.

## EKS / RDS example

60% of requests return HTTP 500; pods are Running; logs show `MySQL: Too many connections`.

Possible contributing factors: connection leak, oversized per-pod pools, slow queries, abnormal demand, or configuration limits. Check CloudWatch `DatabaseConnections`, freeable memory, application pools, sessions, and recent changes. Avoid blindly raising the connection limit or restarting every workload.

### Helpful read-only Kubernetes checks (authorized cluster)

```bash
kubectl get pods -n production
kubectl logs deployment/student-app -n production --since=15m
kubectl rollout history deployment/student-app -n production
```

These illustrate diagnostic commands; replace placeholder names and use only in authorized environments. For Argo CD-managed workloads, follow the GitOps rollback process rather than assuming a direct `kubectl rollout undo` will persist.
