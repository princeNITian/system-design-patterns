# Connection Pooling

## Introduction

Connection Pooling is a scalability pattern that manages and reuses database connections instead of creating a new connection for every request.

Creating database connections repeatedly is expensive because it requires:

- Network handshake.
- Authentication.
- Resource allocation.
- Memory allocation.

A connection pool maintains a set of reusable database connections that applications can borrow and return.

The main goals of connection pooling are:

- Reduce connection overhead.
- Improve application performance.
- Control database connection usage.
- Handle high concurrent traffic.

---

## Why was it Introduced?

Without connection pooling, every request creates a new database connection.

Example:

```text
User Request

      |

Application

      |

Create DB Connection

      |

Execute Query

      |

Close Connection
```

For thousands of requests:

```text
10000 Requests

      |

10000 New Connections
```

Problems:

- High latency.
- Increased CPU usage.
- Database connection exhaustion.
- Poor resource utilization.

Connection pooling solves this by reusing existing connections.

---

## Architecture Diagram

### Without Connection Pooling

```text
              Application


 Request 1 ───────► DB Connection 1

 Request 2 ───────► DB Connection 2

 Request 3 ───────► DB Connection 3

 Request 4 ───────► DB Connection 4
```

Every request creates a new connection.

---

### With Connection Pooling

```text
                 Application

                      |

                      ▼

              Connection Pool

        ┌────────┬────────┬────────┐

        ▼        ▼        ▼        ▼

     Conn 1   Conn 2   Conn 3   Conn 4

        \        |        |        /

                 Database
```

Connections are reused.

---

## How It Works

The flow:

```text
1. Application starts.

2. Connection pool creates database connections.

3. Request arrives.

4. Application borrows an available connection.

5. Query executes.

6. Connection returns to the pool.
```

Example:

```text
Request

   |

Get Connection

   |

Execute Query

   |

Release Connection

   |

Pool Reuses Connection
```

---

# Connection Pool Components

## 1. Pool Size

Defines the maximum number of database connections.

Example:

```text
Pool Size = 20

Maximum active connections = 20
```

---

## 2. Idle Connections

Connections waiting for requests.

Example:

```text
Available Connections

Conn 1
Conn 2
Conn 3
```

---

## 3. Active Connections

Connections currently executing queries.

Example:

```text
Active:

Conn 4 → Running Query
```

---

## 4. Connection Timeout

Maximum time a request waits for an available connection.

Example:

```text
No connection available

        |

Wait 5 seconds

        |

Fail Request
```

---

# Connection Pool Lifecycle

```text
Application Starts

        |

Create Connection Pool

        |

Open Connections

        |

Receive Requests

        |

Borrow Connection

        |

Execute Query

        |

Return Connection

        |

Reuse Connection
```

---

# Pool Sizing Strategies

## 1. Small Pool

Example:

```text
Pool Size = 5
```

Advantages:

- Less database load.

Disadvantages:

- Requests may wait.

---

## 2. Large Pool

Example:

```text
Pool Size = 500
```

Advantages:

- More concurrency.

Disadvantages:

- Can overload database.

---

## 3. Optimal Pool

Depends on:

- Database capacity.
- Application workload.
- Query execution time.
- Number of servers.

---

# Core Characteristics

## 1. Connection Reuse

Existing connections are reused.

---

## 2. Resource Management

Controls maximum database connections.

---

## 3. Improved Latency

Avoids connection creation overhead.

---

## 4. Concurrency Control

Limits simultaneous database access.

---

## 5. Application-Level Optimization

Usually implemented inside application servers.

---

# Advantages

## 1. Faster Database Access

Connection creation overhead is removed.

---

## 2. Reduced Database Load

Database handles fewer connection creations.

---

## 3. Better Resource Utilization

Connections are efficiently reused.

---

## 4. Handles High Traffic

Supports many concurrent users.

---

## 5. Prevents Connection Exhaustion

Limits the number of active connections.

---

# Disadvantages

## 1. Incorrect Pool Size

Too large:

```text
Application

      |

Too Many Connections

      |

Database Overload
```

Too small:

```text
Requests Waiting For Connections
```

---

## 2. Connection Leaks

If applications fail to release connections:

```text
Borrow Connection

      |

Forget To Return

      |

Pool Exhausted
```

---

## 3. Additional Configuration

Requires tuning:

- Pool size.
- Timeout.
- Idle limits.

---

## 4. Long Running Queries

Slow queries can occupy connections.

---

# Real-World Examples

## E-Commerce Applications

During high traffic:

```text
Millions of Requests

        |

Connection Pool

        |

Database
```

---

## Banking Systems

Connection pooling helps manage large numbers of transactions.

---

## Backend APIs

Common architecture:

```text
Users

 |

API Servers

 |

Connection Pool

 |

Database
```

---

# When to Use

Use connection pooling when:

- Application communicates with databases frequently.
- High request volume exists.
- Database connection creation is expensive.
- Multiple users access the system simultaneously.

---

# When NOT to Use

Avoid connection pooling when:

- Application rarely accesses databases.
- Database connections are extremely lightweight.
- Serverless functions create short-lived execution environments without pool management.

---

# Comparison

| Feature | Without Pooling | With Pooling |
|---|---|---|
| Connection Creation | Every request | Reused |
| Performance | Lower | Higher |
| Database Load | Higher | Lower |
| Resource Control | Poor | Better |
| Complexity | Low | Higher |

---

# Interview Questions

## 1. What is connection pooling?

Connection pooling maintains reusable database connections to avoid creating a new connection for every request.

---

## 2. Why is connection creation expensive?

Because it involves:

- Network communication.
- Authentication.
- Resource allocation.

---

## 3. What happens when all connections are busy?

New requests wait until a connection becomes available or timeout occurs.

---

## 4. What is a connection leak?

A connection leak occurs when an application does not return borrowed connections back to the pool.

---

## 5. How do you decide connection pool size?

Based on:

- Database capacity.
- Application concurrency.
- Query performance.
- Number of application instances.

---

# Key Takeaways

- Connection pooling improves database performance.
- Connections are reused instead of recreated.
- Pool size must be carefully configured.
- It prevents database connection exhaustion.
- It is essential for high-traffic backend systems.
- Proper connection management improves scalability.

---

## Previous & Next

← Previous: [Read Replicas](09-Read-Replicas.md)

→ Next: [Consistent Hashing](11-Consistent-Hashing.md)