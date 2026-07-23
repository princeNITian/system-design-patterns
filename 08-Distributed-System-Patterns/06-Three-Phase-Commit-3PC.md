# Three-Phase Commit (3PC)

## Introduction

Three-Phase Commit (3PC) is a distributed transaction protocol that **extends Two-Phase Commit (2PC) by introducing an additional coordination phase to reduce blocking during failures**.

Unlike 2PC, where participants may wait indefinitely if the coordinator fails, 3PC attempts to ensure that participants can eventually make progress without remaining blocked forever.

The three phases are:

1. **CanCommit**
2. **PreCommit**
3. **DoCommit**

The main goals of Three-Phase Commit are:

- Reduce blocking.
- Improve fault tolerance.
- Maintain atomic distributed transactions.
- Increase coordinator failure resilience.

---

## Why was it Introduced?

Two-Phase Commit has a major limitation.

```text
Coordinator

↓

Prepare

↓

Participants Vote YES

↓

Coordinator Fails
```

Participants have voted **YES** but do not know whether to commit or abort.

They must wait indefinitely until the coordinator recovers.

3PC introduces an intermediate **PreCommit** phase so participants have enough information to make progress if failures occur.

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

The coordinator manages all three phases of the protocol.

---

# Phase 1 — CanCommit

The coordinator asks whether participants can commit.

```text
Coordinator

      |

CanCommit?

      |

-----------------------

|         |          |

▼         ▼          ▼

Node A  Node B   Node C

 YES      YES      YES
```

Participants verify that they are able to execute the transaction but do not perform the commit.

---

# Phase 2 — PreCommit

If every participant responds **YES**, the coordinator sends a **PreCommit** message.

```text
Coordinator

      |

PreCommit

      |

-----------------------

|         |          |

▼         ▼          ▼

Node A  Node B   Node C

 Ready    Ready    Ready
```

Participants:

- Perform the transaction.
- Write changes to durable storage.
- Enter a prepared state.
- Acknowledge readiness.

---

# Phase 3 — DoCommit

After receiving acknowledgments, the coordinator instructs participants to commit.

```text
Coordinator

      |

DoCommit

      |

-----------------------

|         |          |

▼         ▼          ▼

Node A  Node B   Node C

Commit   Commit   Commit
```

All participants permanently commit the transaction.

---

## Abort Scenario

If any participant rejects the transaction during the CanCommit phase:

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

The transaction is cancelled for all participants.

---

## How It Works

The execution flow:

```text
1. Coordinator sends CanCommit.

2. Participants respond YES or NO.

3. Coordinator sends PreCommit.

4. Participants prepare locally.

5. Coordinator sends DoCommit.

6. Participants commit permanently.
```

---

# Core Characteristics

## 1. Three Communication Phases

The protocol introduces an additional PreCommit phase between voting and committing.

---

## 2. Reduced Blocking

Participants are less likely to remain indefinitely blocked during coordinator failures.

---

## 3. Coordinator-Based

A coordinator manages the entire protocol.

---

## 4. Timeout Mechanisms

Participants use timeouts to determine recovery actions when communication is lost.

---

## 5. Atomic Transactions

All participants eventually reach the same transaction outcome.

---

# Advantages

## 1. Less Blocking than 2PC

Participants can often recover without waiting forever.

---

## 2. Better Failure Handling

Additional protocol state improves recovery decisions.

---

## 3. Strong Consistency

All participants reach a consistent final state.

---

## 4. Improved Fault Tolerance

Handles certain coordinator failures more gracefully than 2PC.

---

## 5. Distributed Coordination

Supports atomic transactions across multiple participants.

---

# Disadvantages

## 1. More Complex Protocol

The additional phase increases implementation complexity.

---

## 2. Higher Communication Overhead

Three phases require more network messages than 2PC.

---

## 3. Network Assumptions

3PC assumes bounded communication delays and reliable timeout detection, which may not hold in real-world asynchronous networks.

---

## 4. Limited Adoption

Modern distributed systems rarely use 3PC in production.

---

## 5. Does Not Eliminate All Failure Scenarios

Certain network partitions and failures can still prevent safe progress.

---

# Real-World Examples

Unlike 2PC, Three-Phase Commit is **primarily an academic protocol** and is rarely implemented in production systems.

It is mainly studied to understand the evolution of distributed transaction protocols.

---

# When to Use

Use Three-Phase Commit when:

- Studying distributed transaction protocols.
- Understanding improvements over 2PC.
- Designing systems with synchronous network assumptions.

---

# When NOT to Use

Avoid Three-Phase Commit when:

- Building modern cloud-native applications.
- Operating over asynchronous or unreliable networks.
- Saga Pattern or consensus-based approaches are more appropriate.

---

# Comparison

| Feature | Two-Phase Commit | Three-Phase Commit |
|---|---|---|
| Communication Phases | 2 | 3 |
| Blocking | Yes | Reduced |
| Coordinator | Required | Required |
| Communication Overhead | Lower | Higher |
| Production Usage | Common | Rare |

---

# Interview Questions

## 1. What is Three-Phase Commit?

A distributed transaction protocol that extends Two-Phase Commit by adding a PreCommit phase to reduce blocking.

---

## 2. What are the three phases?

1. CanCommit
2. PreCommit
3. DoCommit

---

## 3. Why was Three-Phase Commit introduced?

To reduce the blocking problem present in Two-Phase Commit during coordinator failures.

---

## 4. Why is 3PC rarely used today?

Because it relies on assumptions about network timing that are difficult to guarantee in real distributed systems, and alternative approaches such as Saga or consensus-based systems are often preferred.

---

## 5. What is the biggest difference between 2PC and 3PC?

3PC introduces a PreCommit phase and timeout-based recovery to reduce blocking.

---

# Key Takeaways

- Three-Phase Commit extends Two-Phase Commit with an additional coordination phase.
- It reduces blocking but increases protocol complexity.
- It assumes bounded network delays and timeout-based failure detection.
- Modern distributed systems rarely use 3PC in production.
- Understanding 3PC helps explain the evolution of distributed transaction protocols.

---

## Previous & Next

← Previous: [Two-Phase Commit (2PC)](05-Two-Phase-Commit-2PC.md)

→ Next: [Gossip Protocol](07-Gossip-Protocol.md)