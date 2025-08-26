# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Spring Boot microservices architecture project implementing an EazyBank system with the following core services:

- **accounts**: Customer account management service (port 8080)
- **cards**: Credit card management service 
- **loans**: Loan management service
- **configserver**: Spring Cloud Config Server for centralized configuration (port 8071)
- **gatewayserver**: Spring Cloud Gateway API Gateway with OAuth2/Keycloak integration
- **message**: Message processing service with Kafka integration

## Technology Stack

- **Framework**: Spring Boot 3.3.2 with Spring Cloud 2023.0.3
- **Java Version**: Java 21 (though running in Java 17 environment)
- **Database**: H2 in-memory database for development
- **Service Discovery**: Kubernetes Discovery Client
- **Circuit Breaker**: Resilience4j
- **Inter-service Communication**: OpenFeign
- **Message Broker**: Apache Kafka
- **Monitoring**: OpenTelemetry, Micrometer with Prometheus
- **Security**: OAuth2 with Keycloak
- **Documentation**: OpenAPI 3 (Swagger)

## Development Commands

### Build Commands
```bash
# Build individual service (run from service directory)
./mvnw clean compile

# Package service
./mvnw clean package

# Build Docker image using Jib
./mvnw jib:dockerBuild

# Skip tests during build
./mvnw clean package -DskipTests
```

### Test Commands
```bash
# Run tests for individual service
./mvnw test

# Run all tests
./mvnw clean test
```

### Running Services
```bash
# Run individual service (from service directory)
./mvnw spring-boot:run

# Run with specific profile
./mvnw spring-boot:run -Dspring-boot.run.profiles=dev
```

## Architecture Notes

### Service Communication
- Services communicate via OpenFeign clients with fallback mechanisms
- Circuit breaker patterns implemented with Resilience4j
- Correlation IDs used for distributed tracing (`eazybank-correlation-id` header)

### Configuration Management
- External configuration managed by configserver pulling from Git repository
- Profile-based configuration (dev, qa, prod) available in configserver
- Default fallback to local configuration if config server unavailable

### Observability
- OpenTelemetry integration for distributed tracing
- Prometheus metrics available at `/actuator/prometheus`
- Health checks and readiness probes configured
- Log correlation with trace and span IDs

### Security
- OAuth2 Resource Server configuration in gateway
- JWT token validation via Keycloak
- CORS and security filters in gateway

### Kubernetes Deployment
- Helm charts available in `/helm` directory for all services
- Common chart templates for consistent deployments
- Environment-specific values files (dev, qa, prod)
- Full observability stack with Grafana, Loki, Tempo, and Prometheus

## Database Schema
Each service maintains its own database schema via `schema.sql` files in resources directory.

## Key Configuration Files
- `application.yml`: Service-specific configuration
- `config/`: External configuration files in configserver
- `helm/`: Kubernetes deployment manifests
- `pom.xml`: Maven dependencies and build configuration