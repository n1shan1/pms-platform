# PMS Platform - Validation Service

## Overview
The Validation service is part of the PMS high-frequency trading platform.

## Module Registration
This service is automatically registered in the parent POM as:
```xml
<module>pms-validation</module>
```

## Build Instructions

### Build this service only:
```bash
cd pms-validation
mvn clean package
```

### Build from root:
```bash
cd ..
mvn clean package -pl pms-validation
```

### Run locally:
```bash
mvn spring-boot:run
```

## Docker Build

### Build Docker image:
```bash
docker build -t pms-validation:latest .
```

### Run Docker container:
```bash
docker run -p 8080:8080 pms-validation:latest
```

## Configuration
Configure this service via `src/main/resources/application.yml`.

## Testing
```bash
mvn test
```

## Service Details
- **Artifact ID:** pms-validation
- **Port:** 8080 (default)
- **Health Check:** /actuator/health
