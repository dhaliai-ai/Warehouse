# ADR-0001: Use a Three-Tier Architecture

**Status:** Proposed\
**Date:** 2026-10-28\
**Deciders:** Warehouse System Design Team\
**Project:** Warehouse Management System

## Context

The Warehouse Management System must support multiple user roles, including managers, office clerks, warehouse workers, and drivers.

The system must manage supplier orders, store orders, inventory, receiving, putaway, picking, shipping, deliveries, and reporting.

The architecture must separate user interaction, business logic, and data storage to support maintainability, security, and future enhancements.

## Decision

The Warehouse Management System will use a three-tier architecture consisting of:

1. **Presentation Tier:** Warehouse Web Application, which provides the user interface.
2. **Application Tier:** Warehouse Backend API, which processes business rules and warehouse operations.
3. **Data Tier:** Warehouse Database, which stores warehouse information.

The frontend will communicate with the backend through an API. The backend will be responsible for accessing and updating the database.

This three-tier split matches the C4 model used in the project diagrams: people and external systems at the system-context level, the web application / backend API / database as containers, and warehouse workflow components inside the backend.

### Proposed technologies

| Tier | Proposed technologies |
|---|---|
| Presentation | Vue 3, Vuetify, Vite, Vue Router, and Axios |
| Application | Node.js, Express, and Sequelize |
| Data | MySQL |

These technologies are the proposed implementation baseline documented in the root README. The presentation tier is a web application for desktop and compatible handheld devices. The application tier exposes a REST API. The data tier is a relational MySQL database accessed only through the backend.

## Rationale

This architecture was selected because it separates responsibilities, supports multiple user roles, improves maintainability, and allows each tier to evolve independently.

It also aligns with the C4 Container Diagram developed for the Warehouse Management System.

The selected technologies keep the presentation, application, and data tiers independent while remaining consistent with the OC Speckit starter kit used by this project.

## Consequences

**Positive:**

- Separates user interface, business logic, and data storage.
- Improves code organization and maintainability.
- Supports centralized validation and authorization.
- Allows future changes to individual tiers.

**Negative:**

- Requires communication between separate application layers.
- Introduces additional configuration and deployment complexity.
- Requires consistent API contracts between frontend and backend.

## Alternatives Considered

**Single-tier application:** Rejected because combining the user interface, business logic, and data storage responsibilities would make the system harder to maintain as warehouse features grow.

## Related Artifacts

- [Level 1 — System Context](../Arch_Diagrams/Warehouse-C4-System-Context.png)
- [Level 2 — Container Diagram](../Arch_Diagrams/Warehouse-C4-Container1.drawio.png)
- [Level 3 — Component Diagram](../Arch_Diagrams/Warehouse-C4-Component.drawio.png)
- [Project README](../../README.md)
- [ADR-0002: REST API](./0002-rest-api.md)
- [ADR-0003: Relational Database](./0003-relational-database.md)
- Warehouse feature specifications in `features/`.
