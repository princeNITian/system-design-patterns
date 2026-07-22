# Health Check

## Introduction

The Health Check pattern is a resilience pattern that **continuously monitors the health and availability of applications, services, and infrastructure**.

Instead of assuming that a service is operational, health checks periodically verify whether it is functioning correctly. This enables load balancers, orchestrators, and monitoring systems to route traffic only to healthy instances.

The main goals of the Health Check pattern are:

- Detect unhealthy services.
- Improve availability.
- Enable automatic recovery.
- Support intelligent traffic routing.

---

## Why was it Introduced?

In distributed systems, services can fail because of:

- Application crashes.
- Database failures.
- Resource exhaustion.
- Network issues.

Without health checks:

```text
Load Balancer

      |

      ▼

Dead Service
```

Traffic continues to be sent to unavailable instances.

Health checks allow unhealthy services to be removed from rotation.

---

## Architecture Diagram

```text
           Client

              |

              ▼

        Load Balancer

        /          \

       ▼            ▼

 Service A      Service B

      ▲             ▲

      |             |

 Health Check   Health Check

      |             |

 Monitoring System
```

Only healthy services receive traffic.

---

## How It Works

The communication flow:

```text
1. Monitoring system sends periodic health requests.

2. Service performs health validation.

3. Service returns its health status.

4. Healthy services remain available.

5. Unhealthy services are removed from traffic.

6. Recovery is detected through subsequent health checks.
```

Example:

```text
GET /health

      |

Database Connected

Cache Connected

Memory Normal

      |

HTTP 200 OK
```

---

# Core Components

## 1. Health Endpoint

An endpoint that reports the service's health.

Example:

```text
GET /health
```

---

## 2. Monitoring System

Continuously checks service health.

Examples:

- Kubernetes
- Load Balancers
- Monitoring platforms

---

## 3. Health Status

Typical responses include:

- Healthy
- Unhealthy
- Degraded

---

## 4. Recovery Logic

Returns the service to normal operation after successful health checks.

---

# Core Characteristics

## 1. Continuous Monitoring

Health is checked at regular intervals.

---

## 2. Automatic Detection

Failures are identified without manual intervention.

---

## 3. Traffic Protection

Requests are routed only to healthy instances.

---

## 4. Fast Recovery

Recovered services automatically return to service.

---

## 5. Operational Visibility

Health information is available for monitoring and alerting.

---

# Types of Health Checks

## 1. Liveness Check

Determines whether the application is still running.

---

## 2. Readiness Check

Determines whether the application is ready to accept traffic.

---

## 3. Startup Check

Determines whether the application has completed startup successfully.

---

## 4. Dependency Check

Verifies external dependencies such as databases, caches, and message brokers.

---

# Advantages

## 1. Improved Availability

Traffic is routed only to healthy instances.

---

## 2. Automatic Recovery

Recovered services can automatically receive traffic again.

---

## 3. Better Fault Detection

Problems are detected quickly.

---

## 4. Supports Auto Scaling

Healthy instances can be added or removed automatically.

---

## 5. Better Monitoring

Provides valuable operational insights.

---

# Disadvantages

## 1. Additional Overhead

Health checks consume network and compute resources.

---

## 2. Configuration Challenges

Incorrect health checks can remove healthy services or keep unhealthy ones active.

---

## 3. Limited Validation

A healthy endpoint does not always guarantee correct business functionality.

---

## 4. Dependency Complexity

Determining which dependencies to include requires careful design.

---

## 5. Monitoring Infrastructure Required

Health checks rely on monitoring systems to be effective.

---

# Real-World Examples

## Kubernetes

Uses liveness, readiness, and startup probes to manage containers.

---

## Load Balancers

Route traffic only to healthy backend servers.

---

## Cloud Platforms

Continuously monitor virtual machines and managed services.

---

## Microservices

Expose health endpoints for orchestration and monitoring.

---

# When to Use

Use the Health Check pattern when:

- Deploying distributed systems.
- Using load balancers.
- Running containerized applications.
- Automatic recovery is required.

---

# When NOT to Use

Avoid relying solely on Health Checks when:

- Business-level validation is required.
- A simple process check is insufficient to determine service health.

---

# Comparison

| Feature | No Health Check | Health Check |
|---|---|---|
| Failure Detection | Manual | Automatic |
| Traffic Routing | Unaware | Health-Based |
| Recovery | Manual | Automatic |
| Availability | Lower | Higher |
| Monitoring | Limited | Comprehensive |

---

# Interview Questions

## 1. What is the Health Check pattern?

A resilience pattern that monitors whether a service is healthy and capable of handling requests.

---

## 2. What is the difference between liveness and readiness checks?

Liveness checks determine whether the application is running.

Readiness checks determine whether it is ready to receive traffic.

---

## 3. Why are Health Checks important?

They allow unhealthy services to be removed from traffic automatically, improving availability.

---

## 4. What dependencies are commonly checked?

- Databases.
- Caches.
- Message brokers.
- External APIs.

---

## 5. Where are Health Checks commonly used?

- Kubernetes.
- Load Balancers.
- Microservices.
- Cloud-native applications.

---

# Key Takeaways

- Health Checks continuously monitor service availability.
- They help route traffic only to healthy instances.
- Liveness, readiness, and startup checks serve different purposes.
- They improve reliability, availability, and automatic recovery.
- They are a foundational practice in modern cloud-native systems.

---

## Previous & Next

← Previous: [Dead Letter Queue (DLQ)](06-Dead-Letter-Queue-DLQ.md)

→ Next: [Leader Election](08-Leader-Election.md)