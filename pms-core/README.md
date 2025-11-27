# PMS Platform - Core Service

## Overview
The Core service is part of the PMS high-frequency trading platform.

## Module Registration
This service is automatically registered in the parent POM as:
```xml
<module>pms-core</module>
```

## Build Instructions

### Build this service only:
```bash
cd pms-core
mvn clean package
```

### Build from root:
```bash
cd ..
mvn clean package -pl pms-core
```

### Run locally:
```bash
mvn spring-boot:run
```

## Docker Build

### Build Docker image:
```bash
docker build -t pms-core:latest .
```

### Run Docker container:
```bash
docker run -p 8080:8080 pms-core:latest
```

## Configuration
Configure this service via `src/main/resources/application.yml`.

## Testing
```bash
mvn test
```

## Service Details
- **Artifact ID:** pms-core
- **Port:** 8080 (default)
- **Health Check:** /actuator/health
