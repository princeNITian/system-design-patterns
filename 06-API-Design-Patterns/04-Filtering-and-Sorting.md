# Filtering & Sorting

## Introduction

Filtering & Sorting is an API design pattern that **allows clients to retrieve only the data they need and control the order in which it is returned**.

Instead of returning every resource in a fixed order, APIs expose query parameters that enable clients to narrow results and sort them based on specific fields.

The main goals of Filtering & Sorting are:

- Reduce unnecessary data transfer.
- Improve API flexibility.
- Enhance query performance.
- Provide a better user experience.

---

## Why was it Introduced?

Consider an API:

```text
GET /products
```

If the database contains millions of products, clients may only want:

- Mobile phones.
- Products under $500.
- Items sorted by price.
- Recently added products.

Returning every product wastes bandwidth and processing time.

Filtering and sorting solve this problem.

---

## Architecture Diagram

```text
            Client

               |

               ▼

GET /products?category=mobile&sort=price

               |

               ▼

            REST API

               |

               ▼

      Apply Filters & Sorting

               |

               ▼

           Database

               |

               ▼

     Filtered Response
```

Only matching records are returned in the requested order.

---

## How It Works

The communication flow:

```text
1. Client sends filter and sort parameters.

2. API validates the parameters.

3. Database applies filtering.

4. Database sorts the results.

5. API returns the filtered dataset.
```

Example:

```text
GET /products?category=laptop&sort=price
```

Returns only laptops ordered by price.

---

# Filtering

Filtering selects only the records that satisfy specific conditions.

Examples:

```text
GET /products?category=mobile

GET /orders?status=completed

GET /users?country=India
```

Multiple filters can be combined.

Example:

```text
GET /products?category=mobile&brand=Apple
```

---

# Sorting

Sorting controls the order of the returned data.

Ascending order:

```text
GET /products?sort=price
```

Descending order:

```text
GET /products?sort=-price
```

Multiple sort fields:

```text
GET /orders?sort=-createdAt,total
```

---

# Core Characteristics

## 1. Flexible Queries

Clients retrieve only the data they need.

---

## 2. Reduced Response Size

Filtering removes unnecessary records.

---

## 3. Custom Ordering

Clients choose how results are sorted.

---

## 4. Better Performance

Smaller result sets reduce processing time and bandwidth usage.

---

## 5. Works with Pagination

Filtering and sorting are commonly combined with pagination.

---

# Advantages

## 1. Improved User Experience

Clients receive relevant data.

---

## 2. Reduced Network Traffic

Only matching records are returned.

---

## 3. Better Performance

Smaller datasets are processed and transferred.

---

## 4. Flexible API Design

One endpoint supports many query combinations.

---

## 5. Scalable

Efficiently handles large datasets when supported by proper indexing.

---

# Disadvantages

## 1. More Complex Queries

Multiple filters increase query complexity.

---

## 2. Validation Required

APIs must validate filter and sort fields.

---

## 3. Performance Risks

Sorting or filtering on non-indexed fields can be slow.

---

## 4. Increased Testing

Many combinations of filters and sort orders must be verified.

---

## 5. Documentation Overhead

Supported query parameters should be clearly documented.

---

# Real-World Examples

## E-Commerce

```text
GET /products?category=mobile&brand=Samsung&sort=-price
```

---

## Banking

```text
GET /transactions?type=credit&sort=-date
```

---

## Food Delivery

```text
GET /restaurants?city=Delhi&sort=rating
```

---

## Social Media

```text
GET /posts?author=101&sort=-createdAt
```

---

# When to Use

Use Filtering & Sorting when:

- APIs return collections of data.
- Clients require customized queries.
- Large datasets need to be narrowed down.
- User interfaces provide search and sorting options.

---

# When NOT to Use

Avoid Filtering & Sorting when:

- APIs return a single resource.
- Result sets are very small.
- Query customization is unnecessary.

---

# Comparison

| Feature | Without Filtering & Sorting | With Filtering & Sorting |
|---|---|---|
| Response Size | Larger | Smaller |
| Query Flexibility | Limited | High |
| Performance | Lower | Higher |
| User Experience | Fixed Results | Customized Results |
| Scalability | Moderate | High |

---

# Interview Questions

## 1. What is Filtering in an API?

Filtering allows clients to retrieve only records that match specific conditions.

---

## 2. What is Sorting in an API?

Sorting determines the order in which records are returned.

---

## 3. Why are Filtering and Sorting important?

They reduce unnecessary data transfer and improve API flexibility.

---

## 4. Can Filtering and Sorting be used together?

Yes.

They are commonly combined with pagination in production APIs.

---

## 5. Why should filtered and sorted fields be indexed?

Indexes improve query performance by reducing the amount of data the database must scan.

---

# Key Takeaways

- Filtering returns only relevant records.
- Sorting controls the order of results.
- Together they improve API flexibility and performance.
- Proper indexing is essential for efficient queries.
- They are commonly combined with pagination in production systems.

---

## Previous & Next

← Previous: [Pagination](03-Pagination.md)

→ Next: [Idempotency](05-Idempotency.md)