# ADR-002: Use a REST API for Communication

**Status:** Proposed  
**Date:** 2026-10-28  
**Project:** Warehouse Management System

## Context

The Warehouse Management System consists of a Web Application, Backend API, and Database.

Managers, office clerks, warehouse workers, and drivers interact with the system through the user interface.

The frontend needs a consistent and secure method to communicate with the backend for operations such as creating orders, receiving shipments, updating inventory, picking items, shipping orders, and generating reports.

## Decision

The Warehouse Management System will use a REST API over HTTPS for communication between the Warehouse Web Application and the Warehouse Backend API.

The API will use standard HTTP methods:

- **GET:** Retrieve warehouse information.
- **POST:** Create new records or initiate operations.
- **PUT/PATCH:** Update existing records.
- **DELETE:** Remove records when permitted by business rules.

JSON will be used for request and response data.

The Backend API will validate requests, enforce authorization rules, execute business logic, and communicate with the database.

## Rationale

REST was selected because it provides a standardized interface between the frontend and backend.

It supports separation of responsibilities, allows multiple client interfaces to use the same backend, and simplifies API testing and documentation.

HTTPS protects information transmitted between the frontend and backend.

## Consequences

**Positive:**
- Provides consistent communication between application layers.
- Supports future web and mobile interfaces.
- Makes API endpoints easier to test independently.
- Allows centralized validation and authorization.
- Supports integration with barcode-scanning workflows.

**Negative:**
- Requires careful API design and documentation.
- Network communication may introduce latency.
- Requires error handling and secure authentication.
- API changes must be coordinated with frontend development.

## Alternatives Considered

**Direct frontend-to-database communication:** Rejected because it would expose data access and make centralized authorization more difficult.

**GraphQL:** Considered but not selected for the initial design because REST provides a simpler approach for the proposed warehouse operations.

## Related Artifacts

- `docs/Arch_Diagrams/Warehouse-C4-Container.png`
- Warehouse feature specifications in `features/`.