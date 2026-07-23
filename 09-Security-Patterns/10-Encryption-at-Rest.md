# Encryption at Rest

## Introduction

Encryption at Rest is a security pattern that **protects data stored on persistent storage by encrypting it when it is not actively being transmitted or processed**.

If an attacker gains physical or unauthorized access to storage devices, encrypted data remains unreadable without the appropriate decryption keys.

Encryption at Rest answers the question:

> **"How do we protect stored data from unauthorized access?"**

The main goals of Encryption at Rest are:

- Protect stored data.
- Prevent unauthorized disclosure.
- Meet regulatory compliance requirements.
- Reduce the impact of storage compromise.

---

## Why was it Introduced?

Imagine a database server storing customer information.

Without encryption:

```text
Database Disk

↓

Customer Data

↓

Readable
```

If someone steals the disk or gains direct storage access, all data can be read.

With Encryption at Rest:

```text
Database Disk

↓

Encrypted Data

↓

Unreadable Without Key
```

Even if storage is compromised, the data remains protected.

---

## Architecture Diagram

```text
          Application

               |

         Read / Write

               |

               ▼

     Encryption Engine

               |

      Encrypt / Decrypt

               |

               ▼

      Encrypted Storage

               |

         Encryption Key

               |

               ▼

        Key Management
```

The application works with plaintext, while the storage layer contains only encrypted data.

---

## How It Works

The encryption flow:

```text
1. Application writes data.

2. Data is encrypted.

3. Encrypted data is stored.

4. Application requests data.

5. Stored data is decrypted.

6. Plaintext is returned to the application.
```

Example:

```text
Customer Name

↓

Encrypt

↓

Encrypted Data

↓

Store on Disk
```

---

# Common Encryption Algorithms

## 1. AES (Advanced Encryption Standard)

The most widely used symmetric encryption algorithm.

Common key sizes:

- AES-128
- AES-192
- AES-256

AES-256 is commonly used for enterprise-grade security.

---

## 2. ChaCha20

A modern symmetric encryption algorithm optimized for software performance.

---

# Where Encryption at Rest is Used

## Databases

Examples:

- MySQL
- PostgreSQL
- MongoDB
- DynamoDB

---

## Object Storage

Examples:

- Amazon S3
- Azure Blob Storage
- Google Cloud Storage

---

## Block Storage

Examples:

- Amazon EBS
- Azure Managed Disks
- Google Persistent Disk

---

## File Systems

Examples:

- BitLocker
- FileVault
- LUKS

---

# Key Management

Encryption is only as secure as the encryption keys.

Common approaches include:

- Hardware Security Modules (HSMs)
- Cloud Key Management Services (KMS)
- Dedicated secrets management systems

Keys should never be stored alongside encrypted data.

---

# Core Characteristics

## 1. Persistent Data Protection

Protects stored data regardless of the storage medium.

---

## 2. Transparent Operation

Many storage systems automatically encrypt and decrypt data.

---

## 3. Key-Based Security

Authorized access requires the appropriate encryption keys.

---

## 4. Compliance Support

Helps satisfy regulations such as GDPR, HIPAA, and PCI DSS.

---

## 5. Defense Against Physical Theft

Protects data if storage devices are lost or stolen.

---

# Advantages

## 1. Strong Data Protection

Data remains unreadable without the encryption key.

---

## 2. Compliance

Supports legal and regulatory security requirements.

---

## 3. Transparent to Applications

Many cloud providers implement encryption without application changes.

---

## 4. Reduced Risk

Limits exposure from compromised storage media.

---

## 5. Widely Supported

Most cloud services and databases provide built-in encryption at rest.

---

# Disadvantages

## 1. Key Management Complexity

Securely storing, rotating, and auditing keys requires careful planning.

---

## 2. Performance Overhead

Encryption and decryption introduce some computational cost, although hardware acceleration often minimizes the impact.

---

## 3. Lost Keys

If encryption keys are permanently lost, encrypted data may become unrecoverable.

---

## 4. Insider Threats

Authorized users with valid keys can still access the data.

---

## 5. Does Not Protect Data in Transit

Encryption at Rest protects stored data only. Data moving across networks requires Encryption in Transit.

---

# Real-World Examples

## Amazon S3 Server-Side Encryption (SSE)

Encrypts objects before storing them.

---

## Amazon RDS

Supports database encryption using AWS KMS.

---

## Azure Storage

Encrypts stored data by default.

---

## Google Cloud Storage

Encrypts all stored objects automatically.

---

# When to Use

Use Encryption at Rest when:

- Storing sensitive customer information.
- Managing financial or healthcare records.
- Protecting confidential business data.
- Using cloud storage services.
- Meeting compliance requirements.

---

# When NOT to Use

Encryption at Rest should generally be enabled whenever sensitive or valuable data is stored.

---

# Comparison

| Feature | Encryption at Rest | Encryption in Transit |
|---|---|---|
| Protects | Stored Data | Network Traffic |
| Typical Protocol | AES | TLS/SSL |
| Attack Prevented | Disk Theft | Network Interception |
| Applies To | Storage Systems | Communication Channels |
| Key Usage | Storage Encryption Keys | Session Keys |

---

# Interview Questions

## 1. What is Encryption at Rest?

The process of encrypting stored data so that it remains unreadable without the appropriate decryption key.

---

## 2. Why is Encryption at Rest important?

It protects stored data from unauthorized access if storage media is compromised.

---

## 3. Which encryption algorithm is commonly used?

AES, particularly AES-256.

---

## 4. Why is key management critical?

Because anyone with access to the encryption keys can decrypt the protected data.

---

## 5. Which cloud services support Encryption at Rest?

- Amazon S3
- Amazon RDS
- Azure Storage
- Google Cloud Storage
- Amazon DynamoDB

---

# Key Takeaways

- Encryption at Rest protects stored data from unauthorized access.
- AES is the most commonly used encryption algorithm.
- Secure key management is as important as encryption itself.
- Most modern cloud storage services support encryption by default.
- Encryption at Rest complements Encryption in Transit to provide end-to-end data protection.

---

## Previous & Next

← Previous: [Attribute-Based Access Control (ABAC)](09-Attribute-Based-Access-Control-ABAC.md)

→ Next: [Encryption in Transit](11-Encryption-in-Transit.md)