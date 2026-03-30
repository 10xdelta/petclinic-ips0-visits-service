# PetClinic Visits Service

## Overview
Manages pet visit records. Part of the PetClinic multi-repo microservices demo.

## Tech Stack
- Java 17, Spring Boot 4.0.1, Spring Cloud 2025.1.0
- Spring Data JPA + HSQLDB (in-memory, default) or MySQL (`mysql` profile)
- Eureka client for service discovery
- Spring Cloud Config client

## Package Structure
```
org.springframework.samples.petclinic.visits
├── VisitsServiceApplication.java   # Main class
├── config/
│   └── MetricConfig.java           # Custom metrics
├── model/
│   ├── Visit.java                  # JPA entity
│   └── VisitRepository.java        # Spring Data repo
└── web/
    └── VisitResource.java          # REST controller — /owners/*/pets/{petId}/visits
```

## API Endpoints
- `GET /pets/visits?petId={id}` — get visits for a pet
- `POST /owners/*/pets/{petId}/visits` — create a visit

## Build & Run
```bash
mvn clean package -DskipTests
# Runs on port 8082 (set by Config Server, random locally)
```

## Database
- Schema: `src/main/resources/db/hsqldb/schema.sql`
- Seed data: `src/main/resources/db/hsqldb/data.sql`
- Tables: `visits`

## Service Registration
Registers as `visits-service` with Eureka. The API Gateway routes `/api/visit/**` to this service.
