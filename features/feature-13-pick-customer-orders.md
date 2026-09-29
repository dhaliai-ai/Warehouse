# Feature: Pick Customer Orders

**Feature ID:** 13  
**Branch pattern:** `feature/13-pick-customer-orders`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system assists a picker in picking items for a Customer Order by directing the worker through warehouse locations, identifying the item and quantity to pick, verifying locations and products by scanning, and recording the quantity actually picked.

---

## User Stories

### US-13.1: Start Picking a Customer Order

**As a** picker  
**I want to** receive a Customer Order that is ready to be picked  
**So that** I know which order I am responsible for picking

**Priority:** P1  
**Independent test:** Start the picking process and confirm that the system identifies a Customer Order ready for picking.

### US-13.2: Follow Picking Sequence

**As a** picker  
**I want to** receive picking instructions in an efficient sequence  
**So that** I can move through the warehouse efficiently

**Priority:** P1  
**Independent test:** Begin picking an order and confirm that the system provides the item, Warehouse Location, and quantity to pick.

### US-13.3: Verify Pick Location and Product

**As a** picker  
**I want to** scan the location and product during picking  
**So that** the system can verify that I am picking the correct product from the correct location

**Priority:** P1  
**Independent test:** Scan the Warehouse Location and product and confirm that the system verifies them against the Picking Instruction.

### US-13.4: Record Quantity Picked

**As a** picker  
**I want to** record the quantity actually picked  
**So that** the system knows whether the Customer Order was completely or partially picked

**Priority:** P1  
**Independent test:** Record the quantity actually picked and confirm that the system keeps it separate from Quantity Ordered.

### US-13.5: Record Picking Shortage

**As a** picker  
**I want to** record when the required quantity is not available at the location  
**So that** the shortage is recorded electronically instead of on a paper pick ticket

**Priority:** P1  
**Independent test:** Attempt to pick more product than is available and confirm that the actual Quantity Picked can be recorded.

---

## Functional Requirements

- **FR-001:** The system MUST identify Customer Orders that are ready for picking.
- **FR-002:** The system MUST provide the picker with instructions for picking the Customer Order.
- **FR-003:** The system MUST determine the sequence in which items should be picked.
- **FR-004:** Each Picking Instruction MUST identify the Individual Item, Warehouse Location, and quantity to pick.
- **FR-005:** The system MUST direct the picker to the next Warehouse Location in the picking sequence.
- **FR-006:** The system MUST allow the picker to scan the Warehouse Location to verify that the correct location has been reached.
- **FR-007:** The system MUST allow the picker to scan the product to verify that the correct Individual Item is being picked.
- **FR-008:** The system MUST identify when the scanned Warehouse Location or product does not match the Picking Instruction.
- **FR-009:** The system MUST record Quantity Picked for each item.
- **FR-010:** The system MUST keep Quantity Picked separate from Quantity Ordered.
- **FR-011:** The system MUST allow the picker to record the actual Quantity Picked when the full required quantity is not available.
- **FR-012:** The system MUST identify a difference between Quantity Ordered and Quantity Picked.
- **FR-013:** After a picking step is completed, the system MUST provide the next Picking Instruction when more items remain.
- **FR-014:** The system MUST identify when picking for the Customer Order has been completed.
- **FR-015:** Picking information MUST be recorded electronically rather than requiring a paper pick ticket.
- **FR-016:** The exact method used to determine the most efficient picking sequence is **TBD**.
- **FR-017:** The exact process for handling or replenishing Inventory when a picking shortage occurs is **TBD**.
- **FR-018:** Behavior when a Warehouse Location or product barcode cannot be scanned or read is **TBD**.
- **FR-019:** Behavior when no Customer Orders are ready for picking is **TBD**.
- **FR-020:** How a Customer Order that is only partially picked is represented is **TBD**.

---

## Key Entities

- **Picking Assignment:** A Customer Order that is ready to be picked.
- **Picking Instruction:** A step in the system-directed picking sequence.
- **Customer Order:** An order received from a Customer and ready for picking.
- **Customer Order Item:** An Individual Item requested on a Customer Order with Quantity Ordered and Quantity Picked.
- **Warehouse Location:** A location where Inventory is stored and picked.
- **Inventory:** The quantity of an Individual Item in a Warehouse Location.
- **Individual Item:** A product included in a Customer Order.

---

## Initial Data Model

### Picking Assignment

Represents a Customer Order that is ready to be picked.

**Attributes:**
- [TBD: Assignment identifier]
- Status [exact values TBD]

**Relationships:**
- A Picking Assignment is associated with a Customer Order.
- A Picking Assignment contains one or more Picking Instructions.
- A picker performs the Picking Assignment.

### Picking Instruction

Represents one step in the system-directed picking sequence.

**Attributes:**
- Individual Item
- Quantity to Pick
- Quantity Picked
- Warehouse Location
- Sequence Order

**Relationships:**
- A Picking Assignment contains one or more Picking Instructions.
- Each Picking Instruction refers to an Individual Item.
- Each Picking Instruction directs the picker to a Warehouse Location.
- Quantity Picked is recorded separately from Quantity Ordered.

### Customer Order

Represents an order received from a Customer.

**Relevant Attributes:**
- [TBD: Customer Order identifier]
- Status [exact values TBD]

**Relationships:**
- A Customer Order contains one or more Customer Order Items.
- A Customer Order may become a Picking Assignment when it is ready for picking.

### Customer Order Item

Represents an Individual Item requested on a Customer Order.

**Attributes:**
- Individual Item
- Quantity Ordered
- Quantity Picked

**Relationships:**
- A Customer Order contains one or more Customer Order Items.
- Each Customer Order Item refers to an Individual Item.
- Quantity Picked is compared with Quantity Ordered during picking.

### Warehouse Location

Represents a location where Inventory is stored and picked.

**Relevant Attributes:**
- [TBD: Location identifier]
- [TBD: Scannable bin/location identifier]

**Relationships:**
- A Warehouse Location contains Inventory.
- A Picking Instruction directs the picker to a Warehouse Location.
- The picker scans the location to verify that the correct location has been reached.

### Inventory

Represents an Individual Item quantity in a Warehouse Location.

**Attributes:**
- Individual Item
- Warehouse Location
- Quantity

**Relationships:**
- Inventory is associated with an Individual Item.
- Inventory is associated with a Warehouse Location.
- Available Inventory affects the quantity that can be picked.

### Individual Item

Represents a product included in a Customer Order.

**Relevant Attributes:**
- SKU / Item Number
- UPC
- Description

**Relationships:**
- An Individual Item may appear on multiple Customer Orders.
- An Individual Item may exist as Inventory in one or more Warehouse Locations.
- The product can be scanned during picking to verify that the correct item is being picked.

---

## Gherkin AC

### US-13.1: Start Picking a Customer Order

#### AC-13.1.1: Customer Order is ready for Picking

**Given** a Customer Order is ready for picking  
**When** the picker starts the picking process  
**Then** the system identifies a Customer Order that is ready to be picked

### US-13.2: Follow Picking Sequence

#### AC-13.2.1: System provides first Picking Instruction

**Given** the picker has started picking a Customer Order  
**When** the picking process begins  
**Then** the system determines the picking sequence  
**And** provides the Individual Item, Warehouse Location, and quantity to pick

#### AC-13.2.2: System provides next Picking Instruction

**Given** the picker has completed a picking step  
**And** more items remain to be picked  
**When** the picking process continues  
**Then** the system provides the next Picking Instruction

### US-13.3: Verify Pick Location and Product

#### AC-13.3.1: Correct Location is scanned

**Given** the system has directed the picker to a Warehouse Location  
**When** the picker scans the expected location  
**Then** the system verifies that the picker is at the correct location

#### AC-13.3.2: Incorrect Location is scanned

**Given** the system has directed the picker to a Warehouse Location  
**When** the picker scans a different location  
**Then** the system identifies that the scanned location does not match the Picking Instruction

#### AC-13.3.3: Correct Product is scanned

**Given** the picker is at the correct Warehouse Location  
**When** the picker scans the expected product  
**Then** the system verifies that the correct Individual Item is being picked

#### AC-13.3.4: Incorrect Product is scanned

**Given** the picker is at the correct Warehouse Location  
**When** the picker scans a different product  
**Then** the system identifies that the scanned product does not match the Picking Instruction

#### AC-13.3.5: Barcode cannot be read

**Given** the picker attempts to scan a Warehouse Location or product  
**When** the barcode cannot be read  
**Then** [TBD: behavior not specified in the interview or class notes]

### US-13.4: Record Quantity Picked

#### AC-13.4.1: Full Quantity is picked

**Given** the required quantity is available  
**When** the picker records Quantity Picked  
**Then** the system records Quantity Picked separately from Quantity Ordered

#### AC-13.4.2: Picking Step is completed

**Given** the picker has verified the correct Warehouse Location and product  
**And** recorded Quantity Picked  
**When** the picking step is completed  
**Then** the system saves the picking information  
**And** provides the next Picking Instruction when more items remain

#### AC-13.4.3: Customer Order Picking is completed

**Given** all required picking steps for the Customer Order have been completed  
**When** the final picking step is confirmed  
**Then** the system completes the picking process for that Customer Order

### US-13.5: Record Picking Shortage

#### AC-13.5.1: Available Quantity is less than required

**Given** the available quantity at the picking location is less than the required quantity  
**When** the picker records the actual Quantity Picked  
**Then** the system records the actual Quantity Picked  
**And** identifies the difference between Quantity Ordered and Quantity Picked

#### AC-13.5.2: No Product is available

**Given** no product is available at the expected picking location  
**When** the picker records that no quantity was picked  
**Then** the system records the shortage electronically

#### AC-13.5.3: Shortage requires Replenishment

**Given** a picking shortage has been identified  
**When** additional Inventory may be needed  
**Then** [TBD: replenishment process not specified in the interview or class notes]