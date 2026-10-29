# Lesson 4 — Error Budgets

An **error budget** is the permitted amount of unreliability while meeting an SLO.

For a request-success SLO:

`Allowed failure fraction = 1 - SLO fraction`

## Worked example

- SLO: 99.9% success
- Eligible requests: 100,000
- Allowed failed requests: 100,000 × 0.001 = **100**
- Observed failed requests: **250**
- Actual SLI: (100,000 − 250) / 100,000 × 100 = **99.75%**
- Budget consumption: 250 / 100 × 100 = **250%**
- Failures beyond budget: **150**

**Result:** SLO missed. This does not, by itself, establish an SLA violation.

## Operational use

When budget is consumed rapidly or exhausted, assess ongoing user impact, investigate causes, and consider reducing risky releases according to the agreed error-budget policy. Reliability fixes or urgent security changes may still be appropriate. Previously recorded failures are not erased by fixing the issue.
