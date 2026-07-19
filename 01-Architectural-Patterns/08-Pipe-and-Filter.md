# Pipe and Filter Architecture

## Introduction

Pipe and Filter Architecture is an architectural style where data processing is divided into a sequence of independent processing steps called **filters**.

Each filter performs a specific transformation on data and passes the result to the next filter through a communication channel called a **pipe**.

This architecture is commonly used for data processing pipelines, compilers, ETL systems, and stream processing applications.

---

## Why was it Introduced?

Many applications require processing data through multiple stages.

A tightly coupled implementation makes the system difficult to:

* Modify.
* Test.
* Reuse.
* Scale.

Example:

```text
Read File
   |
Parse Data
   |
Validate Data
   |
Transform Data
   |
Store Result
```

If all processing logic exists in one component, changing one step affects the entire system.

Pipe and Filter Architecture was introduced to separate each processing stage into independent components.

---

## Architecture Diagram

```text
              Input Data

                  |
                  ▼

              Filter 1
            (Extraction)

                  |
                  ▼

              Pipe

                  |
                  ▼

              Filter 2
           (Transformation)

                  |
                  ▼

              Pipe

                  |
                  ▼

              Filter 3
             (Loading)

                  |
                  ▼

              Output Data
```

Each filter processes data independently and passes the result through pipes.

---

## How It Works

The flow follows these steps:

```text
1. Data enters the first filter.

2. Filter processes the data.

3. Processed data moves through a pipe.

4. The next filter receives the data.

5. The final output is produced.
```

Example: Image Processing Pipeline

```text
Original Image

      |

Resize Filter

      |

Compression Filter

      |

Watermark Filter

      |

Final Image
```

Each stage has a single responsibility.

---

## Core Characteristics

### 1. Independent Filters

Each filter performs one specific transformation.

Examples:

* Parser
* Validator
* Transformer
* Formatter

---

### 2. Data Flow Through Pipes

Pipes transfer data between filters.

They can be:

* In-memory communication.
* Files.
* Message queues.
* Streams.

---

### 3. Reusable Components

Filters can be reused in different pipelines.

Example:

A validation filter can be used by multiple data processing workflows.

---

### 4. Sequential Processing

Filters are arranged as a processing chain.

```text
Filter A → Filter B → Filter C
```

---

### 5. Loose Coupling

Filters do not need to know the internal implementation of other filters.

They only understand the input and output format.

---

## Advantages

### 1. Easy Maintenance

Each processing stage can be modified independently.

---

### 2. Reusability

Existing filters can be reused across different pipelines.

---

### 3. Parallel Processing

Independent filters can execute concurrently.

---

### 4. Better Testing

Each filter can be tested separately.

---

### 5. Flexible Pipelines

Filters can be added, removed, or rearranged easily.

---

## Disadvantages

### 1. Data Transformation Overhead

Passing data between multiple filters can introduce latency.

---

### 2. Complex Error Handling

Handling failures across multiple processing stages can become difficult.

---

### 3. Data Format Dependency

Filters must agree on input and output formats.

---

### 4. Not Suitable for All Applications

Applications with complex business workflows may not fit this model.

---

## Real-World Examples

### Compiler Design

A compiler uses multiple processing stages:

```text
Source Code

↓

Lexical Analysis

↓

Parsing

↓

Optimization

↓

Code Generation
```

---

### Data Processing Pipelines

Examples:

* ETL pipelines
* Data cleaning systems
* Analytics workflows

---

### Image Processing

Processing steps:

```text
Upload Image

↓

Resize

↓

Compress

↓

Apply Filters

↓

Store
```

---

### Stream Processing Systems

Platforms like Kafka Streams and Apache Flink commonly implement pipeline-style processing.

---

## When to Use

Use Pipe and Filter Architecture when:

* Data processing happens in multiple stages.
* Each stage has a clear responsibility.
* Processing steps need reuse.
* Pipelines may change frequently.
* Parallel processing is beneficial.

---

## When NOT to Use

Avoid this architecture when:

* Business logic is highly interconnected.
* Processing requires frequent communication between stages.
* Strong transactional consistency is required.
* The workflow does not naturally form a pipeline.

---

## Comparison

| Feature       | Pipe and Filter     | Layered Architecture           |
| ------------- | ------------------- | ------------------------------ |
| Main Goal     | Data transformation | Separation of responsibilities |
| Structure     | Processing pipeline | Application layers             |
| Communication | Data flow           | Layer calls                    |
| Coupling      | Low                 | Moderate                       |
| Best For      | Data processing     | Business applications          |

---

## Interview Questions

### 1. What is Pipe and Filter Architecture?

It is an architecture where data processing is divided into independent stages called filters connected through pipes.

---

### 2. What is a filter?

A filter is a component responsible for one specific transformation or processing operation.

---

### 3. What is a pipe?

A pipe is a communication channel that transfers output from one filter to the next filter.

---

### 4. Where is Pipe and Filter Architecture used?

Common examples:

* Compilers.
* ETL pipelines.
* Data processing systems.
* Stream processing applications.

---

### 5. What are the benefits of this architecture?

* Modularity.
* Reusability.
* Easy testing.
* Flexible pipeline design.

---

## Key Takeaways

* Pipe and Filter divides processing into independent stages.
* Filters perform specific transformations.
* Pipes connect filters and transfer data.
* The architecture is highly suitable for data processing workflows.
* It improves modularity and reusability.
* It is less suitable for tightly coupled business workflows.

---

## Previous & Next

← Previous: [Serverless Architecture](07-Serverless-Architecture.md)

→ Next: [Hexagonal Architecture](09-Hexagonal-Architecture.md)
