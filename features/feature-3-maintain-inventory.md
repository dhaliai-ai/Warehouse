
# Feature: Maintain Inventory

**Feature ID:** 3  
**Branch pattern:** `feature/3-maintain-inventory`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System maintains accurate quantities of individual items in warehouse storage locations. Stored Inventory quantities are updated through confirmed Put Away, picking, authorized inventory adjustments, and movements between locations. Receiving records actual received quantities separately; received products do not increase stored bin Inventory until Put Away is confirmed. The system supports multiple warehouses, uses barcode scanning to verify physical storage locations, prevents duplicate or incomplete inventory updates, and preserves transaction history.

---

## User Stories

### US-3.1: Add Inventory

**As a** Warehouse Worker or Inventory Clerk  
**I want to** establish an inventory record for an existing item in a warehouse location  
**So that** the system can accurately track where products are stored and how many units are available.

**Priority:** P1  
**Independent test:** Create a zero-quantity Inventory record for an existing Item and Warehouse Location and verify that the record is saved without increasing physical stock. Verify that positive quantities require an authorized inventory transaction.

### US-3.2: Edit Inventory

**As an** Inventory Clerk or Warehouse Supervisor  
**I want to** correct an inventory quantity when a physical count identifies a discrepancy  
**So that** the system reflects the actual quantity stored in the warehouse.

**Priority:** P1  
**Independent test:** Adjust an existing Inventory quantity after a physical count and verify that the new quantity, reason, authorization, and adjustment history are recorded.

### US-3.3: Delete Inventory

**As a** Warehouse Supervisor or Administrator  
**I want to** remove an unused inventory record when its quantity is zero and no historical transactions depend on it  
**So that** unnecessary inventory records can be removed without losing business history.

**Priority:** P1  
**Independent test:** Delete an unused zero-quantity Inventory record and verify that records with positive quantities or historical dependencies cannot be deleted.

### US-3.4: Count Inventory

**As a** Warehouse Worker  
**I want to** count the physical quantity of an item in a storage location  
**So that** differences between actual inventory and system inventory can be identified.

**Priority:** P1  
**Independent test:** Scan the storage location and Item, record a physical count, and verify that the system identifies any difference without automatically changing Inventory.

### US-3.5: Move Inventory

**As a** Warehouse Worker  
**I want to** move inventory from one warehouse location to another  
**So that** products can be relocated while maintaining accurate inventory quantities.

**Priority:** P1  
**Independent test:** Scan and verify the Item, source location, and destination location, move a valid quantity, and verify that both Inventory balances and the movement history are updated together.

---

## Functional Requirements

- **FR-001:** The system MUST maintain inventory quantities for individual items stored in warehouse locations.
- **FR-002:** Each Inventory record MUST identify an existing Individual Item.
- **FR-003:** Each Inventory record MUST identify an existing Warehouse Location.
- **FR-004:** Each Warehouse Location MUST belong to a Warehouse.
- **FR-005:** The system MUST support inventory stored across multiple warehouses.
- **FR-006:** The system MUST assign a unique Inventory ID to each Inventory record.
- **FR-007:** Each Inventory record MUST maintain the quantity of an Item in a specific warehouse location.
- **FR-008:** Inventory quantities MUST be recorded in individual units (eaches).
- **FR-009:** The system MUST prevent negative Inventory quantities.
- **FR-010:** The system MUST prevent duplicate Inventory balance records for the same Item and Warehouse Location.
- **FR-011:** The system MUST allow authorized personnel to create Inventory records for existing Items and locations.
- **FR-012:** The system MUST validate Inventory information before saving.
- **FR-013:** The system MUST reject invalid Inventory information without changing existing records.
- **FR-014:** The system MUST allow authorized personnel to view Inventory quantities by Item, Warehouse, and storage location.
- **FR-015:** The system MUST support physical Inventory counting.
- **FR-016:** The system MUST record the actual quantity counted during an Inventory count.
- **FR-017:** The system MUST compare the physical count with the recorded Inventory quantity.
- **FR-018:** The system MUST identify discrepancies between physical and recorded quantities.
- **FR-019:** The system MUST allow an authorized Inventory Clerk or Warehouse Supervisor to approve or record Inventory adjustments according to configured permissions.
- **FR-020:** The system MUST record the previous quantity, adjusted quantity, adjustment reason, user, and adjustment date/time.
- **FR-021:** The system MUST support movement of Inventory between warehouse locations.
- **FR-022:** The system MUST identify the source location, destination location, Item, and quantity for each Inventory movement.
- **FR-023:** The system MUST verify source and destination Warehouse Locations through barcode scanning before confirming a physical Inventory movement.
- **FR-024:** The system MUST prevent movement of quantities greater than the available quantity at the source location.
- **FR-025:** The system MUST decrease the source Inventory quantity and increase the destination Inventory quantity when a movement is completed.
- **FR-026:** Inventory movements MUST preserve the total quantity of the Item across the affected locations.
- **FR-027:** The system MUST update stored Inventory quantities when received products are successfully put away through Feature 11.
- **FR-028:** The system MUST update Inventory quantities when Items are picked for customer orders according to the picking workflow.
- **FR-029:** The system MUST maintain stored Inventory quantities separately from Quantity Ordered, Quantity Received, Quantity Awaiting Put Away, Quantity Picked, Quantity Shipped, and Quantity Delivered.
- **FR-030:** The system MUST prevent deletion of Inventory records with quantities greater than zero.
- **FR-031:** The system MUST prevent deletion of Inventory records required for historical transactions.
- **FR-032:** The system MUST restrict Inventory record deletion to Warehouse Supervisors and Administrators.
- **FR-033:** The system MUST reject attempts to modify or delete nonexistent Inventory records.
- **FR-034:** The system MUST maintain Inventory adjustment and movement history for accountability.
- **FR-035:** The system MUST prevent unauthorized users from directly modifying Inventory quantities.
- **FR-036:** The system MUST maintain the relationship between Inventory, Individual Item, Warehouse Location, and Warehouse.

- **FR-037:** The system MUST distinguish creation of an Inventory balance record from a transaction that increases physical stock.
- **FR-038:** The system MUST allow an authorized user to create a new Inventory balance record with an initial quantity of zero without creating a stock movement.
- **FR-039:** The system MUST require an authorized, recorded stock transaction before an Inventory balance can be increased above zero.
- **FR-040:** The system MUST NOT allow ordinary Inventory record creation to bypass receiving, Put Away, or Inventory adjustment controls.
- **FR-041:** The system MUST create a missing destination Inventory balance automatically, when appropriate, as part of a valid confirmed Putaway Movement or Inventory Movement.
- **FR-042:** The system MUST prevent duplicate stock increases when the same transaction is submitted more than once.

- **FR-043:** The system MUST treat stored Inventory as quantities physically recorded in Warehouse storage locations.
- **FR-044:** The system MUST NOT increase stored bin Inventory merely because a Receiving Record has been completed.
- **FR-045:** The system MUST increase stored Inventory only when a Putaway Movement is successfully confirmed and recorded.
- **FR-046:** The system MUST preserve the original Quantity Received when Put Away increases stored Inventory.
- **FR-047:** The system MUST reduce Quantity Awaiting Put Away by the same number of units added to stored Inventory during a confirmed Putaway Movement.
- **FR-048:** The system MUST prevent the same received units from being added to stored Inventory more than once.
- **FR-049:** The system MUST preserve a traceable relationship between Inventory added through Put Away and the corresponding Putaway Movement and Receiving Record Line.
- **FR-050:** The system MUST allow authorized users to view received quantities awaiting Put Away separately from stored Inventory.

- **FR-051:** The system MUST require successful source and destination location verification before completing a physical Inventory Movement.
- **FR-052:** The system MUST reject an incorrect, unknown, inactive, or unreadable location barcode without changing Inventory.
- **FR-053:** The system MUST require the Item barcode to identify the Item being moved.
- **FR-054:** The system MUST reject an incorrect or unknown Item barcode without completing the movement.
- **FR-055:** The system MUST require movement quantities to be positive integers expressed in individual units.
- **FR-056:** The system MUST reject a movement when the source and destination Warehouse Locations are identical.
- **FR-057:** The system MUST prevent a physical Inventory Movement from being completed without the required verification of both locations and the Item.
- **FR-058:** The system MUST require an explicitly authorized transfer workflow for movements between different Warehouses. [NEEDS CLARIFICATION: Confirm whether inter-warehouse transfers belong in Feature 3 or a separate feature.]

- **FR-059:** Before confirming an Inventory Movement, the system MUST verify that the destination Warehouse Location has sufficient available capacity.
- **FR-060:** The system MUST apply the same configured location-capacity and storage-restriction rules used by Feature 11.
- **FR-061:** The system MUST reject a movement that would exceed the destination's available capacity.
- **FR-062:** The system MUST prevent Inventory from being moved into inactive or unsuitable storage locations.
- **FR-063:** The system MUST account for current occupancy and applicable reserved capacity when determining available storage capacity.
- **FR-064:** The system MUST prevent concurrent movements or placements from collectively exceeding a destination location's capacity.
- **FR-065:** The system MUST validate an authorized Inventory adjustment against applicable storage capacity and restrictions before increasing the stored quantity.

- **FR-066:** The system MUST complete the source decrease, destination increase, and Inventory Movement history record as one consistent transaction.
- **FR-067:** If any required part of an Inventory Movement fails, the system MUST leave both Inventory balances unchanged.
- **FR-068:** The system MUST prevent a confirmed Inventory Movement from being applied more than once.
- **FR-069:** The system MUST prevent concurrent transactions from reducing a source Inventory balance below zero.
- **FR-070:** The system MUST record the User and date/time associated with each completed Inventory Movement.
- **FR-071:** The system MUST preserve the original transaction history when an authorized correction is made.
- **FR-072:** The system MUST maintain an auditable record of Inventory changes caused by Put Away, picking, movement, and adjustment.
- **FR-073:** The system MUST distinguish transaction types so that authorized users can identify why an Inventory quantity changed.

- **FR-074:** The system MUST record a physical Inventory Count without automatically changing the stored Inventory balance.
- **FR-075:** The system MUST calculate Count Difference as Counted Quantity minus Recorded Quantity.
- **FR-076:** The system MUST identify a negative Count Difference as a shortage and a positive Count Difference as an overage.
- **FR-077:** The system MUST require an adjustment reason before an Inventory discrepancy is corrected.
- **FR-078:** The system MUST prevent an unauthorized Warehouse Worker from approving an Inventory adjustment.
- **FR-079:** The system MUST preserve the original physical count and the resulting adjustment as separate records.
- **FR-080:** The system MUST prevent an adjustment based on a stale recorded quantity from silently overwriting newer Inventory transactions.

- **FR-081:** The system MUST prevent deletion of an Inventory record referenced by Putaway Movements, Inventory Movements, Inventory Counts, Inventory Adjustments, or other retained stock transactions.
- **FR-082:** The system MUST preserve transaction history even when an unused Inventory record is eligible for deletion.
- **FR-083:** The system MUST prevent a deleted Inventory record from causing loss of historical Item or Warehouse Location information.
- **FR-084:** The system MUST record authorized Inventory record deletions for auditing.
- **FR-085:** The system MUST restrict direct changes to Inventory balances to approved transaction workflows rather than unrestricted field editing.

---

## Key Entities

### Inventory

Represents the recorded quantity of an Individual Item stored in a particular Warehouse Location.

Inventory does not include received products still awaiting Put Away at a Receiving Door.

### Individual Item

Represents a product purchased from suppliers and sold to customers.

Item identification, UPCs, descriptions, and other product information are maintained in Feature 4.

### Warehouse

Represents a physical warehouse operated by the company.

The company may operate multiple warehouses, as defined in Feature 2.

### Warehouse Location

Represents a physical storage location or bin within a Warehouse.

Warehouse Locations are identified through location codes or barcodes and may have configured capacity and storage restrictions.

### Inventory Count

Represents a physical count of an Item's quantity in a Warehouse Location.

A count does not automatically modify the Inventory balance.

### Inventory Adjustment

Represents an authorized correction made to a recorded Inventory quantity.

The adjustment preserves the original quantity, corrected quantity, reason, and authorization information.

### Inventory Movement

Represents the transfer of stored Inventory from one Warehouse Location to another.

A completed movement decreases the source balance and increases the destination balance by the same quantity.

### Receiving Record Line

Represents the actual quantity of an Item received during a receiving session.

Receiving Record Lines are maintained through Feature 10 and provide the quantities available for Put Away.

### Putaway Movement

Represents a confirmed placement of received products into a storage location.

Putaway Movements are maintained through Feature 11 and cause stored Inventory to increase.

### User

Represents the employee performing or authorizing an Inventory operation.

---

## Initial Data Model

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique Inventory record identifier; primary key |
| itemId | Integer | Foreign key referencing Individual Item |
| locationId | Integer | Foreign key referencing Warehouse Location |
| quantity | Integer | Stored quantity in individual units |
| updatedAt | DateTime | Date and time of the latest successful balance change |

**Relationships:**
- Each Inventory record belongs to one Individual Item.
- Each Inventory record belongs to one Warehouse Location.
- An Individual Item can have Inventory in multiple locations.
- A Warehouse Location can contain Inventory records for multiple Items.
- The combination of itemId and locationId must be unique.

**Constraints:**
- quantity must be a nonnegative integer.
- itemId must reference an existing Individual Item.
- locationId must reference an existing Warehouse Location.
- New Inventory balance records created directly begin with quantity zero.
- Positive balance changes require authorized stock transactions.
- Stored Inventory excludes quantities awaiting Put Away.
- An Inventory record with historical transaction dependencies cannot be deleted.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Item identifier |

**Relationships:**
- One Individual Item can have multiple Inventory records.
- Additional Item attributes and UPCs are defined in Feature 4.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique Warehouse identifier |

**Relationships:**
- One Warehouse contains multiple Warehouse Locations.
- Warehouse maintenance is defined in Feature 2.

### Warehouse Location

| Attribute | Type | Description |
|---|---|---|
| locationId | Integer | Unique Warehouse Location identifier |
| warehouseId | Integer | Foreign key referencing Warehouse |
| locationCode | String | Identifier displayed or encoded on the location barcode |
| locationType | String | Primary or Reserve |
| capacityUnits | Integer | Configured maximum capacity, when unit-based capacity is applicable |
| isActive | Boolean | Indicates whether the location is available for operations |

**Relationships:**
- Each Warehouse Location belongs to one Warehouse.
- One Warehouse Location can have multiple Inventory records for different Items.
- Location capacity and storage suitability rules are shared with Feature 11.

**Constraints:**
- A location must exist and be active before receiving a new Inventory Movement.
- The system must respect configured capacity and storage restrictions.
- A location must not be overfilled by a movement or adjustment.

**Derived Value:**
- Available Capacity = Configured Capacity - Current Occupancy - Reserved Capacity, expressed in the location's configured capacity measurement.

**Assumption:**
- The exact capacity measurement and calculation method must be consistent with Feature 11. [NEEDS CLARIFICATION: Confirm whether capacity is measured by units, volume, weight, or another configured method.]

### Inventory Count

| Attribute | Type | Description |
|---|---|---|
| countId | Integer | Unique Inventory Count identifier |
| inventoryId | Integer | Inventory record being counted |
| recordedQuantity | Integer | Quantity recorded at the time of the count |
| countedQuantity | Integer | Actual quantity physically counted |
| countedBy | Integer | User who performed the count |
| countedAt | DateTime | Date and time of the count |
| status | String | Recorded or Reviewed |

**Relationships:**
- Each Inventory Count references an Inventory record.
- Each Inventory Count is associated with a User.
- An Inventory Count may support a later Inventory Adjustment.

**Constraints:**
- countedQuantity must be a nonnegative integer.
- Recording a count does not automatically modify Inventory.

**Derived Value:**
- Count Difference = countedQuantity - recordedQuantity.

### Inventory Adjustment

| Attribute | Type | Description |
|---|---|---|
| adjustmentId | Integer | Unique Inventory Adjustment identifier |
| inventoryId | Integer | Inventory record being adjusted |
| countId | Integer | Related Inventory Count, when applicable |
| previousQuantity | Integer | Quantity immediately before adjustment |
| adjustedQuantity | Integer | Corrected quantity |
| reason | String | Explanation for the adjustment |
| adjustedBy | Integer | User who performed the adjustment |
| approvedBy | Integer | User who approved the adjustment, when approval is required |
| adjustedAt | DateTime | Date and time of the adjustment |

**Relationships:**
- Each Inventory Adjustment references an Inventory record.
- Each adjustment is associated with the User who performed it.
- An adjustment may reference a supporting physical Inventory Count.

**Constraints:**
- adjustedQuantity must be a nonnegative integer.
- reason must not be blank.
- The User must have the required adjustment permission.
- Adjustments must not silently overwrite intervening stock transactions.
- Increases must comply with configured storage-capacity rules.

### Inventory Movement

| Attribute | Type | Description |
|---|---|---|
| movementId | Integer | Unique Inventory Movement identifier |
| itemId | Integer | Item being moved |
| sourceLocationId | Integer | Location Inventory is moved from |
| destinationLocationId | Integer | Location Inventory is moved to |
| quantity | Integer | Number of individual units moved |
| movedBy | Integer | User performing the movement |
| movedAt | DateTime | Date and time of the movement |
| status | String | Completed for a successfully recorded movement |

**Relationships:**
- Each Inventory Movement references one Individual Item.
- Each movement has one source and one destination location.
- Each movement is associated with a User.
- Each completed movement updates two Inventory balances.

**Constraints:**
- quantity must be a positive integer.
- The source and destination must be different locations.
- The source must contain sufficient quantity.
- The destination must be active, suitable, and have sufficient capacity.
- The Item, source location, and destination location must be verified.
- Source decrease, destination increase, and movement history must be saved together.
- A movement cannot be applied more than once.

### Receiving Record Line

| Attribute | Type | Description |
|---|---|---|
| receivingRecordLineId | Integer | Unique Receiving Record Line identifier |
| receivingRecordId | Integer | Foreign key referencing Receiving Record |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityReceivedUnits | Integer | Actual quantity received in individual units |
| quantityPutawayUnits | Integer | Cumulative quantity confirmed as put away |

**Relationships:**
- Receiving Record Lines are maintained through Feature 10.
- Putaway Movements reference the corresponding Receiving Record Line.
- Stored Inventory increases only after Put Away confirmation.

**Derived Value:**
- Quantity Awaiting Put Away = quantityReceivedUnits - quantityPutawayUnits.

### Putaway Movement

| Attribute | Type | Description |
|---|---|---|
| putawayMovementId | Integer | Unique Putaway Movement identifier |
| putawayInstructionId | Integer | Foreign key referencing Putaway Instruction |
| receivingRecordLineId | Integer | Foreign key referencing Receiving Record Line |
| itemId | Integer | Foreign key referencing Individual Item |
| destinationLocationId | Integer | Verified destination Warehouse Location |
| quantityMoved | Integer | Quantity placed in individual units |
| movedBy | Integer | User who confirmed placement |
| movedAt | DateTime | Date and time of confirmation |

**Relationships:**
- Putaway Movements are created in Feature 11.
- Each confirmed movement references a Receiving Record Line.
- Each confirmed movement increases stored Inventory and reduces Quantity Awaiting Put Away.

**Constraints:**
- A movement must not be applied more than once.
- Inventory and receiving-related quantity updates must remain consistent.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | User authorization role |

**Relationships:**
- Users perform Inventory counts, adjustments, and movements.
- Role permissions determine which operations Users may perform.
- Warehouse Workers may count or move Inventory when authorized.
- Inventory Clerks and Warehouse Supervisors may perform adjustments according to configured permissions.
- Warehouse Supervisors and Administrators may delete eligible unused Inventory records.

---

## Gherkin AC

### US-3.1: Add Inventory

#### AC-3.1.1: Successfully create Inventory

**Given** an Individual Item exists  
**And** a valid Warehouse Location exists  
**And** the user is authorized to create Inventory balance records  
**When** the user creates an Inventory record with an initial quantity of zero  
**Then** the system saves the Inventory record  
**And** associates it with the correct Item and Warehouse Location  
**And** does not increase physical stock.

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

#### AC-3.1.6: Reject unrecorded positive opening quantity

**Given** an Individual Item and Warehouse Location exist  
**And** no Inventory record exists for that combination  
**When** a user attempts to create an Inventory record with 25 units without an authorized stock transaction  
**Then** the system rejects the positive opening quantity  
**And** does not add 25 units to stored Inventory  
**And** directs the user to the appropriate authorized transaction workflow.

#### AC-3.1.7: Create missing destination balance during Put Away

**Given** a completed Receiving Record contains 20 units awaiting Put Away  
**And** no Inventory balance record exists for that Item at the assigned destination bin  
**And** the worker has successfully verified the Item and destination  
**When** the worker confirms a valid Putaway Movement of 20 units  
**Then** the system creates the required destination Inventory balance if needed  
**And** records 20 units in that destination  
**And** reduces Quantity Awaiting Put Away by 20 units  
**And** records the corresponding Putaway Movement.

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

#### AC-3.2.5: Require adjustment reason

**Given** an Inventory record contains 30 units  
**And** a physical count identifies 28 units  
**And** the user has permission to adjust Inventory  
**When** the user attempts to change the quantity to 28 without a reason  
**Then** the system rejects the adjustment  
**And** the Inventory balance remains 30 units.

#### AC-3.2.6: Reject adjustment exceeding storage capacity

**Given** a Warehouse Location has capacity for 10 additional units  
**And** an Inventory record at that location contains 40 units  
**When** an authorized user attempts to adjust the recorded quantity to 55 units  
**Then** the system rejects the increase under the configured capacity rules  
**And** does not change the Inventory balance  
**And** reports that the adjustment exceeds available storage capacity.

#### AC-3.2.7: Prevent stale adjustment

**Given** an Inventory Count recorded 40 units as the system balance  
**And** a later authorized transaction changes the current balance to 35 units  
**When** a user attempts to apply an adjustment based on the older balance of 40 units  
**Then** the system identifies that the recorded balance has changed  
**And** does not silently overwrite the newer quantity  
**And** requires the discrepancy to be reviewed or recalculated.

### US-3.3: Delete Inventory

#### AC-3.3.1: Successfully delete unused Inventory

**Given** an Inventory record exists with a quantity of zero  
**And** no historical transactions depend on the record  
**And** the user is authenticated as a Warehouse Supervisor or Administrator  
**When** the user requests deletion  
**Then** the system deletes the Inventory record  
**And** records the authorized deletion in the audit history.

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

#### AC-3.3.6: Preserve Inventory transaction history

**Given** an Inventory record has a zero quantity  
**And** the record is referenced by a completed Putaway Movement  
**When** a Warehouse Supervisor requests deletion  
**Then** the system rejects deletion  
**And** preserves the Putaway Movement history  
**And** preserves the Inventory record required by that history.

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
**And** identifies a Count Difference of -3 units  
**And** identifies a shortage of 3 units  
**And** the recorded Inventory quantity remains unchanged until an authorized adjustment is completed.

#### AC-3.4.3: Identify physical count overage

**Given** an Inventory record shows 25 units  
**And** the user is authorized to count Inventory  
**When** the user records a physical count of 29 units  
**Then** the system records a Count Difference of +4 units  
**And** identifies an overage of 4 units  
**And** leaves the Inventory balance unchanged until an authorized adjustment is completed.

#### AC-3.4.4: Reject invalid physical count

**Given** an Inventory record exists  
**When** an authorized Warehouse Worker attempts to record a physical count of -2 units  
**Then** the system rejects the count  
**And** does not change the Inventory balance.

#### AC-3.4.5: Require location and Item verification during counting

**Given** a Warehouse Worker is counting Item A at Location A  
**When** the worker scans a barcode identifying a different Item or location  
**Then** the system reports the mismatch  
**And** does not record the count against the wrong Item or location  
**And** allows the worker to scan the correct barcodes.

#### AC-3.4.6: Separate count from adjustment approval

**Given** a Warehouse Worker records a physical count of 18 units  
**And** the system balance is 20 units  
**And** the worker does not have Inventory adjustment permission  
**When** the worker submits the physical count  
**Then** the system records the discrepancy  
**And** preserves the system Inventory balance at 20 units  
**And** requires an authorized adjustment before the balance changes.

### US-3.5: Move Inventory

#### AC-3.5.1: Successfully move Inventory

**Given** Location A contains 50 units of an Item  
**And** Location B contains 10 units of the same Item  
**And** the user is authorized to move Inventory  
**And** Location B has sufficient available capacity  
**When** the user scans and verifies the Item, Location A, and Location B  
**And** confirms a movement of 20 units from Location A to Location B  
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

**Given** a Warehouse Worker is performing an Inventory Movement  
**And** the system identifies the required destination Location  
**When** the worker scans a different destination Location  
**Then** the system identifies the location mismatch  
**And** does not complete the movement until the correct destination is verified.

#### AC-3.5.5: Reject incorrect source location

**Given** an Inventory Movement requires Item A to be moved from Location A  
**When** the worker scans Location B as the source  
**Then** the system reports that the source location is incorrect  
**And** does not decrease Inventory at either location  
**And** requires the correct source barcode.

#### AC-3.5.6: Reject incorrect Item barcode

**Given** a Warehouse Worker is moving Item A  
**And** the source and destination locations have been verified  
**When** the worker scans a UPC identifying Item B  
**Then** the system rejects the Item verification  
**And** does not complete the movement  
**And** leaves Inventory unchanged.

#### AC-3.5.7: Reject movement exceeding destination capacity

**Given** Location A contains 30 units of Item A  
**And** Location B has available capacity for only 10 additional units  
**When** an authorized worker attempts to move 15 units from Location A to Location B  
**Then** the system rejects the movement  
**And** leaves both Inventory balances unchanged  
**And** reports insufficient destination capacity.

#### AC-3.5.8: Prevent duplicate movement

**Given** a completed Inventory Movement transferred 10 units from Location A to Location B  
**When** the same movement confirmation is submitted again  
**Then** the system rejects the duplicate confirmation  
**And** does not decrease Location A again  
**And** does not increase Location B again.

#### AC-3.5.9: Preserve both balances when movement fails

**Given** Location A contains 40 units of Item A  
**And** Location B contains 10 units of Item A  
**And** an authorized worker confirms a valid movement of 15 units  
**When** the system cannot save the destination Inventory update  
**Then** the system does not retain a decrease at Location A  
**And** Location A remains at 40 units  
**And** Location B remains at 10 units  
**And** no completed Inventory Movement is recorded.

#### AC-3.5.10: Reject movement to same location

**Given** Location A contains 25 units of Item A  
**When** an authorized worker attempts to move 10 units from Location A to Location A  
**Then** the system rejects the movement  
**And** Inventory remains unchanged.

#### AC-3.5.11: Prevent concurrent overdraw

**Given** Location A contains 10 units of Item A  
**And** two authorized workers each attempt to move 8 units from Location A  
**When** the system processes both movement confirmations  
**Then** the system permits only movements supported by the remaining source quantity  
**And** does not allow the source balance to become negative  
**And** preserves accurate movement history.

#### AC-3.5.12: Reject unauthorized Inventory Movement

**Given** a Driver does not have Inventory Movement permission  
**When** the Driver attempts to move 10 units between Warehouse Locations  
**Then** the system denies the operation  
**And** does not change either Inventory balance.

#### AC-3.5.13: Require authorization for inter-warehouse transfer

**Given** Location A belongs to Warehouse A  
**And** Location B belongs to Warehouse B  
**When** a Warehouse Worker attempts an ordinary Inventory Movement from Location A to Location B  
**Then** the system rejects the ordinary movement  
**And** requires an authorized inter-warehouse transfer workflow  
**And** leaves both Inventory balances unchanged.
