# ADR-003: Use a Relational Database

**Status:** Proposed  
**Date:** 2026-10-28  
**Project:** Warehouse Management System

## Context

The Warehouse Management System must store and manage structured information about companies, warehouses, suppliers, items, inventory locations, supplier orders, store orders, shipments, deliveries, and users.

These records have relationships. For example, a warehouse contains inventory locations, an order contains order lines, and each order line references an item.

Warehouse operations also require accurate inventory quantities and reliable updates when items are received, moved, picked, or shipped.

## Decision

The Warehouse Management System will use a relational database to store operational data.

The database will organize information into related tables with primary keys and foreign keys.

Database transactions will be used for operations that require multiple related records to be updated consistently.

The Warehouse Backend API will be responsible for accessing and modifying the database. Users will not access the database directly through the frontend.

The specific relational database management system will be selected during implementation.

## Rationale

A relational database is appropriate because the Warehouse Management System manages structured and interconnected information.

Relational databases support data integrity, transactions, relationships between records, and structured queries for reporting.

These capabilities are important for maintaining accurate inventory and order information.

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

- `docs/Arch_Diagrams/Warehouse-C4-Container.png`
- `docs/Arch_Diagrams/Warehouse-C4-Component.png`
- Warehouse feature specifications in `features/`.