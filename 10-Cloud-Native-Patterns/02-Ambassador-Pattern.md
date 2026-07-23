# Ambassador Pattern

## Introduction

The Ambassador Pattern is a cloud-native design pattern where **a dedicated proxy container acts as an intermediary between an application and external services**.

Instead of allowing the application to communicate directly with external systems, all outbound traffic is routed through the Ambassador container.

The Ambassador handles responsibilities such as:

- Service discovery
- Load balancing
- TLS termination
- Retries
- Traffic routing
- Protocol translation

The Ambassador Pattern answers the question:

> **"How can applications communicate with external services without embedding networking logic?"**

The main goals of the Ambassador Pattern are:

- Decouple networking from application code.
- Centralize outbound communication.
- Simplify service discovery.
- Improve resilience and observability.

---

# Why was it Introduced?

Imagine an application that communicates with several external services.

Without an Ambassador:

```text
Application

↓

Service Discovery

Load Balancing

Retries

TLS

Authentication

↓

External Services
```

The application must implement networking logic itself.

With an Ambassador:

```text
Application

↓

Ambassador Proxy

↓

External Services
```

The application simply sends requests to the local proxy.

---

# Architecture Diagram

```text
          Kubernetes Pod

+------------------------------------+

|  Application Container             |

|                                    |

|  localhost:8080                    |

+------------------------------------+

|  Ambassador Container              |

|                                    |

| Service Discovery                  |

| Load Balancing                     |

| TLS                                |

| Retries                            |

+------------------------------------+

               |

               ▼

      External Services
```

The Ambassador manages all outbound communication.

---

# How It Works

The workflow:

```text
1. Application sends a request.

2. Request goes to the Ambassador.

3. Ambassador discovers the destination.

4. Ambassador applies networking policies.

5. Ambassador forwards the request.

6. Response returns through the Ambassador.
```

---

# Common Responsibilities

## Service Discovery

Applications always communicate with localhost.

Example:

```text
Application

↓

localhost

↓

Ambassador

↓

orders-service.company.com
```

---

## Load Balancing

The Ambassador distributes requests across multiple service instances.

---

## Retry Logic

Automatically retries failed requests.

---

## TLS

Encrypts outbound communication.

---

## Authentication

Adds API keys, JWTs, or OAuth tokens before forwarding requests.

---

## Traffic Routing

Routes requests to different environments or service versions.

---

# Core Characteristics

## 1. Proxy-Based

The Ambassador acts as a network proxy.

---

## 2. Local Communication

Applications communicate only with localhost.

---

## 3. Transparent

Applications do not need to know service locations.

---

## 4. Independent Deployment

Networking logic evolves independently of application code.

---

## 5. Reusable

The same Ambassador configuration can support many services.

---

# Advantages

## 1. Separation of Concerns

Business logic remains independent of networking logic.

---

## 2. Simplified Applications

Applications communicate with a local endpoint.

---

## 3. Easier Configuration Changes

Networking behavior changes without modifying application code.

---

## 4. Better Resilience

Retries and failover can be handled centrally.

---

## 5. Improved Observability

Traffic can be monitored and logged by the Ambassador.

---

# Disadvantages

## 1. Additional Resource Usage

The proxy consumes CPU and memory.

---

## 2. Increased Latency

Every request passes through an additional component.

---

## 3. Operational Complexity

Proxy configuration must be managed carefully.

---

## 4. Debugging Challenges

Network issues may originate from the Ambassador rather than the application.

---

## 5. More Components

Each Pod contains additional containers.

---

# Real-World Examples

## Envoy Proxy

Acts as an Ambassador for outbound traffic in many cloud-native environments.

---

## NGINX Sidecar

Routes outbound requests from applications.

---

## HAProxy

Can function as an Ambassador proxy.

---

## Kubernetes Service Mesh

Envoy proxies used by Istio often perform Ambassador responsibilities for outbound traffic.

---

# When to Use

Use the Ambassador Pattern when:

- Accessing external APIs.
- Performing service discovery.
- Applying retries and timeouts.
- Centralizing TLS handling.
- Implementing outbound traffic policies.

---

# When NOT to Use

Avoid the Ambassador Pattern when:

- Applications communicate only with simple internal services.
- Networking requirements are minimal.
- The added proxy introduces unnecessary overhead.

---

# Comparison

| Feature | Ambassador | Sidecar |
|---|---|---|
| Primary Purpose | Outbound Communication | General Supporting Functionality |
| Acts as Proxy | Yes | Sometimes |
| Handles Networking | Yes | Optional |
| Scope | External Communication | Cross-Cutting Concerns |
| Runs in Same Pod | Yes | Yes |

---

# Interview Questions

## 1. What is the Ambassador Pattern?

A cloud-native pattern where a proxy container manages outbound communication between an application and external services.

---

## 2. Why do applications communicate with localhost?

Because the Ambassador proxy runs within the same Pod and forwards requests to external destinations.

---

## 3. What responsibilities can an Ambassador handle?

- Service discovery
- Load balancing
- Retries
- TLS
- Authentication
- Traffic routing

---

## 4. How does the Ambassador Pattern improve application design?

It separates networking concerns from business logic, making applications simpler and easier to maintain.

---

## 5. What is the difference between an Ambassador and a Sidecar?

A Sidecar provides any supporting functionality, while an Ambassador specifically manages outbound network communication.

---

# Key Takeaways

- The Ambassador Pattern centralizes outbound communication through a local proxy.
- Applications communicate with localhost instead of external services directly.
- The Ambassador handles service discovery, retries, TLS, and traffic routing.
- The pattern improves maintainability by separating networking concerns from business logic.
- It is commonly implemented using proxies such as Envoy or NGINX.

---

## Previous & Next

← Previous: [Sidecar Pattern](01-Sidecar-Pattern.md)

→ Next: [Adapter Pattern](03-Adapter-Pattern.md)