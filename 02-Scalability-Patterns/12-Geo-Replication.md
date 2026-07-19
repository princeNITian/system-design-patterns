# Geo Replication

## Introduction

Geo Replication is a scalability pattern where data is replicated across multiple geographical locations to improve availability, reduce latency, and provide disaster recovery.

Instead of storing data in a single region, systems maintain copies of data across different regions around the world.

The main goals of geo replication are:

- Reduce latency for global users.
- Improve disaster recovery.
- Increase availability.
- Support global-scale applications.

---

## Why was it Introduced?

Traditional systems store all data in one geographical location.

Example:

```text
                Users Worldwide

        /          |          \

       ▼           ▼           ▼


              Single Region

              Database
```

Problems:

- Users far away experience high latency.
- Regional failures cause downtime.
- Disaster recovery becomes difficult.
- Global expansion becomes challenging.

Example:

A user in Asia accessing a database hosted in the US experiences additional network delay.

Geo replication solves this by placing data closer to users.

---

## Architecture Diagram

### Single Region

```text
              Users

                |

                ▼

          US Region

                |

                ▼

            Database
```

---

### Multi Region

```text
                    Users

        ┌────────────┼────────────┐

        ▼            ▼            ▼


    US Region    EU Region    Asia Region


        DB           DB           DB
```

Each region maintains a copy of application data.

---

## How It Works

The basic flow:

```text
1. User request arrives.

2. Traffic is routed to nearest region.

3. Data is read from local replica.

4. Updates are replicated across regions.
```

Example:

```text
User in India

      |

      ▼

Asia Region Database


User in USA

      |

      ▼

US Region Database
```

---

# Types of Geo Replication

## 1. Active-Passive Replication

One region handles traffic.

Other regions act as backups.

Architecture:

```text
              Users

                |

                ▼

          Primary Region

                |

          Replication

                |

                ▼

        Backup Region
```

Advantages:

- Simple.
- Easier consistency management.

Disadvantages:

- Backup resources may be underutilized.

---

## 2. Active-Active Replication

Multiple regions handle traffic simultaneously.

Architecture:

```text
              Users

       ┌────────┼────────┐

       ▼        ▼        ▼

     US       EU       Asia

      DB       DB       DB
```

Advantages:

- Lower latency.
- High availability.

Disadvantages:

- Conflict resolution is difficult.

---

## 3. Read-Only Regional Replicas

One region handles writes while other regions serve reads.

Example:

```text
             Write Requests

                    |

                    ▼

              Primary Region


             Read Requests

          /        |        \

         ▼         ▼         ▼

       EU        US        Asia
```

---

# Data Synchronization Models

## 1. Synchronous Replication

Data must be written to multiple regions before confirming success.

Example:

```text
Write Request

      |

Primary Region

      |

Other Regions Confirm

      |

Success
```

Advantages:

- Strong consistency.

Disadvantages:

- Higher latency.

---

## 2. Asynchronous Replication

Data is replicated after the primary write succeeds.

Example:

```text
Write Request

      |

Primary Region

      |

Success Response

      |

Replication Later
```

Advantages:

- Faster writes.

Disadvantages:

- Temporary inconsistency.

---

# Core Characteristics

## 1. Geographic Distribution

Data exists in multiple regions.

---

## 2. Regional Failover

Traffic can move to another region during failures.

---

## 3. Lower Latency

Users access nearby data centers.

---

## 4. Data Synchronization

Changes must propagate between regions.

---

## 5. Disaster Recovery

A complete region failure does not destroy data availability.

---

# Advantages

## 1. Reduced Latency

Users connect to nearby regions.

Example:

```text
India User

     |

India Region

instead of

US Region
```

---

## 2. High Availability

A region outage does not stop the entire application.

---

## 3. Disaster Recovery

Data survives regional failures.

---

## 4. Global Scalability

Supports users across different continents.

---

## 5. Better User Experience

Improves response time for international users.

---

# Disadvantages

## 1. Data Consistency Challenges

Multiple regions may contain different versions of data.

Example:

```text
US Database

Balance = $100


Asia Database

Balance = $120
```

---

## 2. Conflict Resolution

Active-active systems must resolve simultaneous updates.

---

## 3. Higher Cost

Requires:

- Multiple regions.
- Additional infrastructure.
- Data transfer.

---

## 4. Operational Complexity

Requires managing:

- Replication.
- Failover.
- Monitoring.

---

## 5. Compliance Challenges

Some data must remain in specific regions.

---

# Real-World Examples

## Netflix

Uses multiple global regions to provide reliable streaming worldwide.

---

## Amazon

Uses multiple geographic regions for:

- Availability.
- Disaster recovery.
- Low latency.

---

## Banking Systems

Use geo replication for:

- Disaster recovery.
- Business continuity.

---

## Social Media Platforms

Store user data closer to global users.

---

# When to Use

Use geo replication when:

- Users are distributed globally.
- Low latency is important.
- Disaster recovery is required.
- Application requires high availability.
- Regional failures cannot be tolerated.

---

# When NOT to Use

Avoid geo replication when:

- Application serves a single region.
- Data consistency requirements are extremely strict.
- Infrastructure cost must remain minimal.
- Operational complexity is unnecessary.

---

# Comparison

| Feature | Single Region | Geo Replication |
|---|---|---|
| Data Location | One region | Multiple regions |
| Latency | Higher globally | Lower |
| Availability | Lower | Higher |
| Cost | Lower | Higher |
| Complexity | Low | High |

---

# Interview Questions

## 1. What is geo replication?

Geo replication is the process of maintaining data copies across multiple geographical regions.

---

## 2. Why do we need geo replication?

To reduce latency, improve availability, and provide disaster recovery.

---

## 3. Difference between replication and geo replication?

Replication creates copies of data.

Geo replication creates copies across different geographical locations.

---

## 4. What are challenges of geo replication?

Main challenges:

- Data consistency.
- Conflict resolution.
- Higher cost.
- Operational complexity.

---

## 5. Active-active vs active-passive replication?

Active-active allows multiple regions to serve traffic.

Active-passive uses one primary region and backup regions.

---

# Key Takeaways

- Geo replication distributes data across regions.
- It improves global performance and availability.
- Active-active provides better availability but increases complexity.
- Asynchronous replication is commonly used for global systems.
- Geo replication is essential for large-scale worldwide applications.

---

## Previous & Next

← Previous: [Consistent Hashing](11-Consistent-Hashing.md)

→ Next: [Rate Limiting](13-Rate-Limiting.md)