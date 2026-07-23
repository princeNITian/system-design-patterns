# Service Level Objectives (SLOs)

## Introduction

Service Level Objectives (SLOs) are **target reliability goals defined for one or more Service Level Indicators (SLIs)**.

While an SLI measures current service performance, an SLO defines **the acceptable level of performance that the service should achieve**.

For example:

- **SLI:** Availability = 99.96%
- **SLO:** Availability ≥ 99.9%

SLOs answer the question:

> **"What level of service quality are we committed to achieving?"**

The main goals of SLOs are:

- Define measurable reliability targets.
- Align engineering with business expectations.
- Guide operational decisions.
- Improve user experience.
- Balance innovation with reliability.

---

# Why were SLOs Introduced?

Imagine a service without defined reliability goals.

```text
Latency

120 ms

↓

Is this good?
```

No one knows.

Now define an SLO:

```text
P95 Latency

Target

< 200 ms
```

The service can now be objectively evaluated.

---

# Architecture Diagram

```text
      Applications

             |

             ▼

Logs • Metrics • Traces

             |

             ▼

      SLI Calculation

             |

             ▼

     Compare Against SLO

             |

     Meets Target?

      /          \

    Yes          No

     |            |

 Continue    Investigate
```

SLIs are continuously evaluated against predefined SLO targets.

---

# How It Works

The workflow:

```text
1. Applications generate telemetry.

2. SLIs are calculated.

3. SLO targets are defined.

4. SLIs are compared against SLOs.

5. Teams monitor compliance.

6. Violations trigger investigation or corrective actions.
```

---

# Components of an SLO

## Service Level Indicator (SLI)

The metric being measured.

Example:

```text
Availability
```

---

## Target

The reliability goal.

Example:

```text
99.9%
```

---

## Measurement Window

The time period over which compliance is evaluated.

Examples:

- 30 days
- 7 days
- 1 quarter

---

# Common SLO Examples

## Availability

```text
SLI

Availability

Target

99.95%

Window

30 Days
```

---

## Latency

```text
95% of Requests

< 200 ms
```

---

## Error Rate

```text
Error Rate

< 0.1%
```

---

## Successful Checkout

```text
99.9%

Successful Checkout Requests
```

---

## Login Success

```text
99.95%

Successful Logins
```

---

# Good SLO Characteristics

A good SLO should be:

- Measurable
- User-focused
- Realistic
- Actionable
- Time-bound

---

# Core Characteristics

## 1. Objective

Defines measurable reliability goals.

---

## 2. User-Centric

Focuses on customer experience rather than internal infrastructure.

---

## 3. Time-Based

Evaluated over defined time windows.

---

## 4. Operational

Guides engineering priorities and operational decisions.

---

## 5. Quantifiable

Based on numerical targets.

---

# Advantages

## 1. Clear Reliability Goals

Everyone understands expected service quality.

---

## 2. Better Decision Making

Engineering teams prioritize work using objective targets.

---

## 3. Improved User Experience

Reliability goals align with customer expectations.

---

## 4. Performance Visibility

Provides measurable operational success criteria.

---

## 5. Supports Continuous Improvement

Historical compliance data identifies long-term reliability trends.

---

# Disadvantages

## 1. Poorly Defined Targets

Unrealistic SLOs can create unnecessary operational pressure.

---

## 2. Maintenance

SLOs should evolve as products and customer expectations change.

---

## 3. Measurement Challenges

Some user experiences are difficult to measure accurately.

---

## 4. Operational Complexity

Requires reliable telemetry and accurate SLI calculations.

---

## 5. Business Alignment Required

Technical teams and business stakeholders must agree on meaningful targets.

---

# Best Practices

- Define user-focused objectives.
- Keep SLOs measurable.
- Select realistic targets.
- Review SLOs regularly.
- Use SLOs to prioritize reliability work.
- Combine SLOs with Error Budgets for release decisions.

---

# Real-World Examples

## Google SRE

Uses SLOs as the primary reliability target for production services.

---

## Kubernetes Platforms

Track API availability and request latency against SLOs.

---

## Prometheus

Collects the telemetry used to evaluate SLO compliance.

---

## Grafana

Visualizes SLO dashboards.

---

## Datadog

Supports SLO tracking and reporting.

---

# When to Use

Use SLOs when:

- Operating production services.
- Managing customer-facing applications.
- Measuring reliability.
- Building SRE practices.
- Tracking long-term service quality.

---

# When NOT to Use

Avoid defining SLOs when:

- Reliable SLIs do not exist.
- Targets cannot be measured objectively.
- Internal engineering metrics are mistaken for customer-facing reliability indicators.

---

# Comparison

| Feature | SLI | SLO |
|---|---|---|
| Purpose | Measure Performance | Define Target |
| Example | Availability = 99.96% | Availability ≥ 99.9% |
| Nature | Measurement | Goal |
| Usage | Observability | Reliability Management |

---

# Interview Questions

## 1. What is an SLO?

A measurable reliability target defined for one or more Service Level Indicators.

---

## 2. How is an SLO different from an SLI?

An SLI measures current performance, while an SLO defines the desired target for that performance.

---

## 3. Give examples of common SLOs.

- Availability ≥ 99.9%
- P95 latency < 200 ms
- Error rate < 0.1%
- Successful login rate ≥ 99.95%

---

## 4. Why should SLOs be user-focused?

Because they should reflect the quality of service experienced by customers rather than internal infrastructure metrics.

---

## 5. How do SLOs help engineering teams?

They provide objective reliability goals that guide operational priorities and continuous improvement.

---

# Key Takeaways

- SLOs define measurable reliability targets based on SLIs.
- They align engineering efforts with user expectations and business goals.
- Effective SLOs are measurable, realistic, and time-bound.
- SLOs are a core practice in Site Reliability Engineering.
- Error Budgets are derived from SLOs and help balance reliability with feature development.

---

## Previous & Next

← Previous: [Service Level Indicators (SLIs)](07-Service-Level-Indicators-SLIs.md)

→ Next: [Error Budget](09-Error-Budget.md)