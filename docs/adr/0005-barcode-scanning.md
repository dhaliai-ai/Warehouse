# ADR-0005: Use Barcode Scanning for Warehouse Operations

**Status:** Proposed\
**Date:** 2026-10-28\
**Deciders:** Warehouse System Design Team\
**Project:** Warehouse Management System

## Context

The Warehouse Management System must support accurate and efficient warehouse operations, including receiving shipments, putting away inventory, picking store orders, and moving items between storage locations.

Warehouse workers need to identify products and storage locations reliably.

Manual entry of item numbers and location identifiers can introduce errors and slow down warehouse operations.

The warehouse requirements emphasize using barcode scanners to verify products, quantities, and storage locations.

## Decision

The Warehouse Management System will support barcode scanning for warehouse operations.

Workers will use compatible scanning devices to identify items and warehouse locations.

The system will support scanning:

- Product UPC barcodes to identify items.
- Case-level barcodes when available.
- Storage bin barcodes to verify locations.
- Relevant order or shipment identifiers when supported by the workflow.

These barcode types are distinct:

| Barcode | Identifies | Quantity meaning |
|---|---|---|
| Individual-item UPC | One sellable unit of an item | One unit, unless the workflow records a separately entered quantity |
| Case-level barcode | A case of an item | Individual units derived from validated item packaging information, such as units per case |
| Storage-location barcode | A warehouse bin, door, or other location | No item quantity; used to verify the location |

A case scan must not assume an unverified quantity. Case quantities must be determined using validated item packaging information maintained with the item. If packaging on a received case differs from the packaging preserved on an order, the difference is handled by the receiving feature rules rather than by silently changing ordered quantities.

During receiving, workers will scan items and enter or confirm received quantities.

During putaway, workers will scan the destination bin to confirm the correct storage location.

During picking, workers will scan items to verify that the correct products are selected.

The Backend API will validate scanned identifiers against warehouse records before accepting operations.

The specific scanner hardware and integration method will be selected during implementation.

Scan errors, unknown barcodes, duplicate submissions, network interruptions, and device recovery are defined in [ADR-0010](./0010-barcode-error-handling.md). This ADR does not add full offline processing.

## Rationale

Barcode scanning was selected because it improves accuracy, reduces manual data entry, and supports efficient warehouse workflows.

It also helps ensure that workers place and retrieve items from the correct locations.

Barcode validation supports inventory accuracy and reduces operational mistakes.

Distinguishing item, case, and location barcodes prevents a location scan from being treated as a product and prevents a case scan from being counted as a single unit.

## Consequences

**Positive:**
- Reduces errors caused by manual item identification.
- Improves receiving, putaway, and picking accuracy.
- Supports faster warehouse operations.
- Helps verify storage locations.
- Provides more reliable inventory transaction records.

**Negative:**
- Requires compatible barcode-scanning devices.
- Damaged or unreadable barcodes may interrupt workflows.
- Scanner connectivity or device failures may affect operations.
- Requires procedures for handling missing or invalid barcodes.
- Case-level and individual-item barcodes must be distinguished correctly.

## Alternatives Considered

**Manual entry of item and location identifiers:** Not selected as the primary approach because it is slower and more error-prone.

**RFID-based tracking:** Considered as a possible future enhancement but not selected for the initial design because barcode scanning aligns with the identified warehouse requirements.

## Related Artifacts

- [Level 3 — Component Diagram](../Arch_Diagrams/Warehouse-C4-Component.drawio.png)
- [ADR-0010: Barcode Error Handling and Device Reliability](./0010-barcode-error-handling.md)
- Receiving, Putaway, Picking, and Inventory Movement feature specifications in `features/`.
