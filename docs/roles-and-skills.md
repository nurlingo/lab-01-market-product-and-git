# Roles and Skills

## Components and roles

- **MTProto Gateway (DC Entry)**
  - Backend Engineer
  - Network Engineer
  - Security Engineer
  - SRE / DevOps

- **Message Handling Service**
  - Backend Engineer
  - Database Engineer
  - QA Engineer

- **Media & File Service**
  - Backend Engineer
  - Storage / Infrastructure Engineer
  - QA Engineer

- **Auth & Session Service**
  - Backend Engineer
  - Security Engineer
  - QA Engineer

- **Notification/Updates Service**
  - Backend Engineer
  - Mobile Engineer (iOS/Android) — for push integration on client side
  - DevOps / SRE

- **Channel/Broadcast Service**
  - Backend Engineer
  - Database Engineer
  - QA Engineer

- **Mobile App (iOS/Android)**
  - Mobile Engineer (iOS)
  - Mobile Engineer (Android)
  - UI/UX Designer
  - QA Engineer

- **Desktop App / Web Client**
  - Frontend Engineer
  - Desktop Engineer (C++/Electron)
  - UI/UX Designer
  - QA Engineer

## Roles and responsibilities

1. **Backend Engineer** — designs and implements server-side services (Message Service, Auth Service, etc.). Writes API endpoints, business logic, and integrations between components. Optimizes for high throughput and low latency to handle millions of concurrent users.

2. **Mobile Engineer (iOS/Android)** — develops the Telegram mobile app for a specific platform. Implements the UI, handles local data storage and caching, integrates with the MTProto protocol for communication, and works with push notification APIs (APNs/FCM).

3. **Security Engineer** — ensures the MTProto protocol is implemented correctly, reviews authentication flows for vulnerabilities, and audits the secret chat (E2E encryption) implementation. Conducts threat modeling and penetration testing.

4. **Database Engineer** — designs and maintains the Sharded Chat DB schema and sharding strategy. Optimizes queries for message retrieval, manages replication across data centers, and monitors storage performance and capacity.

5. **SRE / DevOps** — manages the deployment and operation of all services across Telegram's data centers. Sets up CI/CD pipelines, configures monitoring and alerting (for Kafka, Redis, DB clusters), handles incident response, and ensures high availability.

## Common skills across roles

Based on the responsibilities above, the following technical skills appear across multiple roles:

- **Distributed systems** — Backend, Database, and SRE roles all need to understand how distributed systems work, since Telegram runs across multiple data centers with sharded databases, message queues, and caches.
- **Networking (TCP/IP, HTTP/2, WebSocket)** — Backend Engineers, Security Engineers, and Mobile Engineers all work with network protocols for communication between clients and servers.
- **Linux / Unix administration** — Backend Engineers, SREs, and Database Engineers all operate and troubleshoot services running on Linux servers.
- **Git and CI/CD** — every engineering role uses version control and automated build/deploy pipelines to collaborate and ship code.
- **Monitoring and observability** — SREs, Backend Engineers, and Database Engineers all need to track service health using tools like Prometheus, Grafana, etc.
- **Security fundamentals** — not only Security Engineers but also Backend and Mobile Engineers need to understand encryption, secure coding, and authentication mechanisms.
