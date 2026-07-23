# Service Discovery

## Introduction

Service Discovery is a distributed system pattern that **enables services to automatically find and communicate with one another without hardcoding network locations**.

In modern distributed systems, services are frequently created, terminated, scaled, and moved across different machines. Service Discovery ensures that clients can always locate the correct service instance.

The main goals of Service Discovery are:

- Eliminate hardcoded service addresses.
- Support dynamic infrastructure.
- Enable automatic service registration.
- Improve scalability and availability.

---

## Why was it Introduced?

Consider a microservices application.

```text
Order Service

↓

Payment Service

↓

Inventory Service
```

If every service stores fixed IP addresses:

```text
Payment Service

↓

10.0.0.15
```

Problems occur when:

- Containers restart.
- Virtual machines are replaced.
- Kubernetes schedules pods on new nodes.
- Auto Scaling creates new instances.

IP addresses change frequently, making hardcoded addresses unreliable.

Service Discovery solves this by maintaining a dynamic registry of available service instances.

---

## Architecture Diagram

```text
             Service Registry

          (Consul / etcd / Eureka)

                  ▲

        Register  |  Lookup

                  |

     -----------------------------

     |             |            |

     ▼             ▼            ▼

Order Service  Payment Service  Inventory Service
```

Services register themselves and clients discover them through the registry.

---

## How It Works

The execution flow:

```text
1. Service starts.

2. Service registers with the registry.

3. Clients query the registry.

4. Registry returns available instances.

5. Client communicates with the selected service.

6. Unhealthy instances are removed automatically.
```

Example:

```text
Payment Service

↓

Register

↓

Registry

↓

Order Service Lookup

↓

Payment Service Address Returned
```

---

# Types of Service Discovery

## 1. Client-Side Discovery

The client queries the service registry and selects a service instance.

```text
Client

↓

Service Registry

↓

Service Instance
```

Examples:

- Netflix Ribbon (legacy)
- Consul clients

---

## 2. Server-Side Discovery

The client sends requests to a load balancer, which queries the registry and forwards traffic.

```text
Client

↓

Load Balancer

↓

Service Registry

↓

Service Instance
```

Examples:

- Kubernetes Services
- AWS Elastic Load Balancer
- Envoy Proxy

---

# Core Characteristics

## 1. Dynamic Registration

Services register automatically when they start.

---

## 2. Health Monitoring

Unhealthy instances are removed from the registry.

---

## 3. Automatic Discovery

Clients locate services without knowing IP addresses.

---

## 4. Scalability

Supports rapidly changing service instances.

---

## 5. Decoupling

Clients depend on service names rather than physical locations.

---

# Advantages

## 1. No Hardcoded Addresses

Infrastructure changes do not require application updates.

---

## 2. Automatic Scaling

New instances become discoverable immediately after registration.

---

## 3. High Availability

Clients can route traffic to healthy service instances.

---

## 4. Cloud-Native Friendly

Works naturally with containers and orchestration platforms.

---

## 5. Simplified Operations

Infrastructure changes become transparent to applications.

---

# Disadvantages

## 1. Additional Infrastructure

A service registry must be deployed and maintained.

---

## 2. Registry Availability

The registry becomes a critical system component.

---

## 3. Health Check Complexity

Incorrect health checks can expose unhealthy instances.

---

## 4. Registration Delays

New instances may require time before becoming discoverable.

---

## 5. Operational Overhead

Monitoring and securing the registry require additional effort.

---

# Real-World Examples

## Kubernetes

Uses Services and DNS-based discovery for locating Pods.

---

## Consul

Provides service registration, discovery, and health checking.

---

## Netflix Eureka

Maintains dynamic service registration for microservices.

---

## etcd

Stores cluster metadata and service information for distributed systems.

---

# When to Use

Use Service Discovery when:

- Building microservices.
- Running dynamic cloud infrastructure.
- Using containers or Kubernetes.
- Supporting automatic scaling.
- Avoiding hardcoded service locations.

---

# When NOT to Use

Avoid Service Discovery when:

- Running a simple monolithic application.
- Service endpoints rarely change.
- Infrastructure is static and manually managed.

---

# Comparison

| Feature | Static Configuration | Service Discovery |
|---|---|---|
| Service Address | Hardcoded | Dynamic |
| Scaling | Manual | Automatic |
| Infrastructure Changes | Application Updates Required | Transparent |
| Fault Tolerance | Lower | Higher |
| Cloud-Native Support | Limited | Excellent |

---

# Interview Questions

## 1. What is Service Discovery?

A pattern that allows services to automatically locate and communicate with one another without using fixed network addresses.

---

## 2. Why is Service Discovery important?

Because service instances frequently change in cloud-native and distributed environments.

---

## 3. What are the two main types of Service Discovery?

- Client-Side Discovery
- Server-Side Discovery

---

## 4. Which systems commonly provide Service Discovery?

- Kubernetes
- Consul
- Eureka
- etcd

---

## 5. What is the role of a Service Registry?

It stores service locations, health information, and metadata so clients can discover available instances.

---

# Key Takeaways

- Service Discovery eliminates hardcoded service addresses.
- Services dynamically register with a service registry.
- Clients discover healthy service instances automatically.
- It is a core component of cloud-native and microservices architectures.
- Kubernetes, Consul, Eureka, and etcd all provide service discovery capabilities.

---

## Previous & Next

← Previous: [Gossip Protocol](07-Gossip-Protocol.md)

→ Next: [Heartbeat](09-Heartbeat.md)