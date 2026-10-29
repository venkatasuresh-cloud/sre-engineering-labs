# Lesson 10 — Scenario-Based Fundamentals Assessment

**Status:** Conceptual scenario completed. Hypothetical scenario only, not a hands-on production incident.

## Scenario

Student API: ALB → Amazon EKS → RDS MySQL.

Observed: 25% HTTP 5xx, p95 latency 6.5 s, traffic 1,500 RPS versus 300 normal, CPU 92%, six pods Running, RDS connection count near limit.

## SRE response

1. Confirm affected user journeys, request distribution, current error rates, and severity.
2. Coordinate incident channel and notify application/database owners early.
3. Correlate all four golden signals with logs, RDS connection metrics, scaling, throttling, and changes. Avoid assuming a root cause.
4. Choose an authorized, evidence-based mitigation and verify recovery with user-facing tests.
5. Conduct RCA and a blameless postmortem with improvement actions.

## Error-budget exercise

- Request-success SLO: 99.9%
- Eligible requests: 100,000
- Failed requests: 250
- Actual SLI: **99.75%**
- Allowed failures: **100**
- Budget used: **250%**; excess failures: **150**
- Outcome: **SLO missed**; SLA status unknown without contract terms.

## Next validation goals

Implement these measurements with real instrumentation and reproducible synthetic incidents in an isolated Phase 2 lab.
