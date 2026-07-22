# Data Warehouse

## Introduction

A Data Warehouse is a data management pattern used to **store processed, structured, and integrated data** from multiple sources for reporting, analytics, and business intelligence (BI).

Unlike a Data Lake, which stores raw data, a Data Warehouse stores **cleaned, transformed, and organized data** optimized for analytical queries.

The main goals of the Data Warehouse pattern are:

- Support business intelligence and reporting.
- Enable fast analytical queries.
- Integrate data from multiple sources.
- Provide a single source of truth for decision-making.

---

## Why was it Introduced?

Operational databases are designed for transaction processing.

Example:

```text
Place Order

Update Inventory

Process Payment
```

Running complex analytical queries on these databases can:

- Slow down transactions.
- Increase database load.
- Impact application performance.

A Data Warehouse separates analytical workloads from transactional systems.

---

## Architecture Diagram

```text
          Data Sources

   /        |        |        \

  ▼         ▼        ▼         ▼

 Apps   Databases   CRM      ERP

                |

                ▼

         ETL / ELT Pipeline

                |

                ▼

         Data Warehouse

                |

      ---------------------

      |         |         |

      ▼         ▼         ▼

 Dashboards  Reports   Analytics
```

The Data Warehouse stores processed data ready for analysis.

---

## How It Works

The communication flow:

```text
1. Data is collected from multiple sources.

2. Data is cleaned and transformed.

3. Processed data is loaded into the Data Warehouse.

4. Business users query the warehouse.

5. Dashboards and reports are generated.
```

Example:

```text
Sales Database

        |

ETL Process

        |

Data Warehouse

        |

Sales Dashboard
```

---

# Core Components

## 1. Data Sources

Provide operational data.

Examples:

- Applications
- Databases
- CRM systems
- ERP systems

---

## 2. ETL / ELT Pipeline

Extracts, transforms, and loads data into the warehouse.

---

## 3. Data Warehouse

Stores structured and optimized analytical data.

---

## 4. BI Tools

Query the warehouse to create reports and dashboards.

Examples:

- Power BI
- Tableau
- Looker

---

# Core Characteristics

## 1. Structured Data

Stores cleaned and organized datasets.

---

## 2. Schema-on-Write

Data is transformed before it is stored.

---

## 3. Read Optimization

Designed for analytical queries rather than transactions.

---

## 4. Historical Data

Maintains historical records for trend analysis.

---

## 5. Centralized Analytics

Combines data from multiple business systems.

---

# Advantages

## 1. Fast Analytical Queries

Optimized for reporting and aggregation.

---

## 2. Better Business Insights

Provides a unified view of enterprise data.

---

## 3. Historical Analysis

Supports long-term trend analysis.

---

## 4. Improved Data Quality

Data is cleaned and standardized before storage.

---

## 5. Supports Business Intelligence

Enables dashboards, KPIs, and executive reporting.

---

# Disadvantages

## 1. Data Latency

Data is refreshed periodically rather than in real time.

---

## 2. Higher Storage Costs

Processed and optimized data may require additional storage.

---

## 3. ETL Complexity

Building and maintaining ETL/ELT pipelines can be challenging.

---

## 4. Limited Transaction Support

Not designed for OLTP workloads.

---

## 5. Operational Overhead

Requires governance, monitoring, and maintenance.

---

# Real-World Examples

## E-Commerce

Analyze:

- Sales performance.
- Customer behavior.
- Revenue trends.

---

## Banking

Generate:

- Financial reports.
- Risk analysis.
- Regulatory compliance reports.

---

## Retail

Track:

- Inventory performance.
- Regional sales.
- Seasonal demand.

---

## Healthcare

Analyze:

- Patient outcomes.
- Hospital utilization.
- Treatment trends.

---

# When to Use

Use a Data Warehouse when:

- Building business intelligence solutions.
- Running complex analytical queries.
- Combining data from multiple systems.
- Historical reporting is important.

---

# When NOT to Use

Avoid a Data Warehouse when:

- Building transactional applications.
- Storing raw or unstructured data.
- Low-latency operational workloads are the primary requirement.

---

# Comparison

| Feature | Data Lake | Data Warehouse |
|---|---|---|
| Data Type | Structured, Semi-structured, Unstructured | Primarily Structured |
| Data Format | Raw | Processed |
| Schema | Schema-on-Read | Schema-on-Write |
| Primary Use | Analytics, AI, ML | Business Intelligence & Reporting |
| Query Performance | Moderate | High |
| Storage Cost | Lower | Higher |

---

# Interview Questions

## 1. What is a Data Warehouse?

A centralized repository that stores processed and structured data for reporting and analytics.

---

## 2. How is a Data Warehouse different from a Data Lake?

A Data Warehouse stores processed, structured data, while a Data Lake stores raw data in its original format.

---

## 3. What is Schema-on-Write?

Data is transformed and validated before being stored in the warehouse.

---

## 4. What is ETL?

ETL stands for **Extract, Transform, and Load**, the process of preparing data before loading it into the Data Warehouse.

---

## 5. Where are Data Warehouses commonly used?

- Business intelligence.
- Executive dashboards.
- Financial reporting.
- Enterprise analytics.
- Historical trend analysis.

---

# Key Takeaways

- A Data Warehouse stores processed and structured data.
- It is optimized for reporting and analytical queries.
- Data is transformed before storage using ETL or ELT pipelines.
- It provides a centralized source of truth for business intelligence.
- It complements Data Lakes by serving clean, analysis-ready data.

---

## Previous & Next

← Previous: [Data Lake](09-Data-Lake.md)

→ Next Module: [05-Resilience-Patterns](../05-Resilience-Patterns/README.md)