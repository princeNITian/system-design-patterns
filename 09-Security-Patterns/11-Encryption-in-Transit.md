# Encryption in Transit

## Introduction

Encryption in Transit is a security pattern that **protects data while it is being transmitted between clients, servers, services, or data centers**.

It ensures that data cannot be read or modified by unauthorized parties while traveling across a network.

Encryption in Transit answers the question:

> **"How do we securely transmit data over a network?"**

The main goals of Encryption in Transit are:

- Protect data confidentiality.
- Prevent eavesdropping.
- Prevent data tampering.
- Verify the identity of communicating parties.

---

## Why was it Introduced?

Imagine a user logging into an application over the internet.

Without encryption:

```text
User

↓

Username

Password

↓

Internet

↓

Server
```

Anyone intercepting the network traffic can read the credentials.

With Encryption in Transit:

```text
User

↓

Encrypted Traffic

↓

Internet

↓

Server
```

Even if traffic is intercepted, the data remains unreadable.

---

## Architecture Diagram

```text
          Client

             |

      TLS Handshake

             |

             ▼

      Secure Channel

             |

      Encrypted Traffic

             |

             ▼

          Server
```

A secure communication channel is established before sensitive data is exchanged.

---

## How It Works

The communication flow:

```text
1. Client connects to the server.

2. TLS handshake begins.

3. Server presents its digital certificate.

4. Client verifies the certificate.

5. Session keys are negotiated.

6. Secure encrypted channel is established.

7. All application data is encrypted.
```

---

# TLS Handshake (Simplified)

```text
Client

↓

Hello

↓

Server

↓

Certificate

↓

Key Exchange

↓

Shared Session Key

↓

Encrypted Communication
```

The session key is then used for efficient symmetric encryption during the connection.

---

# Common Protocols

## 1. TLS (Transport Layer Security)

The modern standard for secure network communication.

Used by:

- HTTPS
- SMTP
- IMAP
- POP3
- MQTT
- gRPC

---

## 2. HTTPS

HTTP secured using TLS.

Example:

```text
https://example.com
```

---

## 3. SSH

Encrypts remote terminal sessions and secure file transfers.

---

## 4. VPN Protocols

Secure communication between private networks.

Examples:

- WireGuard
- IPsec
- OpenVPN

---

# Digital Certificates

TLS relies on digital certificates issued by trusted Certificate Authorities (CAs).

A certificate contains information such as:

- Domain name
- Public key
- Issuer
- Validity period
- Digital signature

The client verifies the certificate before establishing trust.

---

# Core Characteristics

## 1. Confidentiality

Encrypted communication prevents unauthorized reading of transmitted data.

---

## 2. Integrity

Detects if transmitted data has been modified.

---

## 3. Authentication

Certificates verify the identity of servers (and optionally clients).

---

## 4. Session Keys

Temporary symmetric keys provide efficient encryption after the handshake.

---

## 5. Automatic Protection

Applications using HTTPS benefit from transparent transport encryption.

---

# Advantages

## 1. Prevents Eavesdropping

Protects sensitive information transmitted over networks.

---

## 2. Prevents Tampering

Ensures transmitted data has not been altered.

---

## 3. Authenticates Servers

Clients can verify they are communicating with the intended server.

---

## 4. Industry Standard

TLS is supported by virtually all modern operating systems, browsers, and cloud platforms.

---

## 5. Regulatory Compliance

Supports compliance requirements for secure data transmission.

---

# Disadvantages

## 1. Performance Overhead

TLS handshakes introduce additional latency, though modern hardware and protocols minimize the impact.

---

## 2. Certificate Management

Certificates must be issued, renewed, and rotated before expiration.

---

## 3. Configuration Complexity

Weak cipher suites or outdated TLS versions can reduce security.

---

## 4. Does Not Protect Stored Data

Encryption in Transit protects only network traffic, not stored information.

---

## 5. Trust Dependency

Security depends on properly managed certificates and trusted Certificate Authorities.

---

# Best Practices

- Use HTTPS for all web applications.
- Use TLS 1.2 or TLS 1.3.
- Disable outdated SSL and TLS versions.
- Automate certificate renewal.
- Enable HTTP Strict Transport Security (HSTS).
- Validate certificates properly.
- Use mutual TLS (mTLS) for service-to-service communication when appropriate.

---

# Real-World Examples

## Online Banking

Protects login credentials and financial transactions.

---

## Amazon API Gateway

Uses HTTPS endpoints secured with TLS.

---

## Kubernetes Ingress

Terminates TLS connections before routing traffic.

---

## gRPC

Uses HTTP/2 with TLS for secure service communication.

---

# When to Use

Use Encryption in Transit when:

- Transmitting sensitive information.
- Exposing APIs over the internet.
- Communicating between microservices.
- Connecting cloud services.
- Supporting mobile and web applications.

---

# When NOT to Use

Encryption in Transit should generally be enabled whenever data is transmitted across a network, especially untrusted networks.

---

# Comparison

| Feature | Encryption at Rest | Encryption in Transit |
|---|---|---|
| Protects | Stored Data | Network Traffic |
| Primary Technology | AES | TLS/SSL |
| Threat Mitigated | Disk Theft | Network Interception |
| Applies To | Storage | Communication Channels |
| Typical Example | Encrypted Database | HTTPS |

---

# Interview Questions

## 1. What is Encryption in Transit?

The process of encrypting data while it is being transmitted across a network.

---

## 2. Which protocol is most commonly used?

Transport Layer Security (TLS).

---

## 3. Why is HTTPS considered secure?

Because it uses TLS to encrypt HTTP communication and authenticate the server.

---

## 4. What is the purpose of the TLS handshake?

To authenticate the communicating parties and establish shared session keys for encrypted communication.

---

## 5. What is the difference between Encryption at Rest and Encryption in Transit?

Encryption at Rest protects stored data, while Encryption in Transit protects data moving across networks.

---

# Key Takeaways

- Encryption in Transit protects data traveling across networks.
- TLS is the industry standard for secure communication.
- HTTPS, gRPC, SSH, and many VPNs rely on transport encryption.
- Digital certificates establish trust between communicating parties.
- Encryption in Transit and Encryption at Rest work together to provide comprehensive data protection.

---

## Previous & Next

← Previous: [Encryption at Rest](10-Encryption-at-Rest.md)

→ Next: [Secrets Management](12-Secrets-Management.md)