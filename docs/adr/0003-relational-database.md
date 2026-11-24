# ADR-0003: Use a Relational Database

**Status:** Proposed\
**Date:** 2026-10-28\
**Deciders:** Warehouse System Design Team\
**Project:** Warehouse Management System

## Context

The Warehouse Management System must store and manage structured information about companies, warehouses, suppliers, items, inventory locations, supplier orders, store orders, shipments, deliveries, and users.

These records have relationships. For example, a warehouse contains inventory locations, an order contains order lines, and each order line references an item.

Warehouse operations also require accurate inventory quantities and reliable updates when items are received, moved, picked, or shipped.

## Decision

The Warehouse Management System will use a relational database to store operational data.

The proposed database is **MySQL** using the **InnoDB** storage engine. The proposed object-relational mapping layer is **Sequelize**, used by the Warehouse Backend API.

The database will organize information into related tables with primary keys and foreign keys.

Database transactions will be used for operations that require multiple related records to be updated consistently.

The Warehouse Backend API will be responsible for accessing and modifying the database. Users will not access the database directly through the frontend.

### Schema and integrity

| Mechanism | Purpose |
|---|---|
| Primary keys | Uniquely identify each company, warehouse, item, order, inventory, and related record. |
| Foreign keys | Preserve relationships such as locations belonging to a warehouse and order lines referencing items. |
| Unique constraints | Prevent duplicate business identifiers, including warehouse identifiers and item numbers, where required. |
| Indexes | Support lookup by identifiers, barcodes, warehouse scope, and operational queries. |
| Schema migrations | Apply controlled schema changes as warehouse features are implemented. |
| Database transactions | Commit related inventory and order updates together, or roll them back together. |

InnoDB is the proposed engine because it supports foreign keys and transactional updates required for inventory movements.

Company and warehouse structure is defined in [ADR-0007](./0007-company-multi-warehouse.md). Warehouse-scoped queries and constraints are defined in [ADR-0008](./0008-cross-warehouse-data-isolation.md). Atomic inventory updates are defined in [ADR-0009](./0009-inventory-transaction-integrity.md).

## Rationale

A relational database is appropriate because the Warehouse Management System manages structured and interconnected information.

Relational databases support data integrity, transactions, relationships between records, and structured queries for reporting.

These capabilities are important for maintaining accurate inventory and order information.

MySQL with InnoDB is suitable for warehouse inventory and order management because quantities, locations, orders, and shipments are strongly related and must change together. Foreign keys keep storage locations associated with the correct warehouse. Transactions prevent a putaway or pick from updating only one side of a quantity movement. Unique constraints and indexes support reliable item, barcode, and order lookups during warehouse operations.

## Consequences

**Positive:**
- Supports relationships between warehouse entities.
- Helps maintain data integrity through database constraints.
- Supports transactions for inventory updates.
- Enables structured reporting and data retrieval.
- Reduces unnecessary data duplication through normalization.

**Negative:**
- Requires careful database schema design.
- Schema changes may require migrations.
- Complex queries may need performance optimization.
- Database administration, backup, and recovery procedures are required.

## Alternatives Considered

**Document-oriented NoSQL database:** Considered but not selected because the initial Warehouse Management System has strongly related entities and requires reliable transactional updates.

**Flat-file storage:** Rejected because it would make relationships, concurrent updates, and data consistency more difficult to manage.

## Related Artifacts

- [Level 2 — Container Diagram](../Arch_Diagrams/Warehouse-C4-Container1.drawio.png)
- [Level 3 — Component Diagram](../Arch_Diagrams/Warehouse-C4-Component.drawio.png)
- [Project README](../../README.md)
- [ADR-0007: Company and Multi-Warehouse Architecture](./0007-company-multi-warehouse.md)
- [ADR-0008: Cross-Warehouse Data Isolation](./0008-cross-warehouse-data-isolation.md)
- [ADR-0009: Inventory Transaction Integrity](./0009-inventory-transaction-integrity.md)
- Warehouse feature specifications in `features/`.
