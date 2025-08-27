# Project Overview
This repository contains the hands-on project developed during the "Master Microservices with Spring, Docker, Kubernetes" course on Udemy. The project demonstrates modern microservices architecture patterns and best practices using industry-standard technologies.

## 📚 Course Reference
This project is based on the comprehensive Udemy course: [![Master Microservices with Spring, Docker, Kubernetes](https://www.udemy.com/course/master-microservices-with-spring-docker-kubernetes/?couponCode=MT260825A)]

## 🏗️ Architecture Overview

This project demonstrates a production-ready microservices architecture with the following core services:

| Service | Port | Description | Key Features |
|---------|------|-------------|--------------|
| **accounts** | 8080 | Customer account management | JPA, H2, Circuit Breaker |
| **cards** | 9000 | Credit card management | RESTful APIs, Data validation |
| **loans** | 8090 | Loan management system | Business logic, Entity mapping |
| **configserver** | 8071 | Centralized configuration | Git-based config, Encryption |
| **gatewayserver** | 8072 | API Gateway & Security | OAuth2, Rate limiting, Routing |
| **message** | 8080 | Event processing | Kafka integration, Async messaging |

## ⚡ Technical Highlights

### 🔧 Core Technologies
- **Framework**: Spring Boot 3.3.2 with Spring Cloud 2023.0.3
- **Java**: Java 21 with modern language features
- **Database**: H2 in-memory database for development
- **Build Tool**: Maven with wrapper scripts

### 🌐 Microservices Patterns
- **Service Discovery**: Kubernetes Discovery Client
- **Circuit Breaker**: Resilience4j with fallback mechanisms
- **API Gateway**: Spring Cloud Gateway with custom filters
- **Configuration Management**: Spring Cloud Config Server
- **Inter-service Communication**: OpenFeign clients

### 🔒 Security & Authentication
- **OAuth2 Resource Server**: JWT token validation
- **Keycloak Integration**: Identity and access management
- **CORS Configuration**: Cross-origin resource sharing
- **Request Tracing**: Correlation ID propagation

### 📊 Observability Stack
- **Metrics**: Micrometer with Prometheus integration
- **Distributed Tracing**: OpenTelemetry (OTEL v1.33.5)
- **Logging**: Structured logging with trace correlation
- **Health Checks**: Spring Boot Actuator endpoints
- **Monitoring**: Grafana dashboards and alerting

### 📨 Messaging & Events
- **Message Broker**: Apache Kafka
- **Event Streaming**: Spring Cloud Stream
- **Async Processing**: Event-driven architecture patterns

### ☁️ Cloud-Native Features
- **Containerization**: Docker support with Jib plugin
- **Kubernetes Deployment**: Complete Helm charts
- **Environment Management**: Multi-environment configurations (dev/qa/prod)
- **Service Mesh Ready**: OpenTelemetry instrumentation

## 🚀 Quick Start

### Prerequisites
- Java 21+ installed
- Maven 3.6+
- Docker (optional, for containerized deployment)
- Kubernetes cluster (optional, for K8s deployment)

### 1. Clone the Repository
```bash
git clone https://github.com/achiichou/spring-cloud-microservices.git
cd spring-cloud-microservices
```

### 2. Start Config Server (Required First)
```bash
cd configserver
./mvnw spring-boot:run
```

### 3. Start Core Services
```bash
# In separate terminals
cd accounts && ./mvnw spring-boot:run
cd cards && ./mvnw spring-boot:run
cd loans && ./mvnw spring-boot:run
```

### 4. Start Gateway Server
```bash
cd gatewayserver
./mvnw spring-boot:run
```

## 🛠️ Development Commands

### Build & Test
```bash
# Build all services
./mvnw clean compile

# Run tests
./mvnw test

# Package applications
./mvnw clean package

# Skip tests during build
./mvnw clean package -DskipTests
```

### Docker Operations
```bash
# Build Docker images using Jib
./mvnw jib:dockerBuild

# Build and push to registry
./mvnw jib:build
```

## 🎯 Key Features

### 🔄 Resilience Patterns
- **Circuit Breaker**: Prevents cascade failures with Resilience4j
- **Retry Mechanism**: Configurable retry policies with exponential backoff
- **Bulkhead**: Resource isolation between service calls
- **Rate Limiting**: Request throttling and traffic shaping

### 📈 Monitoring & Metrics
- **Prometheus Metrics**: Exposed at `/actuator/prometheus`
- **Health Indicators**: Liveness and readiness probes
- **Custom Metrics**: Business-specific KPIs and SLAs
- **Distributed Tracing**: Request flow across all services

### 🔐 Security Features
- **JWT Token Validation**: Stateless authentication
- **Role-based Access Control**: Keycloak integration
- **Request/Response Filtering**: Custom gateway filters
- **Secure Configuration**: Encrypted configuration properties

### 📦 Deployment Options

#### Local Development
```bash
# Start all services locally
./start-services.sh
```

#### Kubernetes with Helm
```bash
# Deploy to Kubernetes cluster
helm install eazybank ./helm/environments/dev-env

# Deploy observability stack
helm install prometheus ./helm/kube-prometheus
helm install grafana ./helm/grafana
helm install loki ./helm/grafana-loki
```

## 📊 API Documentation

Each service exposes OpenAPI 3.0 documentation:
- **Accounts**: http://localhost:8080/swagger-ui.html
- **Cards**: http://localhost:9000/swagger-ui.html
- **Loans**: http://localhost:8090/swagger-ui.html

## 🎨 Architecture Patterns Implemented

- **Database per Service**: Each microservice owns its data
- **API Gateway Pattern**: Single entry point for client requests
- **Configuration Externalization**: Environment-specific configurations
- **Health Check Pattern**: Service health monitoring
- **Circuit Breaker Pattern**: Fault tolerance and resilience
- **Saga Pattern**: Distributed transaction management (via events)
- **CQRS**: Command Query Responsibility Segregation in complex flows

## 📁 Project Structure

```
spring-cloud-microservices/
├── accounts/           # Account management service
├── cards/              # Card management service
├── loans/              # Loan management service
├── configserver/       # Configuration server
├── gatewayserver/      # API Gateway
├── message/            # Event processing service
├── helm/               # Kubernetes deployment charts
│   ├── eazybank-services/
│   ├── environments/
│   └── grafana*/       # Observability stack
└── kubernetes/         # K8s service discovery
```

