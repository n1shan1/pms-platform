# PMS Platform - Risk Service

## Overview
The Risk service is part of the PMS high-frequency trading platform.

## Module Registration
This service is automatically registered in the parent POM as:
```xml
<module>pms-risk</module>
```

## Build Instructions

### Build this service only:
```bash
cd pms-risk
mvn clean package
```

### Build from root:
```bash
cd ..
mvn clean package -pl pms-risk
```

### Run locally:
```bash
mvn spring-boot:run
```

## Docker Build

### Build Docker image:
```bash
docker build -t pms-risk:latest .
```

### Run Docker container:
```bash
docker run -p 8080:8080 pms-risk:latest
```

## Configuration
Configure this service via `src/main/resources/application.yml`.

## Testing
```bash
mvn test
```

## Service Details
- **Artifact ID:** pms-risk
- **Port:** 8080 (default)
- **Health Check:** /actuator/health
