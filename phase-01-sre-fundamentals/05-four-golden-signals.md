# Lesson 5 — Four Golden Signals

| Signal | Question | Examples |
|---|---|---|
| Latency | How long do requests take? | HTTP request duration, p95/p99 |
| Traffic | How much demand exists? | Requests/second |
| Errors | How often do operations fail? | Failed eligible requests / total |
| Saturation | How close are resources to their effective limits? | CPU throttling, DB connections, queues |

## EKS incident thought experiment

Traffic rises from 200 to 2,000 RPS, p95 latency increases from 200 ms to 4 seconds, and CPU reaches 95%. This suggests possible capacity pressure, **not proof of the root cause**. Investigate HPA, throttling, request mix, downstream services, and logs.

## Instrumentation examples

ALB CloudWatch `RequestCount`, `TargetResponseTime`, and HTTP 5xx metrics can help, while application instrumentation gives more user-operation-specific measurements.
