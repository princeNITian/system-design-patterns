# Caching

## Introduction

Caching is a scalability pattern that stores frequently accessed data in a faster storage layer to reduce response time and decrease the load on the primary data source.

Instead of fetching the same data repeatedly from a database or external service, applications store frequently requested data in a cache.

The main goals of caching are:

- Reduce latency.
- Improve application performance.
- Reduce database load.
- Increase system scalability.

---

## Why was it Introduced?

In a traditional system, every request directly accesses the database.

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

- Database receives more queries.
- Query processing becomes slower.
- Database becomes a bottleneck.
- Response time increases.

Many applications have repeated read requests for the same data.

Example:

```text
Product Details

User Profile

Configuration Data

Popular Content
```

Caching was introduced to store frequently accessed data closer to the application.

---

## Architecture Diagram

```text
                  Users

                    |

                    ▼

            Application Server

                    |

          ┌─────────┴─────────┐

          ▼                   ▼

       Cache              Database


          |
          |
      Fast Response
```

Request flow:

1. Check cache first.
2. Return data if available.
3. Fetch from database if missing.
4. Store result in cache.

---

# How It Works

The basic caching flow:

```text
1. Client sends request.

2. Application checks cache.

3. If data exists:

        Return cached data


4. If data does not exist:

        Fetch from database

        Store in cache

        Return response
```

Example:

```text
Request Product Details

        |

        ▼

Check Redis Cache

        |

   ┌────┴────┐

   ▼         ▼

 HIT        MISS

   |          |

Return     Query DB

Data          |

              ▼

          Store Cache
```

---

# Types of Caching

## 1. Client-Side Cache

Data is stored on the user's device.

Examples:

- Browser cache.
- Mobile application cache.

Advantages:

- Very fast.
- Reduces server requests.

Disadvantages:

- Data may become stale.
- Limited storage.

---

## 2. Server-Side Cache

Data is stored on application infrastructure.

Examples:

- Redis.
- Memcached.

Commonly used for:

- User sessions.
- API responses.
- Frequently accessed data.

---

## 3. Database Cache

Databases internally cache frequently accessed data.

Examples:

- Query cache.
- Buffer pool.

---

## 4. CDN Cache

Stores static content closer to users.

Examples:

- Images.
- Videos.
- JavaScript files.
- CSS files.

---

# Common Caching Strategies

## 1. Cache-Aside (Lazy Loading)

Application manages cache manually.

Flow:

```text
Application

    |

Check Cache

    |

Miss?

    |

Query Database

    |

Update Cache
```

Advantages:

- Simple.
- Flexible.

Disadvantages:

- Cache miss causes database load.

---

## 2. Write-Through Cache

Data is written to cache and database together.

Flow:

```text
Application

      |

      ▼

   Cache

      |

      ▼

 Database
```

Advantages:

- Cache always contains latest data.

Disadvantages:

- Higher write latency.

---

## 3. Write-Back Cache

Data is written to cache first and database later.

Flow:

```text
Application

      |

      ▼

   Cache

      |

Async Update

      |

      ▼

 Database
```

Advantages:

- Very fast writes.

Disadvantages:

- Risk of data loss if cache fails.

---

## 4. Read-Through Cache

Cache automatically fetches missing data from the database.

Flow:

```text
Application

      |

      ▼

   Cache

      |

      ▼

 Database
```

Application does not directly communicate with database for reads.

---

# Cache Eviction Strategies

When cache storage becomes full, old data must be removed.

## 1. LRU (Least Recently Used)

Removes data that has not been accessed recently.

---

## 2. LFU (Least Frequently Used)

Removes data accessed the least number of times.

---

## 3. TTL (Time To Live)

Data automatically expires after a fixed duration.

Example:

```text
User Session

TTL = 30 minutes
```

---

# Core Characteristics

## 1. Faster Data Access

Memory access is much faster than database queries.

---

## 2. Reduced Database Load

Frequently requested data is served from cache.

---

## 3. Temporary Storage

Cached data can be regenerated from the primary source.

---

## 4. Data Expiration

Cache entries usually have a lifetime.

---

## 5. Distributed Caching

Multiple application servers can share the same cache.

Example:

```text
Server 1
    \
     \
    Redis Cluster
     /
    /
Server 2
```

---

# Advantages

## 1. Improved Performance

Reduces response latency.

---

## 2. Increased Scalability

Allows systems to handle more requests.

---

## 3. Reduced Database Pressure

Fewer database operations are required.

---

## 4. Better User Experience

Faster response times improve application experience.

---

## 5. Cost Optimization

Reduces expensive database operations.

---

# Disadvantages

## 1. Data Consistency Challenges

Cached data may become outdated.

Example:

```text
Database:

Price = $100


Cache:

Price = $90
```

---

## 2. Cache Invalidation Complexity

Updating or deleting stale cache data is difficult.

---

## 3. Additional Infrastructure

Requires:

- Cache servers.
- Monitoring.
- Management.

---

## 4. Cache Failures

Cache outages can increase database load.

---

# Real-World Examples

## E-Commerce Systems

Cache:

- Product details.
- Product categories.
- Recommendations.

Example:

```text
Millions of users

        |

Redis Cache

        |

Database
```

---

## Social Media Platforms

Cache:

- User profiles.
- Feeds.
- Trending content.

---

## Streaming Platforms

Cache:

- Metadata.
- Content information.
- User preferences.

---

# When to Use

Use caching when:

- Data is read frequently.
- Data changes less often.
- Low latency is required.
- Database load is high.
- Large numbers of users access similar data.

---

# When NOT to Use

Avoid caching when:

- Data changes constantly.
- Strong consistency is required.
- Data is rarely accessed.
- Cache management complexity is not justified.

---

# Comparison

| Feature | Database Access | Cache Access |
|---|---|---|
| Speed | Slower | Faster |
| Storage | Persistent | Temporary |
| Cost | Higher | Lower |
| Consistency | Strong | Eventual possible |
| Capacity | Larger | Limited |

---

# Interview Questions

## 1. What is caching?

Caching is storing frequently accessed data in a faster storage layer to improve performance and reduce database load.

---

## 2. Why is cache faster than a database?

Cache usually stores data in memory, while databases may require query processing and disk access.

---

## 3. What is cache invalidation?

Cache invalidation is the process of removing or updating stale data stored in cache.

---

## 4. Difference between Cache-Aside and Write-Through?

Cache-Aside lets the application manage cache operations.

Write-Through updates cache and database together.

---

## 5. What happens if cache goes down?

Requests fall back to the database, but increased database load may occur.

---

# Key Takeaways

- Caching improves system performance and scalability.
- Cache stores frequently accessed data closer to applications.
- Cache-Aside is the most commonly used strategy.
- TTL and eviction policies control cache size.
- Cache consistency is the biggest challenge.
- Redis and Memcached are common caching solutions.

---

## Previous & Next

← Previous: [Auto Scaling](03-Auto-Scaling.md)

→ Next: [CDN](05-CDN.md)