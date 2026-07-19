# Client-Server Architecture

## Overview

Client-Server Architecture is one of the earliest and most fundamental software architecture patterns.

It divides an application into two primary components:

- **Client** – Requests services or resources.
- **Server** – Processes requests and returns responses.

The client and server communicate over a network using protocols such as HTTP, HTTPS, TCP, or WebSocket.

Almost every modern web application—from a simple portfolio website to platforms like Amazon and Netflix—follows the Client-Server model at its core.

---

## Why Do We Need It?

Imagine every user had to store the entire application and database on their own computer.

Problems:

- Data would become inconsistent.
- Sharing information would be difficult.
- Updates would require updating every user's machine.
- Security would be almost impossible to manage.

Instead, we centralize the application's business logic and data on a server while users interact through lightweight clients.

This separation makes applications easier to maintain, secure, and scale.

---

## Components

### Client

The client is responsible for:

- Presenting the user interface
- Collecting user input
- Sending requests
- Displaying responses

Examples:

- Web Browser
- Mobile App
- Desktop Application
- Smart TV App

---

### Server

The server is responsible for:

- Processing requests
- Executing business logic
- Authenticating users
- Accessing databases
- Returning responses

Examples:

- Node.js
- Spring Boot
- ASP.NET
- Django
- Flask

---

## Architecture

```text
              HTTP / HTTPS

+-----------+             +----------------+
|           |  Request    |                |
|  Client   | ----------> |     Server     |
|           |             |                |
|           | <---------- |                |
+-----------+  Response   +----------------+
                              |
                              |
                              ▼
                       +--------------+
                       |   Database   |
                       +--------------+
```

---

## How It Works

1. User performs an action on the client.
2. Client sends a request to the server.
3. Server validates the request.
4. Server executes business logic.
5. Server reads or writes data to the database.
6. Server returns a response.
7. Client displays the result to the user.

---

## Example

A user logs into an e-commerce application.

```text
User

   │

Browser

   │

POST /login

   │

Backend Server

   │

Validate Credentials

   │

MySQL

   │

User Found

   │

JWT Token

   │

Browser
```

---

## Advantages

- Clear separation of responsibilities
- Centralized data management
- Easier maintenance
- Better security
- Multiple clients can use the same backend
- Easier to scale than standalone applications

---

## Disadvantages

- Server can become a bottleneck
- Single point of failure without redundancy
- Network dependency
- Higher latency than local applications
- Requires server infrastructure

---

## When to Use

Use Client-Server Architecture when:

- Building web applications
- Building mobile applications
- Multiple users need shared data
- Business logic should remain centralized
- Security is important

Examples:

- Banking Applications
- E-commerce Platforms
- Social Media
- SaaS Applications
- Learning Platforms

---

## When NOT to Use

It may not be suitable for:

- Fully offline applications
- Small standalone desktop tools
- Peer-to-peer applications
- Blockchain-based systems

---

## Real-World Examples

Almost every modern application follows this architecture:

- Amazon
- Netflix
- YouTube
- Instagram
- WhatsApp Web
- Gmail
- Facebook

---

## Evolution

Client-Server Architecture laid the foundation for modern software architectures.

```text
Client-Server
      │
      ▼
Monolithic
      │
      ▼
Layered Architecture
      │
      ▼
SOA
      │
      ▼
Microservices
      │
      ▼
Event-Driven
```

Nearly every modern architecture still contains clients communicating with servers.

---

## Interview Questions

### What is Client-Server Architecture?

### Difference between Client and Server?

### Can multiple clients communicate with one server?

### Is Client-Server the same as Monolithic Architecture?

### Can Microservices still follow Client-Server Architecture?

---

## Key Takeaways

- Client-Server is the foundation of modern software systems.
- Clients request services; servers process requests.
- Business logic and data remain centralized on the server.
- It improves security, maintainability, and scalability.
- Modern architectures like Monoliths, Microservices, and Serverless are all built upon the Client-Server communication model.

---

## Previous

None (First Topic)

## Next

➡️ 02-Monolithic-Architecture.md