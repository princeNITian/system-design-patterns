# Serverless Pattern

## Introduction

The Serverless Pattern is a cloud-native architectural pattern where **developers build and deploy applications without managing the underlying servers or infrastructure**.

The cloud provider automatically provisions, scales, patches, and manages the compute resources.

Despite the name, **servers still exist**—they are simply managed by the cloud provider rather than the application team.

The Serverless Pattern answers the question:

> **"How can developers focus on application logic without managing infrastructure?"**

The main goals of the Serverless Pattern are:

- Eliminate server management.
- Automatically scale applications.
- Reduce operational overhead.
- Optimize costs through pay-per-use billing.
- Accelerate application development.

---

# Why was it Introduced?

Imagine a REST API running on virtual machines.

Without Serverless:

```text
Developer

↓

Provision Servers

↓

Install Runtime

↓

Deploy Application

↓

Configure Scaling

↓

Monitor Servers
```

Developers spend significant effort managing infrastructure.

With Serverless:

```text
Developer

↓

Deploy Function

↓

Cloud Platform

↓

Handles Infrastructure
```

Developers focus only on business logic.

---

# Architecture Diagram

```text
            Client

              |

        API Gateway

              |

              ▼

      Serverless Function

              |

      Business Logic

              |

              ▼

 Database / Queue / Storage
```

The cloud platform automatically executes functions when events occur.

---

# How It Works

The workflow:

```text
1. An event occurs.

2. Cloud platform invokes the function.

3. Function executes business logic.

4. Function accesses required services.

5. Function returns a response.

6. Resources are released after execution.
```

Functions are created on demand and scale automatically.

---

# Event Sources

## HTTP Requests

Example:

```text
API Gateway

↓

Function
```

---

## Object Storage

Example:

```text
File Upload

↓

Function
```

---

## Message Queues

Example:

```text
Queue Message

↓

Function
```

---

## Scheduled Events

Example:

```text
Cron Schedule

↓

Function
```

---

## Database Changes

Example:

```text
New Record

↓

Function
```

---

# Core Characteristics

## 1. Event-Driven

Functions execute in response to events.

---

## 2. Stateless

Each invocation should be independent.

---

## 3. Automatic Scaling

Cloud platforms create additional function instances automatically.

---

## 4. Pay Per Use

Billing is based on requests and execution duration.

---

## 5. Fully Managed Infrastructure

The cloud provider manages servers, operating systems, and runtime environments.

---

# Advantages

## 1. No Server Management

Developers focus entirely on application code.

---

## 2. Automatic Scaling

Functions scale automatically based on incoming events.

---

## 3. Cost Efficient

You pay only when functions execute.

---

## 4. Faster Development

Infrastructure provisioning is greatly simplified.

---

## 5. Cloud-Native Friendly

Integrates naturally with managed cloud services.

---

# Disadvantages

## 1. Cold Starts

Functions that have been idle may experience higher latency on their next invocation.

---

## 2. Execution Limits

Functions typically have maximum execution time and resource limits.

---

## 3. Stateless Nature

Persistent state must be stored in external services.

---

## 4. Vendor Lock-In

Applications may become tightly coupled to cloud-specific services.

---

## 5. Debugging Complexity

Distributed event-driven systems can be harder to troubleshoot.

---

# Real-World Examples

## AWS Lambda

Executes code in response to events from services such as API Gateway, S3, DynamoDB, and EventBridge.

---

## Azure Functions

Runs event-driven workloads on Microsoft Azure.

---

## Google Cloud Functions

Provides serverless execution for Google Cloud applications.

---

## Cloudflare Workers

Executes lightweight functions at edge locations worldwide.

---

## Vercel Functions

Supports serverless APIs for web applications.

---

# Common Use Cases

- REST APIs
- Image processing
- File uploads
- Event processing
- Scheduled jobs
- IoT data processing
- Chatbots
- Webhooks

---

# When to Use

Use the Serverless Pattern when:

- Building event-driven applications.
- Implementing REST APIs.
- Processing asynchronous workloads.
- Handling unpredictable traffic.
- Reducing infrastructure management.

---

# When NOT to Use

Avoid the Serverless Pattern when:

- Running long-lived processes.
- Requiring extremely low and consistent latency where cold starts are unacceptable.
- Needing full control over the operating system or runtime.
- Running workloads with specialized hardware requirements.

---

# Comparison

| Feature | Serverless | Virtual Machines |
|---|---|---|
| Server Management | Cloud Provider | User |
| Scaling | Automatic | Manual or Auto Scaling |
| Billing | Per Request / Duration | Per Running Instance |
| Startup Latency | Possible Cold Starts | Always Running |
| Best For | Event-Driven Workloads | Long-Running Applications |

---

# Interview Questions

## 1. What is the Serverless Pattern?

A cloud-native pattern where developers deploy code while the cloud provider manages the underlying infrastructure.

---

## 2. Does Serverless mean there are no servers?

No. Servers still exist, but they are managed by the cloud provider.

---

## 3. What is a cold start?

The additional startup latency that occurs when a serverless platform initializes a new function instance after a period of inactivity.

---

## 4. What types of events can trigger serverless functions?

- HTTP requests
- File uploads
- Queue messages
- Scheduled events
- Database changes

---

## 5. Name popular serverless platforms.

- AWS Lambda
- Azure Functions
- Google Cloud Functions
- Cloudflare Workers
- Vercel Functions

---

# Key Takeaways

- Serverless abstracts infrastructure management from developers.
- Functions are event-driven, stateless, and automatically scalable.
- Pay-per-use pricing can reduce costs for variable workloads.
- Cold starts and execution limits are important design considerations.
- Serverless is a core cloud-native pattern for modern distributed applications.

---

## Previous & Next

← Previous: [Multi-Tenancy](07-Multi-Tenancy.md)

→ Next: [Control Plane vs Data Plane](09-Control-Plane-vs-Data-Plane.md)