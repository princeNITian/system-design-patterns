# Heartbeat Pattern

## Introduction

The Heartbeat Pattern is an observability pattern where **services periodically send a signal (heartbeat) to indicate that they are alive and functioning**.

If heartbeats stop arriving within an expected time window, monitoring systems assume that the service has failed or become unreachable.

The Heartbeat Pattern answers the question:

> **"Is this service still alive?"**

The main goals of the Heartbeat Pattern are:

- Detect service failures quickly.
- Monitor long-running processes.
- Support self-healing systems.
- Improve system reliability.
- Enable automated failure detection.

---

# Why was it Introduced?

Imagine a background worker processing jobs.

Without heartbeats:

```text
Worker

↓

Stops Running

↓

Nobody Knows
```

The worker silently fails.

With heartbeats:

```text
Worker

↓

Heartbeat Every 30 Seconds

↓

Monitoring System

↓

Heartbeat Missing

↓

Failure Detected
```

The monitoring system detects failures automatically.

---

# Architecture Diagram

```text
        Worker Service

              |

      Heartbeat Signal

              |

              ▼

    Monitoring System

              |

              ▼

 Alert / Recovery Action
```

The monitoring system expects periodic heartbeat messages from the service.

---

# How It Works

The workflow:

```text
1. Service starts.

2. Service periodically sends a heartbeat.

3. Monitoring system records heartbeat timestamps.

4. If heartbeats continue:
      Service is healthy.

5. If heartbeats stop:
      Service is marked as unhealthy.

6. Alerts or recovery actions are triggered.
```

---

# Common Heartbeat Mechanisms

## HTTP Request

Example:

```text
Worker

↓

POST /heartbeat
```

---

## Message Queue

Example:

```text
Worker

↓

Heartbeat Event

↓

Kafka
```

---

## Database Update

Example:

```text
Worker

↓

Update Last Seen Timestamp
```

---

## Distributed Cache

Example:

```text
Redis

↓

Heartbeat Key Updated
```

---

## Monitoring Agent

Infrastructure agents periodically report system health.

---

# Heartbeat Components

## Sender

The application or service sending heartbeat signals.

---

## Receiver

The monitoring platform receiving heartbeat messages.

---

## Timeout

Maximum allowed interval before considering a heartbeat missing.

Example:

```text
Heartbeat Every

30 Seconds

↓

Timeout

90 Seconds
```

---

## Recovery

Automated actions taken after heartbeat failure.

Examples:

- Restart service
- Replace container
- Notify operators

---

# Core Characteristics

## 1. Periodic

Heartbeats are sent at regular intervals.

---

## 2. Lightweight

Heartbeat messages should contain minimal data.

---

## 3. Automated

Sending and monitoring heartbeats requires no manual intervention.

---

## 4. Failure Detection

Missing heartbeats indicate potential failures.

---

## 5. Independent

Monitoring is external to the application being monitored.

---

# Advantages

## 1. Fast Failure Detection

Quickly identifies failed or unreachable services.

---

## 2. Improved Reliability

Supports automated recovery mechanisms.

---

## 3. Simple Implementation

Heartbeat messages are small and easy to generate.

---

## 4. Cloud-Native Friendly

Works well with distributed and containerized systems.

---

## 5. Continuous Monitoring

Provides ongoing confirmation that services remain operational.

---

# Disadvantages

## 1. False Positives

Temporary network interruptions may appear as service failures.

---

## 2. Additional Network Traffic

Periodic heartbeats consume bandwidth, although typically minimal.

---

## 3. Timeout Configuration

Timeouts that are too short or too long can reduce effectiveness.

---

## 4. Limited Information

A heartbeat confirms that a service is alive, but not necessarily that it is functioning correctly.

---

## 5. Monitoring Dependency

Heartbeat detection relies on the availability of the monitoring system.

---

# Best Practices

- Keep heartbeat messages lightweight.
- Choose heartbeat intervals appropriate for business requirements.
- Configure reasonable timeout thresholds.
- Combine heartbeats with health checks and metrics.
- Trigger automated recovery only after confirming sustained heartbeat failures.

---

# Real-World Examples

## Kubernetes Node Heartbeats

Worker nodes periodically report their status to the Kubernetes control plane.

---

## Apache Kafka Consumers

Consumers periodically send heartbeats to the consumer group coordinator to maintain membership.

---

## ZooKeeper

Distributed systems use heartbeats to maintain active sessions.

---

## Redis Sentinel

Monitors Redis instances through periodic health communication.

---

## Monitoring Platforms

Tools such as Datadog, Nagios, and Amazon CloudWatch Synthetics can monitor heartbeat signals.

---

# When to Use

Use the Heartbeat Pattern when:

- Monitoring long-running background workers.
- Supervising distributed services.
- Detecting node failures.
- Managing scheduled jobs.
- Building self-healing systems.

---

# When NOT to Use

Avoid relying solely on heartbeats when:

- You need detailed application health beyond simple liveness.
- Event-driven systems already provide reliable activity signals.
- Health checks or distributed tracing provide more appropriate operational insight.

---

# Comparison

| Feature | Health Check | Heartbeat |
|---|---|---|
| Trigger | External System | Service Itself |
| Purpose | Verify Health | Confirm Liveness |
| Communication | Request-Response | Periodic Signal |
| Typical Use | APIs, Web Services | Workers, Nodes, Distributed Systems |

---

# Interview Questions

## 1. What is the Heartbeat Pattern?

A pattern where services periodically send signals indicating that they are alive.

---

## 2. How is a heartbeat different from a health check?

A heartbeat is proactively sent by the service, while a health check is initiated by an external system.

---

## 3. What happens when heartbeats stop arriving?

The monitoring system assumes the service may have failed and can trigger alerts or recovery actions.

---

## 4. Name systems that commonly use heartbeats.

- Kubernetes
- Apache Kafka
- ZooKeeper
- Redis Sentinel

---

## 5. Why shouldn't heartbeats be the only monitoring mechanism?

Because a service can still send heartbeats while experiencing degraded functionality; metrics, logs, and health checks provide additional context.

---

# Key Takeaways

- Heartbeats provide continuous confirmation that services are alive.
- Missing heartbeats enable fast failure detection and automated recovery.
- The pattern is widely used in distributed systems and orchestration platforms.
- Heartbeats complement health checks rather than replace them.
- Proper timeout configuration is essential to avoid false alarms.

---

## Previous & Next

← Previous: [Health Check Pattern](04-Health-Check-Pattern.md)

→ Next: [Alerting Pattern](06-Alerting-Pattern.md)