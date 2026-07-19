# Serverless Architecture

## Introduction

Serverless Architecture is a cloud computing architecture where developers build and run applications without managing servers directly.

The cloud provider is responsible for:

- Server provisioning
- Infrastructure management
- Scaling
- Availability
- Maintenance

Developers focus mainly on writing application logic.

Despite the name, servers still exist. The difference is that developers do not manage them.

---

## Why was it Introduced?

Traditional server-based architectures require teams to manage infrastructure.

Example:

```text
Developer

      |

Virtual Machine

      |

Operating System

      |

Server Maintenance
```

Teams had to handle:

- Server provisioning.
- Capacity planning.
- Scaling.
- Patching.
- Availability management.

This created operational overhead.

Serverless Architecture was introduced to reduce infrastructure management and enable automatic scaling.

---

## Architecture Diagram

```text
                 Client

                   |

                   ▼

              API Gateway

                   |

                   ▼

              Serverless Function

            (AWS Lambda / Cloud Functions)

                   |

        ┌──────────┼──────────┐

        ▼          ▼          ▼

    Database    Storage    Message Queue
```

The cloud provider executes functions when requests or events occur.

---

## How It Works

The basic flow:

```text
1. An event occurs.

2. Cloud provider triggers a function.

3. Function executes business logic.

4. Required resources are accessed.

5. Function execution ends.
```

Example:

```text
User uploads image

        |

        ▼

Storage Event

        |

        ▼

Image Processing Function

        |

        ▼

Processed Image Stored
```

The application automatically scales based on incoming requests.

---

## Core Characteristics

### 1. No Server Management

Developers do not manage:

- Operating systems
- Virtual machines
- Server patches
- Infrastructure scaling

---

### 2. Event-Based Execution

Functions execute when triggered by events.

Examples:

- HTTP request
- File upload
- Database change
- Message queue event
- Scheduled job

---

### 3. Automatic Scaling

The cloud provider automatically increases or decreases function instances based on demand.

Example:

```text
Low Traffic

1 Function Instance
```

```text
High Traffic

100 Function Instances
```

---

### 4. Pay Per Usage

Traditional servers are paid for based on uptime.

Serverless follows a usage-based model.

Example:

Pay for:

- Number of requests.
- Execution duration.
- Resources consumed.

---

### 5. Stateless Execution

Functions are usually stateless.

Each execution should not depend on previous executions.

Persistent data is stored externally.

Examples:

- Databases
- Object Storage
- Caches

---

## Advantages

### 1. Reduced Infrastructure Management

Cloud providers handle servers, scaling, and availability.

---

### 2. Automatic Scaling

Applications automatically handle traffic spikes.

---

### 3. Cost Efficiency

You pay only when functions execute.

This is useful for:

- Low traffic applications.
- Periodic workloads.
- Event-based processing.

---

### 4. Faster Development

Developers focus on business logic instead of infrastructure.

---

### 5. High Availability

Cloud providers manage:

- Hardware failures.
- Infrastructure redundancy.
- Regional availability.

---

## Disadvantages

### 1. Cold Start Problem

Functions that are not frequently used may take extra time to start.

Example:

```text
Request

↓

Initialize Runtime

↓

Execute Function
```

This increases latency.

---

### 2. Vendor Lock-In

Applications may become tightly coupled to cloud provider services.

Example:

```text
AWS Lambda

+

Amazon DynamoDB

+

Amazon S3
```

Moving to another provider may require changes.

---

### 3. Limited Execution Time

Serverless functions usually have execution limits.

Long-running workloads may not be suitable.

---

### 4. Debugging Complexity

Distributed serverless systems involve:

- Multiple services.
- Event flows.
- Managed infrastructure.

Debugging can become challenging.

---

### 5. Stateless Nature

Functions cannot rely on local memory for persistent state.

External storage is required.

---

## Real-World Examples

### Netflix

Uses serverless technologies for:

- Automation tasks.
- Data processing.
- Operational workflows.

---

### Coca-Cola

Uses serverless computing for:

- Marketing applications.
- Event-driven workloads.

---

### Financial Systems

Common serverless use cases:

- Transaction processing.
- Fraud detection.
- Notifications.

---

### Modern Web Applications

Common architecture:

```text
Frontend

   |

API Gateway

   |

Serverless Functions

   |

Database
```

---

## When to Use

Use Serverless Architecture when:

- Workloads are event-driven.
- Traffic is unpredictable.
- Automatic scaling is needed.
- Infrastructure management should be minimized.
- Applications consist of independent functions.

Good examples:

- APIs
- Background jobs
- File processing
- Notifications
- Scheduled tasks

---

## When NOT to Use

Avoid Serverless when:

- Long-running processing is required.
- Extremely low latency is mandatory.
- Full infrastructure control is needed.
- Applications require persistent server state.
- Vendor independence is important.

---

## Comparison

| Feature | Traditional Servers | Serverless |
|---|---|---|
| Infrastructure | Managed by team | Managed by cloud provider |
| Scaling | Manual / configured | Automatic |
| Cost Model | Pay for uptime | Pay per usage |
| Maintenance | Required | Minimal |
| Execution | Long-running | Event-based |
| Control | High | Lower |

---

## Interview Questions

### 1. What is Serverless Architecture?

Serverless Architecture is a cloud architecture where developers run applications without managing servers directly.

---

### 2. Does serverless mean there are no servers?

No.

Servers still exist, but the cloud provider manages them.

---

### 3. What are examples of serverless services?

Examples:

- AWS Lambda
- Google Cloud Functions
- Azure Functions

---

### 4. What is a cold start?

Cold start is the additional startup latency when a function instance needs to be initialized before execution.

---

### 5. When should you avoid serverless?

Avoid it for long-running workloads, strict latency requirements, or applications requiring complete infrastructure control.

---

## Key Takeaways

- Serverless removes infrastructure management responsibilities from developers.
- Cloud providers handle provisioning, scaling, and availability.
- Functions execute in response to events.
- Serverless follows a pay-per-use model.
- It provides automatic scaling and faster development.
- Challenges include cold starts, vendor lock-in, and execution limits.
- Serverless is best suited for event-driven and unpredictable workloads.

---

## Previous & Next

← Previous: [Event-Driven Architecture](06-Event-Driven-Architecture.md)

→ Next: [Pipe and Filter Architecture](08-Pipe-and-Filter.md)
