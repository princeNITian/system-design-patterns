# Health Check Pattern

## Introduction

The Health Check Pattern is an observability pattern where **applications expose endpoints or mechanisms that allow external systems to determine whether the application is healthy and ready to handle requests**.

Health checks enable orchestrators, load balancers, and monitoring systems to automatically detect unhealthy instances and take corrective actions.

The Health Check Pattern answers the question:

> **"Is this service healthy enough to receive traffic?"**

The main goals of the Health Check Pattern are:

- Detect unhealthy applications.
- Prevent traffic from reaching failed instances.
- Enable self-healing.
- Improve availability.
- Support automated orchestration.

---

# Why was it Introduced?

Imagine an application that has crashed internally but is still running.

Without health checks:

```text
Client

↓

Load Balancer

↓

Broken Application
```

The load balancer continues sending requests to a non-functional instance.

With health checks:

```text
Client

↓

Load Balancer

↓

Healthy Instance

❌ Unhealthy Instance Removed
```

Only healthy instances receive traffic.

---

# Architecture Diagram

```text
          Monitoring

               |

               ▼

        Health Endpoint

               |

               ▼

        Application

               |

               ▼

      Database / Cache
```

Health endpoints expose the application's current status.

---

# How It Works

The workflow:

```text
1. Monitoring system sends a health check request.

2. Application evaluates its health.

3. Application returns its status.

4. If healthy:
      Continue serving traffic.

5. If unhealthy:
      Remove instance from service or restart it.
```

---

# Types of Health Checks

## 1. Liveness Probe

Determines whether the application is still running.

If the liveness check fails:

```text
Restart Application
```

Common in Kubernetes.

---

## 2. Readiness Probe

Determines whether the application is ready to receive requests.

Example:

```text
Application Starting

↓

Not Ready

↓

Initialization Complete

↓

Ready
```

The application is not added to the load balancer until it is ready.

---

## 3. Startup Probe

Determines whether a slow-starting application has completed initialization.

Useful for applications with long startup times.

---

## 4. Dependency Health Check

Verifies connectivity to critical dependencies.

Examples:

- Database
- Cache
- Message Broker
- External APIs

---

# Example Health Endpoint

```http
GET /health
```

Healthy response:

```json
{
  "status": "UP"
}
```

Unhealthy response:

```json
{
  "status": "DOWN"
}
```

---

# Core Characteristics

## 1. Lightweight

Health checks should execute quickly.

---

## 2. Automated

External systems perform health checks continuously.

---

## 3. Observable

Expose application state in a standard format.

---

## 4. Actionable

Failures trigger automated responses.

---

## 5. Independent

Health checks should avoid unnecessary dependencies whenever possible.

---

# Advantages

## 1. Improved Availability

Unhealthy instances are removed automatically.

---

## 2. Self-Healing

Orchestrators can restart failed services.

---

## 3. Better Load Balancing

Traffic is routed only to healthy instances.

---

## 4. Faster Failure Detection

Issues are identified within seconds.

---

## 5. Cloud-Native Friendly

Integrates naturally with Kubernetes and cloud platforms.

---

# Disadvantages

## 1. False Positives

Poorly designed checks may incorrectly report failures.

---

## 2. Dependency Complexity

Checking every dependency can slow health responses.

---

## 3. Additional Requests

Health checks generate continuous traffic.

---

## 4. Incorrect Health Logic

Returning "healthy" despite critical failures can mislead orchestration systems.

---

## 5. Operational Tuning

Probe intervals, timeouts, and thresholds require careful configuration.

---

# Best Practices

- Keep health checks lightweight.
- Separate liveness and readiness logic.
- Avoid expensive database queries.
- Return appropriate HTTP status codes.
- Include dependency checks only when necessary.
- Use startup probes for applications with long initialization times.

---

# Real-World Examples

## Kubernetes

Uses Liveness, Readiness, and Startup Probes.

---

## AWS Elastic Load Balancer

Performs health checks before routing traffic.

---

## Google Kubernetes Engine (GKE)

Uses Kubernetes health probes for workload management.

---

## Azure Application Gateway

Routes traffic based on backend health.

---

## Spring Boot Actuator

Provides production-ready health endpoints.

---

# When to Use

Use the Health Check Pattern when:

- Deploying applications behind load balancers.
- Running Kubernetes workloads.
- Building highly available systems.
- Monitoring production services.
- Implementing self-healing architectures.

---

# When NOT to Use

Avoid overly complex health checks when:

- The application is simple and has no critical dependencies.
- Health checks would perform expensive operations that impact performance.
- Every dependency failure should not necessarily make the application unavailable.

---

# Comparison

| Feature | Liveness Probe | Readiness Probe |
|---|---|---|
| Purpose | Detect Crashed Application | Determine Traffic Readiness |
| Failure Action | Restart Container | Stop Receiving Traffic |
| Typical Usage | Self-Healing | Load Balancing |
| Kubernetes Support | Yes | Yes |

---

# Interview Questions

## 1. What is the Health Check Pattern?

A pattern where applications expose endpoints that allow external systems to determine whether they are healthy and ready to serve requests.

---

## 2. What is the difference between a Liveness Probe and a Readiness Probe?

A Liveness Probe determines whether an application should be restarted, while a Readiness Probe determines whether it should receive traffic.

---

## 3. Why are health checks important?

They improve availability by automatically detecting and removing unhealthy instances.

---

## 4. What is a Startup Probe?

A probe used to determine when slow-starting applications have completed initialization.

---

## 5. Name systems that commonly use health checks.

- Kubernetes
- AWS Elastic Load Balancer
- Azure Application Gateway
- Google Kubernetes Engine
- Spring Boot Actuator

---

# Key Takeaways

- Health checks allow automated systems to determine application health.
- Liveness, Readiness, and Startup Probes serve different operational purposes.
- Proper health checks improve availability, self-healing, and load balancing.
- Health checks should be lightweight and accurately reflect application state.
- They are a fundamental pattern in cloud-native and containerized environments.

---

## Previous & Next

← Previous: [Metrics Collection](03-Metrics-Collection.md)

→ Next: [Heartbeat Pattern](05-Heartbeat-Pattern.md)