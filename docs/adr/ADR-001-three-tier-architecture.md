# ADR-001: Use a Three-Tier Architecture

**Status:** Proposed  
**Date:** 2026-10-28  
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

## Rationale

This architecture was selected because it separates responsibilities, supports multiple user roles, improves maintainability, and allows each tier to evolve independently.

It also aligns with the C4 Container Diagram developed for the Warehouse Management System.

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

- `docs/Arch_Diagrams/Warehouse-C4-Container.png`
- Warehouse feature specifications in `features/`.

