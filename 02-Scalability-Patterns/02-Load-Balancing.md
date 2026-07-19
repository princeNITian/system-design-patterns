# Load Balancing

## Introduction

Load Balancing is a scalability pattern used to distribute incoming client requests across multiple servers or service instances.

The main goal of load balancing is to:

- Prevent a single server from becoming overloaded.
- Improve system availability.
- Increase scalability.
- Improve response time.

Instead of sending all traffic to one server, a load balancer distributes traffic across multiple servers.

---

## Why was it Introduced?

Initially, applications were deployed on a single server.

Example:

```text
              Users

                |

                ▼

          Application Server

                |

                ▼

            Database
```

As traffic increases:

- Server resources become exhausted.
- Response time increases.
- Server failures impact the entire application.

A single server creates:

- Performance bottlenecks.
- Single point of failure.
- Limited scalability.

Load Balancing was introduced to distribute workload across multiple servers.

---

## Architecture Diagram

```text
                  Users

                    |

                    ▼

             Load Balancer

          /        |        \

         ▼         ▼         ▼

    Server 1   Server 2   Server 3

         \         |         /

          \        |        /

             Application

```

The load balancer acts as an entry point and routes requests to available servers.

---

## How It Works

The request flow:

```text
1. Client sends request.

2. Request reaches load balancer.

3. Load balancer selects an available server.

4. Server processes the request.

5. Response is returned to the client.
```

Example:

```text
1000 Requests/sec

        |

        ▼

   Load Balancer

        |

   ┌────┼────┐

   ▼    ▼    ▼

 S1    S2    S3


Each server handles a portion of traffic.
```

---

# Types of Load Balancing

## 1. Hardware Load Balancer

A physical device used to distribute network traffic.

Examples:

- F5 BIG-IP
- Citrix ADC

Used mainly in enterprise data centers.

---

## 2. Software Load Balancer

A software-based solution running on servers.

Examples:

- NGINX
- HAProxy
- Envoy

---

## 3. Cloud Load Balancer

Managed load balancing services provided by cloud providers.

Examples:

- AWS Elastic Load Balancer
- Google Cloud Load Balancing
- Azure Load Balancer

---

# Load Balancing Algorithms

## 1. Round Robin

Requests are distributed sequentially across servers.

Example:

```text
Request 1 → Server 1

Request 2 → Server 2

Request 3 → Server 3

Request 4 → Server 1
```

Advantages:

- Simple.
- Easy to implement.

Disadvantages:

- Does not consider server capacity.

---

## 2. Weighted Round Robin

Servers receive traffic based on their capacity.

Example:

```text
Server 1 → Weight 5

Server 2 → Weight 3

Server 3 → Weight 1
```

A more powerful server receives more requests.

---

## 3. Least Connections

Routes traffic to the server with the fewest active connections.

Example:

```text
Server 1 → 100 connections

Server 2 → 20 connections

Server 3 → 50 connections


New request → Server 2
```

Useful when request processing time varies.

---

## 4. IP Hash

Uses client IP address to determine the server.

Example:

```text
Client IP

     |

Hash Function

     |

Server Selection
```

Useful for maintaining session persistence.

---

## 5. Least Response Time

Routes requests to the server responding fastest.

Considers:

- Current latency.
- Active connections.

---

# Load Balancer Types by Network Layer

## Layer 4 Load Balancer

Works at the transport layer.

Uses:

- IP address.
- TCP/UDP ports.

Example:

```text
Client

 |

TCP Connection

 |

Load Balancer

 |

Server
```

Advantages:

- Faster.
- Lower latency.

---

## Layer 7 Load Balancer

Works at the application layer.

Uses:

- HTTP headers.
- URL paths.
- Cookies.
- Hostnames.

Example:

```text
/api/users

        → User Service


/api/orders

        → Order Service
```

Advantages:

- Intelligent routing.
- Application-aware decisions.

---

# Advantages

## 1. High Availability

If one server fails, traffic can be redirected to healthy servers.

Example:

```text
Server 1 ❌

        |

Load Balancer

        |

Server 2 ✅
```

---

## 2. Horizontal Scalability

New servers can be added without changing client configuration.

---

## 3. Better Performance

Requests are distributed evenly across servers.

---

## 4. Health Monitoring

Load balancers continuously check server health.

Example:

```text
Health Check

Server Available?

Yes → Send Traffic

No → Remove From Pool
```

---

## 5. Maintenance Without Downtime

Servers can be removed temporarily for updates.

---

# Disadvantages

## 1. Additional Complexity

Requires managing:

- Load balancer configuration.
- Routing rules.
- Health checks.

---

## 2. Additional Cost

Managed load balancers increase infrastructure cost.

---

## 3. Configuration Mistakes

Incorrect routing rules can impact availability.

---

## 4. Single Point of Failure

A load balancer itself must be highly available.

Usually solved by:

- Multiple load balancers.
- Managed cloud services.

---

# Real-World Examples

## Netflix

Uses load balancing to distribute user requests across thousands of services.

Example:

```text
Users

 |

Load Balancer

 |

Multiple Netflix Services
```

---

## Amazon

Uses load balancing to distribute traffic across large-scale infrastructure.

---

## Modern Cloud Applications

Common architecture:

```text
Internet

   |

Load Balancer

   |

Application Servers

   |

Database
```

---

# When to Use

Use Load Balancing when:

- Multiple application servers exist.
- High availability is required.
- Traffic is unpredictable.
- Horizontal scaling is needed.
- Zero downtime deployment is required.

---

# When NOT to Use

Avoid load balancing when:

- Application runs on a single small server.
- Traffic is very low.
- Additional infrastructure complexity is unnecessary.

---

# Comparison

| Feature | Without Load Balancer | With Load Balancer |
|---|---|---|
| Servers | Single server | Multiple servers |
| Availability | Low | High |
| Scalability | Limited | High |
| Failure Handling | Poor | Better |
| Traffic Distribution | None | Automatic |

---

# Interview Questions

## 1. What is Load Balancing?

Load balancing is the process of distributing incoming requests across multiple servers to improve scalability and availability.

---

## 2. Why do we need a load balancer?

A load balancer prevents server overload, improves performance, and provides fault tolerance.

---

## 3. Difference between Layer 4 and Layer 7 Load Balancer?

Layer 4 works using network information like IP and ports.

Layer 7 works using application information like URLs, headers, and cookies.

---

## 4. What happens if a server fails?

The load balancer detects the failure through health checks and removes that server from the available pool.

---

## 5. Which load balancing algorithm is commonly used?

Common algorithms:

- Round Robin.
- Least Connections.
- Weighted Round Robin.
- IP Hash.

---

# Key Takeaways

- Load balancing distributes traffic across multiple servers.
- It improves availability, scalability, and performance.
- Layer 4 works at the transport layer.
- Layer 7 provides application-aware routing.
- Health checks ensure traffic reaches healthy servers.
- Load balancing is a fundamental pattern in distributed systems.

---

## Previous & Next

← Previous: [Horizontal vs Vertical Scaling](01-Horizontal-vs-Vertical-Scaling.md)

→ Next: [Auto Scaling](03-Auto-Scaling.md)