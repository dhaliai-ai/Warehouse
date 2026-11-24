# ADR-0002: Use a REST API for Communication

**Status:** Proposed\
**Date:** 2026-10-28\
**Deciders:** Warehouse System Design Team\
**Project:** Warehouse Management System

## Context

The Warehouse Management System consists of a Web Application, Backend API, and Database.

Managers, office clerks, warehouse workers, and drivers interact with the system through the user interface.

The frontend needs a consistent and secure method to communicate with the backend for operations such as creating orders, receiving shipments, updating inventory, picking items, shipping orders, and generating reports.

## Decision

The Warehouse Management System will use a REST API over HTTPS for communication between the Warehouse Web Application and the Warehouse Backend API.

Protected API routes will be mounted under the proposed `/api` base path documented in the root README.

The API will use standard HTTP methods:

- **GET:** Retrieve warehouse information.
- **POST:** Create new records or initiate operations.
- **PUT/PATCH:** Update existing records.
- **DELETE:** Remove records when permitted by business rules.

JSON will be used for request and response data.

The Backend API will validate requests, enforce authorization rules, execute business logic, and communicate with the database.

### JSON conventions

- Request and response bodies are JSON.
- Success responses return the resource fields directly. They do not wrap payloads in a `{ success, data }` envelope.
- Error responses use `{ "message": "..." }`.
- Authenticated requests send `Authorization: Bearer <token>`.

### HTTP status codes

| Status | When |
|---|---|
| `200 OK` | Successful read or update. |
| `201 Created` | Successful create. |
| `204 No Content` | Successful delete when no body is returned. |
| `400 Bad Request` | Invalid input or failed validation. |
| `401 Unauthorized` | Missing or invalid authentication. |
| `403 Forbidden` | Authenticated user lacks the required role or permission. |
| `404 Not Found` | Resource does not exist, or warehouse-scoped access must not confirm that a restricted record exists. |
| `409 Conflict` | Uniqueness, state, or dependency conflict. |

### Backend enforcement

Every protected `/api` operation shall be enforced on the backend:

- **Authentication:** reject unauthenticated requests.
- **Authorization:** enforce role-based permissions ([ADR-0004](./0004-role-based-access.md)).
- **Warehouse scoping:** restrict warehouse-specific records to authorized warehouses ([ADR-0008](./0008-cross-warehouse-data-isolation.md)).
- **Input validation:** reject invalid identifiers, quantities, barcodes, and other request data before changing stored records.
- **Inventory-changing operations:** apply database transaction rules ([ADR-0009](./0009-inventory-transaction-integrity.md)) and barcode retry / duplicate-submission rules ([ADR-0010](./0010-barcode-error-handling.md)).

Frontend menu hiding does not replace these backend checks.

## Rationale

REST was selected because it provides a standardized interface between the frontend and backend.

It supports separation of responsibilities, allows multiple client interfaces to use the same backend, and simplifies API testing and documentation.

HTTPS protects information transmitted between the frontend and backend.

A shared `/api` prefix, flat JSON bodies, and consistent status codes keep the Vue client and Express backend aligned with the OC Speckit conventions used by this project.

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

- [Level 2 — Container Diagram](../Arch_Diagrams/Warehouse-C4-Container1.drawio.png)
- [Project README](../../README.md)
- [ADR-0004: Role-Based Access Control](./0004-role-based-access.md)
- [ADR-0008: Cross-Warehouse Data Isolation](./0008-cross-warehouse-data-isolation.md)
- [ADR-0009: Inventory Transaction Integrity](./0009-inventory-transaction-integrity.md)
- [ADR-0010: Barcode Error Handling and Device Reliability](./0010-barcode-error-handling.md)
- Warehouse feature specifications in `features/`.
