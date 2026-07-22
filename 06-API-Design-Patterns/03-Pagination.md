# Pagination

## Introduction

Pagination is an API design pattern that **returns large collections of data in smaller, manageable chunks instead of sending the entire dataset in a single response**.

Without pagination, APIs may return thousands or even millions of records, leading to high memory usage, increased network latency, and poor user experience.

The main goals of Pagination are:

- Improve API performance.
- Reduce response size.
- Lower memory consumption.
- Support efficient browsing of large datasets.

---

## Why was it Introduced?

Consider an API:

```text
GET /products
```

If the database contains 10 million products, returning all of them in one response is impractical.

Problems include:

- Slow response times.
- High memory usage.
- Increased bandwidth consumption.
- Poor client performance.

Pagination returns only a subset of the data.

---

## Architecture Diagram

```text
            Client

               |

               ▼

 GET /products?page=2&limit=20

               |

               ▼

            REST API

               |

               ▼

           Database

               |

               ▼

     Return 20 Products
```

Only the requested records are returned.

---

## How It Works

The communication flow:

```text
1. Client requests a page.

2. API validates pagination parameters.

3. Database retrieves only the requested records.

4. API returns the page of data.

5. Client requests additional pages as needed.
```

Example:

```text
GET /products?page=3&limit=10

        |

Products 21–30
```

---

# Common Pagination Strategies

## 1. Offset Pagination

Uses an offset and limit.

Example:

```text
GET /products?offset=20&limit=10
```

Returns records starting from the specified offset.

---

## 2. Page-Based Pagination

Uses page number and page size.

Example:

```text
GET /products?page=2&limit=10
```

Simple and commonly used.

---

## 3. Cursor Pagination

Uses a cursor returned from the previous response.

Example:

```text
GET /products?cursor=abc123
```

Efficient for large datasets.

---

## 4. Keyset Pagination

Uses a unique sortable column.

Example:

```text
GET /products?id>100
```

Efficient for continuously growing datasets.

---

# Core Characteristics

## 1. Smaller Responses

Only a limited number of records are returned.

---

## 2. Better Performance

Databases process fewer records per request.

---

## 3. Reduced Network Traffic

Smaller payloads improve response times.

---

## 4. Scalable

Works well with very large datasets.

---

## 5. Improved User Experience

Applications can load data incrementally.

---

# Advantages

## 1. Faster Responses

Smaller datasets are retrieved more quickly.

---

## 2. Lower Memory Usage

Servers and clients process fewer records.

---

## 3. Better Scalability

Supports applications with millions of records.

---

## 4. Reduced Bandwidth

Only necessary data is transferred.

---

## 5. Improved Database Performance

Queries are limited to smaller result sets.

---

# Disadvantages

## 1. Additional Client Logic

Clients must request multiple pages.

---

## 2. Offset Performance

Large offsets can become inefficient on large tables.

---

## 3. Data Changes

New or deleted records may cause inconsistent results between page requests.

---

## 4. More Requests

Retrieving all records requires multiple API calls.

---

## 5. Strategy Selection

Different datasets may require different pagination techniques.

---

# Real-World Examples

## E-Commerce

```text
GET /products?page=2&limit=20
```

---

## Social Media

Load posts page by page as the user scrolls.

---

## Banking

Retrieve transaction history in pages.

---

## Admin Dashboards

Display users or orders in paginated tables.

---

# When to Use

Use Pagination when:

- APIs return large collections.
- Database tables contain many records.
- Performance is important.
- Clients browse data incrementally.

---

# When NOT to Use

Avoid Pagination when:

- Result sets are very small.
- The complete dataset is always required.
- The response size is negligible.

---

# Comparison

| Feature | No Pagination | Pagination |
|---|---|---|
| Response Size | Large | Small |
| Memory Usage | Higher | Lower |
| Database Performance | Lower | Higher |
| Network Usage | Higher | Lower |
| Scalability | Limited | High |

---

# Interview Questions

## 1. What is Pagination?

A technique that divides large datasets into smaller pages returned across multiple API requests.

---

## 2. Why is Pagination important?

It improves performance, reduces response size, and makes APIs more scalable.

---

## 3. What are the common pagination strategies?

- Offset Pagination
- Page-Based Pagination
- Cursor Pagination
- Keyset Pagination

---

## 4. Which pagination strategy is best for very large datasets?

Cursor Pagination or Keyset Pagination, because they avoid the performance issues of large offsets.

---

## 5. Why can Offset Pagination become slow?

The database must skip an increasing number of records before returning the requested page.

---

# Key Takeaways

- Pagination returns data in manageable chunks.
- It improves performance and scalability.
- Multiple pagination strategies exist for different use cases.
- Cursor and Keyset Pagination are preferred for very large datasets.
- Pagination is a standard practice in production APIs.

---

## Previous & Next

← Previous: [API Versioning](02-API-Versioning.md)

→ Next: [Filtering & Sorting](04-Filtering-and-Sorting.md)