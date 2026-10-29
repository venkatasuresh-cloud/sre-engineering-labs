# Lesson 2 — Reliability and Availability

**Availability:** Whether a service meets a defined usable/operational condition over a measurement window.

**Reliability:** Whether a service consistently performs its intended operations correctly and within acceptable performance limits. A service can have high basic uptime while still producing slow or failed user requests.

## Time-based availability example

For a 30-day window: 30 × 24 × 60 = **43,200 minutes**.

At **99.9% availability**, permitted full-outage time is 43,200 × 0.001 = **43.2 minutes**.

If complete downtime is 40 minutes, measured availability = (43,200 − 40) / 43,200 × 100 ≈ **99.9074%**.

> This is a simplified time-based model. Request-based availability requires a clearly defined set of eligible requests and success conditions.

## User-impact example

EKS pods can be Running while login fails because the application cannot reach RDS. Pod health alone does not establish service availability.
