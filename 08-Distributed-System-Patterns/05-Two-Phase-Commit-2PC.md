# Two-Phase Commit (2PC)

## Introduction

Two-Phase Commit (2PC) is a distributed transaction protocol that **ensures all participating nodes either commit or abort a transaction together**.

It provides **atomicity** across multiple databases or services by coordinating every participant through two distinct phases:

1. **Prepare Phase**
2. **Commit Phase**

The main goals of Two-Phase Commit are:

- Guarantee atomic distributed transactions.
- Prevent partial commits.
- Maintain strong consistency.
- Coordinate multiple participants.

---

## Why was it Introduced?

Consider a banking transaction.

```text
Withdraw Money

↓

Deposit Money
```

Suppose:

```text
Account A

Withdraw ✓

↓

Account B

Deposit ✗
```

Money disappears because only one operation completed.

2PC prevents this situation by ensuring that **either every participant commits or every participant aborts**.

---

## Architecture Diagram

```text
                 Client

                    |

                    ▼

      Transaction Coordinator

          /       |       \

         ▼        ▼        ▼

      Node A   Node B   Node C
```

The coordinator manages the transaction across all participating nodes.

---

# Phase 1 — Prepare Phase

The coordinator asks every participant whether it is ready to commit.

```text
Coordinator

      |

Prepare?

      |

-----------------------

|         |          |

▼         ▼          ▼

Node A  Node B   Node C

 Ready    Ready    Ready
```

Each participant:

- Executes the transaction locally.
- Does **not** commit.
- Writes changes to durable storage.
- Responds with **YES** or **NO**.

---

# Phase 2 — Commit Phase

If every participant votes **YES**, the coordinator sends a **COMMIT** message.

```text
Coordinator

      |

Commit

      |

-----------------------

|         |          |

▼         ▼          ▼

Node A  Node B   Node C

Commit   Commit   Commit
```

Every participant permanently commits the transaction.

---

## Abort Scenario

If any participant votes **NO**, the coordinator instructs every participant to abort.

```text
Coordinator

      |

Abort

      |

-----------------------

|         |          |

▼         ▼          ▼

Node A  Node B   Node C

Abort    Abort    Abort
```

No participant commits the transaction.

---

## How It Works

The execution flow:

```text
1. Client starts transaction.

2. Coordinator sends PREPARE.

3. Participants vote YES or NO.

4. If all vote YES:
      Send COMMIT.

5. Otherwise:
      Send ABORT.

6. Participants complete the transaction.
```

---

# Core Characteristics

## 1. Two Distinct Phases

The protocol consists of a prepare phase followed by a commit or abort phase.

---

## 2. Atomicity

All participants either commit together or abort together.

---

## 3. Coordinator-Based

A single coordinator manages the protocol.

---

## 4. Durable Logging

Participants persist transaction state before voting.

---

## 5. Strong Consistency

Every participant reaches the same final outcome.

---

# Advantages

## 1. Strong Atomicity

Prevents partial transaction completion.

---

## 2. Consistent State

All participating systems remain synchronized.

---

## 3. Reliable Recovery

Durable logs support recovery after failures.

---

## 4. Widely Understood

2PC is a foundational distributed transaction protocol.

---

## 5. Database Support

Many relational databases support two-phase commit.

---

# Disadvantages

## 1. Blocking Protocol

If the coordinator fails after participants vote YES but before sending COMMIT or ABORT, participants must wait.

---

## 2. Single Point of Failure

The coordinator is critical to transaction completion.

---

## 3. Increased Latency

Two communication phases are required.

---

## 4. Reduced Scalability

Coordinating many participants increases overhead.

---

## 5. Lock Contention

Resources may remain locked until the transaction finishes.

---

# Real-World Examples

## Distributed SQL Databases

Coordinate transactions across multiple database nodes.

---

## Banking Systems

Maintain consistency across multiple accounts.

---

## Enterprise Resource Planning (ERP)

Synchronize updates across financial and inventory systems.

---

## XA Transactions

Use the XA protocol to coordinate distributed transactions across multiple resource managers.

---

# When to Use

Use Two-Phase Commit when:

- Strong consistency is mandatory.
- Partial commits cannot be tolerated.
- Multiple databases participate in a transaction.
- ACID guarantees are required.

---

# When NOT to Use

Avoid Two-Phase Commit when:

- High throughput is more important than strict consistency.
- Temporary inconsistency is acceptable.
- Long-running workflows span multiple services.
- Eventual consistency or Saga is a better fit.

---

# Comparison

| Feature | Local Transaction | Two-Phase Commit |
|---|---|---|
| Scope | Single Database | Multiple Participants |
| Atomicity | Yes | Yes |
| Coordinator | Database | External Coordinator |
| Blocking | No | Yes |
| Complexity | Low | High |

---

# Interview Questions

## 1. What is Two-Phase Commit?

A distributed transaction protocol that guarantees all participants either commit or abort together.

---

## 2. What are the two phases?

1. Prepare Phase
2. Commit (or Abort) Phase

---

## 3. Why is 2PC considered a blocking protocol?

Participants may wait indefinitely if the coordinator fails after the prepare phase.

---

## 4. What is the coordinator's responsibility?

To collect participant votes and decide whether to commit or abort the transaction.

---

## 5. Where is Two-Phase Commit commonly used?

- Distributed SQL databases
- Banking systems
- XA transaction managers
- Enterprise applications

---

# Key Takeaways

- Two-Phase Commit guarantees atomic distributed transactions.
- Every participant either commits or aborts together.
- The protocol consists of a prepare phase and a commit/abort phase.
- It provides strong consistency but introduces blocking and coordination overhead.
- 2PC is best suited for systems that require strict transactional guarantees.

---

## Previous & Next

← Previous: [Distributed Transactions](04-Distributed-Transactions.md)

→ Next: [Three-Phase Commit (3PC)](06-Three-Phase-Commit-3PC.md)