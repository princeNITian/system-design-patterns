# Horizontal vs Vertical Scaling

## Introduction

Scaling is the process of increasing a system's ability to handle more workload, users, traffic, or data.

When an application grows, a single server may no longer handle the increasing demand.

There are two fundamental approaches to scaling:

1. **Vertical Scaling (Scale Up)**  
2. **Horizontal Scaling (Scale Out)**

Understanding the difference between these approaches is the foundation of designing scalable systems.

---

## Why was it Introduced?

Initially, applications usually run on a single server.

Example:

```text
             Users

               |

               ▼

        Application Server

               |

               ▼

          Database
````

As traffic increases:

* CPU usage increases.
* Memory becomes insufficient.
* Requests take longer.
* Server becomes a bottleneck.

To handle growth, engineers introduced scaling strategies.

---

# Vertical Scaling (Scale Up)

## What is Vertical Scaling?

Vertical Scaling means increasing the capacity of an existing machine by adding more resources.

Resources increased:

* CPU
* RAM
* Storage
* Network capacity

Example:

```text
Before Scaling

      Application Server

      4 CPU
      16 GB RAM


              |

              ▼


After Scaling

      Application Server

      32 CPU
      128 GB RAM
```

The system continues running on the same machine.

---

## How Vertical Scaling Works

Flow:

```text
1. Identify resource bottleneck.

2. Increase server capacity.

3. Restart or migrate application.

4. Application handles higher load.
```

Example:

A database server running out of memory can be upgraded with more RAM.

---

## Advantages of Vertical Scaling

### 1. Simple Implementation

No major architectural changes are required.

---

### 2. Lower Complexity

The application continues running on a single machine.

---

### 3. Useful for Databases

Many databases benefit from powerful machines.

Examples:

* MySQL
* PostgreSQL
* Oracle

---

### 4. Lower Operational Overhead

Managing one powerful server is easier than managing many servers.

---

## Disadvantages of Vertical Scaling

### 1. Hardware Limitations

A machine can only be upgraded up to a certain limit.

---

### 2. Single Point of Failure

The entire system depends on one server.

```text
Server Failure

       |

       ▼

Application Down
```

---

### 3. Downtime During Upgrades

Increasing resources may require:

* Server restart.
* Migration.
* Maintenance window.

---

### 4. Expensive at Large Scale

High-end machines become increasingly expensive.

---

# Horizontal Scaling (Scale Out)

## What is Horizontal Scaling?

Horizontal Scaling means adding more machines to distribute workload.

Instead of making one server more powerful, we add multiple servers.

Example:

```text
Before Scaling


        Application Server



After Scaling


        Server 1
             \
              \
        Server 2 ---- Load Balancer
              /
             /
        Server 3
```

---

## How Horizontal Scaling Works

Flow:

```text
1. Add more application servers.

2. Place a load balancer in front.

3. Distribute incoming requests.

4. Scale servers based on traffic.
```

Example:

```text
1000 Requests/sec


Single Server

        ↓

Add 5 Servers


Each Server Handles
200 Requests/sec
```

---

## Advantages of Horizontal Scaling

### 1. High Scalability

More servers can be added as traffic grows.

---

### 2. Better Availability

If one server fails, others continue serving requests.

---

### 3. No Hardware Limit

Capacity can continuously increase by adding machines.

---

### 4. Better Traffic Distribution

Load balancers distribute requests efficiently.

---

### 5. Cloud Friendly

Modern cloud platforms are designed around horizontal scaling.

Examples:

* AWS Auto Scaling Groups
* Kubernetes Pods

---

## Disadvantages of Horizontal Scaling

### 1. Increased Complexity

Managing multiple servers requires:

* Load balancing.
* Service discovery.
* Monitoring.

---

### 2. Data Synchronization Challenges

Multiple servers need consistent data.

---

### 3. Distributed System Problems

Introduces challenges like:

* Network failures.
* Latency.
* Consistency issues.

---

# Real-World Examples

## Vertical Scaling Example

A database server is upgraded:

```text
Before:

8 CPU
32 GB RAM


After:

64 CPU
256 GB RAM
```

Common for:

* Database servers.
* Legacy applications.

---

## Horizontal Scaling Example

Netflix handles millions of users by running thousands of service instances.

```text
Users

 |

Load Balancer

 |

Multiple Service Instances
```

---

## Cloud Applications

Modern applications commonly use:

```text
Users

 |

Load Balancer

 |

Auto Scaling Group

 |

Multiple Instances
```

---

# When to Use Vertical Scaling

Use Vertical Scaling when:

* Application is small or medium sized.
* Simplicity is important.
* Database performance needs improvement.
* Architecture changes are expensive.
* Traffic growth is predictable.

---

# When to Use Horizontal Scaling

Use Horizontal Scaling when:

* Millions of users are expected.
* High availability is required.
* Traffic is unpredictable.
* Zero downtime is important.
* Cloud-native architecture is used.

---

# Comparison

| Feature             | Vertical Scaling         | Horizontal Scaling  |
| ------------------- | ------------------------ | ------------------- |
| Approach            | Increase machine power   | Add more machines   |
| Complexity          | Low                      | High                |
| Cost                | Expensive at large scale | More cost efficient |
| Availability        | Lower                    | Higher              |
| Limit               | Hardware limit           | Almost unlimited    |
| Architecture Change | Minimal                  | Required            |
| Cloud Suitability   | Moderate                 | Excellent           |

---

# Interview Questions

## 1. What is Vertical Scaling?

Vertical Scaling increases the capacity of an existing machine by adding more CPU, memory, or storage.

---

## 2. What is Horizontal Scaling?

Horizontal Scaling increases capacity by adding more machines and distributing workload among them.

---

## 3. Which scaling approach is preferred for large distributed systems?

Horizontal Scaling is preferred because it provides better scalability, availability, and fault tolerance.

---

## 4. Why are databases often vertically scaled?

Because databases often require:

* Strong consistency.
* Large memory.
* Fast storage access.

---

## 5. What challenges come with horizontal scaling?

Challenges include:

* Data consistency.
* Load distribution.
* Service discovery.
* Network failures.

---

# Key Takeaways

* Scaling helps systems handle increasing workload.
* Vertical Scaling increases the power of existing machines.
* Horizontal Scaling adds more machines to distribute workload.
* Vertical Scaling is simple but has physical limits.
* Horizontal Scaling supports large distributed systems.
* Modern cloud applications usually prefer horizontal scaling.
* Real-world systems often combine both approaches.

---

## Previous & Next

← Previous: [Architectural Patterns](../01-Architectural-Patterns/README.md)

→ Next: [Load Balancing](02-Load-Balancing.md)

```

Next: **`02-Load-Balancing.md`**.

