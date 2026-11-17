# Sudocu — Vista de Arquitectura

![Angular](https://img.shields.io/badge/Angular-DD0031?style=flat-square&logo=angular&logoColor=white)
![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

[English](README.md) | [Español](README.es.md)

> Arquitectura de alto nivel de **Sudocu**, la plataforma de gestión documental del SIU implementada en **UNGS**.
> El código, la infraestructura y los datos son privados. Este repositorio contiene solo diagramas de arquitectura.

**Mi alcance:** funcionalidades del MPD, compartición de documentos con OTP, filtros avanzados, despliegue con Docker Swarm y desarrollo spec-driven con OpenSpec.

## Despliegue

```mermaid
flowchart TB
    U[Usuarios] --> T[Traefik]
    T --> W[Angular web]
    T --> A[NestJS API]
    A --> DB[(PostgreSQL)]
    A --> K[Worker / BullMQ]
    A --> M[(MinIO)]
    A --> L[LDAP / SSO]
    K --> DB
    K --> M
    CI[GitLab CI] --> R[Registry de contenedores]
    R --> S[Docker Swarm]
    S --> T
```

## Componentes

```mermaid
flowchart LR
    subgraph Frontend
        WEB[Web app]
        MPD[Módulo MPD]
    end
    subgraph Backend
        API[API]
        AUTH[Auth / SSO]
        WORKER[Worker]
        SHARED[Librería compartida]
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

## Notas

- No se publica código, capturas ni datos institucionales.
- Repositorio pensado como vista de alto nivel para portfolio y entrevistas.
