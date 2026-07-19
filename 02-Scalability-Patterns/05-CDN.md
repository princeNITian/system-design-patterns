# Content Delivery Network (CDN)

## Introduction

A Content Delivery Network (CDN) is a scalability pattern that distributes static content across geographically distributed servers to deliver data faster to users.

Instead of every user requesting content from the origin server, a CDN stores copies of content at locations closer to users.

The main goals of CDN are:

- Reduce latency.
- Improve content delivery speed.
- Reduce load on origin servers.
- Improve global scalability.

---

## Why was it Introduced?

In a traditional architecture, all users access content from a central server.

Example:

```text
                Users Worldwide

          /        |        \

         ▼         ▼         ▼

              Origin Server
```

Problems:

- Users far from the server experience higher latency.
- Origin server handles all requests.
- Bandwidth usage increases.
- Performance decreases during traffic spikes.

Example:

A user in India accessing a server in the US experiences additional network delay.

CDNs were introduced to bring content closer to users.

---

## Architecture Diagram

```text
                     Users

        ┌────────────┼────────────┐

        ▼            ▼            ▼

    CDN Edge      CDN Edge      CDN Edge

     (US)          (EU)          (Asia)

        \            |            /

         \           |           /

              Origin Server
```

The CDN consists of:

- Edge servers.
- Regional caches.
- Origin servers.

---

## How It Works

The request flow:

```text
1. User requests content.

2. Request reaches nearest CDN edge server.

3. CDN checks if content exists.

4. If available:

        Return cached content


5. If unavailable:

        Fetch from origin server

        Store in CDN cache

        Return response
```

Example:

```text
User requests image

        |

        ▼

CDN Edge Server

        |

   ┌────┴────┐

   ▼         ▼

 HIT        MISS

Return    Fetch from

Cache     Origin
```

---

# CDN Components

## 1. Edge Servers

Servers located close to users.

Responsibilities:

- Store cached content.
- Serve user requests.
- Reduce latency.

---

## 2. Origin Server

The original source of content.

Examples:

- Application servers.
- Cloud storage.
- Web servers.

---

## 3. Points of Presence (PoPs)

Physical locations where CDN infrastructure exists.

Example:

```text
USA

Europe

Asia

Australia
```

Users are routed to the nearest PoP.

---

# Types of CDN Content

## 1. Static Content

Content that rarely changes.

Examples:

- Images.
- Videos.
- CSS.
- JavaScript files.
- Fonts.

---

## 2. Dynamic Content

Content generated based on user requests.

Examples:

- Personalized pages.
- API responses.

Modern CDNs can accelerate some dynamic content using edge computing.

---

# CDN Caching Strategies

## 1. Pull CDN

Content is fetched from origin when requested.

Flow:

```text
User Request

      |

CDN Miss

      |

Fetch Origin

      |

Store Cache
```

Advantages:

- No manual upload required.

---

## 2. Push CDN

Content is uploaded to CDN before users request it.

Flow:

```text
Origin

   |

Push Content

   |

CDN Edge Servers
```

Advantages:

- Faster availability.

---

# Core Characteristics

## 1. Geographic Distribution

Content is stored across multiple locations.

---

## 2. Edge Caching

Frequently accessed content is stored near users.

---

## 3. Reduced Origin Load

CDN handles repeated requests.

---

## 4. High Availability

Multiple edge locations provide redundancy.

---

## 5. Traffic Optimization

CDNs optimize:

- Routing.
- Compression.
- Bandwidth usage.

---

# Advantages

## 1. Lower Latency

Users receive content from nearby servers.

Example:

```text
User → Nearby CDN

instead of

User → Distant Origin Server
```

---

## 2. Reduced Server Load

Origin servers handle fewer requests.

---

## 3. Improved Scalability

CDNs handle millions of requests globally.

---

## 4. Better Availability

Traffic can be served from multiple edge locations.

---

## 5. Reduced Bandwidth Cost

Less data transfer from origin servers.

---

# Disadvantages

## 1. Cache Invalidation Challenges

Updated content may not immediately appear.

Example:

```text
Old Image

still available in CDN cache
```

---

## 2. Additional Cost

CDN services introduce operational expenses.

---

## 3. Configuration Complexity

Requires managing:

- Cache rules.
- Expiration policies.
- Routing.

---

## 4. Not Suitable For All Data

Highly personalized or frequently changing data may not benefit.

---

# Real-World Examples

## Netflix

Uses CDN infrastructure to deliver video content closer to users.

Example:

```text
User

 |

Netflix CDN Edge

 |

Video Content
```

---

## Amazon

Uses CDN services to deliver:

- Product images.
- Static assets.
- Web content.

---

## Social Media Platforms

CDNs are used for:

- Images.
- Videos.
- Static resources.

---

# When to Use

Use CDN when:

- Serving global users.
- Delivering static content.
- Reducing latency is important.
- Origin server receives heavy traffic.
- Large files need efficient delivery.

---

# When NOT to Use

Avoid CDN when:

- Data is highly dynamic.
- Content changes constantly.
- Application has only local users.
- Additional infrastructure is unnecessary.

---

# Comparison

| Feature | Without CDN | With CDN |
|---|---|---|
| Content Location | Single origin | Distributed edge locations |
| Latency | Higher | Lower |
| Origin Load | High | Reduced |
| Global Performance | Poor | Better |
| Scalability | Limited | High |

---

# Interview Questions

## 1. What is a CDN?

A CDN is a distributed network of servers that stores and delivers content closer to users to reduce latency and improve scalability.

---

## 2. How does CDN reduce latency?

CDN reduces latency by serving content from edge servers located closer to users.

---

## 3. Difference between CDN and Cache?

Cache stores frequently accessed data for faster access.

CDN is a globally distributed caching system designed mainly for content delivery.

---

## 4. What happens when CDN cache misses?

The CDN fetches content from the origin server, stores it, and serves it to the user.

---

## 5. Does CDN provide security benefits?

Yes. CDNs can provide:

- DDoS protection.
- Traffic filtering.
- Web application firewall integration.

---

# Key Takeaways

- CDN improves global content delivery.
- It stores content closer to users.
- Edge servers reduce latency and origin load.
- Cache invalidation is a major challenge.
- CDNs are essential for globally distributed applications.
- Modern systems combine CDN with caching and load balancing.

---

## Previous & Next

← Previous: [Caching](04-Caching.md)

→ Next: [Database Sharding](06-Database-Sharding.md)