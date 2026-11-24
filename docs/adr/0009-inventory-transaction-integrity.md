# ADR-0009: Inventory Transaction Integrity

**Status:** Proposed\
**Date:** 2026-11-23\
**Deciders:** Warehouse System Design Team

## Context

The Warehouse Management System manages inventory through receiving, putaway, picking, inventory movement, shipping, and authorized inventory adjustments.

Multiple warehouse employees may perform operations simultaneously. Incorrect or incomplete inventory updates could result in inaccurate quantities, duplicate transactions, missing inventory, and incorrect customer order fulfillment.

For example, when inventory is moved from one storage location to another, the quantity must be removed from the original location and added to the destination location. If only one operation succeeds, the inventory records become inconsistent.

The system requires a reliable mechanism to maintain accurate, consistent, and traceable inventory records.

## Decision

The system shall use relational database transactions to maintain inventory integrity.

Related inventory updates shall be executed as a single atomic transaction. If any required operation fails, the entire transaction shall be rolled back.

The backend shall validate inventory operations before committing changes to the database.

Inventory-changing operations shall maintain an audit trail identifying the responsible user, warehouse, affected item, quantity, operation type, and transaction date and time.

### Inventory Operations

Stored bin Inventory is the quantity of an Item at a Warehouse Location (Feature 3). Quantity Ordered, Quantity Received, Quantity Picked, Quantity Shipped, and Quantity Delivered are separate (Feature 3 **FR-029**).

| Operation | Stored bin Inventory impact | Source |
|---|---|---|
| Receiving | Records Quantity Received. Does **not** increase stored bin Inventory. | Feature 10; Feature 3 Input and **EC-004** |
| Putaway | Confirmed Putaway Movement **increases** stored Inventory at the destination location. Quantity Received is unchanged. | Feature 11; Feature 3 **FR-046** |
| Inventory movement | Intra-warehouse movement **decreases** the source location and **increases** the destination location by the same quantity. Inter-warehouse transfers are not ordinary bin movements and remain unresolved (Feature 3 **A-017**). | Feature 3 |
| Picking | Successful pick confirmation **decreases** stored Inventory at the verified source Warehouse Location and increases Quantity Picked by the same amount. | Feature 13 **FR-026**, **FR-027** |
| Shipping | Records Quantity Shipped. Does **not** deduct stored Inventory again. | Feature 14 |
| Inventory adjustment | Authorized correction of stored Inventory, with history. A physical count does not automatically change the balance. | Feature 3 |
| Delivery confirmation | Updates Quantity Delivered and delivery status. Does **not** deduct stored Inventory a second time. | Feature 15; Feature 3 **FR-029** |

Whether picked units occupy a separate staging-location Inventory balance is **not** specified. Feature 13 decreases the source location and does not require a staging-location increase. This ADR does not invent staging inventory.

Inventory updates shall follow the business rules defined in the corresponding feature specifications. Feature specifications take precedence if an architecture sketch conflicts with an **FR-00N**.

### Transaction Integrity Rules

- Related inventory updates shall succeed or fail together.
- Failed transactions shall not leave partially updated inventory records.
- Inventory quantities shall not become negative unless explicitly authorized by a documented business rule.
- The backend shall validate item identifiers, warehouse identifiers, storage locations, and quantities.
- Inventory movements shall validate both source and destination locations.
- Concurrent inventory updates shall use appropriate database locking or concurrency controls.
- Repeated submissions of the same inventory operation shall not create duplicate inventory changes.
- Inventory adjustments shall require appropriate authorization.
- Inventory discrepancies shall be recorded and resolved according to the applicable feature requirements.
- Inventory records shall remain associated with the correct warehouse.
- Successful inventory changes shall be traceable through transaction history.

### Transaction Processing

1. Authenticate the user.
2. Verify the user's role and warehouse authorization.
3. Validate the requested inventory operation.
4. Begin a database transaction.
5. Check the current inventory quantities using appropriate concurrency controls.
6. Apply the required inventory changes.
7. Record the inventory transaction history.
8. Commit the transaction if all operations succeed.
9. Roll back the transaction if any required operation fails.
10. Return the operation result to the user.

## Consequences

### Positive

- Improves inventory accuracy and consistency.
- Prevents partially completed inventory movements.
- Reduces duplicate inventory transactions.
- Supports reliable concurrent warehouse operations.
- Improves accountability through transaction history.
- Supports investigation and reconciliation of inventory discrepancies.
- Reduces the risk of incorrect order fulfillment.

### Negative / Tradeoffs

- Database transaction management increases implementation complexity.
- Concurrent operations may experience temporary delays due to database locking.
- Transaction history requires additional database storage.
- Additional integration and concurrency testing is required.
- Failed transactions require appropriate error handling and recovery procedures.

## Alternatives Considered

| Option | Why not |
|---|---|
| Independent database updates without transactions | Failed operations could leave inventory records inconsistent. |
| Frontend-only inventory validation | Cannot reliably prevent concurrent updates or unauthorized API operations. |
| Manual inventory reconciliation as the primary approach | Increases human error and delays the identification of inventory discrepancies. |
| Inventory updates without transaction history | Reduces accountability and makes discrepancy investigation difficult. |

## Related Artifacts

- [ADR-0003: Relational Database](./0003-relational-database.md)
- [ADR-0007: Company and Multi-Warehouse Architecture](./0007-company-multi-warehouse.md)
- [ADR-0008: Cross-Warehouse Data Isolation](./0008-cross-warehouse-data-isolation.md)
- [Feature Specifications](../../features/)
- [Warehouse Domain Model](../warehouse-domain-model.md)
- [Quality Attributes](../nfr/quality-attributes.md)
- [Architecture Diagrams](../Arch_Diagrams/)

## Verification

The architectural decision shall be verified through the following scenarios:

- A successful inventory movement decreases the source quantity and increases the destination quantity correctly.
- A failed inventory movement leaves both inventory quantities unchanged.
- Concurrent inventory operations do not produce incorrect or unauthorized negative quantities.
- Repeated submission of the same transaction does not modify inventory more than once.
- Unauthorized inventory adjustments are rejected.
- Inventory transactions cannot modify records belonging to unauthorized warehouses.
- Successful inventory changes include the required transaction history.
- Failed transactions do not leave partially updated records.
- Delivery confirmation does not deduct stored Inventory a second time.
- Shipping finalization does not deduct stored Inventory that was already decreased at pick confirmation.
- Receiving completion does not increase stored bin Inventory until Putaway is confirmed.
- Inventory discrepancies can be investigated using recorded transaction history.