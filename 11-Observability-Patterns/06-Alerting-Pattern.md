# Alerting Pattern

## Introduction

The Alerting Pattern is an observability pattern where **monitoring systems continuously evaluate metrics, logs, traces, or events and notify operators when predefined conditions indicate potential issues**.

Rather than waiting for users to report problems, alerting enables engineering teams to detect and respond to incidents proactively.

The Alerting Pattern answers the question:

> **"How do we know when something requires immediate attention?"**

The main goals of the Alerting Pattern are:

- Detect production incidents quickly.
- Reduce Mean Time to Detect (MTTD).
- Enable rapid incident response.
- Minimize service downtime.
- Improve system reliability.

---

# Why was it Introduced?

Imagine an API whose response time suddenly increases.

Without alerting:

```text
API Latency

↓

Increases

↓

Users Notice

↓

Support Tickets
```

Engineers only become aware after customers are affected.

With alerting:

```text
API Latency

↓

Threshold Exceeded

↓

Alert Generated

↓

Engineer Notified
```

The operations team can investigate before widespread impact occurs.

---

# Architecture Diagram

```text
      Applications

      |     |     |

      ▼     ▼     ▼

Logs • Metrics • Traces

             |

             ▼

 Monitoring Platform

             |

 Alert Rules Evaluation

             |

             ▼

 Notification System

             |

             ▼

 Engineers / SRE Team
```

Telemetry is continuously evaluated against alerting rules.

---

# How It Works

The workflow:

```text
1. Applications generate telemetry.

2. Monitoring system collects telemetry.

3. Alert rules are evaluated.

4. A condition is met.

5. An alert is generated.

6. Notifications are sent.

7. Engineers investigate and resolve the issue.
```

---

# Alert Sources

## Metrics

Examples:

- CPU usage
- Memory utilization
- Error rate
- Request latency

---

## Logs

Examples:

- Exception frequency
- Authentication failures
- Database connection errors

---

## Traces

Examples:

- High request latency
- Slow downstream services

---

## Infrastructure Events

Examples:

- Node failures
- Disk space exhaustion
- Network outages

---

# Alert Severity Levels

## Informational

Provides operational information without requiring immediate action.

Example:

```text
Deployment Completed
```

---

## Warning

Indicates a potential issue that should be monitored.

Example:

```text
CPU Usage

70%
```

---

## Critical

Requires immediate attention.

Example:

```text
Database Down
```

---

# Alert Components

## Condition

The rule that determines when an alert is triggered.

Example:

```text
CPU > 90%
```

---

## Threshold

The value at which an alert should fire.

---

## Evaluation Window

The period over which conditions are evaluated.

Example:

```text
CPU > 90%

For

5 Minutes
```

---

## Notification

Delivery channels for alerts.

Examples:

- Email
- Slack
- Microsoft Teams
- PagerDuty
- SMS

---

# Core Characteristics

## 1. Automated

Alert generation requires no manual intervention.

---

## 2. Threshold-Based

Alerts are triggered by defined conditions.

---

## 3. Timely

Designed to notify operators as quickly as possible.

---

## 4. Actionable

Alerts should indicate a problem that requires investigation or action.

---

## 5. Observable

Built using telemetry such as metrics, logs, and traces.

---

# Advantages

## 1. Faster Incident Detection

Problems are identified before customers report them.

---

## 2. Reduced Downtime

Teams can respond quickly to failures.

---

## 3. Improved Reliability

Continuous monitoring helps maintain service availability.

---

## 4. Operational Awareness

Provides visibility into production systems.

---

## 5. Automation Friendly

Integrates with incident management and on-call systems.

---

# Disadvantages

## 1. Alert Fatigue

Too many unnecessary alerts can cause important alerts to be ignored.

---

## 2. False Positives

Poorly configured rules may generate unnecessary notifications.

---

## 3. False Negatives

Incorrect thresholds may fail to detect real issues.

---

## 4. Maintenance Overhead

Alert rules require continuous tuning as systems evolve.

---

## 5. Dependency on Monitoring

Alerting quality depends on accurate telemetry collection.

---

# Best Practices

- Alert only on actionable issues.
- Avoid duplicate alerts.
- Define clear severity levels.
- Use meaningful alert descriptions.
- Include runbooks or remediation links.
- Continuously review and refine alert thresholds.

---

# Real-World Examples

## Prometheus Alertmanager

Manages alert routing, grouping, and notifications.

---

## Grafana Alerting

Creates alerts from dashboards and metric queries.

---

## Amazon CloudWatch Alarms

Monitors AWS metrics and triggers notifications.

---

## Datadog Monitors

Supports infrastructure, application, and log-based alerts.

---

## PagerDuty

Provides incident management and on-call notification workflows.

---

# When to Use

Use the Alerting Pattern when:

- Operating production systems.
- Monitoring service health.
- Managing on-call rotations.
- Detecting infrastructure failures.
- Supporting Site Reliability Engineering (SRE) practices.

---

# When NOT to Use

Avoid creating alerts when:

- The condition is informational and requires no action.
- Thresholds are not well understood.
- Frequent, non-actionable notifications would contribute to alert fatigue.

---

# Comparison

| Feature | Monitoring | Alerting |
|---|---|---|
| Purpose | Observe System Health | Notify About Problems |
| User Interaction | Dashboards | Notifications |
| Trigger | Continuous Observation | Threshold Violation |
| Response | Manual Analysis | Immediate Investigation |
| Goal | Visibility | Incident Response |

---

# Interview Questions

## 1. What is the Alerting Pattern?

A pattern where monitoring systems evaluate telemetry and notify operators when predefined conditions indicate potential issues.

---

## 2. What causes alert fatigue?

Receiving excessive or non-actionable alerts, leading operators to ignore important notifications.

---

## 3. What types of telemetry can trigger alerts?

- Metrics
- Logs
- Traces
- Infrastructure events

---

## 4. Why should alerts be actionable?

Because every alert should represent a condition that requires investigation or corrective action.

---

## 5. Name popular alerting tools.

- Prometheus Alertmanager
- Grafana Alerting
- Amazon CloudWatch Alarms
- Datadog
- PagerDuty

---

# Key Takeaways

- Alerting enables proactive detection of production issues.
- Alerts are generated by evaluating telemetry against predefined rules.
- Well-designed alerts reduce downtime and improve operational response.
- Alert fatigue can be minimized by creating actionable, meaningful alerts.
- Alerting is a critical component of modern observability and Site Reliability Engineering.

---

## Previous & Next

← Previous: [Heartbeat Pattern](05-Heartbeat-Pattern.md)

→ Next: [Service Level Indicators (SLIs)](07-Service-Level-Indicators-SLIs.md)