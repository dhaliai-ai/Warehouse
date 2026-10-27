
# Feature: Put Away Received Items

**Feature ID:** 11  
**Branch pattern:** `feature/11-put-away-received-items`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System assists put-away workers in moving received products from receiving doors to designated warehouse storage locations. The system identifies completed receiving records awaiting Put Away, offers assignments to workers, determines an efficient sequence of storage locations, verifies products and destination bins through barcode scanning, supports alternate locations when necessary, and updates stored Inventory after each confirmed placement. Put Away remains separate from Supplier Order receiving. Received quantities awaiting Put Away are tracked separately from quantities already placed in warehouse storage bins.

---

## User Stories

### US-11.1: Select Received Order for Put Away

**As a** Put Away Worker  
**I want to** receive an assignment for products that have completed receiving  
**So that** I know which products to move and which Receiving Door to collect them from.

**Priority:** P1  
**Independent test:** Start Put Away with a completed Receiving Record available and verify that the system offers an assignment identifying the Supplier Order, Receiving Door, and quantities awaiting Put Away.

### US-11.2: Follow Putaway Sequence

**As a** Put Away Worker  
**I want to** receive storage locations in an efficient sequence  
**So that** I can move received products through the warehouse without unnecessary travel.

**Priority:** P1  
**Independent test:** Accept an assignment containing multiple products and verify that the system provides an ordered sequence of suitable destination locations and consistently applies its configured sequencing rules.

### US-11.3: Verify Putaway Location

**As a** Put Away Worker  
**I want to** scan the product and destination bin before placing products  
**So that** the system confirms that I am moving the correct Item to the correct storage location.

**Priority:** P1  
**Independent test:** Scan the assigned Item UPC and destination bin barcode, verify that matching barcodes are accepted, and confirm that incorrect Item or destination barcodes are rejected.

### US-11.4: Complete Item Putaway

**As a** Put Away Worker  
**I want to** confirm the quantity placed in each destination bin  
**So that** inventory is updated accurately and the system can direct me to the next task.

**Priority:** P1  
**Independent test:** Confirm placement of a valid quantity in a verified destination bin and verify that stored Inventory increases by exactly that amount while the quantity awaiting Put Away decreases by the same amount.

### US-11.5: Request Another Location

**As a** Put Away Worker  
**I want to** request another storage location when the assigned bin cannot hold the products  
**So that** I can continue Put Away without placing products in an unsuitable location.

**Priority:** P1  
**Independent test:** Report insufficient capacity in the assigned bin and verify that the system offers a suitable alternative or reports that no location is available.

### US-11.6: Complete Putaway Assignment

**As a** Put Away Worker  
**I want to** finish an assignment after all received quantities assigned to me have been placed  
**So that** the system records completion and makes another assignment available.

**Priority:** P1  
**Independent test:** Complete every instruction in an assignment and verify that the assignment is marked Completed, its movement history is preserved, and the same quantities cannot be put away again.

---

## Functional Requirements

- **FR-001:** The system MUST identify completed Receiving Records containing quantities that have not yet been fully put away.
- **FR-002:** The system MUST make received products available for Put Away only after their receiving session has been completed.
- **FR-003:** The system MUST identify the Supplier Order associated with each available Receiving Record.
- **FR-004:** The system MUST identify the Receiving Door where the received products are waiting.
- **FR-005:** The system MUST offer available Putaway Assignments to authorized Put Away Workers.
- **FR-006:** The system MUST allow a worker to accept or reject an offered Putaway Assignment.
- **FR-007:** The system MUST record which worker accepts a Putaway Assignment.
- **FR-008:** The system MUST prevent the same received quantities from being assigned to multiple active Putaway Assignments.
- **FR-009:** When a worker rejects an offered assignment, the system MUST leave the received products available for reassignment.
- **FR-010:** The system MUST identify when no received products are waiting for Put Away.

- **FR-011:** After an assignment is accepted, the system MUST determine a sequence of Putaway Instructions.
- **FR-012:** Each Putaway Instruction MUST identify the Individual Item, quantity to move, and destination Warehouse Location.
- **FR-013:** Each Putaway Instruction MUST identify the destination aisle, row, and slot.
- **FR-014:** The system MUST provide the worker with the next Putaway Instruction in the assigned sequence.
- **FR-015:** The system MUST prioritize suitable existing primary storage bins when they can accept the products.
- **FR-016:** The system MUST support selecting suitable reserve or overflow bins when a primary bin cannot accept the full quantity.
- **FR-017:** The system MUST consider configured storage restrictions and available capacity when recommending a destination bin.
- **FR-018:** The system MUST prevent an inactive or unavailable Warehouse Location from being selected for new Put Away.
- **FR-019:** The system MUST keep all destinations within the Warehouse associated with the receiving work.

- **FR-020:** The system MUST allow the worker to scan the destination bin barcode.
- **FR-021:** The system MUST verify that the scanned bin matches the expected destination Warehouse Location.
- **FR-022:** The system MUST reject confirmation of Put Away when the scanned bin does not match the assigned destination.
- **FR-023:** The system MUST identify an unknown or unreadable destination barcode without recording the placement.
- **FR-024:** The system MUST require successful destination verification before confirming an instruction.

- **FR-025:** The system MUST allow the worker to confirm the actual quantity placed in the verified destination bin.
- **FR-026:** The system MUST require confirmed Put Away quantities to be positive integers expressed in individual units.
- **FR-027:** The system MUST prevent the confirmed quantity from exceeding the quantity remaining for the instruction.
- **FR-028:** The system MUST update Inventory at the verified destination Warehouse Location after a successful Put Away confirmation.
- **FR-029:** The system MUST increase the destination Inventory quantity by exactly the confirmed quantity.
- **FR-030:** The system MUST reduce the quantity awaiting Put Away by the same confirmed quantity.
- **FR-031:** The system MUST preserve a record of each confirmed Put Away movement.
- **FR-032:** The system MUST prevent the same Put Away confirmation from increasing Inventory more than once.

- **FR-033:** The system MUST allow a worker to request another location when the assigned bin lacks sufficient capacity.
- **FR-034:** The system MUST recommend an alternative suitable Warehouse Location when one is available.
- **FR-035:** The system MUST require the worker to scan and verify an alternative bin before confirming placement.
- **FR-036:** The system MUST allow an instruction to be divided between multiple suitable bins when necessary.
- **FR-037:** The system MUST preserve the quantity remaining to be put away when only part of an instruction is completed.
- **FR-038:** The system MUST identify when no suitable alternative location is available.
- **FR-039:** When no suitable location is available, the system MUST leave the remaining quantity awaiting Put Away.
- **FR-040:** The system MUST notify an authorized Supervisor when Put Away cannot continue because no suitable location is available.

- **FR-041:** After an instruction is completed, the system MUST provide the next outstanding instruction in the sequence.
- **FR-042:** The system MUST identify when all instructions for an assignment have been completed.
- **FR-043:** The system MUST mark a Putaway Assignment as Completed only when all assigned quantities have been successfully put away.
- **FR-044:** The system MUST record the completion date and time of the Putaway Assignment.
- **FR-045:** The system MUST allow the worker to request another available Putaway Assignment after completing the current assignment.
- **FR-046:** The system MUST maintain Putaway Assignment statuses of Offered, Accepted, In Progress, Rejected, Blocked, and Completed.
- **FR-047:** The system MUST prevent completed assignments from being modified through ordinary Put Away operations.
- **FR-048:** The system MUST reject attempts to complete nonexistent or already completed assignments.
- **FR-049:** The system MUST restrict Put Away operations to authorized warehouse personnel.
- **FR-050:** The system MUST preserve the relationship between Putaway Assignments, Receiving Records, Supplier Orders, Warehouse Locations, and Inventory.
- **FR-051:** The system MUST maintain received quantities separately from quantities already put away.
- **FR-052:** The system MUST NOT treat completion of Supplier Order receiving as completion of Put Away.
- **FR-053:** The system MUST preserve Put Away movement history for inventory reconciliation and auditing.

- **FR-054:** The system MUST require the worker to scan a configured UPC for the Item being put away before confirming placement.
- **FR-055:** The system MUST verify that the scanned Item UPC identifies the Individual Item specified by the Putaway Instruction.
- **FR-056:** The system MUST reject an incorrect, unknown, or unreadable Item UPC without recording a Putaway Movement or updating Inventory.
- **FR-057:** When a Case UPC is used for Item verification, the system MUST identify the associated Item and the number of individual units represented by the barcode.
- **FR-058:** The system MUST preserve the actual quantity confirmed as put away in individual units, independently of the package type scanned.

- **FR-059:** The system MUST generate a Putaway Instruction sequence using configured warehouse location and travel-order information.
- **FR-060:** The system MUST use the Receiving Door as the starting location when determining the sequence of destination bins.
- **FR-061:** The system MUST select a sequence intended to reduce unnecessary travel while respecting storage suitability, capacity, and Warehouse boundaries.
- **FR-062:** The system MUST display the resulting instruction sequence to the assigned worker.
- **FR-063:** The system MUST preserve the generated sequence and any subsequent changes to it for audit purposes.
- **FR-064:** The system MUST recalculate the remaining sequence when an assigned destination becomes unavailable or an alternative destination is selected.
- **FR-065:** The system MUST NOT prioritize a shorter travel sequence over required storage restrictions or bin capacity.
- **FR-066:** The system MUST apply a documented, repeatable sequencing rule to the same warehouse configuration and set of destinations. [NEEDS CLARIFICATION: Confirm the required routing algorithm, travel-distance information, and whether the system must guarantee an optimal route or only recommend an efficient route.]

- **FR-067:** Before confirming a Putaway Movement, the system MUST verify that the destination bin has sufficient available capacity for the quantity being placed.
- **FR-068:** The system MUST calculate available bin capacity using configured capacity minus current occupancy, accounting for any applicable reserved capacity.
- **FR-069:** The system MUST reject a placement that would exceed the destination bin's available capacity.
- **FR-070:** The system MUST require a different suitable destination or a smaller confirmed quantity when the full quantity cannot fit.
- **FR-071:** The system MUST ensure that concurrent Putaway Movements cannot collectively exceed the same bin's available capacity.

- **FR-072:** The system MUST calculate Quantity Awaiting Put Away for each Receiving Record Line as Quantity Received Units minus Quantity Putaway Units.
- **FR-073:** The system MUST prevent Quantity Putaway Units from exceeding Quantity Received Units for the associated Receiving Record Line.
- **FR-074:** The system MUST preserve cumulative Quantity Received when Put Away is performed. Put Away MUST update Quantity Putaway separately without changing the original receiving totals.
- **FR-075:** The system MUST distinguish quantities awaiting Put Away at a Receiving Door from quantities already stored in destination bins.
- **FR-076:** The system MUST update the Putaway Movement, destination Inventory, and Quantity Putaway Units as one consistent operation so that a failed confirmation does not produce a partial inventory update.
- **FR-077:** The system MUST prevent multiple workers from confirming movements that collectively exceed the quantity awaiting Put Away.
- **FR-078:** The system MUST preserve a traceable relationship from each confirmed Putaway Movement to its original Receiving Record Line.
- **FR-079:** The system MUST make the remaining quantity awaiting Put Away visible to authorized workers and Supervisors.
- **FR-080:** The system MUST preserve quantities that cannot be put away because of capacity, barcode, or storage-location exceptions until they are successfully placed or handled through an authorized exception process. [NEEDS CLARIFICATION: Confirm the authorized process for damaged, missing, or otherwise unplaceable received products.]

---

## Key Entities

### Putaway Assignment

Represents a set of received products offered or assigned to a Put Away Worker.

The assignment identifies the receiving source, assigned worker, and current processing status.

### Putaway Instruction

Represents an individual storage task within a Putaway Assignment.

Each instruction identifies an Item, a quantity, a destination Warehouse Location, and its position in the put-away sequence.

### Receiving Record

Represents a completed receiving session containing products awaiting Put Away.

Receiving Records are created in Feature 10.

### Receiving Record Line

Represents the quantity of a particular Item received during a receiving session.

The quantity received is tracked separately from the quantity already put away.

### Supplier Order

Represents the purchase order associated with the received shipment.

### Warehouse Location

Represents a scannable storage bin or slot within a Warehouse.

Warehouse Locations identify where Inventory is physically stored.

### Inventory

Represents the quantity of an Individual Item at a specific Warehouse Location.

Inventory maintenance is defined in Feature 3.

### Receiving Door

Represents the location where received products wait before being moved to storage.

### Individual Item

Represents a product being put away.

Each Item may have an individual-unit UPC and a Case UPC.

### UPC

Represents a barcode identifying an Individual Item or a case containing multiple units of that Item.

UPC information is maintained through the Item-related features and used during receiving in Feature 10.

### Putaway Movement

Represents a completed movement of a specific quantity of an Item from a receiving location into a storage bin.

### User

Represents an employee authorized to perform Put Away or review blocked assignments.

---

## Initial Data Model

### Putaway Assignment

| Attribute | Type | Description |
|---|---|---|
| putawayAssignmentId | Integer | Unique Putaway Assignment identifier |
| receivingRecordId | Integer | Foreign key referencing Receiving Record |
| assignedUserId | Integer | User who accepted the assignment; nullable before acceptance |
| status | String | Offered, Accepted, In Progress, Rejected, Blocked, or Completed |
| offeredAt | DateTime | Date and time the assignment was offered |
| acceptedAt | DateTime | Date and time the worker accepted it |
| completedAt | DateTime | Date and time all assigned work was completed |

**Relationships:**
- Each Putaway Assignment references one Receiving Record.
- A Receiving Record may have multiple assignments over time when work is rejected or reassigned.
- An accepted Putaway Assignment contains one or more Putaway Instructions.
- A Putaway Assignment may be accepted by one User.

**Constraints:**
- putawayAssignmentId must be unique.
- The referenced Receiving Record must exist and be Completed.
- The same received quantities cannot be allocated to multiple active assignments.
- Completed assignments cannot be completed again.
- A rejected assignment does not permanently reserve its received quantities.

### Putaway Instruction

| Attribute | Type | Description |
|---|---|---|
| putawayInstructionId | Integer | Unique Putaway Instruction identifier |
| putawayAssignmentId | Integer | Foreign key referencing Putaway Assignment |
| receivingRecordLineId | Integer | Foreign key referencing Receiving Record Line |
| itemId | Integer | Foreign key referencing Individual Item |
| destinationLocationId | Integer | Foreign key referencing Warehouse Location |
| sequenceNumber | Integer | Position in the put-away sequence |
| quantityToPutaway | Integer | Quantity assigned for placement in individual units |
| quantityPutaway | Integer | Quantity already confirmed as placed |
| status | String | Pending, In Progress, Blocked, or Completed |
| itemVerified | Boolean | Whether the Item barcode has been successfully verified for the current placement |
| destinationVerified | Boolean | Whether the destination barcode has been successfully verified for the current placement |

**Relationships:**
- Each Putaway Instruction belongs to one Putaway Assignment.
- Each instruction references a received Item and a destination Warehouse Location.
- One instruction may result in multiple Putaway Movements if products are split between bins.
- Each instruction references the original Receiving Record Line.

**Constraints:**
- quantityToPutaway must be greater than zero.
- quantityPutaway cannot be negative.
- quantityPutaway cannot exceed quantityToPutaway.
- The destination must belong to the same Warehouse as the receiving work.
- The Item and destination must be verified before a movement is confirmed.
- A change to the destination invalidates previous destination verification.

**Derived Value:**
- Remaining Quantity = quantityToPutaway - quantityPutaway.

### Receiving Record

| Attribute | Type | Description |
|---|---|---|
| receivingRecordId | Integer | Unique Receiving Record identifier |
| supplierOrderId | Integer | Foreign key referencing Supplier Order |
| warehouseId | Integer | Foreign key referencing Warehouse |
| receivingDoorId | Integer | Foreign key referencing Receiving Door |
| status | String | In Progress or Completed |

**Relationships:**
- A completed Receiving Record supplies products for Put Away.
- Each Receiving Record contains Receiving Record Lines.
- Receiving is defined in Feature 10.

**Constraints:**
- Only Completed Receiving Records can supply Putaway Assignments.
- Completing receiving does not mean the products have been put away.

### Receiving Record Line

| Attribute | Type | Description |
|---|---|---|
| receivingRecordLineId | Integer | Unique Receiving Record Line identifier |
| receivingRecordId | Integer | Foreign key referencing Receiving Record |
| supplierOrderLineId | Integer | Foreign key referencing Supplier Order Line |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityReceivedUnits | Integer | Actual quantity received in individual units |
| quantityPutawayUnits | Integer | Cumulative quantity confirmed as put away |

**Relationships:**
- Each Receiving Record Line belongs to one Receiving Record.
- One Receiving Record Line may be processed by multiple Putaway Instructions or Movements.
- Each Receiving Record Line is associated with the original Supplier Order Line.

**Constraints:**
- quantityReceivedUnits cannot be negative.
- quantityPutawayUnits cannot be negative.
- quantityPutawayUnits cannot exceed quantityReceivedUnits.
- Receiving quantities must not be modified by Put Away operations.

**Derived Value:**
- Quantity Awaiting Put Away = quantityReceivedUnits - quantityPutawayUnits.

### Supplier Order

| Attribute | Type | Description |
|---|---|---|
| supplierOrderId | Integer | Unique Supplier Order identifier |
| poNumber | String | Unique PO Number |
| warehouseId | Integer | Destination Warehouse recorded on the Supplier Order |
| status | String | Draft, Submitted, Partially Received, Received, or Canceled |

**Relationships:**
- A Supplier Order may have multiple Receiving Records.
- Received products are put away through their associated Receiving Records.
- Supplier Order creation is defined in Feature 9.

**Constraints:**
- Put Away does not modify the original Supplier Order quantities.
- A Supplier Order may remain Partially Received while products from completed receiving sessions are put away.

### Warehouse Location

| Attribute | Type | Description |
|---|---|---|
| locationId | Integer | Unique Warehouse Location identifier |
| warehouseId | Integer | Foreign key referencing Warehouse |
| locationCode | String | Unique scannable bin identifier within the Warehouse |
| aisle | String | Aisle identifier |
| row | String | Row identifier |
| slot | String | Slot or bin identifier |
| locationType | String | Primary or Reserve |
| capacityUnits | Integer | Configured maximum storage capacity in units |
| isActive | Boolean | Indicates whether the location is available |

**Relationships:**
- A Warehouse Location belongs to one Warehouse.
- A Warehouse Location may contain Inventory.
- A Warehouse Location may be assigned to multiple Putaway Instructions over time.

**Constraints:**
- locationCode must be unique within its Warehouse.
- A location must be active before being assigned.
- The system must respect configured capacity and storage restrictions.
- A confirmed placement must not exceed available capacity.

**Derived Value:**
- Available Capacity Units = capacityUnits - Current Occupancy Units - Reserved Capacity Units.

**Assumption:**
- The capacity calculation uses individual units only when all stored Items have compatible unit-based capacity measurements. [NEEDS CLARIFICATION: Confirm whether bin capacity should instead be measured using volume, dimensions, weight, or another warehouse-specific unit.]

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique Inventory identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| locationId | Integer | Foreign key referencing Warehouse Location |
| quantity | Integer | Current stored quantity in individual units |

**Relationships:**
- Each Inventory record references one Item and one Warehouse Location.
- Putaway Movements increase Inventory at verified destination locations.
- Inventory maintenance is defined in Feature 3.

**Constraints:**
- Inventory quantity cannot be negative.
- The combination of itemId and locationId must be unique.
- A Putaway Movement must not increase Inventory more than once.
- Inventory updates and corresponding Putaway Movement records must remain consistent.

### Receiving Door

| Attribute | Type | Description |
|---|---|---|
| receivingDoorId | Integer | Unique Receiving Door identifier |
| warehouseId | Integer | Foreign key referencing Warehouse |
| doorCode | String | Unique Receiving Door code within the Warehouse |

**Relationships:**
- Each Receiving Door belongs to a Warehouse.
- Completed Receiving Records identify where received products await Put Away.
- Putaway sequencing begins from the Receiving Door.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |

**Relationships:**
- One Individual Item may appear in multiple Putaway Instructions.
- One Individual Item may be stored in multiple Warehouse Locations.
- One Individual Item may have multiple UPCs.

### UPC

| Attribute | Type | Description |
|---|---|---|
| upcId | Integer | Unique UPC identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| upcCode | String | Barcode value |
| barcodeType | String | Individual Unit or Case |
| unitsRepresented | Integer | Number of individual units represented by the barcode |

**Relationships:**
- Each UPC identifies one Individual Item.
- A UPC may be used to verify the Item during Put Away.

**Constraints:**
- An individual-unit UPC represents one unit.
- A Case UPC represents the configured number of units for that barcode.
- A barcode must identify the Item required by the Putaway Instruction.

### Putaway Movement

| Attribute | Type | Description |
|---|---|---|
| putawayMovementId | Integer | Unique movement identifier |
| putawayInstructionId | Integer | Foreign key referencing Putaway Instruction |
| receivingRecordLineId | Integer | Foreign key referencing Receiving Record Line |
| itemId | Integer | Foreign key referencing Individual Item |
| destinationLocationId | Integer | Verified destination Warehouse Location |
| quantityMoved | Integer | Quantity placed in individual units |
| movedBy | Integer | User who confirmed placement |
| movedAt | DateTime | Date and time the movement was confirmed |

**Relationships:**
- Each Putaway Movement belongs to a Putaway Instruction.
- Each movement references the received Item and verified destination.
- Confirmed movements increase stored Inventory and reduce the quantity awaiting Put Away.
- Each movement can be traced to its original Receiving Record Line.

**Constraints:**
- quantityMoved must be greater than zero.
- The Item and destination must be verified before a movement is recorded.
- The destination must have sufficient capacity.
- A confirmed movement cannot be applied to Inventory more than once.
- The movement, Inventory update, and quantity awaiting Put Away update must succeed together.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Put Away Workers accept and complete assignments.
- Supervisors review blocked work and storage exceptions.
- Managers may review Put Away movement history.

---

## Gherkin AC

### US-11.1: Select Received Order for Put Away

#### AC-11.1.1: Offer received work

**Given** a Completed Receiving Record contains products awaiting Put Away  
**And** the user is authenticated as a Put Away Worker  
**When** the worker starts the Put Away process  
**Then** the system offers an available Putaway Assignment  
**And** displays the associated Supplier Order and Receiving Door  
**And** displays the quantity awaiting Put Away.

#### AC-11.1.2: Accept assignment

**Given** the system has offered a Putaway Assignment  
**When** the Put Away Worker accepts the assignment  
**Then** the system records the worker as the assigned User  
**And** changes the assignment status to Accepted  
**And** makes its Putaway Instructions available.

#### AC-11.1.3: Reject assignment

**Given** the system has offered a Putaway Assignment  
**When** the Put Away Worker rejects the assignment  
**Then** the system records the assignment as Rejected  
**And** leaves its unassigned received quantities available for another assignment  
**And** offers another eligible assignment when one is available.

#### AC-11.1.4: No Put Away work available

**Given** no completed Receiving Record has products awaiting Put Away  
**When** the worker requests a Putaway Assignment  
**Then** the system reports that no Put Away work is available  
**And** does not create an empty assignment.

#### AC-11.1.5: Prevent duplicate active assignment

**Given** received quantities are already allocated to an active Putaway Assignment  
**When** another worker requests Put Away work  
**Then** the system does not allocate those same quantities to another active assignment.

#### AC-11.1.6: Allow Put Away before final Supplier Order closure

**Given** a Supplier Order is Partially Received  
**And** one of its Receiving Records is Completed  
**And** that Receiving Record contains quantities awaiting Put Away  
**When** an authorized Put Away Worker requests available work  
**Then** the system makes those received quantities available for Put Away  
**And** does not require the Supplier Order to be in Received status.

### US-11.2: Follow Putaway Sequence

#### AC-11.2.1: Generate first Putaway Instruction

**Given** a Put Away Worker has accepted an assignment  
**And** suitable destination locations exist  
**When** the system prepares the put-away sequence  
**Then** the system generates Putaway Instructions  
**And** provides the first destination location with its aisle, row, and slot.

#### AC-11.2.2: Provide next destination

**Given** the worker has completed the current Putaway Instruction  
**And** additional instructions remain  
**When** the system advances the assignment  
**Then** the system displays the next destination location.

#### AC-11.2.3: Prefer suitable primary bin

**Given** an Item has an active primary storage bin with sufficient available capacity  
**When** the system selects a Put Away destination  
**Then** the system recommends the suitable primary bin before an overflow bin.

#### AC-11.2.4: Use reserve location when needed

**Given** the primary storage bin cannot hold the required quantity  
**And** a suitable reserve location exists  
**When** the system selects an alternative destination  
**Then** the system recommends the reserve location  
**And** identifies its aisle, row, and slot.

#### AC-11.2.5: Sequence destinations from Receiving Door

**Given** a completed Receiving Record identifies Receiving Door "DOOR-3"  
**And** a Putaway Assignment contains multiple suitable destination bins  
**And** the Warehouse has configured travel-order information  
**When** the system generates the Putaway Instruction sequence  
**Then** the system uses "DOOR-3" as the starting location  
**And** applies the configured sequencing rules  
**And** displays the ordered destination sequence to the worker.

#### AC-11.2.6: Recalculate sequence after destination change

**Given** a Put Away Worker has accepted an assignment with multiple destinations  
**And** one assigned destination becomes unavailable  
**When** the worker requests an alternative location  
**And** the system selects a suitable replacement  
**Then** the system recalculates the remaining Putaway Instruction sequence  
**And** preserves already completed movements  
**And** does not direct the worker to the unavailable location.

#### AC-11.2.7: Do not sacrifice storage suitability for travel distance

**Given** one nearby bin violates the Item's configured storage restrictions  
**And** another more distant bin is suitable  
**When** the system determines the Put Away destination  
**Then** the system rejects the unsuitable nearby bin  
**And** recommends a suitable destination  
**And** does not prioritize travel distance over storage requirements.

### US-11.3: Verify Putaway Location

#### AC-11.3.1: Verify correct destination bin

**Given** a Putaway Instruction identifies destination bin "A1-R2-S3"  
**And** the assigned Item has been verified  
**When** the worker scans barcode "A1-R2-S3"  
**Then** the system verifies the destination  
**And** allows the worker to proceed to quantity confirmation.

#### AC-11.3.2: Reject incorrect destination bin

**Given** a Putaway Instruction identifies destination bin "A1-R2-S3"  
**When** the worker scans barcode "A1-R2-S4"  
**Then** the system reports that the scanned bin is incorrect  
**And** does not allow the placement to be confirmed for the wrong bin.

#### AC-11.3.3: Handle unreadable barcode

**Given** a worker is at an assigned destination bin  
**When** the destination barcode cannot be read  
**Then** the system reports that the location has not been verified  
**And** does not update Inventory  
**And** allows the worker to retry scanning or request Supervisor assistance.

#### AC-11.3.4: Reject inactive location

**Given** a Warehouse Location is inactive  
**When** a worker attempts to use it as a Put Away destination  
**Then** the system rejects the location  
**And** does not record Inventory placement there.

#### AC-11.3.5: Verify correct Item barcode

**Given** a Putaway Instruction requires Item A  
**And** Item A has a configured UPC  
**When** the Put Away Worker scans Item A's UPC  
**Then** the system identifies Item A  
**And** verifies that the scanned Item matches the Putaway Instruction  
**And** allows the worker to continue with destination verification.

#### AC-11.3.6: Reject incorrect Item barcode

**Given** a Putaway Instruction requires Item A  
**And** Item B has a different configured UPC  
**When** the worker scans Item B's UPC  
**Then** the system identifies that the wrong Item was scanned  
**And** rejects Item verification  
**And** does not record a Putaway Movement  
**And** does not update Inventory.

#### AC-11.3.7: Reject unknown Item barcode

**Given** a Putaway Instruction requires Item A  
**When** the worker scans an unknown Item barcode  
**Then** the system reports that the Item barcode is unknown  
**And** does not mark the Item as verified  
**And** does not update Inventory.

#### AC-11.3.8: Verify Item using Case UPC

**Given** a Putaway Instruction requires Item A  
**And** Item A has a Case UPC representing 12 individual units  
**When** the worker scans that Case UPC  
**Then** the system identifies Item A  
**And** identifies that the barcode represents 12 units  
**And** allows the worker to continue with destination verification  
**And** preserves the requirement to confirm the actual quantity placed.

### US-11.4: Complete Item Putaway

#### AC-11.4.1: Update Inventory after confirmed placement

**Given** a Putaway Instruction requires 20 units of Item A  
**And** Item A has been verified using its UPC  
**And** the correct destination bin has been scanned and verified  
**And** the destination Inventory currently contains 30 units of Item A  
**And** the destination has sufficient available capacity  
**When** the worker confirms placement of 20 units  
**Then** the system updates the destination Inventory to 50 units  
**And** records 20 units as put away  
**And** reduces Quantity Awaiting Put Away by 20 units  
**And** preserves a Putaway Movement record.

#### AC-11.4.2: Reject quantity greater than remaining

**Given** a Putaway Instruction has 10 units remaining  
**And** the Item and destination bin have been verified  
**When** the worker attempts to confirm placement of 15 units  
**Then** the system rejects the confirmation  
**And** Inventory remains unchanged.

#### AC-11.4.3: Reject placement without bin verification

**Given** a Putaway Instruction requires 12 units  
**And** no destination bin has been successfully verified  
**When** the worker attempts to confirm placement  
**Then** the system rejects the confirmation  
**And** Inventory remains unchanged.

#### AC-11.4.4: Complete partial instruction

**Given** a Putaway Instruction requires 30 units  
**And** the assigned destination bin can hold only 20 additional units  
**And** the Item and destination have been verified  
**When** the worker confirms placement of 20 units  
**Then** the system increases Inventory by 20 units  
**And** records 10 units as remaining for Put Away  
**And** does not mark the instruction as fully Completed.

#### AC-11.4.5: Prevent duplicate Inventory update

**Given** a Putaway Movement for 15 units has already been confirmed  
**When** the same confirmation is submitted again  
**Then** the system rejects the duplicate operation  
**And** does not increase Inventory a second time.

#### AC-11.4.6: Reject placement exceeding bin capacity

**Given** a Putaway Instruction requires 20 units of Item A  
**And** the assigned destination bin has capacity for only 12 additional units  
**And** the Item and destination have been verified  
**When** the worker attempts to confirm placement of 20 units  
**Then** the system rejects the confirmation  
**And** does not update Inventory  
**And** informs the worker that the available capacity is insufficient  
**And** allows the worker to confirm a smaller valid quantity or request another location.

#### AC-11.4.7: Preserve receiving quantity after Put Away

**Given** a completed Receiving Record Line contains 60 Received Units  
**And** none of those units have been put away  
**When** the worker verifies the Item and destination and confirms placement of 20 units  
**Then** the system preserves Quantity Received as 60 units  
**And** records Quantity Putaway as 20 units  
**And** calculates Quantity Awaiting Put Away as 40 units  
**And** increases destination Inventory by 20 units.

#### AC-11.4.8: Reject placement without Item verification

**Given** a Putaway Instruction requires 12 units of Item A  
**And** the destination bin has been verified  
**And** the Item barcode has not been verified  
**When** the worker attempts to confirm placement  
**Then** the system rejects the confirmation  
**And** does not record a Putaway Movement  
**And** does not update Inventory.

#### AC-11.4.9: Prevent conflicting concurrent placements

**Given** a destination bin has available capacity for 10 additional units  
**And** two Put Away Workers each attempt to place 8 units in that bin  
**When** the system processes both confirmations  
**Then** the system permits only confirmations that fit within the remaining capacity  
**And** does not allow the combined placements to exceed the bin's capacity  
**And** preserves consistent Inventory and Putaway Movement records.

#### AC-11.4.10: Prevent duplicate allocation of received units

**Given** a completed Receiving Record Line contains 20 units awaiting Put Away  
**And** 15 units have already been allocated to an active Putaway Assignment  
**When** another worker requests an assignment for the same Receiving Record Line  
**Then** the system makes no more than 5 unallocated units available  
**And** does not allocate the same units to two active assignments.

### US-11.5: Request Another Location

#### AC-11.5.1: Request alternative bin

**Given** the assigned destination bin cannot hold all of the product  
**And** another suitable Warehouse Location exists  
**When** the Put Away Worker requests another location  
**Then** the system recommends the alternative location  
**And** displays its aisle, row, and slot  
**And** requires barcode verification before placement.

#### AC-11.5.2: Split quantity between bins

**Given** 30 units of Item A require Put Away  
**And** the primary bin can accept 20 units  
**And** a suitable reserve bin can accept at least 10 units  
**When** the worker verifies Item A and the primary bin and confirms 20 units  
**And** verifies Item A and the reserve bin and confirms 10 units  
**Then** the system records both Putaway Movements  
**And** increases Inventory by the appropriate quantity at each bin  
**And** records all 30 units as put away.

#### AC-11.5.3: No suitable alternative location

**Given** the assigned destination bin cannot hold the remaining products  
**And** no suitable alternative Warehouse Location exists  
**When** the worker requests another location  
**Then** the system reports that no suitable location is available  
**And** leaves the remaining quantity awaiting Put Away  
**And** marks the work as Blocked  
**And** notifies an authorized Supervisor.

#### AC-11.5.4: Reject location in another Warehouse

**Given** a Putaway Assignment belongs to Warehouse A  
**And** a proposed destination belongs to Warehouse B  
**When** the worker attempts to use that destination  
**Then** the system rejects the location  
**And** does not update Inventory.

#### AC-11.5.5: Reverify destination after alternative selection

**Given** the worker has verified an assigned destination bin  
**And** the worker requests and receives a different destination  
**When** the worker attempts to confirm placement without scanning the new destination  
**Then** the system rejects the confirmation  
**And** requires verification of the new destination barcode  
**And** does not update Inventory.

#### AC-11.5.6: Preserve unplaced quantity when work is blocked

**Given** a completed Receiving Record Line contains 40 Received Units  
**And** 25 units have already been put away  
**And** no suitable location exists for the remaining 15 units  
**When** the worker reports that Put Away cannot continue  
**Then** the system preserves 40 Received Units  
**And** preserves 25 Quantity Putaway Units  
**And** records 15 units as awaiting Put Away  
**And** marks the remaining work as Blocked  
**And** notifies an authorized Supervisor.

### US-11.6: Complete Putaway Assignment

#### AC-11.6.1: Complete all Putaway Instructions

**Given** every Putaway Instruction in an assignment has been completed  
**And** no assigned quantity remains awaiting Put Away  
**When** the system evaluates the assignment  
**Then** the system marks the Putaway Assignment as Completed  
**And** records its completion date and time.

#### AC-11.6.2: Prevent premature completion

**Given** a Putaway Assignment still contains unplaced quantities  
**When** the worker attempts to complete the assignment  
**Then** the system rejects completion  
**And** identifies the remaining Putaway Instructions.

#### AC-11.6.3: Request another assignment

**Given** a Put Away Worker has completed an assignment  
**And** another completed Receiving Record has products awaiting Put Away  
**When** the worker requests additional work  
**Then** the system offers another eligible Putaway Assignment.

#### AC-11.6.4: Reject duplicate assignment completion

**Given** a Putaway Assignment has already been marked Completed  
**When** a worker attempts to complete it again  
**Then** the system rejects the duplicate completion  
**And** does not change Inventory.

#### AC-11.6.5: Preserve Put Away history

**Given** a Putaway Assignment has been completed  
**When** an authorized Manager reviews the assignment history  
**Then** the system displays the associated Receiving Record, assigned worker, completed movements, destination bins, quantities, and completion time.

#### AC-11.6.6: Reject unauthorized Put Away

**Given** the user is authenticated as a Customer Service Clerk without Put Away permission  
**When** the user attempts to confirm a Putaway Instruction  
**Then** the system denies the operation  
**And** does not update Inventory.

#### AC-11.6.7: Keep receiving and Put Away completion separate

**Given** a Supplier Order has a Completed Receiving Record  
**And** the Receiving Record contains 50 Received Units  
**And** only 30 units have been put away  
**When** the Manager reviews the receiving and Put Away information  
**Then** the system displays 50 Received Units  
**And** displays 30 Quantity Putaway Units  
**And** identifies 20 units as awaiting Put Away  
**And** does not treat the remaining 20 units as stored Inventory.

#### AC-11.6.8: Preserve consistent movement history

**Given** a Put Away Worker has verified an Item and destination bin  
**And** the worker attempts to confirm a valid placement of 10 units  
**When** the system cannot save the corresponding Putaway Movement  
**Then** the system does not increase destination Inventory  
**And** does not increase Quantity Putaway Units  
**And** preserves the original quantity awaiting Put Away  
**And** reports that the placement was not successfully recorded.
