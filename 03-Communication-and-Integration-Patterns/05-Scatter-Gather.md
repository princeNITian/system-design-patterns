# Scatter-Gather Pattern

## Introduction

The Scatter-Gather Pattern is a communication pattern where a request is **scattered** to multiple services or workers in parallel, and their responses are **gathered** to produce a single result.

Unlike the Fan-Out/Fan-In combination, Scatter-Gather is treated as a complete request-processing pattern. It starts with one request, distributes it to multiple destinations, collects their responses, and returns one consolidated result.

The main goals of the Scatter-Gather pattern are:

- Execute requests in parallel.
- Reduce response time.
- Aggregate results from multiple services.
- Improve scalability.

---

## Why was it Introduced?

Some requests require information from multiple independent systems.

Example:

A travel booking application searches for flights.

Instead of querying airlines one by one:

- Airline A
- Airline B
- Airline C
- Airline D

the request is sent to all airlines simultaneously.

The results are then combined and returned to the user.

---

## Architecture Diagram

```text
              Client

                 |

                 ▼

          Scatter-Gather

        /      |      |      \

       ▼       ▼      ▼       ▼

 Airline A Airline B Airline C Airline D

       \       |      |       /

        \      |      |      /

               ▼

         Combined Result

               |

               ▼

             Client
```

---

## How It Works

The communication flow:

```text
1. Client sends one request.

2. Request is scattered to multiple services.

3. Services process requests in parallel.

4. Responses are gathered.

5. Aggregator combines the results.

6. Client receives one response.
```

Example:

```text
Search Flights

       |

       ├── Airline A

       ├── Airline B

       ├── Airline C

       └── Airline D

              |

              ▼

      Best Flight Results
```

---

# Core Characteristics

## 1. Parallel Requests

Multiple services receive the request simultaneously.

---

## 2. Response Aggregation

Results are collected into a single response.

---

## 3. Independent Processing

Each service processes the request independently.

---

## 4. Reduced Latency

Overall response time is close to the slowest service rather than the sum of all services.

---

## 5. Request-Oriented Pattern

The entire communication starts from one client request.

---

# Advantages

## 1. Faster Response Time

Parallel execution reduces overall latency.

---

## 2. Better Resource Utilization

Multiple services work simultaneously.

---

## 3. High Scalability

Additional services can participate without affecting existing ones.

---

## 4. Improved User Experience

Clients receive one consolidated response.

---

## 5. Fault Isolation

Failures in one service do not necessarily stop the entire request.

---

# Disadvantages

## 1. Aggregation Complexity

The aggregator must merge multiple responses.

---

## 2. Timeout Handling

The system must decide how long to wait for responses.

---

## 3. Partial Results

Some services may fail or respond slowly.

---

## 4. Increased Network Traffic

One request generates multiple backend requests.

---

## 5. Monitoring Complexity

Tracking parallel requests requires distributed tracing.

---

# Real-World Examples

## Travel Booking

Searches multiple:

- Airlines.
- Hotels.
- Car rental providers.

---

## E-Commerce

Searches multiple:

- Warehouses.
- Sellers.
- Inventory systems.

---

## Search Engines

Query multiple search indexes simultaneously.

---

## Financial Systems

Request stock prices from multiple exchanges.

---

# When to Use

Use the Scatter-Gather pattern when:

- Information comes from multiple independent systems.
- Parallel execution improves response time.
- Results need to be combined.
- Partial responses are acceptable.

---

# When NOT to Use

Avoid the Scatter-Gather pattern when:

- Requests depend on sequential execution.
- Only one backend service is involved.
- Network overhead outweighs performance gains.

---

# Comparison

| Feature | Fan-Out/Fan-In | Scatter-Gather |
|---|---|---|
| Purpose | Event processing | Request processing |
| Starts With | Event | Client request |
| Ends With | Independent tasks or aggregation | Single aggregated response |
| Communication | Usually asynchronous | Usually synchronous from the client's perspective |
| Common Use Case | Background processing | Search and aggregation |

---

# Interview Questions

## 1. What is the Scatter-Gather pattern?

A communication pattern where one request is sent to multiple services in parallel and their responses are aggregated into a single result.

---

## 2. How is Scatter-Gather different from Fan-Out?

Fan-Out distributes work after an event.

Scatter-Gather begins with a client request and returns one combined response.

---

## 3. What is the biggest challenge in Scatter-Gather?

Handling slow or failed services while maintaining acceptable response times.

---

## 4. Where is Scatter-Gather commonly used?

- Flight search.
- Product search.
- Dashboard aggregation.
- Search engines.
- Financial applications.

---

## 5. What happens if one service does not respond?

The aggregator may:

- Wait until timeout.
- Return partial results.
- Retry the failed request.
- Ignore the unavailable service based on business requirements.

---

# Key Takeaways

- Scatter-Gather executes multiple requests in parallel.
- Responses are aggregated into a single result.
- It improves performance for multi-source queries.
- Timeout handling is critical.
- It is widely used in search, travel, and aggregation systems.

---

## Previous & Next

← Previous: [Fan-In](04-Fan-In.md)

→ Next: [Competing Consumers](06-Competing-Consumers.md)