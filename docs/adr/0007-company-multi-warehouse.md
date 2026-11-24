# ADR-0007: Company and Multi-Warehouse Architecture

**Status:** Proposed\
**Date:** 2026-11-23\
**Deciders:** Warehouse System Design Team

## Context

The Warehouse Management System must support a company that operates multiple warehouses. The company may initially operate one warehouse but expand by opening additional facilities.

Each warehouse has its own physical layout, receiving doors, shipping doors, storage locations, inventory quantities, and operational activities.

However, company-level information, including item master data and supplier information, may be shared across warehouses.

The architecture must support this organizational structure without requiring a separate application or database for every warehouse.

The initial project requirements describe one company operating multiple warehouses. Supporting multiple independent tenant companies is not an established requirement.

## Decision

The system shall use a centralized application and relational database with a hierarchical company and warehouse data model.

The initial implementation shall support one company with multiple warehouses. Independent multi-tenant company hosting shall remain outside the initial scope unless additional requirements authorize it.

Company-level master data shall be shared where appropriate, while warehouse-specific inventory, locations, orders, tasks, and operational transactions shall be associated with their respective warehouses.

### Organizational Structure

```text
Company
|
+-- Shared Master Data
|   +-- Items
|   +-- Suppliers
|   +-- Customers / Stores
|
+-- Warehouse A
|   +-- Receiving Doors
|   +-- Storage Locations
|   +-- Picking Zones
|   +-- Shipping Doors
|   +-- Inventory
|   +-- Operational Transactions
|
+-- Warehouse B
    +-- Receiving Doors
    +-- Storage Locations
    +-- Picking Zones
    +-- Shipping Doors
    +-- Inventory
    +-- Operational Transactions
```

### Data Relationships

| Entity | Relationship |
|---|---|
| Company | Owns one or more warehouses. |
| Warehouse | Belongs to one company. |
| Storage Location | Belongs to one warehouse. |
| Item | Maintained as company-level master data. |
| Supplier | Maintained as company-level master data. |
| Customer / Store | Maintained as company-level master data. |
| Inventory | Associated with an item and a warehouse storage location. |
| Supplier Order | Identifies the destination warehouse. |
| Customer Order | Identifies the warehouse responsible for fulfillment. |
| Inventory Transaction | Identifies the warehouse in which the transaction occurs. |
| User Warehouse Assignment | Associates an authorized user with one or more warehouses. |

### Architectural Rules

- Every warehouse shall have a unique identifier.
- Every storage location shall belong to exactly one warehouse.
- Inventory quantities shall be maintained separately for each warehouse and storage location.
- Item master data shall not be duplicated unnecessarily across warehouses.
- Warehouse-specific operational records shall include a warehouse identifier or an unambiguous relationship to their warehouse.
- Users shall access warehouse-specific records only when authorized.
- Adding a warehouse shall not require deploying a separate application.
- Cross-warehouse inventory transfers shall not be treated as ordinary movements between bins within the same warehouse.

## Consequences

### Positive

- Supports future warehouse expansion.
- Reduces unnecessary duplication of master data.
- Provides consistent business rules across warehouses.
- Simplifies centralized administration and reporting.
- Supports accurate warehouse-specific inventory tracking.
- Reduces infrastructure and maintenance costs.

### Negative / Tradeoffs

- Warehouse-specific authorization must be enforced consistently.
- Database relationships and queries require careful warehouse scoping.
- A centralized application failure may affect multiple warehouses.
- Shared master data changes may affect operations across multiple warehouses.
- Future support for independent tenant companies may require additional isolation mechanisms.

## Alternatives Considered

| Option | Why not |
|---|---|
| Separate application for each warehouse | Increases deployment, maintenance, and integration complexity. |
| Separate database for each warehouse | Makes shared master data and company-wide reporting more difficult. |
| Single warehouse without warehouse identifiers | Does not support future warehouse expansion. |
| Full multi-tenant SaaS architecture | Introduces complexity beyond the established initial business requirements. |

## Related Artifacts

- [Warehouse Project Overview](../../README.md)
- [Feature Specifications](../../features/)
- [Nonfunctional Requirements](../nfr/)
- [Architecture Diagrams](../Arch_Diagrams/)
- [ADR-0003: Relational Database](./0003-relational-database.md)
- [ADR-0004: Role-Based Access Control](./0004-role-based-access.md)
- [ADR-0008: Cross-Warehouse Data Isolation](./0008-cross-warehouse-data-isolation.md)

## Verification

The architectural decision shall be verified through the following scenarios:

- Creating an additional warehouse without deploying a separate application.
- Maintaining separate inventory quantities for the same item in different warehouses.
- Assigning storage locations to their respective warehouses.
- Sharing authorized company-level master data across warehouses.
- Preventing unauthorized access to another warehouse's operational records.
- Generating warehouse-specific and authorized company-wide reports.