# Feature: Put Away Received Items

**Feature ID:** 11  
**Branch pattern:** `feature/11-put-away-received-items`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system assists a put-away worker in moving received items from the receiving door to warehouse storage locations by assigning received orders, determining the putaway sequence, directing the worker to each location, verifying locations by scanning, and updating inventory after items are put away.

---

## User Stories

### US-11.1: Select Received Order for Put Away

**As a** put-away worker  
**I want to** receive a Supplier Order that is ready for Put Away  
**So that** I know which received order and receiving door to work from

**Priority:** P1  
**Independent test:** Start Put Away and confirm that the system identifies a received Supplier Order and its receiving location.

### US-11.2: Follow Putaway Sequence

**As a** put-away worker  
**I want to** receive putaway locations in an efficient sequence  
**So that** I can move received items through the warehouse efficiently

**Priority:** P1  
**Independent test:** Accept a received order and confirm that the system provides the next Warehouse Location for Put Away.

### US-11.3: Verify Putaway Location

**As a** put-away worker  
**I want to** scan the destination bin before placing items  
**So that** the system can verify that I am putting the items in the correct location

**Priority:** P1  
**Independent test:** Scan the destination bin and confirm that the system verifies whether it is the expected location.

### US-11.4: Complete Item Putaway

**As a** put-away worker  
**I want to** confirm that items have been placed in the assigned location  
**So that** the system can update Inventory and direct me to the next location

**Priority:** P1  
**Independent test:** Complete a putaway step and confirm that Inventory is updated and the next location is provided when more items remain.

### US-11.5: Request Another Location

**As a** put-away worker  
**I want to** request another location when the assigned location cannot hold all of the product  
**So that** I can complete the Put Away process

**Priority:** P1  
**Independent test:** Indicate that the assigned location cannot hold all of the product and confirm that another location can be requested.

---

## Functional Requirements

- **FR-001:** The system MUST identify received Supplier Orders that are ready for Put Away.
- **FR-002:** The system MUST identify the Receiving Door where the selected received Supplier Order is waiting.
- **FR-003:** The system MUST allow the put-away worker to accept or reject a received order offered for Put Away.
- **FR-004:** After the worker accepts an order, the system MUST determine the sequence in which the received items should be put away.
- **FR-005:** The system MUST direct the worker to the next Warehouse Location in the putaway sequence.
- **FR-006:** The putaway instructions MUST identify the Warehouse Location needed by the worker, such as aisle, row, and slot.
- **FR-007:** The system MUST allow the worker to scan the destination bin to verify that the worker is at the correct location.
- **FR-008:** The system MUST identify when the scanned bin does not match the expected destination location.
- **FR-009:** The system MUST allow the worker to confirm that the assigned items have been placed in the destination location.
- **FR-010:** After Put Away is confirmed, the system MUST update the Inventory quantity at that Warehouse Location.
- **FR-011:** If more items remain to be put away, the system MUST provide the worker with the next location in the putaway sequence.
- **FR-012:** The system MUST allow the worker to request another location when the assigned location cannot hold all of the product.
- **FR-013:** The system MUST identify when all items for the received order have been put away.
- **FR-014:** After an order is completely put away, the worker MUST be able to continue with another received order.
- **FR-015:** The exact method used by the system to determine the most efficient putaway sequence is **TBD**.
- **FR-016:** How the system selects the next order after a worker rejects an offered order is **TBD**.
- **FR-017:** Behavior when no received Supplier Orders are waiting for Put Away is **TBD**.
- **FR-018:** Behavior when a destination bin barcode cannot be scanned or read is **TBD**.
- **FR-019:** How the system selects another Warehouse Location when the assigned location cannot hold all of the product is **TBD**.
- **FR-020:** Behavior when no suitable Warehouse Location is available is **TBD**.

---

## Key Entities

- **Putaway Assignment:** A received Supplier Order assigned or offered to a put-away worker.
- **Putaway Instruction:** A step in the system-determined Put Away sequence.
- **Warehouse Location:** A location where Inventory can be stored and verified by scanning.
- **Inventory:** The quantity of an Individual Item stored in a Warehouse Location.
- **Receiving Door:** The location where a received Supplier Order waits before Put Away.
- **Individual Item:** A product being put away.

---

## Initial Data Model

### Putaway Assignment

Represents a received Supplier Order assigned or offered to a put-away worker.

**Attributes:**
- [TBD: Assignment identifier]
- Status [exact values TBD]

**Relationships:**
- A Putaway Assignment is associated with a received Supplier Order.
- A Putaway Assignment identifies the Receiving Door where the order is waiting.
- A put-away worker may accept or reject the assignment.
- An accepted Putaway Assignment contains one or more Putaway Instructions.

### Putaway Instruction

Represents a step in the system-determined putaway sequence.

**Attributes:**
- Individual Item
- Quantity to Put Away
- Destination Warehouse Location
- Sequence Order

**Relationships:**
- A Putaway Assignment contains one or more Putaway Instructions.
- Each Putaway Instruction refers to an Individual Item.
- Each Putaway Instruction directs the worker to a Warehouse Location.
- Completing a Putaway Instruction updates Inventory at that location.

### Warehouse Location

Represents a location where Inventory can be stored.

**Relevant Attributes:**
- Aisle
- Row
- Slot
- [TBD: Scannable location/bin identifier]

**Relationships:**
- A Warehouse Location may contain Inventory.
- A Warehouse Location can be scanned to verify that the put-away worker has reached the expected destination.
- Another Warehouse Location may be requested when the assigned location cannot hold all of the product.

### Inventory

Represents an Individual Item quantity in a Warehouse Location.

**Attributes:**
- Individual Item
- Warehouse Location
- Quantity

**Relationships:**
- Inventory is associated with an Individual Item.
- Inventory is associated with a Warehouse Location.
- Inventory Quantity is updated when Put Away is confirmed.

### Receiving Door

Represents the location where a received Supplier Order waits before Put Away.

**Relevant Attributes:**
- [TBD: Receiving Door identifier]

**Relationships:**
- A received Supplier Order is associated with a Receiving Door.
- The put-away worker uses the Receiving Door to locate the received order.

### Individual Item

Represents a product being put away.

**Relevant Attributes:**
- SKU / Item Number
- Description

**Relationships:**
- An Individual Item may be included in one or more Putaway Instructions.
- An Individual Item may exist as Inventory in one or more Warehouse Locations.

---

## Gherkin AC

### US-11.1: Select Received Order for Put Away

#### AC-11.1.1: Received Order is available for Put Away

**Given** a Supplier Order has completed the receiving process  
**When** the put-away worker starts the Put Away process  
**Then** the system identifies a received Supplier Order that is waiting for Put Away  
**And** shows the Receiving Door where the order is located

#### AC-11.1.2: Worker accepts the Order

**Given** the system offers a received Supplier Order for Put Away  
**When** the put-away worker accepts the order  
**Then** the system begins the Put Away process for that order

#### AC-11.1.3: Worker rejects the Order

**Given** the system offers a received Supplier Order for Put Away  
**When** the put-away worker rejects the order  
**Then** [TBD: how the system selects or assigns the next order]

### US-11.2: Follow Putaway Sequence

#### AC-11.2.1: System provides first Putaway Location

**Given** the put-away worker has accepted a received Supplier Order  
**When** the Put Away process begins  
**Then** the system determines the putaway sequence  
**And** provides the first Warehouse Location

#### AC-11.2.2: System provides next Putaway Location

**Given** the worker has completed a putaway step  
**And** more items remain to be put away  
**When** the system continues the Put Away process  
**Then** the system provides the next Warehouse Location in the putaway sequence

### US-11.3: Verify Putaway Location

#### AC-11.3.1: Correct Destination Bin is scanned

**Given** the system has directed the worker to a Warehouse Location  
**When** the worker scans the expected destination bin  
**Then** the system verifies that the worker is at the correct location

#### AC-11.3.2: Incorrect Destination Bin is scanned

**Given** the system has directed the worker to a Warehouse Location  
**When** the worker scans a different destination bin  
**Then** the system identifies that the scanned location is not the expected location

#### AC-11.3.3: Destination Barcode cannot be read

**Given** the worker is at the destination location  
**When** the destination barcode cannot be scanned or read  
**Then** [TBD: behavior not specified in the interview or class notes]

### US-11.4: Complete Item Putaway

#### AC-11.4.1: Items are placed in assigned Location

**Given** the worker has verified the correct destination location  
**When** the worker confirms that the items have been put away  
**Then** the system updates the Inventory Quantity at that Warehouse Location

#### AC-11.4.2: More Items remain

**Given** the worker has completed a Putaway Instruction  
**And** more items remain to be put away  
**When** the system continues the Put Away process  
**Then** the system provides the next Warehouse Location

#### AC-11.4.3: All Items are put away

**Given** all Putaway Instructions for the received Supplier Order have been completed  
**When** the final putaway step is confirmed  
**Then** the system completes the Put Away process for that order

### US-11.5: Request Another Location

#### AC-11.5.1: Assigned Location cannot hold all Product

**Given** the worker reaches the assigned Warehouse Location  
**And** the location cannot hold all of the product  
**When** the worker requests another location  
**Then** the system allows another Warehouse Location to be used  
**And** [TBD: how the alternate location is selected]

#### AC-11.5.2: No suitable alternate Location is available

**Given** the assigned location cannot hold all of the product  
**When** another suitable Warehouse Location cannot be identified  
**Then** [TBD: behavior not specified in the interview or class notes]