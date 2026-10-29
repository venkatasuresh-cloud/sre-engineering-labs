# Lesson 7 — SRE Roles and Responsibilities

Common areas of SRE ownership include:

- Service reliability goals: SLIs, SLOs, error budgets
- Monitoring, logging, tracing, actionable alerts
- Incident response and communications
- Reliability improvements and resilience testing
- Automation and toil reduction
- Capacity/performance engineering
- Release risk, safe rollout and recovery planning

## Collaboration example

When an EKS API returns HTTP 500, do not assume code or infrastructure is innocent based only on healthy pods. Review user impact, application logs, request metrics, RDS health, and recent changes; work with developers, DBAs, and platform engineers to restore service and prevent recurrence.

Senior SRE responsibilities often add cross-team reliability programs, incident leadership, architecture tradeoffs, and mentoring. Exact role boundaries vary by organization.
