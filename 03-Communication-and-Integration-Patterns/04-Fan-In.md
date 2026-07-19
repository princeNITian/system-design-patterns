# Fan-In Pattern

## Introduction

The Fan-In Pattern is a communication pattern where the outputs from multiple services, workers, or tasks are collected and combined into a single result.

It is commonly used after a Fan-Out operation, where work is distributed to multiple components in parallel and their results are aggregated before proceeding.

The main goals of the Fan-In pattern are:

- Aggregate results from parallel tasks.
- Synchronize multiple processing paths.
- Improve overall throughput.
- Produce a unified response.

---

## Why was it Introduced?

Many distributed systems perform several tasks simultaneously.

Example:

An e-commerce platform generates a dashboard.

The dashboard requires:

- User Profile.
- Recent Orders.
- Recommendations.
- Notifications.

These services can execute in parallel, but the client expects a single response.

The Fan-In pattern combines these independent results into one.

---

## Architecture Diagram

```text
        Service A

             \

              \

        Service B

               \

                ▼

          Aggregator

                |

                ▼

        Combined Result

                ▲

               /

        Service C

             /

        Service D
```

Multiple service outputs are merged into one response.

---

## How It Works

The communication flow:

```text
1. Multiple services process requests independently.

2. Each service returns its result.

3. An aggregator waits for all required responses.

4. Results are combined.

5. A single response is returned.
```

Example:

```text
User Opens Dashboard

        |

        ├── User Service

        ├── Order Service

        ├── Notification Service

        └── Recommendation Service

                |

                ▼

          Dashboard Response
```

---

# Core Characteristics

## 1. Many-to-One Communication

Multiple results are combined into a single output.

---

## 2. Aggregation

An aggregator service collects responses.

---

## 3. Parallel Processing

Upstream services execute simultaneously.

---

## 4. Synchronization

The aggregator coordinates multiple responses.

---

## 5. Single Client Response

Clients receive one unified result instead of multiple responses.

---

# Advantages

## 1. Faster Response Time

Parallel execution is generally faster than sequential service calls.

---

## 2. Simplified Client Logic

Clients receive one combined response.

---

## 3. Better Resource Utilization

Independent services can execute concurrently.

---

## 4. Improved Scalability

Each service can scale independently.

---

## 5. Service Independence

Each participating service remains loosely coupled.

---

# Disadvantages

## 1. Aggregator Complexity

The aggregator must coordinate multiple responses.

---

## 2. Slowest Service Determines Response Time

Overall latency depends on the slowest required service.

---

## 3. Partial Failures

One service failure may prevent a complete response.

---

## 4. Timeout Management

The aggregator must decide how long to wait.

---

## 5. Increased Network Calls

Multiple backend requests increase communication overhead.

---

# Real-World Examples

## E-Commerce Dashboard

Aggregate data from:

- User Service.
- Order Service.
- Cart Service.
- Recommendation Service.

---

## Banking Application

Combine:

- Account Balance.
- Recent Transactions.
- Credit Card Details.
- Loan Information.

---

## Travel Booking

Collect results from:

- Flight Service.
- Hotel Service.
- Car Rental Service.
- Insurance Service.

---

# When to Use

Use the Fan-In pattern when:

- Multiple services contribute to one response.
- Parallel execution improves performance.
- Clients need a unified response.
- Service aggregation is required.

---

# When NOT to Use

Avoid the Fan-In pattern when:

- Tasks depend on one another sequentially.
- Only one service provides the required data.
- Aggregation introduces unnecessary complexity.

---

# Comparison

| Feature | Fan-Out | Fan-In |
|---|---|---|
| Communication | One-to-Many | Many-to-One |
| Purpose | Distribute work | Aggregate results |
| Processing | Parallel execution | Result collection |
| Typical Component | Message Broker | Aggregator |
| Often Used Together | Yes | Yes |

---

# Interview Questions

## 1. What is the Fan-In pattern?

A communication pattern that combines outputs from multiple services into a single result.

---

## 2. Why is Fan-In commonly used after Fan-Out?

Because Fan-Out distributes work, while Fan-In collects and combines the results.

---

## 3. What component performs Fan-In?

Typically an aggregator service or API gateway.

---

## 4. What is the biggest challenge in Fan-In?

Handling slow or failed services while producing a useful response.

---

## 5. Where is Fan-In commonly used?

- Dashboards.
- Search systems.
- Booking platforms.
- Composite APIs.
- Microservice aggregators.

---

# Key Takeaways

- Fan-In aggregates results from multiple services.
- It is commonly paired with Fan-Out.
- Parallel processing improves response time.
- Aggregators simplify client interactions.
- Proper timeout and failure handling are essential for reliable aggregation.

---

## Previous & Next

← Previous: [Fan-Out](03-Fan-Out.md)

→ Next: [Scatter-Gather](05-Scatter-Gather.md)