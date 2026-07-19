# Read Replicas

## Introduction

Read Replicas are a database scalability pattern where copies of a primary database are created specifically to handle read operations.

The primary database handles write operations, while read replicas handle read-heavy workloads.

The main goals of read replicas are:

- Scale database reads.
- Reduce load on the primary database.
- Improve application performance.
- Support high read traffic systems.

---

## Why was it Introduced?

In many applications, read traffic is much higher than write traffic.

Example:

```text
Social Media Application


Reads:

10 Million / day


Writes:

500 Thousand / day
```

A single database handles both operations:

```text
              Application

                   |

                   ▼

              Single Database

          Reads + Writes
```

Problems:

- Read queries consume database resources.
- Write performance decreases.
- Database becomes a bottleneck.

Read replicas separate read workload from write workload.

---

## Architecture Diagram

### Before Read Replicas

```text
                 Users

                   |

                   ▼

              Primary Database

              Reads + Writes
```

---

### After Read Replicas

```text
                     Users

                       |

                       ▼

                 Application


          ┌────────────┴────────────┐

          ▼                         ▼

    Write Requests            Read Requests


          ▼                         ▼

     Primary DB              Read Replicas

                               ┌────┬────┐

                               ▼    ▼    ▼

                            Replica Replica
```

---

## How It Works

The request flow:

```text
1. Application receives request.

2. Write operations go to primary database.

3. Primary database replicates changes.

4. Read operations go to replicas.
```

Example:

```text
Create User

      |

      ▼

 Primary Database


Fetch User Profile

      |

      ▼

 Read Replica
```

---

# Read Replica Architecture

## Primary Database

Responsible for:

- INSERT operations.
- UPDATE operations.
- DELETE operations.

Example:

```sql
INSERT INTO users VALUES (...);
```

---

## Read Replicas

Responsible for:

- SELECT operations.

Example:

```sql
SELECT *
FROM users;
```

---

# Types of Read Replica Routing

## 1. Application-Level Routing

Application decides where queries go.

Example:

```text
Write Query

      |

Primary DB


Read Query

      |

Replica DB
```

Advantages:

- Full control.

Disadvantages:

- Application complexity increases.

---

## 2. Database Proxy Routing

A proxy automatically routes queries.

Example:

```text
Application

      |

Database Proxy

   ┌──┴──┐

Write  Read

 |      |

Primary Replica
```

Advantages:

- Less application logic.

---

## 3. Load Balanced Reads

Multiple replicas receive read traffic.

Example:

```text
             Read Requests

                   |

             Load Balancer

          ┌────────┼────────┐

          ▼        ▼        ▼

      Replica1 Replica2 Replica3
```

---

# Core Characteristics

## 1. Read Scaling

Multiple replicas handle increasing read traffic.

---

## 2. Replication Based

Replicas continuously receive data changes from primary.

---

## 3. Read-Only Databases

Most replicas do not accept writes.

---

## 4. Eventual Consistency

Replicas may temporarily lag behind primary.

---

## 5. Independent Scaling

More replicas can be added as read traffic grows.

---

# Advantages

## 1. Improved Read Performance

Read traffic is distributed across multiple databases.

---

## 2. Reduced Primary Load

Primary focuses mainly on writes.

---

## 3. Better Availability

Replica can be promoted if primary fails.

---

## 4. Supports Large User Bases

Useful for read-heavy applications.

---

## 5. Geographic Distribution

Replicas can be placed closer to users.

Example:

```text
US Users

   |

US Replica


India Users

   |

India Replica
```

---

# Disadvantages

## 1. Replication Lag

A replica may not immediately have the latest data.

Example:

```text
User updates profile

       |

Primary Updated

       |

Replica Updated Later
```

---

## 2. Not Suitable For Write Scaling

Read replicas only improve read capacity.

---

## 3. Additional Cost

Each replica requires:

- Compute resources.
- Storage.
- Monitoring.

---

## 4. Read-After-Write Problems

A user may not immediately see their own update.

Example:

```text
Update Profile

      |

Primary


Fetch Profile

      |

Replica

(old data)
```

---

## 5. Operational Complexity

Requires managing:

- Replica health.
- Replication delay.
- Failover.

---

# Read Replicas vs Database Replication

| Feature | Replication | Read Replica |
|---|---|---|
| Purpose | Create data copies | Scale reads |
| Writes | Depends on model | Usually primary only |
| Reads | Possible | Main purpose |
| Availability | High | High |
| Use Case | Fault tolerance | Read-heavy systems |

---

# Read Replicas vs Caching

| Feature | Read Replica | Cache |
|---|---|---|
| Storage | Database | Memory |
| Data | Persistent | Temporary |
| Consistency | Stronger | Eventual possible |
| Speed | Faster than DB | Much faster |
| Purpose | Scale queries | Reduce repeated access |

---

# Real-World Examples

## Social Media Applications

Read replicas serve:

- User profiles.
- Posts.
- Comments.

---

## E-Commerce Platforms

Read replicas handle:

- Product searches.
- Product details.
- Reviews.

---

## News Platforms

Thousands of users reading articles can be served by replicas.

---

# When to Use

Use Read Replicas when:

- Application has heavy read traffic.
- Writes are comparatively lower.
- Database reads impact performance.
- High availability is required.
- Users are distributed geographically.

---

# When NOT to Use

Avoid read replicas when:

- Application is write-heavy.
- Strong read-after-write consistency is required everywhere.
- Data size is small.
- Database is not the bottleneck.

---

# Comparison

| Feature | Primary Only | Primary + Read Replicas |
|---|---|---|
| Read Capacity | Limited | High |
| Write Capacity | Same | Same |
| Availability | Lower | Higher |
| Complexity | Low | Higher |
| Cost | Lower | Higher |

---

# Interview Questions

## 1. What is a Read Replica?

A read replica is a copy of the primary database used mainly to serve read operations.

---

## 2. Why use read replicas?

To scale read traffic and reduce load on the primary database.

---

## 3. Can we write data to read replicas?

Usually no. Writes are handled by the primary database.

---

## 4. What is replication lag?

The delay between a change in the primary database and its availability in replicas.

---

## 5. Can read replicas improve write performance?

No. They improve read capacity only.

---

# Key Takeaways

- Read replicas scale database read operations.
- Writes continue to go through the primary database.
- Replication lag is the biggest challenge.
- They are commonly used in read-heavy systems.
- Read replicas are often combined with caching and sharding.
- They improve scalability without changing application behavior significantly.

---

## Previous & Next

← Previous: [Replication](08-Replication.md)

→ Next: [Connection Pooling](10-Connection-Pooling.md)