
# Feature: Maintain Inventory

**Feature ID:** 3  
**Branch pattern:** `feature/3-maintain-inventory`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System maintains accurate quantities of individual items in warehouse storage locations. Inventory quantities are updated through receiving, put-away, picking, inventory counting, adjustments, and movement between locations. The system supports multiple warehouses and uses barcode scanning to verify physical storage locations.

---

## User Stories

### US-3.1: Add Inventory

**As a** Warehouse Worker or Inventory Clerk  
**I want to** record inventory for an item in a warehouse location  
**So that** the system accurately tracks where products are stored and how many units are available.

**Priority:** P1  
**Independent test:** Add an inventory record for an existing item and warehouse location, then verify that the item, location, and quantity are saved correctly.

### US-3.2: Edit Inventory

**As an** Inventory Clerk or Warehouse Supervisor  
**I want to** correct an inventory quantity when a physical count identifies a discrepancy  
**So that** the system reflects the actual quantity stored in the warehouse.

**Priority:** P1  
**Independent test:** Adjust an existing inventory quantity after a physical count and verify that the new quantity and adjustment history are recorded.

### US-3.3: Delete Inventory

**As a** Warehouse Supervisor or Administrator  
**I want to** remove an unused inventory record when its quantity is zero and no historical transactions depend on it  
**So that** unnecessary inventory records can be removed without losing business history.

**Priority:** P1  
**Independent test:** Delete an unused inventory record and verify that records with positive quantities or historical dependencies cannot be deleted.

### US-3.4: Count Inventory

**As a** Warehouse Worker  
**I want to** count the physical quantity of an item in a storage location  
**So that** differences between actual inventory and system inventory can be identified.

**Priority:** P1  
**Independent test:** Record a physical count and verify that the system identifies any difference from the recorded quantity.

### US-3.5: Move Inventory

**As a** Warehouse Worker  
**I want to** move inventory from one warehouse location to another  
**So that** products can be relocated while maintaining accurate inventory quantities.

**Priority:** P1  
**Independent test:** Move a specified quantity between two locations and verify that the source and destination quantities are updated correctly.

---

## Functional Requirements

- **FR-001:** The system MUST maintain inventory quantities for individual items stored in warehouse locations.
- **FR-002:** Each inventory record MUST identify an existing Individual Item.
- **FR-003:** Each inventory record MUST identify an existing Warehouse Location.
- **FR-004:** Each Warehouse Location MUST belong to a Warehouse.
- **FR-005:** The system MUST support inventory stored across multiple warehouses.
- **FR-006:** The system MUST assign a unique Inventory ID to each inventory record.
- **FR-007:** Each inventory record MUST maintain the quantity of an item in a specific warehouse location.
- **FR-008:** Inventory quantities MUST be recorded in individual units (eaches).
- **FR-009:** The system MUST prevent negative inventory quantities.
- **FR-010:** The system MUST prevent duplicate inventory balance records for the same item and warehouse location.
- **FR-011:** The system MUST allow authorized personnel to create inventory records for existing items and locations.
- **FR-012:** The system MUST validate inventory information before saving.
- **FR-013:** The system MUST reject invalid inventory information without changing existing records.
- **FR-014:** The system MUST allow authorized personnel to view inventory quantities by item, warehouse, and storage location.
- **FR-015:** The system MUST support physical inventory counting.
- **FR-016:** The system MUST record the actual quantity counted during an inventory count.
- **FR-017:** The system MUST compare the physical count with the recorded inventory quantity.
- **FR-018:** The system MUST identify discrepancies between physical and recorded quantities.
- **FR-019:** The system MUST allow an authorized Inventory Clerk or Warehouse Supervisor to approve or record inventory adjustments.
- **FR-020:** The system MUST record the previous quantity, adjusted quantity, adjustment reason, user, and adjustment date/time.
- **FR-021:** The system MUST support movement of inventory between warehouse locations.
- **FR-022:** The system MUST identify the source location, destination location, item, and quantity for each inventory movement.
- **FR-023:** The system MUST verify warehouse locations through barcode scanning during inventory movement when scanning is available.
- **FR-024:** The system MUST prevent movement of quantities greater than the available quantity at the source location.
- **FR-025:** The system MUST decrease the source inventory quantity and increase the destination inventory quantity when a movement is completed.
- **FR-026:** Inventory movements MUST preserve the total quantity of the item across the affected locations.
- **FR-027:** The system MUST update inventory quantities when received products are successfully put away.
- **FR-028:** The system MUST update inventory quantities when items are picked for customer orders according to the picking workflow.
- **FR-029:** The system MUST maintain inventory quantities separately from Quantity Ordered, Quantity Received, Quantity Picked, Quantity Shipped, and Quantity Delivered.
- **FR-030:** The system MUST prevent deletion of inventory records with quantities greater than zero.
- **FR-031:** The system MUST prevent deletion of inventory records required for historical transactions.
- **FR-032:** The system MUST restrict inventory record deletion to Warehouse Supervisors and Administrators.
- **FR-033:** The system MUST reject attempts to modify or delete nonexistent inventory records.
- **FR-034:** The system MUST maintain inventory adjustment and movement history for accountability.
- **FR-035:** The system MUST prevent unauthorized users from directly modifying inventory quantities.
- **FR-036:** The system MUST maintain the relationship between Inventory, Individual Item, Warehouse Location, and Warehouse.

---

## Key Entities

### Inventory

Represents the recorded quantity of an Individual Item stored in a particular Warehouse Location.

### Individual Item

Represents a product purchased from suppliers and sold to customers.

Item identification, UPCs, descriptions, and other product information are maintained in Feature 4.

### Warehouse

Represents a physical warehouse operated by the company.

The company may operate multiple warehouses, as defined in Feature 2.

### Warehouse Location

Represents a physical storage location or bin within a warehouse.

Warehouse locations are identified through location codes or barcodes.

### Inventory Count

Represents a physical count of an item's quantity in a warehouse location.

### Inventory Adjustment

Represents a correction made to a recorded inventory quantity.

### Inventory Movement

Represents the transfer of inventory from one storage location to another.

### User

Represents the employee performing an inventory operation.

---

## Initial Data Model

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique inventory record identifier; primary key |
| itemId | Integer | Foreign key referencing Individual Item |
| locationId | Integer | Foreign key referencing Warehouse Location |
| quantity | Integer | Recorded item quantity in individual units |

**Relationships:**
- Each Inventory record belongs to one Individual Item.
- Each Inventory record belongs to one Warehouse Location.
- An Individual Item can have inventory in multiple locations.
- A Warehouse Location can contain inventory records.
- The combination of itemId and locationId must be unique.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique item identifier |

**Relationships:**
- One Individual Item can have multiple Inventory records.
- Additional item attributes are defined in Feature 4.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique warehouse identifier |

**Relationships:**
- One Warehouse contains multiple Warehouse Locations.
- Warehouse maintenance is defined in Feature 2.

### Warehouse Location

| Attribute | Type | Description |
|---|---|---|
| locationId | Integer | Unique location identifier |
| warehouseId | Integer | Foreign key referencing Warehouse |
| locationCode | String | Identifier displayed or encoded on the location barcode |
| isActive | Boolean | Indicates whether the location is available for operations |

**Relationships:**
- Each Warehouse Location belongs to one Warehouse.
- One Warehouse Location can have multiple Inventory records for different items.

### Inventory Count

| Attribute | Type | Description |
|---|---|---|
| countId | Integer | Unique inventory count identifier |
| inventoryId | Integer | Inventory record being counted |
| recordedQuantity | Integer | Quantity recorded before the count |
| countedQuantity | Integer | Actual quantity physically counted |
| countedBy | Integer | User who performed the count |
| countedAt | DateTime | Date and time of the count |

**Relationships:**
- Each Inventory Count references an Inventory record.
- Each Inventory Count is associated with a User.

### Inventory Adjustment

| Attribute | Type | Description |
|---|---|---|
| adjustmentId | Integer | Unique adjustment identifier |
| inventoryId | Integer | Inventory record being adjusted |
| previousQuantity | Integer | Quantity before adjustment |
| adjustedQuantity | Integer | Corrected quantity |
| reason | String | Explanation for the adjustment |
| adjustedBy | Integer | User responsible for the adjustment |
| adjustedAt | DateTime | Date and time of the adjustment |

**Relationships:**
- Each Inventory Adjustment references an Inventory record.
- Each adjustment is associated with a User.

### Inventory Movement

| Attribute | Type | Description |
|---|---|---|
| movementId | Integer | Unique movement identifier |
| itemId | Integer | Item being moved |
| sourceLocationId | Integer | Location inventory is moved from |
| destinationLocationId | Integer | Location inventory is moved to |
| quantity | Integer | Number of units moved |
| movedBy | Integer | User performing the movement |
| movedAt | DateTime | Date and time of the movement |

**Relationships:**
- Each Inventory Movement references one Individual Item.
- Each movement has one source and one destination location.
- Each movement is associated with a User.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique user identifier |
| role | String | User authorization role |

**Relationships:**
- Users perform inventory counts, adjustments, and movements.
- Role permissions determine which operations users may perform.

---

## Gherkin AC

### US-3.1: Add Inventory

#### AC-3.1.1: Successfully create Inventory

**Given** an Individual Item exists  
**And** a valid Warehouse Location exists  
**And** the user is authorized to record inventory  
**When** the user creates an Inventory record with a valid nonnegative quantity  
**Then** the system saves the Inventory record  
**And** associates it with the correct Item and Warehouse Location.

#### AC-3.1.2: Reject nonexistent Item

**Given** the requested Individual Item does not exist  
**When** an authorized user attempts to create Inventory for that Item  
**Then** the system rejects the request  
**And** no Inventory record is created.

#### AC-3.1.3: Reject nonexistent Warehouse Location

**Given** an Individual Item exists  
**And** the requested Warehouse Location does not exist  
**When** an authorized user attempts to create Inventory  
**Then** the system rejects the request  
**And** no Inventory record is created.

#### AC-3.1.4: Reject negative Inventory quantity

**Given** an Individual Item and Warehouse Location exist  
**When** an authorized user attempts to create Inventory with a quantity of -5  
**Then** the system rejects the request  
**And** no Inventory record is created.

#### AC-3.1.5: Prevent duplicate Inventory records

**Given** an Inventory record already exists for an Item in a Warehouse Location  
**When** an authorized user attempts to create another Inventory record for the same Item and Location  
**Then** the system rejects the duplicate record  
**And** the original Inventory record remains unchanged.

### US-3.2: Edit Inventory

#### AC-3.2.1: Successfully adjust Inventory

**Given** an Inventory record exists with a recorded quantity of 50  
**And** a physical count confirms that 48 units are present  
**And** the user is authorized to adjust Inventory  
**When** the user records an adjustment to 48 units with a reason  
**Then** the system updates the Inventory quantity to 48  
**And** records the previous quantity, adjusted quantity, user, reason, and date/time.

#### AC-3.2.2: Reject negative Inventory adjustment

**Given** an Inventory record exists with a quantity of 20  
**When** an authorized user attempts to adjust the quantity to -3  
**Then** the system rejects the adjustment  
**And** the Inventory quantity remains 20.

#### AC-3.2.3: Reject unauthorized Inventory adjustment

**Given** an Inventory record exists  
**And** the user is not authorized to adjust Inventory  
**When** the user attempts to modify its quantity  
**Then** the system denies the operation  
**And** the Inventory record remains unchanged.

#### AC-3.2.4: Reject nonexistent Inventory update

**Given** no Inventory record exists with the requested Inventory ID  
**When** an authorized user attempts to update that record  
**Then** the system rejects the request  
**And** no Inventory quantity is changed.

### US-3.3: Delete Inventory

#### AC-3.3.1: Successfully delete unused Inventory

**Given** an Inventory record exists with a quantity of zero  
**And** no historical transactions depend on the record  
**And** the user is authenticated as a Warehouse Supervisor or Administrator  
**When** the user requests deletion  
**Then** the system deletes the Inventory record.

#### AC-3.3.2: Prevent deletion of Inventory with positive quantity

**Given** an Inventory record exists with a quantity of 15  
**And** the user is authenticated as a Warehouse Supervisor  
**When** the user requests deletion  
**Then** the system rejects the deletion  
**And** the Inventory quantity remains 15.

#### AC-3.3.3: Prevent deletion when history exists

**Given** an Inventory record is referenced by historical transactions  
**And** the user is authenticated as an Administrator  
**When** the user requests deletion  
**Then** the system rejects the request  
**And** the Inventory record and its history remain unchanged.

#### AC-3.3.4: Reject unauthorized deletion

**Given** an Inventory record exists  
**And** the user is authenticated as a Driver  
**When** the user attempts to delete the Inventory record  
**Then** the system denies the operation  
**And** the Inventory record remains unchanged.

#### AC-3.3.5: Reject deletion of nonexistent Inventory

**Given** no Inventory record exists with the requested Inventory ID  
**When** an authorized user attempts to delete that record  
**Then** the system rejects the request  
**And** no Inventory record is changed.

### US-3.4: Count Inventory

#### AC-3.4.1: Record matching physical count

**Given** an Inventory record shows 30 units  
**And** the user is authorized to count Inventory  
**When** the user records a physical count of 30 units  
**Then** the system records the count  
**And** identifies no quantity discrepancy  
**And** the Inventory quantity remains 30.

#### AC-3.4.2: Identify Inventory discrepancy

**Given** an Inventory record shows 40 units  
**And** the user is authorized to count Inventory  
**When** the user records a physical count of 37 units  
**Then** the system records the physical count  
**And** identifies a discrepancy of 3 units  
**And** the recorded Inventory quantity remains unchanged until an authorized adjustment is completed.

### US-3.5: Move Inventory

#### AC-3.5.1: Successfully move Inventory

**Given** Location A contains 50 units of an Item  
**And** Location B contains 10 units of the same Item  
**And** the user is authorized to move Inventory  
**When** the user moves 20 units from Location A to Location B  
**And** confirms the source and destination locations  
**Then** Location A contains 30 units  
**And** Location B contains 30 units  
**And** the total Inventory quantity remains 60 units  
**And** the system records the movement.

#### AC-3.5.2: Reject movement exceeding available quantity

**Given** Location A contains 10 units of an Item  
**When** an authorized user attempts to move 15 units from Location A  
**Then** the system rejects the movement  
**And** the Inventory quantities remain unchanged.

#### AC-3.5.3: Reject invalid destination Location

**Given** Location A contains 25 units of an Item  
**And** the requested destination Location does not exist  
**When** an authorized user attempts to move 10 units  
**Then** the system rejects the movement  
**And** the Inventory quantity at Location A remains 25.

#### AC-3.5.4: Verify location during movement

**Given** a Warehouse Worker is performing an Inventory movement  
**And** the system identifies the required destination Location  
**When** the worker scans a different destination Location  
**Then** the system identifies the location mismatch  
**And** does not complete the movement until the correct destination is confirmed.
