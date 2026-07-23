# Part 1

## Introduction → Requirements → Capacity Estimation


# Design a URL Shortener

## Introduction

A URL Shortener is a service that converts a long URL into a short, unique alias that redirects users to the original destination.

Instead of sharing a lengthy URL like:

```text
https://www.example.com/products/electronics/mobile/samsung/galaxy-s26-ultra?ref=homepage&utm_campaign=summer-sale
```

the service generates:

```text
https://tiny.ly/Ab3XkP
```

When users visit the shortened URL, they are automatically redirected to the original URL.

Popular URL shortening services include:

- Bitly
- TinyURL
- Rebrandly
- Short.io

Although the functionality appears simple, designing a URL shortener involves many distributed system concepts such as caching, database design, consistency, scalability, load balancing, fault tolerance, rate limiting, and analytics.

---

# Problem Statement

Design a highly scalable URL shortening service similar to Bitly that can:

- Generate short URLs.
- Redirect users with very low latency.
- Handle billions of URLs.
- Support millions of daily users.
- Scale horizontally.
- Remain highly available.

---

# Functional Requirements

The system should support the following features.

## Core Features

### 1. Shorten URL

Users provide a long URL.

Example:

```text
https://amazon.com/product/123456789
```

System returns:

```text
https://tiny.ly/X7kd92
```

---

### 2. Redirect

When a user visits the shortened URL:

```text
https://tiny.ly/X7kd92
```

they should be redirected to:

```text
https://amazon.com/product/123456789
```

---

### 3. URL Expiration (Optional)

Users may specify an expiration time.

Example:

```text
Expires after

30 Days
```

After expiration, the short URL becomes invalid.

---

### 4. Custom Alias (Optional)

Instead of a random code:

```text
tiny.ly/A7hd9P
```

users may request:

```text
tiny.ly/summer-sale
```

if it is available.

---

### 5. Analytics (Optional)

Track:

- Number of clicks
- Country
- Browser
- Device
- Timestamp
- Referrer

---

### 6. QR Code Generation (Optional)

Generate a QR code for every shortened URL.

---

# Non-Functional Requirements

The system should satisfy the following requirements.

## High Availability

Users should always be able to create and access shortened URLs.

Target:

```text
99.99% Availability
```

---

## Low Latency

Redirects should be extremely fast.

Target:

```text
< 50 ms
```

---

## High Scalability

The system should support:

- Billions of URLs
- Millions of users
- Continuous growth

---

## Durability

URLs must never be lost.

---

## Fault Tolerance

The service should continue operating even if servers fail.

---

## Horizontal Scalability

Additional servers should increase capacity without downtime.

---

## Security

Prevent:

- Spam
- Malicious URLs
- Abuse
- DDoS attacks

---

# Back-of-the-Envelope Estimation

Before designing the architecture, estimate the expected scale.

Assumptions:

- 100 million new URLs created per month
- 1 billion redirects per month
- Average original URL length = 200 bytes
- Short code length = 7 characters
- Metadata = 100 bytes

---

## Storage per URL

Approximate storage:

| Field | Size |
|--------|------|
| Original URL | 200 Bytes |
| Short Code | 7 Bytes |
| Metadata | 100 Bytes |
| Timestamp | 8 Bytes |
| User ID (Optional) | 8 Bytes |

Total:

```text
≈ 325 Bytes
```

For simplicity, round up:

```text
350 Bytes
```

---

## Annual Storage

100 Million URLs

×

350 Bytes

=

35 GB

Per Year

Even after adding indexes, replication, and metadata, the storage requirement remains manageable and can scale horizontally using database partitioning.

---

## Read vs Write Ratio

A URL shortener is heavily read-oriented.

Typical ratio:

```text
Reads

100

:

Writes

1
```

Meaning:

For every new URL created, the system performs approximately 100 redirect requests.

This has important architectural implications:

- Reads should be served from cache whenever possible.
- Redirect latency should be minimized.
- Database reads should be reduced.
- Writes can tolerate slightly higher latency.

---

## Bandwidth Considerations

Redirect responses are lightweight.

Most bandwidth consumption comes from:

- API requests
- Analytics events
- Health checks
- Internal service communication

Therefore, the primary scalability challenge is **handling request volume**, not transferring large amounts of data.

---

# High-Level Requirements Summary

| Metric | Estimated Value |
|---------|-----------------|
| New URLs | 100 Million / Month |
| Redirects | 1 Billion / Month |
| Read/Write Ratio | 100:1 |
| Average URL Size | 350 Bytes |
| Availability | 99.99% |
| Redirect Latency | < 50 ms |
| Scalability | Horizontal |
| Data Loss | Not Acceptable |

---

Next, we'll design the complete architecture, including:

- High-Level Architecture
- API Design
- Database Design
- URL Generation Algorithms
- End-to-End Request Flow

---

# Part 2

This establishes the problem and scale before moving into the architecture, which is the natural next step in a system design interview.

# High-Level Architecture

At a high level, the system consists of the following components:

```text
                    Client
                       |
                DNS / CDN (Optional)
                       |
                Load Balancer
                       |
                API Gateway
                  /          \
                 /            \
        URL Creation API   Redirect API
               |                 |
               |                 |
        Cache (Redis)      Cache (Redis)
               |                 |
               +--------+--------+
                        |
                  URL Database
                        |
                  Analytics Queue
                        |
                  Stream Processing
                        |
                 Analytics Database
```

The system separates **write-heavy URL creation** from **read-heavy redirection**, allowing each component to scale independently.

---

# Component Overview

## Client

The client can be:

- Browser
- Mobile application
- Backend service
- Third-party application

---

## Load Balancer

Responsibilities:

- Distribute requests
- Health checking
- SSL termination
- High availability

Examples:

- AWS ALB
- NGINX
- HAProxy

---

## API Gateway

Responsibilities:

- Authentication
- Rate limiting
- Routing
- Request validation
- Monitoring

---

## URL Creation Service

Responsible for:

- Validating URLs
- Generating unique short codes
- Persisting mappings
- Returning shortened URLs

---

## Redirect Service

Responsible for:

- Looking up short codes
- Returning HTTP redirects
- Recording analytics asynchronously

This service handles the majority of system traffic.

---

## Cache

Stores frequently accessed mappings.

Example:

```text
Ab3XkP

↓

https://amazon.com/product/123
```

Since redirects are read-heavy, most requests should be served directly from cache.

---

## Database

Stores the permanent mapping:

```text
Short URL

↓

Original URL
```

The database is the source of truth.

---

## Analytics Pipeline

Click events are written asynchronously to avoid increasing redirect latency.

Example:

```text
Redirect

↓

Publish Event

↓

Kafka

↓

Analytics Service
```

---

# High-Level Workflow

## Creating a Short URL

```text
Client

↓

API Gateway

↓

URL Service

↓

Generate Short Code

↓

Save to Database

↓

Update Cache

↓

Return Short URL
```

---

## Redirecting

```text
Client

↓

API Gateway

↓

Redirect Service

↓

Redis Cache

↓

Database (Cache Miss)

↓

HTTP 302 Redirect
```

---

# API Design

The API should follow REST principles.

---

## 1. Create Short URL

```http
POST /api/v1/urls
```

Request

```json
{
  "url": "https://amazon.com/product/123456",
  "customAlias": "summer-sale",
  "expiresAt": "2027-01-01T00:00:00Z"
}
```

---

Successful Response

```json
{
  "shortUrl": "https://tiny.ly/Ab3XkP",
  "code": "Ab3XkP",
  "expiresAt": "2027-01-01T00:00:00Z"
}
```

---

## 2. Redirect

```http
GET /Ab3XkP
```

Response

```http
302 Found

Location:
https://amazon.com/product/123456
```

HTTP **302** is commonly used because the destination may change, while **301** can be used for permanent redirects depending on the use case.

---

## 3. Get Analytics

```http
GET /api/v1/urls/Ab3XkP/analytics
```

Response

```json
{
  "totalClicks": 15780,
  "countries": {
    "India": 5400,
    "USA": 3900
  },
  "devices": {
    "Mobile": 12000,
    "Desktop": 3780
  }
}
```

---

## 4. Delete URL (Optional)

```http
DELETE /api/v1/urls/Ab3XkP
```

Response

```http
204 No Content
```

---

# Database Design

The primary responsibility of the database is mapping:

```text
Short Code

↓

Original URL
```

---

## URL Table

| Column | Type |
|---------|------|
| short_code | VARCHAR(10) (PK) |
| original_url | TEXT |
| created_at | TIMESTAMP |
| expires_at | TIMESTAMP |
| user_id | BIGINT |
| click_count | BIGINT |

---

## Primary Key

```text
short_code
```

Reason:

Redirects always begin with:

```text
GET /Ab3XkP
```

Using the short code as the primary key enables fast lookups.

---

# Indexes

Optional indexes:

```text
user_id

created_at

expires_at
```

Useful for:

- Listing user URLs
- Cleanup jobs
- Expiration

---

# Which Database Should We Use?

## Option 1 — MySQL

Pros

- ACID transactions
- Strong consistency
- Mature ecosystem

Cons

- Horizontal scaling is more difficult.

Suitable for:

Small to medium deployments.

---

## Option 2 — PostgreSQL

Pros

- Excellent indexing
- Strong consistency
- Rich SQL features

Suitable for:

Most production systems.

---

## Option 3 — Cassandra

Pros

- Massive horizontal scalability
- Very high write throughput
- Multi-region replication

Cons

- Eventual consistency by default
- More operational complexity

Suitable for:

Large-scale URL shortening services with billions of records.

---

## Option 4 — DynamoDB

Pros

- Fully managed
- Automatic scaling
- Low latency
- High availability

Cons

- Limited query flexibility compared to relational databases

Suitable for:

Cloud-native serverless architectures.

---

# Recommended Choice

| Scale | Database |
|--------|----------|
| Startup | PostgreSQL |
| Medium Scale | PostgreSQL + Read Replicas |
| Large Scale | Cassandra |
| AWS Serverless | DynamoDB |

---

# Data Model Example

| Short Code | Original URL |
|------------|--------------|
| Ab3XkP | https://amazon.com/product/123 |
| Xd91Lp | https://google.com |
| T9KmQa | https://github.com |

Each redirect simply performs:

```text
Lookup

↓

Short Code

↓

Original URL

↓

HTTP Redirect
```

---

# Design Decisions So Far

✅ Stateless API servers

✅ Read-heavy optimized architecture

✅ Redis cache in front of the database

✅ Short code as the primary key

✅ Separate analytics pipeline

✅ Horizontally scalable services

---

Next, we'll dive into the most interesting parts of the design:

- URL Generation Algorithms (Base62, Hashing, Counter, UUID)
- Cache Strategy
- End-to-End Request Flow
- Scaling to Billions of URLs
- Replication & Sharding
- Fault Tolerance
- CDN Optimization

---
# Part 3

## URL Generation → Cache Strategy → End-to-End Request Flow

# URL Generation

One of the most important parts of a URL shortener is generating **unique, compact, and collision-free short codes**.

A good short code should be:

- Unique
- Short
- URL-safe
- Fast to generate
- Difficult to predict (optional)
- Scalable to billions of URLs

---

# Option 1 — Auto Increment + Base62 (Recommended)

Maintain a global numeric ID.

Example:

```text
1000001

↓

Base62 Encoding

↓

4C92X
```

Instead of storing long numbers, encode them using Base62.

Base62 contains:

```text
0-9

A-Z

a-z
```

Total characters:

```text
62
```

---

## Example

```text
Decimal

125

↓

Base62

cb
```

This significantly reduces the length of the generated URL.

---

## Capacity

Using 7 Base62 characters:

```text
62⁷

≈

3.5 Trillion URLs
```

This is sufficient for most production systems.

---

## Advantages

- Guaranteed uniqueness.
- Short URLs.
- No collisions.
- Fast encoding and decoding.

---

## Disadvantages

- Requires a globally unique ID generator.
- Sequential IDs may reveal traffic volume unless obfuscated.

---

# Option 2 — Hashing

Generate a hash from the original URL.

Example:

```text
SHA-256

↓

a93bd67...

↓

Take First 7 Characters

↓

a93bd67
```

---

## Advantages

- Simple implementation.
- Same input can generate the same output.

---

## Disadvantages

- Collision risk when truncating hashes.
- Collision detection logic is required.
- Hash values are longer before truncation.

---

# Option 3 — Random String

Generate a random Base62 string.

Example:

```text
G7Lm9Xa
```

Before saving:

```text
Check Database

↓

Already Exists?

↓

Generate Again
```

---

## Advantages

- Simple.
- Difficult to predict.

---

## Disadvantages

- Collision probability increases as the database grows.
- Extra database lookup for uniqueness.

---

# Option 4 — UUID

Generate a UUID.

Example:

```text
550e8400-e29b-41d4
```

---

## Advantages

- Globally unique.
- No coordination required.

---

## Disadvantages

- Too long for URL shortening.
- Requires encoding or compression to become user-friendly.

---

# Comparison

| Method | Collision | Performance | Scalability | Recommendation |
|---------|-----------|-------------|--------------|----------------|
| Base62 + Counter | None | Excellent | Excellent | ⭐⭐⭐⭐⭐ |
| Hashing | Possible | Good | Good | ⭐⭐⭐ |
| Random String | Possible | Good | Good | ⭐⭐⭐ |
| UUID | None | Good | Excellent | ⭐⭐ |

---

# Recommended Approach

For production systems:

```text
Global ID Generator

↓

Unique Numeric ID

↓

Base62 Encoding

↓

Store Mapping

↓

Return Short URL
```

This approach is used by many large-scale URL shortening systems because it guarantees uniqueness while keeping URLs short.

---

# Cache Strategy

A URL shortener has a very high read-to-write ratio.

Typical traffic:

```text
Redirect Requests

100

:

URL Creation

1
```

Since most operations are redirects, caching significantly reduces database load.

---

# Cache Architecture

```text
Client

↓

Redirect Service

↓

Redis

↓

Database
```

Most requests should be served directly from Redis.

---

# Cache Hit

```text
Redis

↓

Found

↓

Return Original URL

↓

HTTP Redirect
```

Database is never accessed.

---

# Cache Miss

```text
Redis

↓

Not Found

↓

Database Lookup

↓

Update Redis

↓

Return Redirect
```

Future requests are served from cache.

---

# Cache-Aside Pattern

The recommended strategy is **Cache-Aside**.

Workflow:

```text
Read Cache

↓

Hit?

↓

Yes

↓

Return

↓

No

↓

Read Database

↓

Update Cache

↓

Return
```

This keeps Redis synchronized lazily while minimizing unnecessary writes.

---

# TTL

Popular URLs should remain cached.

Example:

```text
TTL

24 Hours
```

Frequently accessed entries naturally stay warm due to repeated access.

---

# Why Redis?

Redis provides:

- Extremely low latency (sub-millisecond)
- High throughput
- Simple key-value lookups
- Horizontal scaling using Redis Cluster
- High availability with Redis Sentinel or managed services

---

# End-to-End Request Flow

## URL Creation Flow

```text
Client

↓

Load Balancer

↓

API Gateway

↓

URL Service

↓

Validate URL

↓

Generate Short Code

↓

Store in Database

↓

Write to Redis

↓

Return Short URL
```

---

## Redirect Flow (Cache Hit)

```text
Client

↓

GET /Ab3XkP

↓

Load Balancer

↓

Redirect Service

↓

Redis Lookup

↓

Original URL Found

↓

HTTP 302 Redirect
```

This is the ideal path and should serve the majority of requests.

---

## Redirect Flow (Cache Miss)

```text
Client

↓

GET /Ab3XkP

↓

Redirect Service

↓

Redis Miss

↓

Database Lookup

↓

Store in Redis

↓

HTTP 302 Redirect
```

Only the first request (or after cache expiration) requires a database read.

---

# Analytics Flow

Redirect performance should not be affected by analytics processing.

Instead of writing analytics synchronously:

```text
Redirect

↓

Write Analytics Event

↓

Kafka

↓

Analytics Service

↓

Analytics Database
```

The user receives the redirect immediately while analytics are processed asynchronously.

---

# Why Use Asynchronous Analytics?

Without asynchronous processing:

```text
Redirect

↓

Database Write

↓

Analytics Write

↓

Return Response
```

The redirect latency increases.

With asynchronous processing:

```text
Redirect

↓

Return Response

↓

Background Analytics Processing
```

This keeps redirect latency consistently low.

---

# Design Decisions So Far

✅ Base62-encoded unique IDs

✅ Redis Cache-Aside pattern

✅ Read-heavy optimization

✅ Asynchronous analytics pipeline

✅ Stateless application servers

✅ Database as the source of truth

---

Next, we'll cover:

- Scaling to Billions of URLs
- Database Replication & Sharding
- High Availability
- Fault Tolerance
- CDN Usage
- Security Considerations
- Monitoring & Observability
- Bottlenecks & Optimizations
- Trade-offs
- Interview Questions
- Key Takeaways

---
# Part 4 (Final)

## Scaling → High Availability → Security → Trade-offs → Interview Preparation

---
# Scaling Strategy

As traffic grows from thousands to billions of requests, every component must scale independently.

```text
                    Users
                      |
                 DNS / CDN
                      |
               Load Balancer
                      |
        +-------------+-------------+
        |                           |
  URL Creation Service      Redirect Service
        |                           |
        |                    Redis Cluster
        |                           |
        +-------------+-------------+
                      |
               Database Cluster
                      |
             Analytics Pipeline
```

The architecture is **horizontally scalable**, meaning additional servers can be added without changing application logic.

---

# Scaling the Application Layer

The application servers are **stateless**.

```text
        LB

   /     |     \

 API1  API2  API3

   \     |     /

      Database
```

Since no user session is stored in memory:

- Any request can be served by any server.
- Servers can be added or removed dynamically.
- Auto Scaling becomes straightforward.

---

# Scaling Redis

A single Redis instance eventually becomes a bottleneck.

Use **Redis Cluster**.

```text
        Redis Cluster

     /       |       \

 Node1    Node2    Node3
```

Benefits:

- Horizontal scaling
- Automatic sharding
- High throughput
- Replication support

---

# Scaling the Database

Initially:

```text
Primary Database
```

As traffic increases:

```text
          Primary

         /      \

Replica1      Replica2
```

Read replicas reduce load for analytics and administrative queries.

---

# Database Sharding

When a single database can no longer hold all records, partition the data.

Example:

```text
Shard 1

A-M

------------

Shard 2

N-Z
```

Or use hash-based partitioning:

```text
hash(shortCode)

↓

Shard Number
```

Benefits:

- Larger storage capacity
- Higher throughput
- Parallel query processing

---

# High Availability

High availability ensures the service remains operational despite failures.

Target:

```text
99.99%
```

---

## Multi-AZ Deployment

```text
Availability Zone A

API

Redis

Database

-------------

Availability Zone B

API

Redis Replica

Database Replica
```

If one availability zone fails, traffic automatically shifts to the other.

---

## Multi-Region Deployment

```text
US-East

↓

Replication

↓

Europe

↓

Replication

↓

Asia
```

Benefits:

- Disaster recovery
- Reduced latency
- Global availability

---

# Fault Tolerance

Every component should tolerate failures.

---

## API Failure

```text
API 1

↓

Fails

↓

Load Balancer

↓

API 2
```

Users continue receiving responses.

---

## Redis Failure

```text
Redis

↓

Unavailable

↓

Database

↓

Restore Cache
```

Performance decreases temporarily, but the service continues functioning.

---

## Database Failure

Use automatic failover.

```text
Primary

↓

Failure

↓

Replica

↓

Promoted
```

---

# CDN Usage

Although redirect responses are dynamic, static assets such as:

- Landing pages
- Documentation
- Images
- JavaScript
- CSS

can be served through a CDN.

```text
Users

↓

CloudFront

↓

Static Assets
```

This reduces latency and origin server load.

---

# Security Considerations

A URL shortener can be abused for spam, phishing, and malware distribution.

Security measures are essential.

---

## URL Validation

Accept only valid URLs.

Reject malformed inputs.

---

## HTTPS

Encrypt all communication.

```text
HTTPS

↓

TLS
```

---

## Rate Limiting

Prevent abuse.

Example:

```text
100 Requests

Per Minute

Per User
```

---

## Malware Detection

Check URLs against:

- Google Safe Browsing
- Internal blocklists
- Threat intelligence feeds

---

## Authentication

Required for:

- Analytics
- URL management
- Administrative operations

Anonymous URL creation may still be allowed depending on business requirements.

---

## Abuse Prevention

Detect:

- Spam campaigns
- Bot traffic
- URL enumeration
- Excessive shortening requests

---

# Monitoring & Observability

The system should expose comprehensive telemetry.

---

## Metrics

Examples:

- Redirect latency
- Cache hit ratio
- Database latency
- Requests per second
- Error rate

---

## Logs

Examples:

- URL creation failures
- Redirect failures
- Authentication errors

---

## Traces

Track request flow across:

```text
Gateway

↓

API

↓

Redis

↓

Database
```

---

## Alerts

Examples:

- High latency
- Database unavailable
- Cache hit ratio drops
- Increased error rate

---

# Bottlenecks

Potential bottlenecks include:

### Database

Too many reads.

Solution:

Redis.

---

### Global ID Generator

If centralized, it may become a bottleneck.

Solutions:

- Snowflake IDs
- Hi-Lo algorithm
- Distributed ID generators

---

### Hot URLs

Popular links may receive millions of requests.

Solution:

- Redis
- CDN
- Multiple cache replicas

---

### Analytics

Massive click volumes.

Solution:

Kafka + asynchronous processing.

---

# Optimizations

## Bloom Filter

Quickly determine whether a short code might exist.

```text
Request

↓

Bloom Filter

↓

Probably Exists

↓

Database
```

This reduces unnecessary database lookups.

---

## Compression

Compress analytics data before archival.

---

## Batch Processing

Write analytics in batches instead of one event at a time.

---

## Lazy Expiration

Delete expired URLs during background cleanup jobs instead of synchronously.

---

# Trade-Offs

| Decision | Benefit | Drawback |
|----------|----------|----------|
| Redis Cache | Low latency | Cache consistency |
| Base62 IDs | Short URLs | Requires ID generator |
| Async Analytics | Fast redirects | Eventual consistency |
| Cassandra | Massive scalability | Eventual consistency |
| PostgreSQL | Strong consistency | Harder horizontal scaling |
| Read Replicas | Scale reads | Replication lag |

---

# Real-World Examples

## Bitly

- Global URL shortening
- Analytics dashboard
- Custom domains
- Enterprise integrations

---

## TinyURL

- Simple URL shortening
- Permanent links
- Minimal feature set

---

## Rebrandly

- Branded short links
- Marketing analytics
- Team collaboration

---

# Interview Questions

## 1. Why is Redis important?

Because redirects are read-heavy, Redis significantly reduces database load and provides sub-millisecond lookups.

---

## 2. Why Base62 instead of UUID?

Base62 produces much shorter, user-friendly URLs while still supporting trillions of unique combinations.

---

## 3. Why process analytics asynchronously?

To avoid increasing redirect latency and improve user experience.

---

## 4. Which database would you choose?

- PostgreSQL for small to medium systems.
- Cassandra for internet-scale deployments.
- DynamoDB for AWS serverless architectures.

---

## 5. How would you prevent duplicate short codes?

Use globally unique ID generation (e.g., auto-increment with Base62, Snowflake IDs) or perform uniqueness checks before insertion.

---

## 6. How would you scale to billions of URLs?

- Stateless services
- Redis Cluster
- Database sharding
- Read replicas
- Load balancers
- Multi-region deployment

---

## 7. What happens if Redis goes down?

The application falls back to the database. Performance degrades temporarily, but the service remains available.

---

## Key Takeaways

- URL shortening is a **read-heavy** distributed system.
- Base62 encoding is a common approach for generating compact unique URLs.
- Redis dramatically reduces redirect latency.
- Analytics should be processed asynchronously using a message queue.
- Stateless services, caching, replication, and sharding enable horizontal scalability.
- Security measures such as rate limiting, URL validation, and malware detection are essential.
- Observability through logs, metrics, traces, and alerts is critical for production reliability.
- This design can scale from a startup deployment to an internet-scale service with billions of URLs.

---

# Complete Architecture

```text
                    Client
                       |
                  DNS / CDN
                       |
                Load Balancer
                       |
                 API Gateway
                  /         \
                 /           \
      URL Creation API   Redirect API
               |               |
         Base62 Generator   Redis Cluster
               |               |
               +-------+-------+
                       |
              Database Cluster
         (Primary + Replicas/Shards)
                       |
                 Kafka / SQS
                       |
              Analytics Service
                       |
             Analytics Database
                       |
          Dashboards & Monitoring
```

---

## Previous & Next

← Previous: README.md

→ Next: [Design Pastebin](02-Pastebin.md)