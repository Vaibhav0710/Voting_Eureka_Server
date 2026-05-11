# 📍 Eureka Server (Service Discovery)

> Part of the **Blockchain-Inspired Online Voting System** — a production-grade, scalable microservices platform.

[![Java](https://img.shields.io/badge/Java-17-orange.svg)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.3.6-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-2023.0.3-blue.svg)](https://spring.io/projects/spring-cloud)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📌 Overview

The **Eureka Server** is the central registry for the microservices ecosystem. It enables **Service Discovery**, allowing services to find and communicate with each other dynamically without hardcoding IP addresses and ports.

### Feature Status
- ✅ Project bootstrapping
- ✅ Eureka Server configuration
- ✅ Self-registration disabled (Standalone mode)
- ✅ Dashboard enabled at `http://localhost:8761`
- ✅ All services registered as clients

---

## 🏗️ Architecture

```
                    ┌──────────────────┐
                    │   API Gateway    │
                    │ (Spring Cloud)   │
                    └────────┬─────────┘
                             │
               ┌──────────────┼──────────────┐
               │              │              │
     ┌─────────▼──┐  ┌───────▼────┐  ┌──────▼──────┐
     │ User       │  │  Candidate │  │  Voting     │
     │ Service    │  │  Service   │  │  Service    │
     └──────┬─────┘  └──────┬─────┘  └──────┬──────┘
            │               │               │
            └───────────────┼───────────────┘
                            │
                  ┌─────────▼─────────┐
                  │ ★EUREKA SERVER★   │
                  │ (Port 8761)       │
                  └───────────────────┘
```

---

## 🛠️ Tech Stack

| Component | Technology | Version |
|-----------|-----------|---------|
| Language | Java | 17 |
| Framework | Spring Boot | 3.3.6 |
| Service Discovery | Netflix Eureka Server | — |
| Cloud Config | Spring Cloud | 2023.0.3 |
| Build Tool | Maven | 3.8+ |

---

## 📦 Project Structure

```
eureka-server/
├── src/
│   ├── main/
│   │   ├── java/com/voting/eurekaserver/
│   │   │   ├── EurekaServerApplication.java  ← @EnableEurekaServer
│   │   │   └── docs/                         ← Implementation Plan
│   │   └── resources/
│   │       └── application.yml               ← Eureka Configuration
├── README.md                                 ← This file
├── pom.xml
└── mvnw
```

---

## 🚀 Getting Started

### Prerequisites
- Java 17+
- Maven 3.8+

### Setup

1. **Build the project**
   ```bash
   ./mvnw clean install
   ```

2. **Run the service**
   ```bash
   ./mvnw spring-boot:run
   ```

3. **Access Dashboard**
   Visit `http://localhost:8761` in your browser.

---

## 📋 Implementation Progress

> Detailed checklist: [IMPLEMENTATION_PLAN.md](src/main/java/com/voting/eurekaserver/docs/IMPLEMENTATION_PLAN.md)

| Task | Description | Status |
|------|-------------|--------|
| 2.1 | Eureka Server Setup | ✅ Done |
| 2.2 | Client Registration | ✅ Done |

---

## 📝 License

This project is licensed under the MIT License.

---

> **Maintainer:** Vaibhav Jain  
> **Last Updated:** May 11, 2026
