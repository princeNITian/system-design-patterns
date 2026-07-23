# Error Budget

## Introduction

An Error Budget is **the maximum amount of unreliability or failure that a service is allowed within a defined Service Level Objective (SLO) measurement window**.

Instead of expecting 100% reliability, engineering teams intentionally allow a small amount of failure so they can continue delivering new features while maintaining an acceptable user experience.

Error Budgets answer the question:

> **"How much unreliability can we safely tolerate?"**

The main goals of Error Budgets are:

- Balance reliability and innovation.
- Guide release decisions.
- Prevent excessive production risk.
- Improve service reliability.
- Support data-driven engineering decisions.

---

# Why were Error Budgets Introduced?

Imagine a service with this SLO:

```text
Availability

99.9%
```

This means the service is allowed to be unavailable for:

```text
0.1%
```

That **0.1%** is the Error Budget.

If the Error Budget is exhausted:

```text
Stop Feature Releases

↓

Focus on Reliability
```

If sufficient Error Budget remains:

```text
Continue Deployments

↓

Ship New Features
```

Error Budgets help balance product velocity with operational stability.

---

# Relationship Between SLI, SLO, and Error Budget

```text
User Requests

↓

Service Level Indicator (SLI)

↓

Measured Availability

↓

Service Level Objective (SLO)

↓

99.9%

↓

Error Budget

↓

0.1%
```

The Error Budget is derived directly from the SLO.

---

# How It Works

The workflow:

```text
1. Define an SLO.

2. Calculate the Error Budget.

3. Monitor the SLI continuously.

4. Compare current performance against the SLO.

5. If Error Budget is available:
      Continue releases.

6. If Error Budget is exhausted:
      Prioritize reliability improvements.
```

---

# Calculating an Error Budget

Example:

```text
Availability SLO

99.9%
```

Error Budget:

```text
100%

-

99.9%

=

0.1%
```

---

## Example for a 30-Day Month

```text
30 Days

↓

43,200 Minutes
```

Allowed downtime:

```text
43,200 × 0.1%

=

43.2 Minutes
```

The service may be unavailable for approximately **43 minutes** during the month while still meeting its SLO.

---

# Error Budget Policy

## Budget Available

Example:

```text
Remaining Budget

80%
```

Actions:

- Continue feature releases.
- Deploy normally.
- Perform experiments.

---

## Budget Nearly Exhausted

Example:

```text
Remaining Budget

10%
```

Actions:

- Increase monitoring.
- Reduce deployment frequency.
- Investigate recurring issues.

---

## Budget Exhausted

Example:

```text
Remaining Budget

0%
```

Actions:

- Pause non-critical feature releases.
- Prioritize reliability improvements.
- Resolve production issues before resuming normal deployment.

---

# Core Characteristics

## 1. SLO-Based

Error Budgets are derived from Service Level Objectives.

---

## 2. Quantitative

Represent measurable allowable failure.

---

## 3. Time-Bound

Calculated over a defined measurement window.

---

## 4. Decision-Oriented

Guide release and operational decisions.

---

## 5. Reliability Focused

Encourage sustainable engineering practices.

---

# Advantages

## 1. Balances Innovation and Stability

Teams can continue delivering features while protecting reliability.

---

## 2. Objective Decision Making

Release decisions are based on measurable data rather than intuition.

---

## 3. Better Risk Management

Reduces the likelihood of repeated reliability issues.

---

## 4. Improved Collaboration

Provides a shared framework for product and engineering teams.

---

## 5. Encourages Continuous Improvement

Recurring Error Budget consumption highlights areas for reliability investment.

---

# Disadvantages

## 1. Requires Well-Defined SLOs

Error Budgets are only meaningful if SLOs are accurate.

---

## 2. Measurement Complexity

Reliable telemetry and SLI calculations are essential.

---

## 3. Organizational Discipline

Teams must consistently follow Error Budget policies.

---

## 4. Business Trade-Offs

Pausing releases may conflict with business priorities.

---

## 5. Continuous Monitoring Required

Budget consumption must be tracked throughout the measurement window.

---

# Best Practices

- Define realistic SLOs before calculating Error Budgets.
- Monitor Error Budget consumption continuously.
- Agree on clear policies for release decisions.
- Review Error Budgets during incident retrospectives.
- Use Error Budgets as a collaboration tool between engineering and product teams.

---

# Real-World Examples

## Google SRE

Popularized the Error Budget concept as a core SRE practice.

---

## Kubernetes Platforms

Use Error Budgets alongside SLO monitoring for production reliability.

---

## Grafana

Visualizes SLO compliance and Error Budget consumption.

---

## Datadog

Tracks Error Budget burn rates for production services.

---

## Prometheus

Provides telemetry for Error Budget calculations.

---

# Burn Rate

Burn Rate measures **how quickly an Error Budget is being consumed**.

Example:

```text
Normal Consumption

↓

Slow Burn
```

```text
Major Outage

↓

Fast Burn
```

A high burn rate indicates that the Error Budget may be exhausted before the measurement window ends.

---

# When to Use

Use Error Budgets when:

- Practicing Site Reliability Engineering (SRE).
- Managing production services.
- Defining Service Level Objectives.
- Balancing reliability with release velocity.
- Making data-driven deployment decisions.

---

# When NOT to Use

Avoid using Error Budgets when:

- No meaningful SLOs exist.
- Service quality cannot be measured objectively.
- Teams are not prepared to act on Error Budget policies.

---

# Comparison

| Feature | SLO | Error Budget |
|---|---|---|
| Purpose | Define Reliability Target | Define Allowed Failure |
| Example | Availability ≥ 99.9% | Remaining 0.1% Failure |
| Focus | Goal | Operational Decision |
| Based On | SLIs | SLOs |

---

# Interview Questions

## 1. What is an Error Budget?

The maximum amount of unreliability a service can experience while still meeting its SLO.

---

## 2. How is an Error Budget calculated?

By subtracting the SLO target from 100%.

Example:

```text
100% − 99.9% = 0.1%
```

---

## 3. What happens when the Error Budget is exhausted?

Engineering teams typically pause non-critical releases and focus on improving reliability.

---

## 4. What is Burn Rate?

The speed at which an Error Budget is being consumed over time.

---

## 5. Why are Error Budgets important?

They help balance feature delivery with system reliability using objective operational data.

---

# Key Takeaways

- Error Budgets define the allowable amount of failure within an SLO window.
- They are derived directly from Service Level Objectives.
- Error Budgets help engineering teams make objective release decisions.
- Burn Rate measures how quickly the budget is being consumed.
- Error Budgets are a foundational practice in modern Site Reliability Engineering.

---

# Module Summary

Congratulations! You have completed the **Observability Patterns** module.

You now understand:

- Centralized Logging
- Distributed Tracing
- Metrics Collection
- Health Check Pattern
- Heartbeat Pattern
- Alerting Pattern
- Service Level Indicators (SLIs)
- Service Level Objectives (SLOs)
- Error Budgets

These patterns provide the operational visibility and reliability practices required to successfully run large-scale distributed systems in production.

---

## Previous & Next

← Previous: [Service Level Objectives (SLOs)](08-Service-Level-Objectives-SLOs.md)

→ Next Module: [12-System-Design-Case-Studies](../12-System-Design-Case-Studies/README.md)