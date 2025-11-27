# PMS Platform - High-Frequency Trading System

## Version Documentation

**Version:** 1.0.0-SNAPSHOT  
**Java Version:** 21  
**Spring Boot:** 3.2.5  
**Spring Cloud:** 2023.0.1  
**Build Tool:** Maven 3.9+  

## Architecture Overview

This is a production-grade Maven monorepo containing microservices for high-frequency trading operations.

### Microservices

| Service | Artifact ID | Description |
|---------|-------------|-------------|
| Ingestion | pms-ingestion | Market data ingestion and streaming |
| Validation | pms-validation | Trade validation and compliance checks |
| Enrichment | pms-enrichment | Data enrichment and normalization |
| Core | pms-core | Core trading engine |
| Risk | pms-risk | Risk management and calculation |
| Leaderboard | pms-leaderboard | Performance tracking and rankings |
| Tracker | pms-tracker | Position and portfolio tracking |
| Notification | pms-notification | Alert and notification service |

## Onboarding Guide

### Prerequisites

Before you begin, ensure you have the following installed:

- **Java 21** (OpenJDK or Oracle JDK)
- **Maven 3.9+**
- **Docker** (for containerization)
- **Git** (for version control)
- **IDE** (IntelliJ IDEA, Eclipse, or VSCode with Java extensions)

### Quick Start

#### 1. Clone the Repository
```bash
git clone <repository-url>
cd pms-platform
```

#### 2. Build All Services
```bash
mvn clean install
```

#### 3. Build Specific Service
```bash
mvn clean package -pl pms-ingestion
```

#### 4. Run a Service Locally
```bash
cd pms-core
mvn spring-boot:run
```

#### 5. Build Docker Image
```bash
cd pms-core
docker build -t pms-core:latest .
```

### Project Structure

```
pms-platform/
├── pom.xml                          # Parent POM
├── .gitignore                       # Git ignore rules
├── .dockerignore                    # Docker ignore rules
├── README.md                        # This file
├── pms-ingestion/                   # Ingestion Service
│   ├── pom.xml
│   ├── Dockerfile
│   ├── README.md
│   └── src/
│       ├── main/
│       │   ├── java/
│       │   └── resources/
│       └── test/
├── pms-validation/                  # Validation Service
├── pms-enrichment/                  # Enrichment Service
├── pms-core/                        # Core Service
├── pms-risk/                        # Risk Service
├── pms-leaderboard/                 # Leaderboard Service
├── pms-tracker/                     # Tracker Service
├── pms-notification/                # Notification Service
├── deployment/                      # Deployment configurations
│   ├── k8s/                         # Kubernetes manifests
│   └── kafka/                       # Kafka configurations
└── environments/                    # Environment-specific configs
    ├── development/
    ├── test/
    └── prod/
```

### Development Workflow

#### Building

```bash
# Build all modules
mvn clean install

# Build without tests
mvn clean install -DskipTests

# Build specific module and its dependencies
mvn clean install -pl pms-core -am
```

#### Testing

```bash
# Run all tests
mvn test

# Run tests for specific module
mvn test -pl pms-validation

# Run integration tests
mvn verify
```

#### Running Services

```bash
# Run service with Spring Boot Maven plugin
cd pms-<service-name>
mvn spring-boot:run

# Run with specific profile
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

### Docker Commands

```bash
# Build image
docker build -t pms-<service>:latest ./pms-<service>

# Run container
docker run -p 8080:8080 pms-<service>:latest

# Run with environment variables
docker run -p 8080:8080 \
  -e SPRING_PROFILES_ACTIVE=prod \
  pms-<service>:latest
```

### Maven Reactor Commands

```bash
# Build specific modules
mvn clean install -pl pms-core,pms-risk

# Build module and dependents
mvn clean install -pl pms-core -amd

# Resume from specific module after failure
mvn clean install -rf :pms-core
```

### IDE Setup

#### IntelliJ IDEA
1. Open the `pms-platform` folder
2. IntelliJ will auto-detect the Maven structure
3. Enable annotation processing: Settings → Build → Compiler → Annotation Processors
4. Install Lombok plugin if not already installed

#### Eclipse
1. Import as "Existing Maven Projects"
2. Select the root `pom.xml`
3. Install Lombok: Download `lombok.jar` and run it

#### VSCode
1. Install "Extension Pack for Java"
2. Install "Spring Boot Extension Pack"
3. Open the workspace folder

### Configuration Management

Each service uses `application.yml` for configuration:

```yaml
# Example application.yml
server:
  port: 8080

spring:
  application:
    name: pms-<service>
  
  kafka:
    bootstrap-servers: localhost:9092
  
  datasource:
    url: jdbc:postgresql://localhost:5432/pms
    username: pms_user
    password: pms_password
```

### Environment-Specific Configs

Use Spring profiles for different environments:

- `application-dev.yml` - Development
- `application-test.yml` - Testing
- `application-prod.yml` - Production

### Health Checks

All services expose actuator endpoints:

```bash
# Health check
curl http://localhost:8080/actuator/health

# Info endpoint
curl http://localhost:8080/actuator/info

# Metrics
curl http://localhost:8080/actuator/metrics
```

### Troubleshooting

#### Maven Build Issues

```bash
# Clean local repository cache
mvn dependency:purge-local-repository

# Force update dependencies
mvn clean install -U

# Debug build
mvn clean install -X
```

#### Common Issues

1. **Java Version Mismatch**: Ensure Java 21 is active
   ```bash
   java -version
   ```

2. **Port Already in Use**: Change port in `application.yml`
   ```yaml
   server.port: 8081
   ```

3. **Lombok Not Working**: Enable annotation processing in IDE

### Contributing

1. Create feature branch from `main`
2. Implement changes with tests
3. Ensure all tests pass: `mvn clean verify`
4. Submit pull request

### Additional Resources

- [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/3.2.5/reference/html/)
- [Maven Documentation](https://maven.apache.org/guides/)
- [Docker Documentation](https://docs.docker.com/)

### Support

For questions or issues, contact the platform team.

---

**Generated:** $(date +"%Y-%m-%d")  
**Platform:** PMS High-Frequency Trading System
