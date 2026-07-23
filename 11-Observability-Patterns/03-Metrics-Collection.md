# Metrics Collection

## Introduction

Metrics Collection is an observability pattern where **applications, infrastructure, and services continuously record numerical measurements over time to monitor system health, performance, and resource utilization**.

Unlike logs, which describe individual events, metrics provide aggregated quantitative data that can be analyzed for trends, anomalies, and operational insights.

Metrics Collection answers the question:

> **"How is the system performing over time?"**

The main goals of Metrics Collection are:

- Monitor application health.
- Measure performance.
- Detect anomalies.
- Enable alerting.
- Support capacity planning.

---

# Why was it Introduced?

Imagine monitoring an API without metrics.

Without Metrics Collection:

```text
Users

↓

Application

↓

Logs
```

To determine CPU usage, request rate, or latency, engineers must manually analyze logs.

With Metrics Collection:

```text
Applications

↓

Metrics Collector

↓

Time-Series Database

↓

Dashboards & Alerts
```

Key performance indicators are continuously available.

---

# Architecture Diagram

```text
      Applications

      |     |     |

      ▼     ▼     ▼

 Metrics Exporters

             |

             ▼

 Metrics Collector

             |

             ▼

 Time-Series Database

             |

             ▼

 Dashboards & Alerts
```

Metrics are collected, stored, and visualized over time.

---

# How It Works

The workflow:

```text
1. Applications expose metrics.

2. Metrics collectors scrape or receive metrics.

3. Metrics are stored in a time-series database.

4. Dashboards visualize trends.

5. Alerting systems evaluate thresholds and notify operators.
```

---

# Types of Metrics

## System Metrics

Measure infrastructure resources.

Examples:

- CPU utilization
- Memory usage
- Disk usage
- Network traffic

---

## Application Metrics

Measure application behavior.

Examples:

- Request count
- Error rate
- Response time
- Active users

---

## Business Metrics

Measure business outcomes.

Examples:

- Orders per minute
- Payments processed
- Revenue
- User sign-ups

---

## Database Metrics

Monitor database performance.

Examples:

- Query latency
- Connections
- Cache hit ratio
- Replication lag

---

# Metric Types

## Counter

A value that only increases.

Example:

```text
HTTP Requests

1

2

3

4
```

Common uses:

- Requests
- Errors
- Jobs processed

---

## Gauge

Represents the current value of something.

Example:

```text
CPU Usage

65%
```

Common uses:

- Memory usage
- Queue size
- Active connections

---

## Histogram

Measures the distribution of observed values.

Example:

```text
API Latency

5 ms

10 ms

20 ms
```

Useful for latency analysis.

---

## Summary

Calculates quantiles such as median or 95th percentile.

Example:

```text
95th Percentile

120 ms
```

---

# Common Metrics

## Latency

Time required to process requests.

---

## Throughput

Number of requests processed per second.

---

## Error Rate

Percentage of failed requests.

---

## Availability

Percentage of successful uptime.

---

## Saturation

Measures how heavily resources are utilized.

---

# Core Characteristics

## 1. Numerical

Metrics represent measurable values.

---

## 2. Time-Based

Values are recorded over time.

---

## 3. Aggregated

Metrics summarize system behavior rather than individual events.

---

## 4. Efficient

Require significantly less storage than logs.

---

## 5. Alert Friendly

Thresholds can trigger automated alerts.

---

# Advantages

## 1. Continuous Monitoring

Provides real-time visibility into system health.

---

## 2. Trend Analysis

Supports historical performance analysis.

---

## 3. Capacity Planning

Helps forecast infrastructure needs.

---

## 4. Automated Alerting

Threshold breaches can trigger notifications.

---

## 5. Low Storage Requirements

Metrics consume less storage than detailed logs.

---

# Disadvantages

## 1. Limited Detail

Metrics show *what* happened, not *why* it happened.

---

## 2. Instrumentation Required

Applications must expose meaningful metrics.

---

## 3. Metric Explosion

Poor metric design can generate excessive cardinality and storage costs.

---

## 4. Retention Costs

Long-term storage of high-resolution metrics can become expensive.

---

## 5. Requires Complementary Data

Metrics alone are insufficient for complete troubleshooting; logs and traces are often needed.

---

# Best Practices

- Use meaningful metric names.
- Include labels carefully to avoid high-cardinality metrics.
- Monitor the "Golden Signals":
  - Latency
  - Traffic
  - Errors
  - Saturation
- Retain metrics at appropriate resolutions.
- Combine metrics with logs and traces for comprehensive observability.

---

# Real-World Examples

## Prometheus

Open-source metrics collection and monitoring system.

---

## Grafana

Visualizes metrics from multiple data sources.

---

## Amazon CloudWatch Metrics

Collects infrastructure and application metrics in AWS.

---

## Google Cloud Monitoring

Managed monitoring platform for Google Cloud workloads.

---

## Datadog

Cloud monitoring and observability platform.

---

# When to Use

Use Metrics Collection when:

- Monitoring production systems.
- Tracking application performance.
- Building dashboards.
- Creating alerting rules.
- Planning infrastructure capacity.

---

# When NOT to Use

Avoid relying solely on metrics when:

- Investigating detailed application behavior.
- Debugging individual requests.
- Performing root cause analysis that requires logs or traces.

---

# Comparison

| Feature | Metrics | Logs |
|---|---|---|
| Data Type | Numerical | Textual |
| Storage | Low | High |
| Trend Analysis | Excellent | Limited |
| Event Detail | Low | High |
| Alerting | Excellent | Limited |

---

# Interview Questions

## 1. What are metrics?

Numerical measurements collected over time to monitor system health and performance.

---

## 2. What is the difference between a Counter and a Gauge?

A Counter only increases, while a Gauge represents a value that can increase or decrease.

---

## 3. What are the four Golden Signals?

- Latency
- Traffic
- Errors
- Saturation

---

## 4. Name popular metrics collection tools.

- Prometheus
- Grafana
- Amazon CloudWatch
- Google Cloud Monitoring
- Datadog

---

## 5. Why are metrics important?

They provide continuous visibility into system health, support alerting, and enable trend analysis and capacity planning.

---

# Key Takeaways

- Metrics provide quantitative insights into system behavior over time.
- Counters, Gauges, Histograms, and Summaries are the primary metric types.
- Metrics are ideal for dashboards, alerting, and performance monitoring.
- The Golden Signals are foundational for production monitoring.
- Metrics complement logs and distributed traces to deliver full observability.

---

## Previous & Next

← Previous: [Distributed Tracing](02-Distributed-Tracing.md)

→ Next: [Health Check Pattern](04-Health-Check-Pattern.md)