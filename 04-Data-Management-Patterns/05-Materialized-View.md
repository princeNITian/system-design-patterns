# Materialized View

## Introduction

A Materialized View is a data management pattern where **query results are precomputed and stored**, allowing applications to retrieve data much faster than executing complex queries every time.

Unlike a regular database view, a materialized view stores the actual data and must be refreshed when the underlying data changes.

The main goals of the Materialized View pattern are:

- Improve query performance.
- Reduce expensive database computations.
- Optimize read-heavy workloads.
- Support fast reporting and dashboards.

---

## Why was it Introduced?

Some queries involve:

- Multiple table joins.
- Aggregations.
- Sorting.
- Filtering millions of records.

Running these queries repeatedly is expensive.

Example:

```text
Orders

+

Customers

+

Payments

+

Products

↓

Sales Dashboard
```

Instead of executing this query every time, the result is precomputed and stored.

---

## Architecture Diagram

```text
          Write Database

                |

          Data Changes

                |

                ▼

      Materialized View Builder

                |

                ▼

      Materialized View Store

                |

                ▼

        Read Applications
```

Applications read directly from the materialized view.

---

## How It Works

The communication flow:

```text
1. Business data changes.

2. Materialized View is refreshed.

3. Updated results are stored.

4. Applications query the Materialized View.

5. Responses are returned quickly.
```

Example:

```text
Orders Updated

        |

Refresh Materialized View

        |

Sales Dashboard

        |

Fast Query
```

---

# Core Components

## 1. Source Data

Original business tables.

Examples:

- Orders
- Customers
- Products
- Payments

---

## 2. Materialized View

Stores precomputed query results.

---

## 3. Refresh Process

Updates the Materialized View after source data changes.

Refresh may be:

- Immediate
- Scheduled
- Event-driven

---

## 4. Read Applications

Applications query the Materialized View instead of the source tables.

---

# Core Characteristics

## 1. Precomputed Results

Complex queries are executed in advance.

---

## 2. Faster Reads

Applications retrieve already-prepared data.

---

## 3. Separate Storage

The Materialized View stores its own copy of data.

---

## 4. Refresh Mechanism

The view must be updated when source data changes.

---

## 5. Read Optimization

Designed specifically for query performance.

---

# Advantages

## 1. High Query Performance

Precomputed data significantly reduces response times.

---

## 2. Reduced Database Load

Expensive joins and aggregations are performed less frequently.

---

## 3. Better User Experience

Dashboards and reports load much faster.

---

## 4. Simplified Queries

Applications read from an optimized structure.

---

## 5. Works Well with CQRS

Materialized Views commonly serve as optimized read models.

---

# Disadvantages

## 1. Additional Storage

The view stores duplicate data.

---

## 2. Refresh Overhead

Keeping the view up to date requires additional processing.

---

## 3. Eventual Consistency

The view may temporarily contain stale data.

---

## 4. Increased Complexity

Refresh strategies must be carefully designed.

---

## 5. Maintenance

Schema changes often require rebuilding the view.

---

# Real-World Examples

## E-Commerce

Precompute:

- Sales dashboards.
- Top-selling products.
- Customer purchase summaries.

---

## Banking

Generate:

- Daily account summaries.
- Transaction reports.
- Financial dashboards.

---

## Analytics Platforms

Store:

- User activity summaries.
- Aggregated metrics.
- Trending reports.

---

## Business Intelligence

Provide optimized datasets for reporting tools.

---

# When to Use

Use the Materialized View pattern when:

- Read queries are expensive.
- Reports and dashboards are frequently accessed.
- Data changes less often than it is read.
- Slightly stale data is acceptable.

---

# When NOT to Use

Avoid the Materialized View pattern when:

- Data changes constantly and must always be current.
- Queries are simple and already fast.
- Storage duplication is unacceptable.

---

# Comparison

| Feature | Database View | Materialized View |
|---|---|---|
| Stores Data | No | Yes |
| Query Speed | Depends on source query | Very Fast |
| Storage Required | No | Yes |
| Refresh Needed | No | Yes |
| Best For | Simple abstraction | High-performance reads |

---

# Interview Questions

## 1. What is a Materialized View?

A precomputed and stored query result used to improve read performance.

---

## 2. How is it different from a normal database view?

A normal view stores only the SQL query.

A Materialized View stores the query results.

---

## 3. Why can a Materialized View become stale?

Because it is refreshed periodically or asynchronously after source data changes.

---

## 4. How are Materialized Views commonly updated?

- Scheduled refreshes.
- Event-driven updates.
- Incremental refreshes.
- Manual refreshes.

---

## 5. Where are Materialized Views commonly used?

- Dashboards.
- Business intelligence.
- Reporting systems.
- CQRS read models.
- Analytics platforms.

---

# Key Takeaways

- Materialized Views store precomputed query results.
- They significantly improve read performance.
- They require a refresh mechanism to stay up to date.
- They trade storage and freshness for speed.
- They are widely used in reporting, analytics, and CQRS architectures.

---

## Previous & Next

← Previous: [Event Sourcing](04-Event-Sourcing.md)

→ Next: [Replication](06-Replication.md)