# Lab 01 — Prometheus Monitoring Fundamentals

**SRE Mastery | Phase 2: Monitoring & Observability**

## 1. Objective

Learn the fundamentals of Prometheus by deploying a monitoring server locally with Docker Compose, configuring metric scraping, validating target health, and exploring metrics using PromQL.

This lab demonstrates the basic monitoring workflow used in Site Reliability Engineering (SRE).

## 2. What Is Prometheus?

Prometheus is an open-source monitoring and time-series database system.

It helps SRE engineers:

- Collect numerical metrics from applications and infrastructure.
- Store measurements with timestamps.
- Query metrics using PromQL.
- Understand system behavior and identify potential reliability problems.

Prometheus commonly uses a **pull-based model**, where the server periodically requests metrics from configured targets.

## 3. Lab Architecture

In this lab, Prometheus monitors itself.

```text
Windows Laptop
    |
    v
Docker Desktop
    |
    v
Prometheus Container
    |  Port 9090
    |
    +---- HTTP GET /metrics
    |          |
    +----------+
         |
         v
Prometheus Time-Series Database
         |
         v
PromQL Queries / Prometheus Web UI
```

Prometheus scrapes its own `/metrics` endpoint every 15 seconds and stores the collected time-series samples.

**Important:** This lab monitors the Prometheus server itself. It does not yet monitor external applications, Kubernetes workloads, or AWS infrastructure.

## 4. Prerequisites

- Windows laptop with Docker Desktop installed and running.
- Docker Compose support.
- Git.
- Web browser.
- Port `9090` available on the local machine.

No AWS or Azure resources are required.

## 5. Project Structure

```text
01-prometheus-basics/
├── compose.yaml
├── prometheus.yml
└── README.md
```

### compose.yaml

Defines the Prometheus Docker container, port mapping, configuration mount, persistent data volume, and startup settings.

### prometheus.yml

Defines which targets Prometheus monitors and how frequently it scrapes their metrics.

## 6. Prometheus Configuration

The `prometheus.yml` file contains:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: prometheus
    static_configs:
      - targets:
          - "localhost:9090"
```

**Explanation:**

| Configuration | Purpose |
|---|---|
| `scrape_interval: 15s` | Attempts to collect metrics every 15 seconds |
| `job_name: prometheus` | Identifies the scrape job |
| `localhost:9090` | Prometheus server's own metrics endpoint |

The target address is interpreted from inside the Prometheus container, where the Prometheus server is running.

## 7. Starting the Monitoring Lab

Navigate to the lab directory:

```powershell
cd phase-02-observability/01-prometheus-basics
```

Validate the Docker Compose configuration:

```powershell
docker compose config -q
```

Start Prometheus:

```powershell
docker compose up -d
```

Check container status:

```powershell
docker ps
```

**Expected result:** The `sre-prometheus` container should be running.

Open the Prometheus web interface:

http://localhost:9090

## 8. Validating the Monitoring Target

In the Prometheus interface, navigate to:

**Status → Targets**

The target should show:

```text
Job: prometheus
Endpoint: http://localhost:9090/metrics
State: UP
```

This confirms that Prometheus can successfully scrape its own metrics endpoint.

## 9. Basic PromQL Queries

### Query 1 — Target Scrape Status

```promql
up
```

Example:

```text
up{instance="localhost:9090",job="prometheus"} 1
```

**Interpretation:**

- `1`: The latest metrics scrape succeeded.
- `0`: The latest metrics scrape failed.

A successful scrape does not guarantee that an application is functioning correctly for its users.

### Query 2 — Active Time Series

```promql
prometheus_tsdb_head_series
```

This metric reports the number of time series in Prometheus's active TSDB head.

During this lab, the observed value was approximately **790**.

This does not mean 790 applications or requests. It indicates approximately 790 distinct active-head time series at the time of observation.

### Query 3 — Total Prometheus HTTP Requests

```promql
prometheus_http_requests_total
```

This metric counts HTTP requests processed by the Prometheus HTTP server.

An example time series:

```text
prometheus_http_requests_total{
  handler="/-/ready",
  code="200",
  instance="localhost:9090",
  job="prometheus"
} 1
```

The labels identify the HTTP handler, response code, instance, and job.

The value is a cumulative request count since the counter last reset.

### Query 4 — Filter Requests by Handler

```promql
prometheus_http_requests_total{handler="/api/v1/query"}
```

This selects the HTTP request counters for the Prometheus query API.

### Query 5 — Average HTTP Request Rate

```promql
rate(prometheus_http_requests_total{handler="/api/v1/query",code="200"}[5m])
```

This calculates the average successful query API request rate per second over a five-minute window.

The result depends on actual request activity and collected samples.

## 10. Key Concepts Learned

| Concept | Description |
|---|---|
| Metric | A numerical measurement of system behavior |
| Target | An endpoint configured for metrics collection |
| Scrape | Prometheus requesting metrics from a target |
| Scrape interval | Time between scheduled scrape attempts |
| Time series | Samples over time identified by a metric name and labels |
| Labels | Key-value pairs identifying specific metric series |
| Counter | A cumulative measurement that increases until reset |
| Gauge | A measurement that can increase or decrease |
| PromQL | Query language used to analyze Prometheus metrics |
| `rate()` | Calculates the average per-second rate of a counter |
| `increase()` | Estimates how much a counter increased over a time interval |

## 11. Production SRE Relevance

In production, Prometheus can help SRE engineers monitor:

- Kubernetes application and infrastructure metrics.
- HTTP request rates and error rates.
- Application latency.
- CPU and memory utilization.
- Availability of monitored targets.
- Infrastructure and application capacity.

Real-world monitoring usually requires application instrumentation, exporters, and appropriate scrape configurations.

Collected metrics can be visualized using Grafana and evaluated against alerting rules.

**An important SRE principle:** Successful metric collection is not the same as a healthy user experience. Reliable monitoring also requires meaningful service-level indicators (SLIs) and service-level objectives (SLOs).

## 12. Validation Summary

The following activities were successfully completed:

- [x] Installed and started Prometheus using Docker Compose.
- [x] Configured a 15-second scrape interval.
- [x] Verified the Prometheus container was running.
- [x] Accessed the Prometheus web interface.
- [x] Verified the self-monitoring target was `UP`.
- [x] Executed the `up` query.
- [x] Inspected active time-series metrics.
- [x] Explored HTTP request counters and metric labels.
- [x] Learned the basic purpose of `rate()` and `increase()`.

## 13. Troubleshooting

**Prometheus web interface does not load**

Check whether Docker Desktop is running and inspect the container:

```powershell
docker ps
docker logs sre-prometheus
```

**Prometheus target is DOWN**

Check the target under **Status → Targets** and review the error message.

Verify the scrape configuration in `prometheus.yml`.

**Port 9090 is already in use**

Check whether another local process or container is using the port before changing the Compose configuration.

## 14. Cleanup

Stop the lab:

```powershell
docker compose down
```

This removes the container and Compose network but retains the named data volume.

To deliberately remove the lab's stored metric data as well:

```powershell
docker compose down -v
```

**Warning:** The `-v` option removes the Compose-managed named volume and its stored Prometheus data.

## 15. Next Steps

Continue Phase 2 with:

1. Grafana installation and Prometheus data-source configuration.
2. Monitoring dashboard creation.
3. Application metrics and exporters.
4. Alerting fundamentals.
5. Production-oriented observability exercises.

---

**Status:** Prometheus fundamentals lab completed and validated locally.

**Repository:** [sre-engineering-labs]