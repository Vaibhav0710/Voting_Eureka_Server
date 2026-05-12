# 📋 Eureka Server — Implementation Plan

> **Project:** Blockchain-Inspired Online Voting System  
> **Service:** `eureka-server`  
> **Tech:** Java 17 · Spring Boot 3.3.x · Spring Cloud 2023.x · Maven  
> **Status:** ✅ COMPLETED

---

## 📌 Overview

The Eureka Server acts as the Service Registry. Every microservice in the voting system registers its location (IP and port) here, allowing for dynamic discovery and load balancing via the API Gateway.

---

## 🏗️ Implementation Checklist

### Step 1: Project Bootstrapping
- [x] 1.1 — Create directory `eureka-server`
- [x] 1.2 — Configure `pom.xml` with `spring-cloud-starter-netflix-eureka-server`
- [x] 1.3 — Add Spring Boot parent and Spring Cloud dependency management

### Step 2: Core Configuration
- [x] 2.1 — Create `EurekaServerApplication.java` with `@EnableEurekaServer`
- [x] 2.2 — Configure `application.yml`:
  - Set `server.port: 8761`
  - Set `eureka.client.register-with-eureka: false` (it's a server, not a client)
  - Set `eureka.client.fetch-registry: false`
- [x] 2.3 — Disable wait time when sync is empty (for local development speed)

### Step 3: Verification
- [x] 3.1 — Build the service using Maven
- [x] 3.2 — Start the service and verify the dashboard at `http://localhost:8761`
- [x] 3.3 — Register `user-service` and `candidate-service` and verify they appear in the dashboard

---

## 📝 Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Port | `8761` | Default port for Eureka Server |
| Mode | Standalone | Single instance is sufficient for local development and small-scale deployment |
| Dashbaord | Enabled | Provides a visual overview of service health |

---

> **Last Updated:** May 11, 2026  
