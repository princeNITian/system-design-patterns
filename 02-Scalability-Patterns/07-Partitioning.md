# Database Partitioning

## Introduction

Database Partitioning is a scalability pattern that divides a large database table into smaller, manageable pieces called **partitions**.

Unlike sharding, where data is distributed across multiple database instances, partitioning usually happens **within a single database system**.

The main goals of database partitioning are:

- Improve query performance.
- Improve data management.
- Reduce query scanning overhead.
- Handle large datasets efficiently.

---

## Why was it Introduced?

In a traditional database, all records are stored in a single large table.

Example:

```text
              Application

                   |

                   ▼

             User Table

      ┌────────────────────┐
      │ Millions of Rows   │
      │                    │
      └────────────────────┘
```

As tables grow:

- Queries become slower.
- Indexes become larger.
- Maintenance becomes difficult.
- Data operations become expensive.

Partitioning was introduced to divide large tables into smaller logical sections.

---

## Architecture Diagram

### Before Partitioning

```text
              User Table

 ┌──────────────────────────────┐
 │                              │
 │  500 Million Records         │
 │                              │
 └──────────────────────────────┘
```

---

### After Partitioning

```text
                 User Table

        ┌────────┬────────┬────────┐

        ▼        ▼        ▼        ▼

   Partition 1 Partition 2 Partition 3

    Jan Data   Feb Data   Mar Data
```

The database manages partitions internally.

---

## How It Works

The database uses a partition key to decide where data should be stored.

Example:

```text
Orders Table


Order Date

     |

Partition Rule

     |

-----------------

Jan Orders

Feb Orders

Mar Orders
```

Query example:

```sql
SELECT *
FROM Orders
WHERE order_date = '2026-01-10';
```

The database only scans the relevant partition instead of the entire table.

---

# Types of Partitioning

## 1. Range Partitioning

Data is divided based on value ranges.

Example:

```text
Orders Table


Partition 1:

January - March


Partition 2:

April - June


Partition 3:

July - September
```

Advantages:

- Good for time-series data.
- Efficient range queries.

Disadvantages:

- Uneven distribution possible.

---

## 2. Hash Partitioning

A hash function determines the partition.

Example:

```text
Hash(User_ID)

        |

        ▼

Partition Selection
```

Advantages:

- Even data distribution.
- Avoids hotspots.

Disadvantages:

- Range queries become harder.

---

## 3. List Partitioning

Data is divided based on specific categories.

Example:

```text
Customers


Partition 1:

India


Partition 2:

USA


Partition 3:

Europe
```

Advantages:

- Simple for categorical data.

Disadvantages:

- Requires known categories.

---

## 4. Composite Partitioning

Combination of multiple partitioning methods.

Example:

```text
Range Partition

        +

Hash Partition
```

Example:

```text
Year

 |

Region

 |

Partition
```

---

# Partitioning vs Sharding

Although both divide data, they work differently.

| Feature | Partitioning | Sharding |
|---|---|---|
| Scope | Single database | Multiple databases |
| Management | Database handles it | Application often handles it |
| Purpose | Organize large tables | Scale database horizontally |
| Complexity | Lower | Higher |
| Infrastructure | Same server/cluster | Multiple servers |

---

# Core Characteristics

## 1. Logical Data Separation

Large tables are divided into smaller sections.

---

## 2. Query Optimization

Database scans only required partitions.

---

## 3. Improved Maintenance

Operations like:

- Backup.
- Archive.
- Delete.

can be performed on individual partitions.

---

## 4. Better Storage Management

Large datasets can be managed efficiently.

---

## 5. Transparent Application Usage

Applications usually do not need to know about partitions.

---

# Advantages

## 1. Faster Queries

Queries scan smaller amounts of data.

Example:

```text
Without Partitioning:

Scan 500M rows


With Partitioning:

Scan 10M rows
```

---

## 2. Easier Data Management

Large tables become easier to maintain.

---

## 3. Improved Index Performance

Indexes are smaller and faster.

---

## 4. Efficient Data Archiving

Old data can be moved or deleted easily.

---

## 5. Better Resource Utilization

Database resources are used more efficiently.

---

# Disadvantages

## 1. Partition Design Complexity

Choosing the wrong partition key impacts performance.

---

## 2. Uneven Data Distribution

Some partitions may become larger than others.

---

## 3. Cross-Partition Queries

Queries across multiple partitions may be slower.

---

## 4. Increased Database Management

Requires careful monitoring.

---

## 5. Not Suitable for Small Tables

Additional complexity provides little benefit.

---

# Real-World Examples

## E-Commerce Systems

Orders are partitioned by date.

Example:

```text
Orders

2025 Partition

2026 Partition

2027 Partition
```

---

## Logging Systems

Logs are partitioned by:

- Date.
- Region.
- Application.

---

## Financial Systems

Transactions are partitioned by:

- Time period.
- Customer region.

---

# When to Use

Use database partitioning when:

- Tables contain millions or billions of records.
- Query performance decreases with table size.
- Data has natural grouping.
- Large historical datasets exist.
- Maintenance operations are frequent.

---

# When NOT to Use

Avoid partitioning when:

- Tables are small.
- Queries already perform well.
- Application complexity is more important.
- Data has no logical partition key.

---

# Comparison

| Feature | Normal Table | Partitioned Table |
|---|---|---|
| Data Organization | Single structure | Multiple partitions |
| Query Performance | Decreases with size | Improved |
| Maintenance | Difficult | Easier |
| Complexity | Low | Higher |
| Large Dataset Support | Limited | Better |

---

# Interview Questions

## 1. What is Database Partitioning?

Database partitioning divides a large table into smaller logical sections to improve performance and manageability.

---

## 2. Difference between Partitioning and Sharding?

Partitioning divides data within one database system.

Sharding distributes data across multiple database servers.

---

## 3. What are common partitioning strategies?

Common strategies:

- Range Partitioning.
- Hash Partitioning.
- List Partitioning.
- Composite Partitioning.

---

## 4. Why is partitioning useful for large tables?

Because queries can scan only relevant partitions instead of the entire dataset.

---

## 5. What happens if partitioning is poorly designed?

It can cause:

- Uneven data distribution.
- Slow queries.
- Maintenance problems.

---

# Key Takeaways

- Partitioning divides large tables into smaller sections.
- It improves query performance and data management.
- Common strategies include range, hash, and list partitioning.
- Partitioning usually happens inside a database.
- Sharding and partitioning solve different scalability problems.
- Proper partition design is critical for performance.

---

## Previous & Next

← Previous: [Database Sharding](06-Database-Sharding.md)

→ Next: [Replication](08-Replication.md)