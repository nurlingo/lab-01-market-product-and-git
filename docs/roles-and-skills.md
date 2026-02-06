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

## My chosen role

### Role

Backend Engineer

### Skills I already have
<!-- from roadmap.sh -->
- Python (OOP, type hints, async/await)
- Git and GitHub (branching, PRs, merges)
- SQL basics (PostgreSQL queries, simple schema design)
- REST API design (HTTP methods, status codes, JSON)
- Docker basics (writing Dockerfiles, docker-compose)
- Linux command line (navigation, file management, SSH)
- Basic algorithms and data structures

### Skills I clearly lack
<!-- 4-5 skills from roadmap.sh that seemed important to have -->
- Message brokers (Kafka, RabbitMQ) — no hands-on experience with event-driven architectures
- System design and high-load architecture — never designed systems for millions of users
- CI/CD pipeline configuration — used existing pipelines but never built one from scratch
- Caching strategies (Redis, Memcached) — know the concept but never implemented cache invalidation in production
- Monitoring and observability (Prometheus, Grafana, ELK) — never set up monitoring for a real service

## Job market snapshot

I searched for Backend Engineer (Python) positions on hh.ru. Here are the postings I found:

1. **Python Backend Developer (FastAPI)** — РОМИР, Moscow
   - Link: [hh.ru/vacancy/130086103](https://hh.ru/vacancy/130086103)
   - Key skills: Python 3.x (OOP, type hints), FastAPI, PostgreSQL, ClickHouse, Docker, Linux, CI/CD

2. **Python Backend Developer** — ПИПЛ КЭПИТАЛ, Moscow
   - Link: [hh.ru/vacancy/130075554](https://hh.ru/vacancy/130075554)
   - Key skills: Python 3.12+, Django + DRF, PostgreSQL, Celery, Redis, Docker, Nginx

3. **Backend Python Developer** — БорисХоф, Moscow (remote)
   - Link: [hh.ru/vacancy/130134484](https://hh.ru/vacancy/130134484)
   - Key skills: Python, FastAPI, asyncio, PostgreSQL/MySQL, Redis/MongoDB, Docker, Linux

4. **Backend Developer Python (Middle+/Senior)** — Киберия, Moscow (remote)
   - Link: [hh.ru/vacancy/130210974](https://hh.ru/vacancy/130210974)
   - Key skills: Python 4+ years, PostgreSQL, Apache Airflow, Docker, Linux, ML/CV basics

5. **Python Backend Developer (Middle)** — Мэйнс Лаборатория, Moscow (remote)
   - Link: [hh.ru/vacancy/129440300](https://hh.ru/vacancy/129440300)
   - Key skills: Python, FastAPI, Pydantic, PostgreSQL, SQLAlchemy, Redis, Celery, pytest

### Skills that appear in several postings
- Python (all 5)
- PostgreSQL (all 5)
- Docker (all 5)
- Linux (all 5)
- FastAPI (3 out of 5)
- Redis (3 out of 5)
- CI/CD (3 out of 5)

### Skills specific to a single posting
- ClickHouse (РОМИР — analytics workload)
- Apache Airflow (Киберия — data pipeline orchestration)
- Ansible (ПИПЛ КЭПИТАЛ — infrastructure-as-code for fintech)
- ML/Computer Vision (Киберия — AI-focused project)
- Pandas (Мэйнс Лаборатория — data processing)

## Personal reflection

I chose Backend Engineer because I enjoy building things that work behind the scenes. When I studied Telegram's architecture in Task 1, I realized that most of the interesting complexity lives on the server side — message routing, data sharding, push notifications — and I want to learn how to build systems like that. Comparing my skills to what employers ask for, I feel confident about Python and basic SQL, but I see a clear gap in production-level tools like Redis, Celery, and proper CI/CD. Almost every posting mentions Docker and Linux, which I have some experience with, so that is reassuring. The two skills I want to focus on this semester are system design (how to structure a backend for high load) and working with message queues, because these keep showing up both in Telegram's architecture and in real job postings. This lab helped me see that knowing a language is just the starting point — what actually matters is understanding how to put components together into a working system. I used Claude to help me research job postings and organize the architecture description. It was helpful for structuring information quickly, but the descriptions it gave were sometimes too generic, and I had to adjust them to be specific to Telegram. Going forward, I plan to build a small project with FastAPI, PostgreSQL, and Redis to close the gap between what I know in theory and what I can actually do.
