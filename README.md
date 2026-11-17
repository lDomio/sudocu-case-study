# Sudocu — Architecture Overview

![Angular](https://img.shields.io/badge/Angular-DD0031?style=flat-square&logo=angular&logoColor=white)
![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

[English](README.md) | [Español](README.es.md)

> High-level architecture of **Sudocu**, the SIU document management platform implemented at **UNGS**.
> Product code, infrastructure details and data are private. This repository contains architecture diagrams only.

**My scope:** MPD features, OTP document sharing, advanced filters, Docker Swarm deployment and spec-driven development with OpenSpec.

## Deployment

```mermaid
flowchart TB
    U[Users] --> T[Traefik]
    T --> W[Angular web]
    T --> A[NestJS API]
    A --> DB[(PostgreSQL)]
    A --> K[Worker / BullMQ]
    A --> M[(MinIO)]
    A --> L[LDAP / SSO]
    K --> DB
    K --> M
    CI[GitLab CI] --> R[Container registry]
    R --> S[Docker Swarm]
    S --> T
```

## Components

```mermaid
flowchart LR
    subgraph Frontend
        WEB[Web app]
        MPD[MPD module]
    end
    subgraph Backend
        API[API]
        AUTH[Auth / SSO]
        WORKER[Worker]
        SHARED[Shared library]
    end
    DB[(PostgreSQL)]
    MINIO[(MinIO)]
    LDAP[(LDAP)]

    WEB --> API
    MPD --> API
    API --> AUTH
    API --> DB
    API --> MINIO
    API --> LDAP
    API --> WORKER
    WORKER --> DB
    WORKER --> MINIO
    SHARED --- API
```

## Notes

- No source code, screenshots or institutional data are published.
- Repository intended as a high-level overview for portfolio and interviews.
