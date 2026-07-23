# Service Level Indicators (SLIs)

## Introduction

Service Level Indicators (SLIs) are **quantitative measurements that indicate how well a service is performing from the user's perspective**.

An SLI measures a specific aspect of service quality, such as availability, latency, throughput, or error rate.

SLIs provide the data used to determine whether a service is meeting its reliability goals.

Service Level Indicators answer the question:

> **"How well is the service performing?"**

The main goals of SLIs are:

- Measure user experience.
- Quantify service reliability.
- Monitor production performance.
- Provide objective operational metrics.
- Support Service Level Objectives (SLOs).

---

# Why were SLIs Introduced?

Imagine an API that appears healthy because CPU and memory usage are normal.

```text
CPU

40%

Memory

55%
```

However, users experience:

```text
5 Seconds Response Time
```

Infrastructure metrics alone cannot describe the actual user experience.

SLIs solve this problem by measuring what users actually experience.

Example:

```text
Availability

99.98%

Latency (P95)

120 ms

Error Rate

0.02%
```

---

# Architecture Diagram

```text
       User Requests

             |

             ▼

       Applications

             |

             ▼

Logs • Metrics • Traces

             |

             ▼

    SLI Calculations

             |

             ▼

 Reliability Dashboard
```

Telemetry data is transformed into meaningful service quality indicators.

---

# How It Works

The workflow:

```text
1. Users interact with the application.

2. Telemetry is collected.

3. Relevant measurements are calculated.

4. SLIs are continuously updated.

5. Engineers monitor service quality.

6. SLO compliance is evaluated using SLIs.
```

---

# Common Service Level Indicators

## Availability

Measures the percentage of successful service availability.

Example:

```text
Successful Requests

--------------------

Total Requests
```

Example result:

```text
99.95%
```

---

## Latency

Measures how quickly requests are processed.

Common measurements:

- Average
- P50
- P95
- P99

Example:

```text
P95

150 ms
```

---

## Error Rate

Measures the percentage of failed requests.

Example:

```text
Failed Requests

----------------

Total Requests
```

---

## Throughput

Measures the number of requests processed over time.

Example:

```text
500 Requests / Second
```

---

## Durability

Measures the likelihood that stored data is preserved without loss.

Example:

```text
99.999999999%
```

---

# User-Centric SLIs

Good SLIs measure what users actually experience.

Examples:

- Successful checkout completion
- Login success rate
- Video playback startup time
- Search response time
- Payment success rate

---

# Core Characteristics

## 1. Quantitative

SLIs are numerical measurements.

---

## 2. User Focused

They measure service quality from the user's perspective.

---

## 3. Continuously Measured

SLIs are updated using production telemetry.

---

## 4. Objective

They are based on measurable data rather than opinions.

---

## 5. Foundation for Reliability

SLIs form the basis for defining SLOs.

---

# Advantages

## 1. Objective Measurement

Provides clear, measurable indicators of service quality.

---

## 2. Better Reliability Tracking

Allows teams to monitor service performance consistently.

---

## 3. Customer-Centric

Focuses on the experience users actually receive.

---

## 4. Supports Automation

SLIs can drive dashboards, alerts, and reliability reporting.

---

## 5. Enables Continuous Improvement

Historical SLI data helps identify long-term trends and improvement opportunities.

---

# Disadvantages

## 1. Metric Selection

Poorly chosen SLIs may not reflect actual user experience.

---

## 2. Measurement Complexity

Some user experiences are difficult to quantify accurately.

---

## 3. Instrumentation Overhead

Applications must expose sufficient telemetry.

---

## 4. Maintenance

SLIs should evolve as applications and business priorities change.

---

## 5. Incomplete Picture

SLIs indicate service quality but do not explain the root cause of issues.

---

# Best Practices

- Measure user-visible behavior.
- Keep SLIs simple and meaningful.
- Use standardized calculations.
- Monitor SLIs continuously.
- Combine SLIs with logs, metrics, and traces for root cause analysis.

---

# Real-World Examples

## Google SRE

Defines SLIs for availability, latency, throughput, and correctness.

---

## Kubernetes Platforms

Track API server availability and request latency.

---

## AWS CloudWatch

Provides metrics that can be used to calculate SLIs.

---

## Prometheus

Collects telemetry for SLI calculations.

---

## Grafana

Visualizes SLIs through dashboards.

---

# When to Use

Use SLIs when:

- Measuring service reliability.
- Monitoring production applications.
- Defining SLOs.
- Tracking user experience.
- Building reliability dashboards.

---

# When NOT to Use

Avoid defining SLIs that:

- Measure only internal infrastructure without reflecting user experience.
- Cannot be measured consistently.
- Do not influence operational or business decisions.

---

# Comparison

| Feature | Metrics | SLIs |
|---|---|---|
| Purpose | Collect Measurements | Measure Service Quality |
| Scope | Any Numerical Value | User-Centric Indicators |
| Examples | CPU, Memory | Availability, Latency |
| Business Value | Indirect | Direct |

---

# Interview Questions

## 1. What is a Service Level Indicator (SLI)?

A quantitative measurement that reflects the quality of service experienced by users.

---

## 2. Give examples of common SLIs.

- Availability
- Latency
- Error Rate
- Throughput
- Durability

---

## 3. Why should SLIs be user-focused?

Because the goal is to measure the quality of service that customers actually experience.

---

## 4. How are SLIs different from ordinary metrics?

Metrics measure many aspects of a system, while SLIs are carefully selected metrics that represent user-facing service quality.

---

## 5. How are SLIs related to SLOs?

SLIs provide the measurements that are evaluated against Service Level Objectives (SLOs).

---

# Key Takeaways

- SLIs quantify service quality from the user's perspective.
- Availability, latency, error rate, throughput, and durability are common SLIs.
- Good SLIs are measurable, user-centric, and continuously monitored.
- SLIs provide the foundation for defining Service Level Objectives.
- They help engineering teams objectively measure and improve service reliability.

---

## Previous & Next

← Previous: [Alerting Pattern](06-Alerting-Pattern.md)

→ Next: [Service Level Objectives (SLOs)](08-Service-Level-Objectives-SLOs.md)