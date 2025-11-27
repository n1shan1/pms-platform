# PMS Platform - Enrichment Service

## Overview
The Enrichment service is part of the PMS high-frequency trading platform.

## Module Registration
This service is automatically registered in the parent POM as:
```xml
<module>pms-enrichment</module>
```

## Build Instructions

### Build this service only:
```bash
cd pms-enrichment
mvn clean package
```

### Build from root:
```bash
cd ..
mvn clean package -pl pms-enrichment
```

### Run locally:
```bash
mvn spring-boot:run
```

## Docker Build

### Build Docker image:
```bash
docker build -t pms-enrichment:latest .
```

### Run Docker container:
```bash
docker run -p 8080:8080 pms-enrichment:latest
```

## Configuration
Configure this service via `src/main/resources/application.yml`.

## Testing
```bash
mvn test
```

## Service Details
- **Artifact ID:** pms-enrichment
- **Port:** 8080 (default)
- **Health Check:** /actuator/health
