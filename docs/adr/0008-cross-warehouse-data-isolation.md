# ADR-0008: Cross-Warehouse Data Isolation

**Status:** Proposed\
**Date:** 2026-11-23\
**Deciders:** Warehouse System Design Team

## Context

The Warehouse Management System supports a company operating multiple warehouses through a centralized application and relational database.

Each warehouse maintains its own inventory, storage locations, receiving activities, picking tasks, shipping activities, and operational records.

Without appropriate data isolation, employees could accidentally or intentionally access or modify records belonging to warehouses they are not authorized to manage.

The system requires an authorization model that considers both the user's assigned role and authorized warehouse access.

## Decision

The system shall implement warehouse-level data isolation through server-side authorization, warehouse-scoped database queries, and relational database constraints.

Role-based access control shall determine which operations a user may perform. Warehouse assignments shall determine which warehouse-specific records the user may access.

The backend shall enforce these restrictions for every warehouse-specific request. Frontend restrictions alone shall not be considered sufficient security.

### Data Ownership and Scope

| Data | Ownership Scope |
|---|---|
| Company information | Company |
| Item master data | Company |
| Supplier information | Company |
| Customer information | Company |
| Warehouse configuration | Warehouse |
| Storage locations | Warehouse |
| Inventory quantities | Warehouse |
| Receiving transactions | Warehouse |
| Putaway tasks | Warehouse |
| Picking tasks | Warehouse |
| Shipping transactions | Warehouse |
| Inventory adjustments | Warehouse |

Company-level records shall remain subject to role-based authorization even when shared across warehouses.

### Authorization Process

1. Authenticate the user.
2. Identify the user's assigned role.
3. Identify the warehouses the user is authorized to access.
4. Identify the warehouse associated with the requested record or operation.
5. Verify that the user's role permits the requested operation.
6. Verify that the user is authorized to access the identified warehouse.
7. Execute the operation only when all authorization checks succeed.
8. Reject unauthorized requests without exposing restricted warehouse information.

### Architectural Rules

- Warehouse-specific database queries shall include appropriate warehouse restrictions.
- The backend shall validate warehouse identifiers received from clients.
- Users shall not gain access to another warehouse by modifying a URL, request parameter, or request body.
- Inventory records shall be associated with their respective warehouse and storage location.
- Database relationships shall prevent inconsistent associations between warehouses and storage locations.
- Users assigned to multiple warehouses shall access only their authorized warehouses.
- Company-wide reporting shall require appropriate permissions.
- Unauthorized requests shall not modify inventory or operational records.
- Security-sensitive operations and inventory changes shall be traceable to the responsible user.

## Consequences

### Positive

- Protects warehouse-specific operational information.
- Prevents unauthorized inventory modifications.
- Reduces accidental cross-warehouse transactions.
- Supports employees assigned to different warehouses.
- Allows centralized administration while maintaining operational separation.
- Improves accountability and inventory accuracy.

### Negative / Tradeoffs

- Backend authorization logic becomes more complex.
- Database queries require consistent warehouse filtering.
- Additional authorization and integration testing is required.
- User warehouse assignments must be maintained accurately.
- Company-wide reporting requires additional permission checks.

## Alternatives Considered

| Option | Why not |
|---|---|
| Frontend-only warehouse restrictions | Users could bypass frontend restrictions by directly accessing the API. |
| Role-based access without warehouse restrictions | A valid role could provide unauthorized access to another warehouse. |
| Separate database for every warehouse | Increases infrastructure complexity and complicates shared master data and reporting. |
| Unrestricted access across warehouses | Creates unacceptable security and inventory integrity risks. |

## Related Artifacts

- [ADR-0007: Company and Multi-Warehouse Architecture](./0007-company-multi-warehouse.md)
- [ADR-0004: Role-Based Access Control](./0004-role-based-access.md)
- [ADR-0003: Relational Database](./0003-relational-database.md)
- [Feature Specifications](../../features/)
- [Quality Attributes](../nfr/quality-attributes.md)
- [Cursor Rules](../../.cursor/rules/)

## Verification

The architectural decision shall be verified through the following scenarios:

- An authorized employee can access inventory belonging to an assigned warehouse.
- An employee cannot access inventory belonging to an unauthorized warehouse.
- Changing a warehouse identifier in an API request does not bypass authorization.
- An unauthorized inventory modification is rejected without changing stored quantities.
- A storage location cannot be incorrectly associated with another warehouse's inventory.
- An employee assigned to multiple warehouses can access only those assigned warehouses.
- Company-wide reports are available only to appropriately authorized users.
- Shared company-level master data remains protected by role-based permissions.