# Adapter Pattern

## Introduction

The Adapter Pattern is a cloud-native design pattern where **a dedicated component translates requests or responses between an application and an external system with an incompatible interface or protocol**.

Instead of modifying the application or the external service, the Adapter acts as a translator between the two.

The Adapter Pattern answers the question:

> **"How can two systems communicate without changing either of them?"**

The main goals of the Adapter Pattern are:

- Bridge incompatible interfaces.
- Decouple applications from external systems.
- Enable protocol transformation.
- Simplify system integration.

---

# Why was it Introduced?

Imagine a modern microservice that produces JSON, but an existing legacy system only understands XML.

Without an Adapter:

```text
Application

↓

Generate JSON

↓

Convert to XML

↓

Legacy System
```

The application must include legacy conversion logic.

With an Adapter:

```text
Application

↓

JSON

↓

Adapter

↓

XML

↓

Legacy System
```

The application remains independent of legacy requirements.

---

# Architecture Diagram

```text
          Kubernetes Pod

+----------------------------------+

|  Application Container           |

|                                  |

|      JSON / HTTP                 |

+----------------------------------+

|  Adapter Container               |

|                                  |

| JSON → XML                       |

| HTTP → gRPC                      |

| Protocol Translation             |

+----------------------------------+

               |

               ▼

        External Service
```

The Adapter converts requests and responses between the application and the external service.

---

# How It Works

The workflow:

```text
1. Application sends a request.

2. Adapter receives the request.

3. Adapter transforms the protocol or data format.

4. Adapter forwards the request.

5. External service responds.

6. Adapter transforms the response.

7. Application receives the translated response.
```

---

# Common Transformations

## Data Format Conversion

Example:

```text
JSON

↓

Adapter

↓

XML
```

---

## Protocol Conversion

Example:

```text
HTTP

↓

Adapter

↓

gRPC
```

---

## API Version Translation

Example:

```text
API v2

↓

Adapter

↓

API v1
```

---

## Message Format Conversion

Example:

```text
Avro

↓

Adapter

↓

JSON
```

---

## Legacy System Integration

Applications communicate with modern interfaces while the Adapter handles legacy communication.

---

# Core Characteristics

## 1. Translation Layer

The Adapter converts incompatible interfaces.

---

## 2. Decoupling

Applications remain independent of external system implementations.

---

## 3. Reusability

A single Adapter can support multiple applications.

---

## 4. Independent Evolution

Applications and external systems can evolve separately.

---

## 5. Transparent Integration

Applications interact with a consistent interface.

---

# Advantages

## 1. Simplifies Integration

Bridges incompatible systems without modifying them.

---

## 2. Protects Business Logic

Applications avoid embedding protocol conversion logic.

---

## 3. Supports Legacy Systems

Modern applications can communicate with older systems.

---

## 4. Easier Maintenance

Changes to external interfaces are isolated within the Adapter.

---

## 5. Encourages Loose Coupling

Applications depend on stable interfaces rather than implementation details.

---

# Disadvantages

## 1. Additional Component

Introduces another service or container to maintain.

---

## 2. Performance Overhead

Request and response transformations add processing time.

---

## 3. Increased Complexity

Translation logic can become complex for large systems.

---

## 4. Debugging Challenges

Issues may occur within the Adapter rather than the application or external service.

---

## 5. Maintenance Cost

Adapters must be updated when external interfaces change.

---

# Real-World Examples

## gRPC-JSON Gateway

Translates REST requests into gRPC calls.

---

## GraphQL Gateway

Aggregates and adapts multiple REST or gRPC APIs into a single GraphQL endpoint.

---

## Kafka Connect

Uses connectors to adapt external systems to Kafka.

---

## Legacy Banking Integration

Converts modern REST requests into SOAP or proprietary protocols.

---

# When to Use

Use the Adapter Pattern when:

- Integrating legacy systems.
- Converting between protocols.
- Supporting multiple API versions.
- Translating data formats.
- Connecting incompatible services.

---

# When NOT to Use

Avoid the Adapter Pattern when:

- Systems already share compatible interfaces.
- The transformation logic is trivial.
- Introducing an additional component provides little value.

---

# Comparison

| Feature | Adapter | Ambassador |
|---|---|---|
| Primary Purpose | Interface Translation | Outbound Communication |
| Protocol Conversion | Yes | No |
| Data Transformation | Yes | No |
| Networking Features | Limited | Extensive |
| Common Use | Legacy Integration | Service Communication |

---

# Interview Questions

## 1. What is the Adapter Pattern?

A cloud-native pattern that translates between incompatible interfaces, protocols, or data formats.

---

## 2. Why is the Adapter Pattern useful?

It allows independent systems to communicate without modifying either system.

---

## 3. What kinds of transformations can an Adapter perform?

- JSON ↔ XML
- REST ↔ gRPC
- API version translation
- Message format conversion

---

## 4. How does the Adapter Pattern improve maintainability?

By isolating transformation logic in one component instead of spreading it across applications.

---

## 5. Give examples of Adapter implementations.

- gRPC Gateway
- GraphQL Gateway
- Kafka Connect
- Legacy SOAP adapters

---

# Key Takeaways

- The Adapter Pattern enables communication between incompatible systems.
- It translates protocols, APIs, and data formats.
- Applications remain independent of legacy or external system implementations.
- Adapters simplify integration while promoting loose coupling.
- The pattern is widely used for protocol conversion and legacy modernization.

---

## Previous & Next

← Previous: [Ambassador Pattern](02-Ambassador-Pattern.md)

→ Next: [Operator Pattern](04-Operator-Pattern.md)