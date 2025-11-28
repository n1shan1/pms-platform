# Stage 1: Build
FROM maven:3.9-eclipse-temurin-21 AS build

WORKDIR /app

# Create a minimal parent POM for this module
RUN echo '<?xml version="1.0" encoding="UTF-8"?><project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"><modelVersion>4.0.0</modelVersion><groupId>com.pms</groupId><artifactId>pms-platform</artifactId><version>1.0.0-SNAPSHOT</version><packaging>pom</packaging><name>PMS Platform - Parent</name><modules><module>pms-core</module></modules><properties><java.version>21</java.version><maven.compiler.source>21</maven.compiler.source><maven.compiler.target>21</maven.compiler.target><project.build.sourceEncoding>UTF-8</project.build.sourceEncoding><spring-boot.version>3.2.5</spring-boot.version></properties><dependencyManagement><dependencies><dependency><groupId>org.springframework.boot</groupId><artifactId>spring-boot-dependencies</artifactId><version>${spring-boot.version}</version><type>pom</type><scope>import</scope></dependency></dependencies></dependencyManagement><build><pluginManagement><plugins><plugin><groupId>org.springframework.boot</groupId><artifactId>spring-boot-maven-plugin</artifactId><version>${spring-boot.version}</version></plugin></plugins></pluginManagement></build></project>' > pom.xml

# Copy service POM
COPY pms-core/pom.xml pms-core/pom.xml

# Copy service source code
COPY pms-core/src pms-core/src

# Build application
RUN mvn clean package spring-boot:repackage -pl pms-core -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app

# Add non-root user for security
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

# Copy JAR from build stage
COPY --from=build /app/pms-core/target/*.jar app.jar

# Expose application port
EXPOSE 8080

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=40s --retries=3 \
    CMD wget --no-verbose --tries=1 --spider http://localhost:8080/actuator/health || exit 1

# JVM optimization for containers
ENV JAVA_OPTS="-XX:+UseContainerSupport -XX:MaxRAMPercentage=75.0 -Djava.security.egd=file:/dev/./urandom"

# Run application
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
