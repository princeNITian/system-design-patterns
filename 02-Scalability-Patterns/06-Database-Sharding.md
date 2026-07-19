# Database Sharding

## Introduction

Database Sharding is a scalability pattern that divides a large database into smaller, independent pieces called **shards**.

Each shard stores a subset of the total data and operates as an independent database.

The main goals of database sharding are:

- Handle massive amounts of data.
- Distribute database workload.
- Improve query performance.
- Enable horizontal database scaling.

---

## Why was it Introduced?

Initially, applications store all data in a single database.

Example:

```text
              Application

                    |

                    ▼

              Single Database
```

As the application grows:

- Data size increases.
- Query performance decreases.
- Storage limits are reached.
- Database becomes a bottleneck.

Vertical scaling a database has limitations.

Example:

```text
Database Server

CPU: 64 cores

RAM: 512 GB

Storage: 20 TB
```

Eventually, increasing machine capacity becomes expensive or impossible.

Database sharding was introduced to distribute data across multiple databases.

---

## Architecture Diagram

### Before Sharding

```text
                Application

                     |

                     ▼

              Single Database

          ┌──────────────────┐
          │                  │
          │  All Application │
          │      Data        │
          │                  │
          └──────────────────┘
```

---

### After Sharding

```text
                 Application

                      |

                      ▼

              Sharding Layer

        ┌─────────────┼─────────────┐

        ▼             ▼             ▼

    Shard 1       Shard 2       Shard 3

   Users A-F     Users G-M     Users N-Z
```

Each shard contains only a portion of the data.

---

## How It Works

The basic flow:

```text
1. Application receives request.

2. Sharding logic determines target shard.

3. Request is routed to the correct database.

4. Data is read or written.

5. Response is returned.
```

Example:

```text
User ID: 1050


Sharding Function:

1050 % 3 = 0


Request goes to:

Shard 1
```

---

# Sharding Strategies

## 1. Range Based Sharding

Data is divided based on value ranges.

Example:

```text
Shard 1:

User IDs 1 - 1 Million


Shard 2:

User IDs 1 Million - 2 Million


Shard 3:

User IDs 2 Million - 3 Million
```

Advantages:

- Simple implementation.
- Easy range queries.

Disadvantages:

- Uneven data distribution possible.

---

## 2. Hash Based Sharding

A hash function determines the shard.

Example:

```text
Hash(User_ID) % Number_of_Shards
```

Example:

```text
User ID = 500

Hash(500) % 4

Result = Shard 2
```

Advantages:

- Better data distribution.
- Avoids hotspots.

Disadvantages:

- Range queries become difficult.

---

## 3. Directory Based Sharding

A lookup service maintains the mapping between data and shards.

Example:

```text
User 101

        |

Directory Service

        |

Shard 3
```

Advantages:

- Flexible routing.

Disadvantages:

- Directory becomes critical infrastructure.

---

## 4. Geographic Sharding

Data is stored based on user location.

Example:

```text
US Users

    |

US Database


India Users

    |

India Database
```

Advantages:

- Lower latency.
- Helps with regional requirements.

---

# Sharding Key

A sharding key determines where data is stored.

Example:

```text
User Table


User_ID

    |

Hash Function

    |

Shard Selection
```

A good sharding key should:

- Distribute data evenly.
- Avoid hotspots.
- Support common queries.

---

# Core Characteristics

## 1. Horizontal Database Scaling

Instead of increasing database size, more databases are added.

---

## 2. Data Distribution

Large datasets are divided across multiple locations.

---

## 3. Independent Shards

Each shard can operate independently.

---

## 4. Query Routing

Requests must be routed to the correct shard.

---

## 5. Increased Capacity

Storage and processing capacity increases by adding shards.

---

# Advantages

## 1. Handles Massive Data

Large datasets can be distributed across multiple databases.

---

## 2. Improved Performance

Queries operate on smaller datasets.

---

## 3. Horizontal Scalability

More shards can be added as data grows.

---

## 4. Reduced Database Load

Workload is distributed across multiple machines.

---

## 5. Regional Optimization

Users can access geographically closer data.

---

# Disadvantages

## 1. Increased Complexity

Application logic becomes more complicated.

Requires:

- Routing.
- Shard management.
- Monitoring.

---

## 2. Cross-Shard Queries

Queries involving multiple shards become expensive.

Example:

```text
JOIN data from Shard 1

with

Shard 2
```

---

## 3. Data Rebalancing

Adding or removing shards requires moving data.

---

## 4. Transaction Complexity

Distributed transactions become difficult.

---

## 5. Hotspot Problems

Poor shard keys can overload one shard.

Example:

```text
Popular User

      |

Single Shard Overloaded
```

---

# Real-World Examples

## Social Media Platforms

Users are distributed across shards.

Example:

```text
Shard 1

Users 1-100M


Shard 2

Users 100M-200M
```

---

## E-Commerce Systems

Large platforms shard:

- Users.
- Orders.
- Products.

---

## Gaming Platforms

Player data is distributed across multiple databases.

---

## Messaging Systems

Large-scale messaging platforms distribute user conversations across shards.

---

# When to Use

Use Database Sharding when:

- Database size is extremely large.
- Single database cannot handle traffic.
- Horizontal database scaling is required.
- Data naturally partitions into groups.
- Application handles millions of users.

---

# When NOT to Use

Avoid sharding when:

- Database size is manageable.
- Queries frequently require joins across all data.
- Strong relational transactions dominate.
- Simpler scaling approaches are sufficient.

---

# Comparison

| Feature | Single Database | Sharded Database |
|---|---|---|
| Data Storage | One database | Multiple databases |
| Scalability | Limited | High |
| Complexity | Low | High |
| Query Simplicity | Easy | More complex |
| Data Distribution | None | Distributed |

---

# Interview Questions

## 1. What is Database Sharding?

Database sharding is the process of splitting a large database into smaller independent databases called shards.

---

## 2. Why do we need sharding?

Sharding helps systems handle massive datasets and high traffic by distributing database workload.

---

## 3. Difference between Replication and Sharding?

Replication creates copies of the same data.

Sharding divides data into different parts across databases.

---

## 4. What makes a good shard key?

A good shard key:

- Distributes data evenly.
- Avoids hotspots.
- Supports common queries.

---

## 5. What are challenges of sharding?

Major challenges:

- Cross-shard queries.
- Data migration.
- Transaction management.
- Shard balancing.

---

# Key Takeaways

- Database Sharding divides data across multiple databases.
- It enables horizontal database scaling.
- Shard keys determine data placement.
- Good partitioning avoids hotspots.
- Sharding improves scalability but increases complexity.
- It is commonly used in large distributed systems.

---

## Previous & Next

← Previous: [CDN](05-CDN.md)

→ Next: [Partitioning](07-Partitioning.md)