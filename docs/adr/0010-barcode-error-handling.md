# ADR-0010: Barcode Error Handling and Device Reliability

**Status:** Proposed\
**Date:** 2026-11-23\
**Deciders:** Warehouse System Design Team

## Context

The Warehouse Management System uses barcode scanning to support receiving, putaway, picking, inventory movement, and other warehouse operations.

Warehouse employees rely on handheld devices to identify items, cases, and storage locations accurately.

Damaged barcodes, incorrect scans, duplicate submissions, network interruptions, and device failures may disrupt warehouse operations or cause inaccurate inventory records.

The system must handle these situations without silently losing confirmed transactions or introducing incorrect inventory quantities.

## Decision

The system shall use backend barcode validation, immediate user feedback, controlled transaction retries, and database transaction protection.

Barcode-based operations shall be validated against the current warehouse, item information, storage location, and applicable operational task.

The initial implementation shall use an online-first approach. Inventory-changing operations shall require successful backend confirmation before being displayed as completed.

Full offline transaction processing and synchronization are outside the initial scope unless authorized by additional feature requirements.

## Barcode Validation

The backend shall validate the following information where applicable:

- Barcode format.
- Item or case identification.
- Storage location identification.
- Warehouse association.
- Expected item for the current operation.
- Quantity associated with the scanned item or case.
- User authorization.
- Current operational task status.

## Error Handling

| Error or Condition | System Response |
|---|---|
| Unknown barcode | Reject the scan and display an understandable error message. |
| Damaged or unreadable barcode | Allow the employee to retry or follow the authorized exception procedure. |
| Incorrect item scanned | Reject the operation and identify the mismatch. |
| Incorrect storage location | Reject the operation and request the correct location. |
| Barcode associated with another warehouse location | Reject the operation. |
| Duplicate transaction submission | Prevent the same operation from modifying inventory more than once. |
| Network interruption | Inform the user that confirmation is unavailable and preserve the pending operation where possible. |
| Server error | Display an error and prevent an unconfirmed operation from appearing successful. |
| Device failure | Allow the employee to recover confirmed task progress after reconnecting or signing in again. |

## Transaction Retry and Duplicate Prevention

Inventory-changing requests shall include a unique operation identifier.

The backend shall use this identifier to distinguish a retry of an existing operation from a new intentional operation.

If an employee scans the same item multiple times intentionally, each valid scan may represent a separate operation according to the applicable feature requirements.

If a network interruption causes the same request to be submitted again, the system shall not apply the inventory change more than once.

A successful operation shall return a confirmation to the handheld device.

If confirmation is lost, the device shall verify the operation status or retry using the original operation identifier before creating a new transaction.

## Handheld Device Reliability

- The interface shall provide clear scan confirmation and error messages.
- Warehouse employees shall be informed when network connectivity is unavailable.
- Unconfirmed operations shall not be displayed as successfully completed.
- Confirmed inventory transactions shall remain stored in the centralized database.
- Employees shall be able to recover confirmed task progress after reconnecting.
- Device failures shall not corrupt committed inventory records.
- Handheld interfaces shall remain consistent with the approved warehouse screen designs.
- Barcode validation shall be performed by the backend rather than relying exclusively on the handheld device.

## Consequences

### Positive

- Reduces inventory errors caused by incorrect barcode scans.
- Prevents duplicate inventory updates caused by repeated requests.
- Improves reliability during network interruptions.
- Provides understandable feedback to warehouse employees.
- Protects confirmed inventory transactions from device failures.
- Supports accurate and traceable warehouse operations.

### Negative / Tradeoffs

- Additional backend validation increases implementation complexity.
- Unique operation identifiers require additional transaction management.
- Network connectivity is required to confirm inventory-changing operations.
- Warehouse operations may be temporarily delayed during connectivity failures.
- Additional testing is required for barcode errors, duplicate requests, and device interruptions.

## Alternatives Considered

| Option | Why not |
|---|---|
| Accept all barcode scans without validation | Could introduce incorrect inventory records and fulfillment errors. |
| Frontend-only barcode validation | Cannot reliably enforce business rules or warehouse authorization. |
| Automatically retry every failed request as a new operation | Could create duplicate inventory transactions. |
| Full offline processing and synchronization | Introduces additional synchronization and conflict-resolution complexity beyond the initial requirements. |
| Paper-based processing as the primary workflow | Conflicts with the objective of reducing paper-dependent warehouse operations. |

## Related Artifacts

- [ADR-0005: Barcode Scanning](./0005-barcode-scanning.md)
- [ADR-0006: Paperless Workflows](./0006-paperless-workflows.md)
- [ADR-0007: Company and Multi-Warehouse Architecture](./0007-company-multi-warehouse.md)
- [ADR-0008: Cross-Warehouse Data Isolation](./0008-cross-warehouse-data-isolation.md)
- [ADR-0009: Inventory Transaction Integrity](./0009-inventory-transaction-integrity.md)
- [Feature Specifications](../../features/)
- [Quality Attributes](../nfr/quality-attributes.md)
- [User Interface Designs](../ui/)

## Verification

The architectural decision shall be verified through the following scenarios:

- A valid barcode is accepted during an authorized warehouse operation.
- An unknown barcode is rejected without modifying inventory.
- An incorrect item or storage location produces an understandable error message.
- An unauthorized warehouse location is rejected.
- Repeated submission of the same operation does not create duplicate inventory changes.
- Multiple intentional scans of the same item are processed according to the applicable feature requirements.
- A network interruption does not cause an unconfirmed operation to appear completed.
- A lost confirmation can be recovered without applying the inventory change twice.
- Confirmed task progress remains available after a device reconnects.
- Device failures do not corrupt committed inventory records.