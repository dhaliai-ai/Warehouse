# Feature: Receive Supplier Order

**Feature ID:** 10  
**Branch pattern:** `feature/10-receive-supplier-order`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system assists a warehouse worker in receiving a Supplier Order by identifying the order from the PO number, recording the receiving door, scanning received items and quantities, and comparing what was ordered with what was actually received.

---

## User Stories

### US-10.1: Identify Supplier Order

**As a** receiving worker  
**I want to** enter the PO number from the bill of lading  
**So that** the system can identify the Supplier Order being received

**Priority:** P1  
**Independent test:** Enter a PO number from the bill of lading and confirm that the correct Supplier Order is identified.

### US-10.2: Record Receiving Location

**As a** receiving worker  
**I want to** identify the receiving door where the shipment was unloaded  
**So that** Put Away workers can locate the received order

**Priority:** P1  
**Independent test:** Record a receiving door for a Supplier Order and confirm that the location is associated with the received order.

### US-10.3: Scan Received Items

**As a** receiving worker  
**I want to** scan the items received from the Supplier  
**So that** the system can accurately record what was received

**Priority:** P1  
**Independent test:** Scan received items and confirm that the system records the items and Quantity Received.

### US-10.4: Reconcile Ordered and Received Quantities

**As a** receiving worker  
**I want to** see differences between Quantity Ordered and Quantity Received  
**So that** I can investigate and confirm discrepancies before completing receiving

**Priority:** P1  
**Independent test:** Receive a quantity different from the Quantity Ordered and confirm that the system identifies the difference.

---

## Functional Requirements

- **FR-001:** The system MUST allow a receiving worker to enter the PO number from the bill of lading.
- **FR-002:** The system MUST use the PO number to identify the Supplier Order being received.
- **FR-003:** The system MUST allow the receiving worker to identify the receiving door where the shipment was unloaded.
- **FR-004:** The system MUST associate the receiving door with the received Supplier Order so the order can later be located for Put Away.
- **FR-005:** The system MUST allow the receiving worker to scan received items.
- **FR-006:** The system MUST record the Quantity Received for each item.
- **FR-007:** The system MUST keep Quantity Received separate from Quantity Ordered.
- **FR-008:** The system MUST compare Quantity Received with Quantity Ordered.
- **FR-009:** The system MUST identify differences between Quantity Ordered and Quantity Received.
- **FR-010:** The system MUST allow the receiving worker to continue scanning if a missing item or case is found while investigating a discrepancy.
- **FR-011:** The system MUST allow the receiving worker to confirm a discrepancy when the actual Quantity Received is different from Quantity Ordered.
- **FR-012:** The system MUST record that receiving has been completed after the worker finishes scanning and reviewing discrepancies.
- **FR-013:** Received items MUST remain available for the separate Put Away process after receiving is completed.
- **FR-014:** The exact Supplier Order status values used during and after receiving are **TBD**.
- **FR-015:** Behavior when a PO number does not identify an existing Supplier Order is **TBD**.
- **FR-016:** Behavior when an item is scanned that is not on the Supplier Order is **TBD**.
- **FR-017:** Behavior when a barcode cannot be read or does not identify an item is **TBD**.
- **FR-018:** Whether receiving can be completed without a Receiving Door is **TBD**.
- **FR-019:** Handling of partially received Supplier Orders is **TBD**.
- **FR-020:** The exact handling of case UPCs, individual UPCs, and quantities contained in a case is **TBD**.

---

## Key Entities

- **Supplier Order:** An order previously placed with a Supplier and identified during receiving.
- **Supplier Order Item:** An Individual Item on the Supplier Order with Quantity Ordered and Quantity Received.
- **Receiving Record:** Information recorded while a Supplier Order is being received.
- **Individual Item:** A product received from a Supplier.
- **Receiving Door:** The warehouse location where the incoming shipment was unloaded and waits for Put Away.

---

## Initial Data Model

### Supplier Order

Represents an order previously placed with a Supplier.

**Relevant Attributes:**
- PO Number
- Status [exact values TBD]

**Relationships:**
- A Supplier Order is associated with a Supplier.
- A Supplier Order contains one or more Supplier Order Items.
- A Supplier Order may have receiving information after the shipment arrives.

### Supplier Order Item

Represents an Individual Item included in a Supplier Order.

**Attributes:**
- Individual Item
- Quantity Ordered
- Quantity Received

**Relationships:**
- A Supplier Order contains one or more Supplier Order Items.
- Each Supplier Order Item refers to an Individual Item.
- Quantity Received is compared with Quantity Ordered during receiving.

### Receiving Record

Represents information recorded when a Supplier Order is received.

**Attributes:**
- Receiving Door
- [TBD: other receiving information]

**Relationships:**
- A Receiving Record is associated with a Supplier Order.
- The Receiving Record identifies where the received order is waiting for Put Away.
- Received items and quantities are recorded as part of the receiving process.

### Individual Item

Represents a product received from a Supplier.

**Relevant Attributes:**
- SKU / Item Number
- UPC
- [TBD: Case UPC]
- [TBD: Quantity contained in a case]

**Relationships:**
- An Individual Item may appear on multiple Supplier Orders.
- An Individual Item may have a Quantity Ordered and Quantity Received for a Supplier Order.

### Receiving Door

Represents the warehouse receiving location where an incoming shipment is unloaded and waits for Put Away.

**Attributes:**
- [TBD: Receiving Door identifier]

**Relationships:**
- A received Supplier Order is associated with a Receiving Door.
- Put Away workers use the Receiving Door to locate received items.

---

## Gherkin AC

### US-10.1: Identify Supplier Order

#### AC-10.1.1: Valid PO Number identifies Supplier Order

**Given** a Supplier Order already exists in the system  
**When** the receiving worker enters the PO number from the bill of lading  
**Then** the system identifies the corresponding Supplier Order

#### AC-10.1.2: PO Number does not identify an order

**Given** the receiving worker enters a PO number that does not identify an existing Supplier Order  
**When** the system attempts to find the order  
**Then** [TBD: behavior not specified in the interview or class notes]

### US-10.2: Record Receiving Location

#### AC-10.2.1: Receiving Door is recorded

**Given** a shipment has arrived at a Receiving Door  
**When** the receiving worker identifies the Receiving Door  
**Then** the system associates that Receiving Door with the Supplier Order

#### AC-10.2.2: Receiving location is available for Put Away

**Given** receiving has been completed for a Supplier Order  
**When** the order becomes available for Put Away  
**Then** the Receiving Door is available so the Put Away worker can locate the order

### US-10.3: Scan Received Items

#### AC-10.3.1: Received item is scanned

**Given** the correct Supplier Order has been identified  
**When** the receiving worker scans an item  
**Then** the system identifies the item  
**And** records its Quantity Received

#### AC-10.3.2: Multiple items are received

**Given** a Supplier Order contains multiple items  
**When** the receiving worker scans the received items  
**Then** the system records the Quantity Received for each item

#### AC-10.3.3: Unknown or unreadable item

**Given** an item's barcode cannot be read or does not identify an expected item  
**When** the receiving worker attempts to scan it  
**Then** [TBD: behavior not specified in the interview or class notes]

### US-10.4: Reconcile Ordered and Received Quantities

#### AC-10.4.1: Received quantity matches Ordered quantity

**Given** Quantity Received equals Quantity Ordered  
**When** the receiving worker reviews the received order  
**Then** the system shows no quantity discrepancy for that item

#### AC-10.4.2: Received quantity is less than Ordered quantity

**Given** Quantity Received is less than Quantity Ordered  
**When** the receiving worker reviews the received order  
**Then** the system identifies the quantity difference for investigation

#### AC-10.4.3: Received quantity is greater than Ordered quantity

**Given** Quantity Received is greater than Quantity Ordered  
**When** the receiving worker reviews the received order  
**Then** the system identifies the quantity difference for investigation

#### AC-10.4.4: Missing item is found during investigation

**Given** the system identifies a receiving discrepancy  
**And** the receiving worker finds an item or case that was not previously scanned  
**When** the worker scans the additional item or case  
**Then** the system updates Quantity Received  
**And** recalculates the difference

#### AC-10.4.5: Actual discrepancy is confirmed

**Given** Quantity Received still differs from Quantity Ordered after investigation  
**When** the receiving worker confirms that the difference is correct  
**Then** the system records the received quantities  
**And** allows the receiving process to be completed

#### AC-10.4.6: Receiving is completed

**Given** the receiving worker has finished scanning and reviewing discrepancies  
**When** the worker completes the receiving process  
**Then** the Supplier Order is recorded as received  
**And** becomes available for the Put Away process