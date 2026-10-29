# Lesson 3 — SLI, SLO and SLA

| Term | Meaning | Example |
|---|---|---|
| SLI (Service Level Indicator) | Measured service performance | 99.5% successful eligible logins |
| SLO (Service Level Objective) | Target for an SLI over a window | ≥99.9% eligible login success over 30 days |
| SLA (Service Level Agreement) | Customer-facing service commitment, often contractual | Monthly availability promise with possible service credits |

## Request-success calculation

For 100,000 valid requests and 500 service failures:

`Success SLI = (100000 - 500) / 100000 * 100 = 99.5%`

If the SLO is 99.9%, it is **not met**.

## Important definition details

Define which requests are eligible, what counts as success, and the reporting window. An expected 401 for an incorrect password should not automatically count as a service-side failure. Compare an SLA with an SLO only when their definitions and windows are compatible.
