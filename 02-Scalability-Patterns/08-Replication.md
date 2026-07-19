# Database Replication

## Introduction

Database Replication is a scalability pattern where data is copied from one database server to one or more additional database servers called replicas.

The main goals of replication are:

- Improve availability.
- Increase read capacity.
- Provide fault tolerance.
- Reduce database load.

Instead of depending on a single database server, multiple copies of data are maintained across different servers.

---

## Why was it Introduced?

In a single database architecture:

```text
              Application

                   |

                   ▼

              Database
```

All operations depend on one database.

Problems:

- Database failure causes downtime.
- Read traffic overloads the database.
- Maintenance becomes difficult.
- Geographical users experience higher latency.

Replication was introduced to create multiple copies of data.

---

## Architecture Diagram

### Before Replication

```text
                 Application

                      |

                      ▼

                 Primary DB
```

---

### After Replication

```text
                    Application

                         |

                         ▼

                    Primary DB

                  /           \

                 ▼             ▼

            Replica 1      Replica 2
```

The primary database handles writes, and replicas maintain copies of the data.

---

## How It Works

The replication flow:

```text
1. Application sends write request.

2. Primary database stores the data.

3. Changes are replicated to replicas.

4. Read requests are served from replicas.
```

Example:

```text
Write Request

      |

      ▼

 Primary Database

      |

 Replication

      |

 ┌────┴────┐

 ▼         ▼

Replica 1 Replica 2
```

---

# Types of Database Replication

## 1. Primary-Replica Replication

One database handles writes.

Other databases handle reads.

Architecture:

```text
              Application

                  |

          ┌───────┴───────┐

          ▼               ▼

     Write Requests   Read Requests


          ▼               ▼

       Primary        Replicas
```

Advantages:

- Simple.
- Commonly used.

Disadvantages:

- Primary becomes write bottleneck.

---

## 2. Multi-Master Replication

Multiple databases can accept writes.

Example:

```text
          Database A

              ↕

          Database B

              ↕

          Database C
```

Advantages:

- High write availability.

Disadvantages:

- Conflict resolution is difficult.

---

## 3. Leaderless Replication

No single primary exists.

All nodes can accept reads and writes.

Example:

```text
        Node 1

       ↗     ↖

Node 2     Node 3
```

Used in distributed databases.

Examples:

- Cassandra.
- DynamoDB style systems.

---

# Replication Types Based on Consistency

## 1. Synchronous Replication

Primary waits for replicas before confirming the write.

Flow:

```text
Write

 |

Primary

 |

Replicas Confirm

 |

Success Response
```

Advantages:

- Strong consistency.

Disadvantages:

- Higher latency.

---

## 2. Asynchronous Replication

Primary confirms immediately and replicas update later.

Flow:

```text
Write

 |

Primary

 |

Success Response

 |

Replica Update Later
```

Advantages:

- Faster writes.

Disadvantages:

- Possible temporary inconsistency.

---

# Core Characteristics

## 1. Data Duplication

Multiple copies of the same data exist.

---

## 2. Improved Availability

Failure of one database does not stop the system.

---

## 3. Read Scaling

Multiple replicas can handle read traffic.

---

## 4. Fault Tolerance

Data remains available even if a server fails.

---

## 5. Data Synchronization

Changes must be propagated between databases.

---

# Advantages

## 1. Higher Availability

If primary fails, another database can take over.

---

## 2. Increased Read Capacity

Reads can be distributed across replicas.

Example:

```text
10,000 Reads/sec


Primary

        +

5 Replicas
```

---

## 3. Disaster Recovery

Replicas can exist in different locations.

---

## 4. Reduced Primary Load

Heavy read traffic does not impact writes.

---

## 5. Geographic Performance

Users can access nearby replicas.

---

# Disadvantages

## 1. Data Consistency Challenges

Replicas may temporarily contain outdated data.

Example:

```text
Primary:

Balance = $100


Replica:

Balance = $80
```

---

## 2. Replication Lag

Changes may take time to reach replicas.

---

## 3. Storage Cost

Multiple copies require additional storage.

---

## 4. Write Scaling Limitations

Primary-replica systems still have one write node.

---

## 5. Conflict Resolution

Multi-master systems require handling conflicting writes.

---

# Real-World Examples

## Social Media Platforms

Replicate:

- User profiles.
- Posts.
- Feeds.

---

## E-Commerce Systems

Replicate:

- Product information.
- Inventory reads.
- Orders.

---

## Banking Systems

Use replication for:

- Disaster recovery.
- High availability.

---

## Distributed Databases

Examples:

- Cassandra.
- DynamoDB.

Use replication for high availability.

---

# When to Use

Use database replication when:

- Read traffic is high.
- High availability is required.
- Disaster recovery is important.
- Users are distributed globally.
- Database downtime is unacceptable.

---

# When NOT to Use

Avoid replication when:

- Strong consistency is mandatory for every read.
- Data volume is small.
- Additional complexity is unnecessary.
- Replication lag causes business issues.

---

# Comparison

| Feature | Single Database | Replicated Database |
|---|---|---|
| Data Copies | One | Multiple |
| Availability | Lower | Higher |
| Read Capacity | Limited | Higher |
| Failure Recovery | Difficult | Easier |
| Complexity | Low | Higher |

---

# Interview Questions

## 1. What is Database Replication?

Database replication is the process of copying data from one database server to multiple servers.

---

## 2. Why do we use replication?

Replication improves availability, read scalability, and disaster recovery.

---

## 3. Difference between replication and sharding?

Replication creates copies of the same data.

Sharding splits different data across different databases.

---

## 4. What is replication lag?

Replication lag is the delay between updating the primary database and receiving the update on replicas.

---

## 5. Synchronous vs asynchronous replication?

Synchronous replication waits for replicas before confirming writes.

Asynchronous replication updates replicas after confirming writes.

---

# Key Takeaways

- Replication creates multiple copies of database data.
- It improves availability and read scalability.
- Primary-replica is the most common replication model.
- Replication introduces consistency challenges.
- Replication and sharding are often combined in large-scale systems.
- Choosing synchronous or asynchronous replication depends on consistency requirements.

---

## Previous & Next

← Previous: [Partitioning](07-Partitioning.md)

→ Next: [Read Replicas](09-Read-Replicas.md)