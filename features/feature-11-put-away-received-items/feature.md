
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


## Assumptions

- **A-001:** Put Away begins only after a Receiving Record has been completed.
- **A-002:** A Supplier Order may remain Partially Received while products from a completed Receiving Record are put away.
- **A-003:** Receiving Records and original received quantities are maintained through Feature 10.
- **A-004:** Products awaiting Put Away remain associated with the Receiving Door where they were received.
- **A-005:** Put Away Workers use electronic devices and barcode scanners instead of paper instructions.
- **A-006:** Only authorized warehouse workers may accept and perform Put Away assignments.
- **A-007:** Workers may accept or reject offered assignments.
- **A-008:** Rejected assignments release unplaced quantities for reassignment.
- **A-009:** The same received units cannot be allocated to multiple active assignments.
- **A-010:** Warehouse Locations and Receiving Doors are maintained through Feature 2.
- **A-011:** Physical Inventory balances are maintained through Feature 3.
- **A-012:** Individual Item and UPC information is maintained through Feature 4.
- **A-013:** Suitable primary storage bins are preferred when sufficient capacity exists.
- **A-014:** Reserve or overflow bins may be used when primary bins cannot accommodate the products.
- **A-015:** Storage restrictions and bin capacity take precedence over travel efficiency.
- **A-016:** The Receiving Door is the starting location for putaway sequencing.
- **A-017:** The Warehouse maintains location and travel-order information for determining an efficient sequence.
- **A-018:** The exact routing algorithm requires stakeholder approval.
- **A-019:** Every destination bin must belong to the same Warehouse as the receiving work.
- **A-020:** Workers must verify the correct Item UPC and destination bin barcode before confirming placement.
- **A-021:** A Case UPC identifies an Item and the number of individual units represented by the barcode.
- **A-022:** The actual quantity placed must be confirmed separately from barcode verification.
- **A-023:** Confirmed Put Away quantities are recorded as positive whole individual units.
- **A-024:** An instruction may be split between multiple suitable bins.
- **A-025:** Selecting a different destination requires new destination barcode verification.
- **A-026:** Available capacity must be checked again when a placement is confirmed.
- **A-027:** Concurrent placements must not collectively exceed available bin capacity.
- **A-028:** Original Quantity Received is preserved during Put Away.
- **A-029:** Quantity Putaway is tracked separately from Quantity Received.
- **A-030:** Quantity Awaiting Put Away equals Quantity Received minus Quantity Putaway.
- **A-031:** Putaway Movement, Inventory, and Quantity Putaway updates must be performed consistently.
- **A-032:** Duplicate confirmations must not increase Inventory twice.
- **A-033:** Blocked work retains its remaining unplaced quantity.
- **A-034:** Supervisors are notified when no suitable storage location is available.
- **A-035:** Completed assignments and movement history remain available for auditing.
- **A-036:** The measurement used for Warehouse bin capacity requires confirmation.
- **A-037:** Damaged, missing, or otherwise unplaceable products require an approved exception process.

---

## Edge Cases

- **EC-001:** A Receiving Record has not been completed.
- **EC-002:** A Supplier Order is Partially Received, but one of its Receiving Records is Completed.
- **EC-003:** No received quantities are awaiting Put Away.
- **EC-004:** A worker rejects an offered assignment.
- **EC-005:** Two workers attempt to accept the same assignment.
- **EC-006:** Received quantities have already been allocated to another active assignment.
- **EC-007:** An assignment references a nonexistent Receiving Record.
- **EC-008:** The Receiving Door is missing or invalid.
- **EC-009:** No suitable primary storage bin exists.
- **EC-010:** The primary bin has insufficient available capacity.
- **EC-011:** A suitable reserve bin is available.
- **EC-012:** No suitable reserve bin is available.
- **EC-013:** The assigned destination bin is inactive.
- **EC-014:** The destination bin belongs to another Warehouse.
- **EC-015:** Storage restrictions prohibit using a nearby bin.
- **EC-016:** Warehouse travel-order information is missing or incomplete.
- **EC-017:** A destination becomes unavailable after the route is generated.
- **EC-018:** The remaining route must be recalculated after a destination change.
- **EC-019:** The scanned Item UPC is unknown.
- **EC-020:** The scanned Item UPC identifies the wrong Item.
- **EC-021:** A Case UPC correctly identifies the required Item.
- **EC-022:** A Case UPC represents multiple individual units.
- **EC-023:** The destination barcode is unreadable.
- **EC-024:** The destination barcode identifies the wrong bin.
- **EC-025:** The destination changes after it was previously verified.
- **EC-026:** A worker attempts placement without Item verification.
- **EC-027:** A worker attempts placement without destination verification.
- **EC-028:** The confirmed quantity is zero.
- **EC-029:** The confirmed quantity is negative or fractional.
- **EC-030:** The confirmed quantity exceeds the instruction's remaining quantity.
- **EC-031:** The confirmed quantity exceeds the received units awaiting Put Away.
- **EC-032:** The confirmed quantity exceeds available bin capacity.
- **EC-033:** A worker confirms only part of an instruction.
- **EC-034:** The remaining quantity must be placed in another bin.
- **EC-035:** Two workers attempt to fill the same bin concurrently.
- **EC-036:** Two workers attempt to confirm the same received units concurrently.
- **EC-037:** A Putaway Movement confirmation is submitted twice.
- **EC-038:** The Putaway Movement record cannot be saved.
- **EC-039:** The Inventory update fails.
- **EC-040:** The Quantity Putaway update fails.
- **EC-041:** A Putaway Instruction becomes Blocked.
- **EC-042:** A Supervisor must be notified about blocked work.
- **EC-043:** A worker attempts to complete an assignment before all quantities are placed.
- **EC-044:** A completed assignment is submitted for completion again.
- **EC-045:** An unauthorized User attempts Put Away.
- **EC-046:** Receiving is completed, but Put Away is incomplete.
- **EC-047:** Quantity Received must remain unchanged after placement.
- **EC-048:** A Manager reviews Putaway Movement history after completion.

---

## Success Criteria

- **SC-001:** Only Completed Receiving Records supply Put Away work.
- **SC-002:** Completed receiving work is available even when the Supplier Order remains Partially Received.
- **SC-003:** Available assignments identify the Supplier Order and Receiving Door.
- **SC-004:** Authorized workers can accept or reject assignments.
- **SC-005:** Rejected work remains available for reassignment.
- **SC-006:** Duplicate allocation of received quantities is prevented.
- **SC-007:** The system reports when no Put Away work is available.
- **SC-008:** Putaway Instructions identify the Item, quantity, and destination.
- **SC-009:** Destinations include aisle, row, and slot information.
- **SC-010:** Suitable primary bins are preferred.
- **SC-011:** Reserve bins are supported when necessary.
- **SC-012:** Inactive or unsuitable bins are excluded.
- **SC-013:** Putaway sequencing begins at the Receiving Door.
- **SC-014:** Sequencing follows documented, repeatable rules.
- **SC-015:** Route changes preserve completed movements.
- **SC-016:** Storage restrictions and capacity take precedence over travel distance.
- **SC-017:** Item UPC verification is required before placement.
- **SC-018:** Destination barcode verification is required before placement.
- **SC-019:** Incorrect or unknown Item and destination barcodes are rejected.
- **SC-020:** Case UPC verification preserves the requirement to confirm actual placement quantity.
- **SC-021:** Confirmed quantities are positive whole individual units.
- **SC-022:** Placement cannot exceed the remaining received quantity.
- **SC-023:** Placement cannot exceed available bin capacity.
- **SC-024:** Concurrent placements cannot overfill a bin.
- **SC-025:** Confirmed movements increase destination Inventory exactly once.
- **SC-026:** Quantity Putaway increases by the confirmed quantity.
- **SC-027:** Original Quantity Received remains unchanged.
- **SC-028:** Partial placements preserve remaining quantities.
- **SC-029:** Alternative locations require new barcode verification.
- **SC-030:** Blocked work remains outstanding until resolved.
- **SC-031:** Supervisors are notified when Put Away cannot continue.
- **SC-032:** Assignments are completed only when all assigned quantities have been placed.
- **SC-033:** Duplicate assignment completion is prevented.
- **SC-034:** Putaway Movement history is preserved.

- **SC-035:** All 45 Gherkin acceptance scenarios defined for Feature 11 have corresponding verification tests.


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
|-----------|------|-------------|
| putawayAssignmentId | UUID | Unique identifier for the assignment |
| receivingRecordId | UUID | Receiving Record associated with the assignment |
| assignedWorkerId | UUID, nullable | Worker who accepted the assignment |
| status | Enum | Offered, Accepted, In Progress, Rejected, Blocked, Completed |
| offeredAt | DateTime | Date and time the assignment was offered |
| acceptedAt | DateTime, nullable | Date and time the assignment was accepted |
| completedAt | DateTime, nullable | Date and time the assignment was completed |

### Putaway Instruction

| Attribute | Type | Description |
|-----------|------|-------------|
| putawayInstructionId | UUID | Unique identifier for the instruction |
| putawayAssignmentId | UUID | Parent Putaway Assignment |
| receivingRecordLineId | UUID | Source Receiving Record Line |
| itemId | UUID | Item being moved |
| destinationLocationId | UUID | Assigned storage location |
| quantityAssignedUnits | Integer | Number of individual units assigned |
| quantityPutawayUnits | Integer | Number of units already placed |
| sequenceNumber | Integer | Order in which the instruction should be performed |
| status | Enum | Pending, In Progress, Blocked, Completed |

### Putaway Movement

| Attribute | Type | Description |
|-----------|------|-------------|
| putawayMovementId | UUID | Unique identifier for the confirmed movement |
| putawayInstructionId | UUID | Instruction associated with the movement |
| receivingRecordLineId | UUID | Original source of the received products |
| itemId | UUID | Item moved |
| destinationLocationId | UUID | Verified destination bin |
| quantityMovedUnits | Integer | Actual quantity placed in individual units |
| performedByUserId | UUID | Worker who confirmed the movement |
| confirmedAt | DateTime | Date and time of confirmation |
| confirmationRequestId | UUID | Identifier used to prevent duplicate confirmation |

### Receiving Record

| Attribute | Type | Description |
|-----------|------|-------------|
| receivingRecordId | UUID | Unique receiving session identifier |
| supplierOrderId | UUID | Associated Supplier Order |
| receivingDoorId | UUID | Door where the products were received |
| status | Enum | Receiving session status |
| completedAt | DateTime, nullable | Time receiving was completed |

### Receiving Record Line

| Attribute | Type | Description |
|-----------|------|-------------|
| receivingRecordLineId | UUID | Unique received line identifier |
| receivingRecordId | UUID | Parent Receiving Record |
| itemId | UUID | Received Item |
| quantityReceivedUnits | Integer | Total individual units received |
| quantityPutawayUnits | Integer | Total individual units successfully put away |

**Derived value:**

`quantityAwaitingPutawayUnits = quantityReceivedUnits - quantityPutawayUnits`

### Warehouse Location

| Attribute | Type | Description |
|-----------|------|-------------|
| warehouseLocationId | UUID | Unique storage location identifier |
| warehouseId | UUID | Warehouse containing the location |
| locationBarcode | String | Barcode used to verify the destination |
| aisle | String | Aisle identifier |
| row | String | Row identifier |
| slot | String | Slot identifier |
| locationType | Enum | Primary, Reserve, Overflow |
| capacityUnits | Integer | Configured storage capacity |
| occupiedUnits | Integer | Currently occupied capacity |
| reservedUnits | Integer | Capacity reserved for other movements |
| status | Enum | Active, Inactive, Unavailable |

### Inventory

| Attribute | Type | Description |
|-----------|------|-------------|
| inventoryId | UUID | Unique Inventory record identifier |
| itemId | UUID | Item being stored |
| warehouseLocationId | UUID | Location where the Item is stored |
| quantityOnHandUnits | Integer | Quantity physically stored at the location |

### Receiving Door

| Attribute | Type | Description |
|-----------|------|-------------|
| receivingDoorId | UUID | Unique Receiving Door identifier |
| warehouseId | UUID | Warehouse containing the door |
| doorNumber | String | Receiving Door identifier |
| status | Enum | Active, Inactive |

### Individual Item

| Attribute | Type | Description |
|-----------|------|-------------|
| itemId | UUID | Unique Item identifier |
| itemNumber | String | Item number |
| description | String | Item description |
| status | Enum | Active, Inactive |

### UPC

| Attribute | Type | Description |
|-----------|------|-------------|
| upcId | UUID | Unique UPC record identifier |
| itemId | UUID | Item identified by the UPC |
| barcode | String | Scannable barcode |
| packageType | Enum | Individual, Case |
| unitsPerPackage | Integer | Number of individual units represented |

### Supplier Order

| Attribute | Type | Description |
|-----------|------|-------------|
| supplierOrderId | UUID | Unique Supplier Order identifier |
| supplierOrderNumber | String | Supplier Order number |
| status | Enum | Supplier Order processing status |

### User

| Attribute | Type | Description |
|-----------|------|-------------|
| userId | UUID | Unique User identifier |
| username | String | User login identifier |
| role | Enum | Worker, Supervisor, Manager |
| active | Boolean | Whether the User is authorized to access the system |

---

### Relationships

- One Supplier Order may have many Receiving Records.
- One Receiving Record contains one or more Receiving Record Lines.
- One Receiving Record may be associated with multiple Putaway Assignments.
- One Putaway Assignment contains one or more Putaway Instructions.
- One Putaway Instruction references one Receiving Record Line.
- One Putaway Instruction may produce multiple Putaway Movements.
- One Putaway Movement references one destination Warehouse Location.
- One Putaway Movement references the User who confirmed it.
- One Warehouse Location may contain multiple Inventory records for permitted Items.
- One Individual Item may have multiple UPC records.
- One Receiving Door belongs to one Warehouse.
- One Warehouse Location belongs to one Warehouse.

### Data Constraints

- `quantityReceivedUnits >= 0`
- `quantityPutawayUnits >= 0`
- `quantityPutawayUnits <= quantityReceivedUnits`
- `quantityAssignedUnits > 0`
- `quantityMovedUnits > 0`
- `quantityMovedUnits <= quantity remaining for the instruction`
- `quantityOnHandUnits >= 0`
- `unitsPerPackage > 0`
- A destination Warehouse Location must belong to the same Warehouse as the Receiving Door.
- A confirmed Putaway Movement must reference a valid Receiving Record Line.
- A Putaway Movement must not be recorded before successful Item and destination verification.
- Inventory and Quantity Putaway updates must succeed or fail together.
- A `confirmationRequestId` must not be processed successfully more than once.
- A completed assignment cannot contain outstanding quantities.
- Storage capacity and storage restrictions must be satisfied before confirming a movement.

### Clarifications Needed

- Confirm whether storage capacity is measured in individual units, physical dimensions, weight, or another measure.
- Confirm the warehouse routing algorithm and required travel-distance information.
- Confirm how reserved bin capacity is calculated and released.
- Confirm the approved process for damaged, missing, or unplaceable products.

---

## Gherkin Acceptance Criteria

### US-11.1: Select Received Order for Put Away

#### AC-11.1.1: Completed Receiving Record Available

```gherkin
Given a Receiving Record has a status of Completed
And the Receiving Record contains quantities awaiting Put Away
When an authorized Put Away Worker requests an assignment
Then the system shall offer an available Putaway Assignment
And the assignment shall identify the Supplier Order
And the assignment shall identify the Receiving Door
And the assignment shall show the quantities awaiting Put Away
```

#### AC-11.1.2: Receiving Not Completed

```gherkin
Given a Receiving Record has not been completed
When a Put Away Worker requests an assignment
Then the system shall not offer the received products for Put Away
```

#### AC-11.1.3: No Products Awaiting Put Away

```gherkin
Given all received quantities have already been put away
When a Put Away Worker requests an assignment
Then the system shall indicate that no Put Away work is available
```

#### AC-11.1.4: Accept Putaway Assignment

```gherkin
Given an authorized Put Away Worker has been offered an assignment
When the worker accepts the assignment
Then the system shall associate the assignment with the worker
And the assignment status shall become Accepted
And the assigned quantities shall not be allocated to another active assignment
```

#### AC-11.1.5: Reject Putaway Assignment

```gherkin
Given a Put Away Worker has been offered an assignment
When the worker rejects the assignment
Then the system shall record the rejection
And the unplaced quantities shall remain available for reassignment
```

#### AC-11.1.6: Partially Received Supplier Order

```gherkin
Given a Supplier Order has a status of Partially Received
And one Receiving Record for that Supplier Order has been completed
And the completed Receiving Record contains quantities awaiting Put Away
When an authorized worker requests an assignment
Then the system shall make the completed receiving work available for Put Away
```

---

### US-11.2: Follow Putaway Sequence

#### AC-11.2.1: Generate Putaway Sequence

```gherkin
Given a Put Away Worker has accepted an assignment
And the assignment contains multiple Items awaiting Put Away
When the system generates the Putaway Instructions
Then the system shall determine suitable destination Warehouse Locations
And the system shall arrange the instructions in an efficient sequence
And the system shall display the sequence to the worker
```

#### AC-11.2.2: Start Sequence at Receiving Door

```gherkin
Given an accepted Putaway Assignment identifies a Receiving Door
And multiple destination bins are available
When the system determines the Putaway Instruction sequence
Then the system shall use the Receiving Door as the starting location
And the sequence shall follow the configured warehouse travel-order rules
```

#### AC-11.2.3: Prefer Primary Storage Location

```gherkin
Given an Item has a suitable primary storage bin
And the primary bin has sufficient available capacity
When the system selects a destination for Put Away
Then the system shall prioritize the primary storage bin
And the system shall identify its aisle, row, and slot
```

#### AC-11.2.4: Use Reserve Storage Location

```gherkin
Given an Item's primary storage bin cannot hold the full quantity
And a suitable reserve storage bin is available
When the system determines the destination
Then the system shall recommend the reserve storage bin
And the system shall preserve any quantity that still requires placement
```

#### AC-11.2.5: Exclude Unsuitable Locations

```gherkin
Given a Warehouse contains inactive or restricted storage locations
When the system generates Putaway Instructions
Then the system shall exclude inactive locations
And the system shall exclude locations that violate storage restrictions
And every selected destination shall belong to the receiving Warehouse
```

#### AC-11.2.6: Recalculate Remaining Sequence

```gherkin
Given a Put Away Worker is following an assigned sequence
And one destination becomes unavailable
When the system selects an alternative destination
Then the system shall recalculate the remaining instruction sequence
And the system shall preserve all previously confirmed movements
And the updated sequence shall be displayed to the worker
```

#### AC-11.2.7: Storage Suitability Takes Priority

```gherkin
Given a nearby destination violates storage restrictions
And a more distant suitable destination is available
When the system determines the Putaway Instruction sequence
Then the system shall select the suitable destination
And the system shall not prioritize shorter travel over storage restrictions
```

#### AC-11.2.8: Display Next Instruction

```gherkin
Given a Put Away Worker has an active assignment
And the assignment contains outstanding Putaway Instructions
When the worker completes the current instruction
Then the system shall display the next outstanding instruction
And the instruction shall identify the Item
And the instruction shall identify the quantity to move
And the instruction shall identify the destination aisle, row, and slot
```

---

### US-11.3: Verify Putaway Location

#### AC-11.3.1: Verify Correct Item UPC

```gherkin
Given a Put Away Worker has an active Putaway Instruction
And the instruction identifies an Individual Item
When the worker scans a UPC associated with the assigned Item
Then the system shall verify the Item successfully
And the worker shall be allowed to continue destination verification
```

#### AC-11.3.2: Reject Incorrect Item UPC

```gherkin
Given a Put Away Worker has an active Putaway Instruction
And the instruction identifies an Individual Item
When the worker scans a UPC belonging to a different Item
Then the system shall reject the scanned UPC
And the system shall display an Item mismatch message
And the system shall not record a Putaway Movement
And Inventory shall remain unchanged
```

#### AC-11.3.3: Reject Unknown Item UPC

```gherkin
Given a Put Away Worker has an active Putaway Instruction
When the worker scans an unknown or unreadable Item UPC
Then the system shall report that the barcode cannot be verified
And the system shall require a valid Item UPC
And the system shall not update Inventory
```

#### AC-11.3.4: Verify Correct Destination Bin

```gherkin
Given a Put Away Worker has successfully verified the assigned Item
And the Putaway Instruction identifies a destination Warehouse Location
When the worker scans the barcode of the assigned destination bin
Then the system shall verify the destination successfully
And the system shall allow the worker to enter the quantity placed
```

#### AC-11.3.5: Reject Incorrect Destination Bin

```gherkin
Given a Put Away Worker has an active Putaway Instruction
And the instruction identifies a destination Warehouse Location
When the worker scans the barcode of a different Warehouse Location
Then the system shall reject the scanned destination
And the system shall display a destination mismatch message
And the system shall not record the placement
And Inventory shall remain unchanged
```

#### AC-11.3.6: Verify Case UPC

```gherkin
Given a Putaway Instruction identifies an Individual Item
And the Item has a configured Case UPC
When the worker scans the Case UPC
Then the system shall identify the correct Individual Item
And the system shall identify the number of individual units represented by the case
And the system shall still require confirmation of the actual quantity placed
```

#### AC-11.3.7: Require Both Item and Destination Verification

```gherkin
Given a Put Away Worker has an active Putaway Instruction
And either the Item UPC or destination barcode has not been verified
When the worker attempts to confirm placement
Then the system shall reject the confirmation
And the system shall identify the missing verification
And the system shall not create a Putaway Movement
And Inventory shall remain unchanged
```

#### AC-11.3.8: Require New Verification After Destination Change

```gherkin
Given a Put Away Worker has verified the assigned destination bin
And the worker requests an alternative destination
When the system selects a different Warehouse Location
Then the previous destination verification shall no longer be valid
And the worker shall be required to scan the new destination barcode
And the system shall prevent confirmation until the new destination is verified
```

---

### US-11.4: Complete Item Putaway

#### AC-11.4.1: Confirm Successful Putaway Movement

```gherkin
Given a Put Away Worker has an active Putaway Instruction
And the assigned Item UPC has been verified
And the destination bin barcode has been verified
And the destination has sufficient available capacity
When the worker confirms a valid quantity of 10 individual units
Then the system shall record a Putaway Movement for 10 units
And the destination Inventory shall increase by 10 units
And Quantity Putaway shall increase by 10 units
And the original Quantity Received shall remain unchanged
```

#### AC-11.4.2: Reject Invalid Quantity

```gherkin
Given a Put Away Worker has verified the Item and destination bin
When the worker enters a quantity of zero, a negative number, or a fractional number
Then the system shall reject the quantity
And the system shall require a positive whole number
And no Putaway Movement shall be recorded
And Inventory shall remain unchanged
```

#### AC-11.4.3: Prevent Excess Putaway Quantity

```gherkin
Given a Receiving Record Line has 20 units awaiting Put Away
And a Putaway Instruction has 20 units remaining
When the worker attempts to confirm 25 units
Then the system shall reject the confirmation
And the system shall indicate that the quantity exceeds the remaining quantity
And Quantity Putaway shall remain unchanged
And Inventory shall remain unchanged
```

#### AC-11.4.4: Confirm Partial Putaway

```gherkin
Given a Putaway Instruction requires 20 individual units
And the Item and destination bin have been verified
And the destination has sufficient capacity for 12 units
When the worker confirms placement of 12 units
Then the system shall record a Putaway Movement for 12 units
And the destination Inventory shall increase by 12 units
And Quantity Putaway shall increase by 12 units
And 8 units shall remain outstanding for Put Away
And the instruction shall not be marked Completed
```

#### AC-11.4.5: Reject Placement Exceeding Bin Capacity

```gherkin
Given a destination bin has available capacity for 5 units
And the worker has verified the Item and destination
When the worker attempts to confirm placement of 10 units
Then the system shall reject the confirmation
And the system shall report insufficient bin capacity
And the system shall allow the worker to enter a smaller quantity or request another location
And Inventory shall remain unchanged
```

#### AC-11.4.6: Prevent Duplicate Putaway Confirmation

```gherkin
Given a Putaway Movement confirmation has already been processed successfully
And the confirmation has a unique confirmationRequestId
When the same confirmationRequestId is submitted again
Then the system shall not create another Putaway Movement
And the system shall not increase Inventory again
And the system shall not increase Quantity Putaway again
```

#### AC-11.4.7: Preserve Consistency When Inventory Update Fails

```gherkin
Given a worker has verified the Item and destination
And the worker submits a valid Putaway Movement confirmation
When the Inventory update fails
Then the system shall not commit the Putaway Movement
And the system shall not increase Quantity Putaway
And the system shall report that the confirmation was unsuccessful
And the original quantities shall remain unchanged
```

#### AC-11.4.8: Prevent Concurrent Over-Placement

```gherkin
Given two authorized workers are processing Putaway Movements concurrently
And both movements reference the same destination bin
When the combined quantities exceed the bin's available capacity
Then the system shall prevent the destination from exceeding its capacity
And only movements that satisfy the capacity constraint shall be committed
And rejected movements shall not update Inventory or Quantity Putaway
```

---

### US-11.5: Request Another Location

#### AC-11.5.1: Request Alternative Storage Location

```gherkin
Given a Put Away Worker has an active Putaway Instruction
And the assigned destination bin cannot hold the required quantity
When the worker requests another storage location
Then the system shall search for another suitable Warehouse Location
And the system shall consider storage restrictions and available capacity
And the system shall keep the destination within the receiving Warehouse
```

#### AC-11.5.2: Recommend Suitable Alternative Bin

```gherkin
Given the assigned destination bin has insufficient capacity
And another suitable storage bin is available
When the worker requests an alternative destination
Then the system shall recommend the suitable alternative bin
And the system shall display its aisle, row, and slot
And the worker shall be required to verify the new destination barcode
```

#### AC-11.5.3: Split Quantity Between Storage Bins

```gherkin
Given a Putaway Instruction requires 20 individual units
And the assigned destination bin has capacity for 12 units
And another suitable bin is available
When the worker confirms placement of 12 units in the first bin
Then the system shall record a movement for 12 units
And 8 units shall remain awaiting Put Away
When the worker verifies the alternative bin and confirms the remaining 8 units
Then the system shall record a second movement for 8 units
And the instruction shall be marked Completed
```

#### AC-11.5.4: No Suitable Alternative Location Available

```gherkin
Given a Put Away Worker cannot place the remaining assigned quantity
And no suitable primary or reserve storage location is available
When the worker requests another destination
Then the system shall report that no suitable location is available
And the remaining quantity shall stay awaiting Put Away
And the instruction shall be marked Blocked
And an authorized Supervisor shall be notified
```

#### AC-11.5.5: Reject Alternative Location in Another Warehouse

```gherkin
Given a Putaway Assignment belongs to Warehouse A
And a proposed alternative destination belongs to Warehouse B
When the system evaluates the alternative destination
Then the system shall reject that destination
And the system shall not allow placement in Warehouse B
And the received quantity shall remain awaiting Put Away
```

#### AC-11.5.6: Alternative Destination Becomes Unavailable

```gherkin
Given a worker has received an alternative destination
And that destination becomes inactive or unavailable
When the worker attempts to confirm placement
Then the system shall reject the confirmation
And the system shall require another suitable destination
And no Inventory update shall occur
```

#### AC-11.5.7: Preserve Remaining Quantity During Blocked Putaway

```gherkin
Given a Putaway Instruction has 15 units remaining
And no suitable destination is available
When the instruction becomes Blocked
Then the system shall preserve the 15 outstanding units
And Quantity Received shall remain unchanged
And Quantity Putaway shall remain unchanged
And the assignment shall not be marked Completed
```

---

### US-11.6: Complete Putaway Assignment

#### AC-11.6.1: Complete All Putaway Instructions

```gherkin
Given a Put Away Worker has an active Putaway Assignment
And every Putaway Instruction has been completed
And all assigned quantities have been successfully placed
When the worker completes the assignment
Then the system shall mark the Putaway Assignment as Completed
And the system shall record the completion date and time
And the system shall preserve the confirmed Putaway Movements
```

#### AC-11.6.2: Prevent Premature Assignment Completion

```gherkin
Given a Putaway Assignment contains outstanding Putaway Instructions
And some assigned quantities have not been placed
When the worker attempts to complete the assignment
Then the system shall reject the completion request
And the assignment shall not be marked Completed
And the outstanding quantities shall remain awaiting Put Away
```

#### AC-11.6.3: Prevent Duplicate Assignment Completion

```gherkin
Given a Putaway Assignment has already been marked Completed
When a worker attempts to complete the same assignment again
Then the system shall reject the duplicate completion
And the system shall not create additional Putaway Movements
And Inventory shall remain unchanged
```

#### AC-11.6.4: Offer Another Assignment After Completion

```gherkin
Given a Put Away Worker has completed an assignment
And another completed Receiving Record contains quantities awaiting Put Away
When the worker requests another assignment
Then the system shall offer available Put Away work
And the new assignment shall identify the Supplier Order
And the new assignment shall identify the Receiving Door
```

#### AC-11.6.5: Prevent Unauthorized Putaway Operations

```gherkin
Given a User is not authorized to perform Put Away
When the User attempts to accept or complete a Putaway Assignment
Then the system shall deny the operation
And the system shall not modify the assignment
And Inventory shall remain unchanged
```

#### AC-11.6.6: Preserve Movement History

```gherkin
Given a Putaway Assignment has been completed
And the assignment contains confirmed Putaway Movements
When an authorized Manager reviews the assignment history
Then the system shall display the completed movements
And each movement shall identify the Item and quantity moved
And each movement shall identify the destination Warehouse Location
And each movement shall identify the worker and confirmation time
And each movement shall reference its original Receiving Record Line
```

#### AC-11.6.7: Keep Receiving and Putaway Status Separate

```gherkin
Given a Receiving Record has a status of Completed
And some received quantities are still awaiting Put Away
When an authorized User reviews the receiving and putaway information
Then the Receiving Record shall remain Completed
And the system shall identify the outstanding Put Away quantities
And the Putaway Assignment shall not be marked Completed prematurely
```

#### AC-11.6.8: Preserve Blocked Work

```gherkin
Given a Putaway Assignment contains a Blocked instruction
And the instruction has outstanding quantities
When the worker attempts to complete the assignment
Then the system shall prevent completion
And the outstanding quantities shall remain available for authorized resolution
And the system shall preserve the existing confirmed movements
```

---

## Data Ownership

### Data Owned by Feature 11: Put Away Received Items


- Feature 11 initiates an update to Quantity Putaway for the associated Receiving Record Line through an approved cross-feature operation. Feature 10 retains ownership of the Receiving Record Line, and Feature 11 MUST NOT independently modify its stored data outside that operation. [NEEDS CLARIFICATION: Confirm whether Quantity Putaway is stored on the Receiving Record Line or derived from confirmed Putaway Movements.]


**Putaway Assignment**
- Creates and maintains Putaway Assignments.
- Records the Receiving Record associated with each assignment.
- Records the worker who accepts the assignment.
- Maintains assignment status: Offered, Accepted, In Progress, Rejected, Blocked, or Completed.
- Records assignment acceptance and completion timestamps.
- Prevents the same received quantities from being allocated to multiple active assignments.

**Putaway Instruction**
- Creates and maintains Putaway Instructions for accepted assignments.
- Records the assigned Item, quantity, destination Warehouse Location, and sequence number.
- Tracks completed and outstanding quantities for each instruction.
- Maintains instruction status: Pending, In Progress, Blocked, or Completed.
- Recalculates remaining instructions when destinations change.
- Preserves sequencing changes for audit purposes.

**Putaway Movement**
- Creates an immutable record of each successfully confirmed placement.
- Records the source Receiving Record Line, Item, destination bin, quantity, worker, and confirmation timestamp.
- Maintains a unique confirmation request identifier to prevent duplicate movements.
- Preserves movement history for inventory reconciliation and auditing.

### Data Owned by Other Features

**Feature 2: Maintain Warehouses**
- Owns Warehouse information, Receiving Doors, and Warehouse Locations.
- Maintains location identifiers, barcodes, aisle, row, slot, status, and configured storage capacity.
- Feature 11 reads this information when selecting and verifying destinations.
- Feature 11 MUST NOT independently modify Warehouse master data.

**Feature 3: Maintain Inventory**
- Owns Inventory records and quantities stored at Warehouse Locations.
- Feature 11 requests Inventory updates after successful Putaway Movement confirmation.
- Inventory updates MUST be coordinated with Putaway Movement creation and Quantity Putaway updates.
- Feature 11 MUST NOT create an independent, conflicting Inventory balance.

**Feature 4: Maintain Items**
- Owns Individual Item information and configured UPCs.
- Maintains Item identifiers, descriptions, package types, and units per package.
- Feature 11 reads this information to verify Item and Case UPCs.
- Feature 11 MUST NOT modify Item or UPC master data.

**Feature 9: Create Supplier Order**
- Owns Supplier Orders and their purchasing information.
- Feature 11 references Supplier Orders to identify the source of received products.
- Feature 11 MUST NOT change Supplier Order quantities or purchasing information.

**Feature 10: Receive Supplier Order**
- Owns Receiving Records, Receiving Record Lines, and original Quantity Received.
- Feature 11 reads completed Receiving Records to identify products awaiting Put Away.
- Feature 11 updates or requests an update to Quantity Putaway for the associated Receiving Record Line.
- Quantity Received MUST remain unchanged during Put Away.
- Receiving completion and Put Away completion MUST remain separate.

### Shared Data and Authorization

**User and Role Information**
- User accounts and role permissions are managed through the Warehouse System's shared authentication and authorization components.
- Feature 11 uses these permissions to determine which workers may accept and perform assignments.
- Supervisors and Managers may review blocked work and movement history according to their authorized permissions.
- Feature 11 MUST NOT independently maintain a separate User account database.

### Cross-Feature Data Integrity

- A Putaway Assignment MUST reference a valid Receiving Record.
- A Putaway Instruction MUST reference a valid Receiving Record Line and Individual Item.
- A Putaway Movement MUST reference its original Receiving Record Line.
- Every destination Warehouse Location MUST belong to the receiving Warehouse.
- Quantity Putaway MUST NOT exceed Quantity Received.
- Confirmed Putaway Movements MUST update Inventory and Quantity Putaway consistently.
- Failed confirmations MUST NOT leave partially committed movement or inventory changes.
- Duplicate confirmation requests MUST NOT increase Inventory more than once.
- Concurrent workers MUST NOT allocate or place the same received units more than once.
- Concurrent placements MUST NOT exceed available bin capacity.
- Completed Putaway Movements MUST remain available for auditing.

### Design Clarifications

- **[NEEDS CLARIFICATION]** Confirm whether Quantity Putaway is physically stored on the Receiving Record Line or maintained through a separate inventory movement ledger.
- **[NEEDS CLARIFICATION]** Confirm the shared transaction or service boundary responsible for coordinating Putaway Movement, Inventory, and Quantity Putaway updates.
- **[NEEDS CLARIFICATION]** Confirm which feature owns the authoritative capacity reservation information.
- **[NEEDS CLARIFICATION]** Confirm the final shared User roles and permissions used across Warehouse features.

---

## API Requirements

### API Overview

Feature 11 requires REST API endpoints to support the Put Away workflow.

All endpoints MUST:
- Use JSON request and response bodies where applicable.
- Require authentication and role-based authorization.
- Validate all supplied identifiers and quantities.
- Return appropriate HTTP status codes.
- Prevent duplicate inventory updates.
- Preserve the separation between Receiving and Put Away.
- Return consistent error responses.
- Record confirmed movements for auditing.

**Base API Path:** `/api/putaway`

The following endpoints are proposed design contracts and may be refined during implementation.

### API-11.1: List Available Putaway Assignments

**Endpoint:** `GET /api/putaway/assignments/available`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Retrieve available assignments associated with completed Receiving Records.

**Response Data:**
- putawayAssignmentId
- receivingRecordId
- supplierOrderId
- supplierOrderNumber
- receivingDoorId
- receivingDoorNumber
- quantityAwaitingPutawayUnits
- status


**Validation and Behavior:**
- Verify that the assignment exists.
- Allow rejection only while the assignment status is Offered.
- Record the rejection and change the assignment status to Rejected.
- Release the offered quantities for reassignment without changing Quantity Received, Quantity Putaway, or Inventory.
- Reject attempts to use this endpoint for an assignment that is already Accepted, In Progress, Blocked, or Completed.
- Reassignment of work already in progress requires a separate authorized process. [NEEDS CLARIFICATION: Confirm the approved reassignment workflow and responsible roles.]


### API-11.2: Offer Putaway Assignment

**Endpoint:** `POST /api/putaway/assignments/offer`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Request an available Putaway Assignment.

**Request Data:**
- warehouseId

**Response Data:**
- putawayAssignmentId
- receivingRecordId
- receivingDoorId
- assignedQuantities
- status

**Validation and Behavior:**
- Verify that receiving has been completed.
- Verify that quantities remain awaiting Put Away.
- Prevent the same received quantities from being allocated twice.
- Return a clear response when no work is available.

### API-11.3: Accept Putaway Assignment

**Endpoint:** `POST /api/putaway/assignments/{assignmentId}/accept`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Accept an offered assignment.

**Request Data:**
- assignmentId

**Response Data:**
- putawayAssignmentId
- assignedWorkerId
- status
- acceptedAt

**Validation and Behavior:**
- Verify that the assignment exists.
- Verify that the assignment is available for acceptance.
- Associate the assignment with the authenticated worker.
- Change the status to Accepted.
- Prevent concurrent acceptance by multiple workers.

### API-11.4: Reject Putaway Assignment

**Endpoint:** `POST /api/putaway/assignments/{assignmentId}/reject`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Reject an offered assignment.

**Request Data:**
- assignmentId
- rejectionReason (optional)

**Response Data:**
- putawayAssignmentId
- status

**Validation and Behavior:**
- Verify that the assignment exists.
- Record the rejection.
- Release unplaced quantities for reassignment.
- Preserve previously confirmed movements, if any.

### API-11.5: Generate Putaway Sequence

**Endpoint:** `POST /api/putaway/assignments/{assignmentId}/sequence`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Generate or recalculate the sequence of Putaway Instructions.

**Request Data:**
- assignmentId
- recalculate (Boolean)

**Response Data:**
- putawayAssignmentId
- receivingDoorId
- instructions
- sequenceNumber
- itemId
- quantityAssignedUnits
- destinationLocationId
- aisle
- row
- slot

**Validation and Behavior:**
- Use the Receiving Door as the starting location.
- Consider configured warehouse travel information.
- Prefer suitable primary storage bins.
- Use suitable reserve locations when necessary.
- Respect capacity and storage restrictions.
- Exclude inactive or unavailable locations.
- Preserve completed movements when recalculating.
- Apply documented, repeatable sequencing rules.

### API-11.6: Verify Item UPC

**Endpoint:** `POST /api/putaway/instructions/{instructionId}/verify-item`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Verify the Item being put away.

**Request Data:**
- instructionId
- scannedUPC

**Response Data:**
- verified
- itemId
- itemNumber
- packageType
- unitsPerPackage
- message

**Validation and Behavior:**
- Verify that the scanned UPC exists.
- Verify that it identifies the assigned Item.
- Support Individual Item and Case UPCs.
- Reject incorrect or unknown UPCs.
- Do not update Inventory during verification.

### API-11.7: Verify Destination Bin

**Endpoint:** `POST /api/putaway/instructions/{instructionId}/verify-location`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Verify the physical destination before placement.

**Request Data:**
- instructionId
- scannedLocationBarcode

**Response Data:**
- verified
- destinationLocationId
- aisle
- row
- slot
- message

**Validation and Behavior:**
- Verify that the destination barcode exists.
- Verify that the scanned location matches the assigned destination.
- Verify that the location belongs to the receiving Warehouse.
- Reject inactive, unavailable, or incorrect locations.
- Require new verification if the destination changes.

### API-11.8: Confirm Putaway Movement

**Endpoint:** `POST /api/putaway/instructions/{instructionId}/movements`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Confirm the quantity physically placed into a verified destination bin.

**Request Data:**
- instructionId
- destinationLocationId
- quantityMovedUnits
- confirmationRequestId

**Response Data:**
- putawayMovementId
- instructionId
- destinationLocationId
- quantityMovedUnits
- quantityRemainingUnits
- confirmedAt
- instructionStatus

**Validation and Behavior:**
- Require successful Item UPC verification.
- Require successful destination barcode verification.
- Require a positive whole-unit quantity.
- Prevent placement beyond the instruction's remaining quantity.
- Prevent Quantity Putaway from exceeding Quantity Received.
- Check available destination capacity at confirmation time.
- Prevent concurrent overfilling or double placement.
- Create the Putaway Movement and update Inventory and Quantity Putaway atomically.
- Reject duplicate confirmation requests without applying the movement twice.
- Preserve original Quantity Received.

### API-11.9: Request Alternative Destination

**Endpoint:** `POST /api/putaway/instructions/{instructionId}/alternative-location`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Find another suitable storage location.

**Request Data:**
- instructionId
- reason

**Response Data:**
- instructionId
- alternativeLocationId
- aisle
- row
- slot
- availableCapacity
- message

**Validation and Behavior:**
- Consider available capacity and storage restrictions.
- Keep destinations within the receiving Warehouse.
- Exclude inactive and unavailable bins.
- Invalidate the previous destination verification when the destination changes.
- Preserve the remaining quantity.
- Recalculate outstanding instructions when necessary.

### API-11.10: Block Putaway Instruction

**Endpoint:** `POST /api/putaway/instructions/{instructionId}/block`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Record an instruction that cannot currently be completed.

**Request Data:**
- instructionId
- reason

**Response Data:**
- instructionId
- status
- quantityRemainingUnits
- supervisorNotificationStatus

**Validation and Behavior:**
- Verify that the instruction exists.
- Preserve all unplaced quantities.
- Change the instruction status to Blocked.
- Notify an authorized Supervisor.
- Preserve previously confirmed movements.
- Prevent premature completion of the assignment.

### API-11.11: Complete Putaway Assignment

**Endpoint:** `POST /api/putaway/assignments/{assignmentId}/complete`

**Authorized Roles:** Put Away Worker, Supervisor, Manager

**Purpose:** Complete an assignment after all assigned quantities have been placed.

**Request Data:**
- assignmentId

**Response Data:**
- putawayAssignmentId
- status
- completedAt
- totalQuantityPutawayUnits

**Validation and Behavior:**
- Verify that the assignment exists.
- Verify that all assigned instructions are Completed.
- Verify that no outstanding assigned quantities remain.
- Reject duplicate completion requests.
- Record the completion timestamp.
- Preserve movement history.

### API-11.12: Retrieve Putaway Movement History

**Endpoint:** `GET /api/putaway/assignments/{assignmentId}/movements`

**Authorized Roles:** Supervisor, Manager, and other explicitly authorized personnel

**Purpose:** Retrieve confirmed movements for auditing and reconciliation.

**Response Data:**
- putawayMovementId
- putawayAssignmentId
- receivingRecordLineId
- itemId
- destinationLocationId
- quantityMovedUnits
- performedByUserId
- confirmedAt

**Validation and Behavior:**
- Verify authorization to view the requested Warehouse information.
- Return confirmed movements without modifying Inventory.
- Preserve traceability to the original Receiving Record Line.

### Standard HTTP Response Codes

| Status Code | Meaning |
|-------------|---------|
| 200 OK | Request completed successfully |
| 201 Created | New assignment or movement created |
| 400 Bad Request | Invalid request data |
| 401 Unauthorized | Authentication required |
| 403 Forbidden | User lacks permission |
| 404 Not Found | Assignment, instruction, or location not found |
| 409 Conflict | Assignment conflict, duplicate operation, or insufficient capacity |
| 422 Unprocessable Content | Quantity or business-rule validation failed |
| 500 Internal Server Error | Unexpected server failure |

### API Security Requirements

- Authentication MUST be required for all Put Away operations.
- Authorization MUST be checked on the server for every request.
- A worker MUST NOT modify another worker's active assignment without authorized reassignment.
- Warehouse access restrictions MUST be enforced.
- Client-provided quantities, UPCs, and destination identifiers MUST be validated.
- The system MUST NOT trust client-side barcode verification alone.
- Confirmed movements MUST be traceable to the authenticated User.
- Errors MUST NOT expose sensitive system information.

### API Transaction and Concurrency Requirements

- Assignment acceptance MUST prevent multiple workers from claiming the same assignment.
- Movement confirmation MUST prevent the same received units from being placed more than once.
- Capacity validation MUST account for concurrent movements.
- Putaway Movement creation, Inventory updates, and Quantity Putaway updates MUST succeed or fail together.
- Duplicate confirmation requests MUST be handled idempotently.
- Failed requests MUST NOT leave inconsistent inventory balances.

### API Design Clarifications

- **[NEEDS CLARIFICATION]** Confirm whether assignment offering and acceptance should be separate API operations.
- **[NEEDS CLARIFICATION]** Confirm the final authorization roles and permission names.
- **[NEEDS CLARIFICATION]** Confirm the routing algorithm and whether sequence generation is synchronous or asynchronous.
- **[NEEDS CLARIFICATION]** Confirm the transaction boundary shared with Feature 3 and Feature 10.
- **[NEEDS CLARIFICATION]** Confirm whether barcode verification state is stored server-side or represented by short-lived verification tokens.
- **[NEEDS CLARIFICATION]** Confirm how blocked instructions are reopened or reassigned after Supervisor resolution.

---

## Screen Requirements

### Screen Overview

Feature 11 requires an electronic, scanner-friendly user interface for managing Put Away assignments and confirming the movement of received products into warehouse storage.

The screens MUST support:
- Role-based access.
- Barcode scanning.
- Clear instructions for warehouse workers.
- Efficient navigation between Putaway Instructions.
- Quantity confirmation in individual units.
- Primary and reserve storage locations.
- Alternative destination requests.
- Blocked work and Supervisor notifications.
- Assignment completion.
- Movement history and auditing.

The interface MUST support the Warehouse System's no-paper workflow.

Screen designs and navigation flows will be documented in Figma before implementation.

### UI-11A: Available Putaway Assignments Screen

**Purpose:** Display completed receiving work available for Put Away.

**Authorized Users:** Put Away Worker, Supervisor, Manager

**Displayed Information:**
- Supplier Order number.
- Receiving Record identifier.
- Receiving Door number.
- Quantity awaiting Put Away.
- Assignment status.
- Warehouse identifier.

**User Actions:**
- View available assignments.
- Request an assignment.
- Accept an offered assignment.
- Reject an offered assignment.
- Refresh available work.

**Validation and Behavior:**
- Display only eligible completed receiving work.
- Do not offer quantities already allocated to another active assignment.
- Show a message when no work is available.
- Prevent unauthorized users from accepting assignments.

### UI-11B: Putaway Assignment Details Screen

**Purpose:** Display the details of an accepted assignment.

**Authorized Users:** Assigned Put Away Worker, Supervisor, Manager

**Displayed Information:**
- Putaway Assignment identifier.
- Supplier Order number.
- Receiving Door number.
- Assigned worker.
- Assignment status.
- Items awaiting Put Away.
- Assigned quantities.
- Remaining quantities.
- Number of outstanding instructions.

**User Actions:**
- Start Put Away.
- View assigned instructions.
- View the generated sequence.
- Return to available assignments.

**Validation and Behavior:**
- Display the correct Receiving Door.
- Preserve the relationship to the original Receiving Record.
- Prevent workers from modifying assignments they are not authorized to perform.

### UI-11C: Putaway Sequence Screen

**Purpose:** Guide the worker through an efficient sequence of storage locations.

**Authorized Users:** Assigned Put Away Worker, Supervisor, Manager

**Displayed Information:**
- Receiving Door starting location.
- Ordered Putaway Instructions.
- Item number and description.
- Quantity assigned.
- Quantity remaining.
- Destination aisle, row, and slot.
- Instruction status.
- Sequence number.

**User Actions:**
- View the next instruction.
- Select the current instruction.
- Request an alternative destination.
- Refresh the remaining sequence.

**Validation and Behavior:**
- Begin sequencing from the Receiving Door.
- Prefer suitable primary storage locations.
- Support suitable reserve locations.
- Respect capacity and storage restrictions.
- Exclude inactive or unavailable destinations.
- Recalculate remaining instructions when necessary.
- Preserve completed movements when recalculating.

### UI-11D: Item UPC Verification Screen

**Purpose:** Verify the product before it is placed in storage.

**Authorized Users:** Assigned Put Away Worker, Supervisor, Manager

**Displayed Information:**
- Expected Item number.
- Item description.
- Required quantity.
- Remaining quantity.
- UPC scan input.
- Verification result.
- Package type.
- Units per package, when applicable.

**User Actions:**
- Scan Item UPC.
- Rescan Item UPC.
- Continue after successful verification.
- Return to the current instruction.

**Validation and Behavior:**
- Accept a configured UPC for the assigned Item.
- Reject unknown or incorrect UPCs.
- Support Individual Item and Case UPC verification.
- Display clear error messages.
- Do not update Inventory during barcode verification.
- Require successful Item verification before movement confirmation.

### UI-11E: Destination Bin Verification Screen

**Purpose:** Confirm that the worker is placing products in the assigned storage location.

**Authorized Users:** Assigned Put Away Worker, Supervisor, Manager

**Displayed Information:**
- Assigned destination barcode.
- Aisle.
- Row.
- Slot.
- Location type.
- Available capacity.
- Barcode scan input.
- Verification status.

**User Actions:**
- Scan destination barcode.
- Rescan destination barcode.
- Request another location.
- Continue after successful verification.

**Validation and Behavior:**
- Verify that the scanned barcode matches the assigned destination.
- Reject unknown or incorrect location barcodes.
- Reject inactive or unavailable locations.
- Prevent placement in another Warehouse.
- Require new verification when the destination changes.

### UI-11F: Confirm Putaway Quantity Screen

**Purpose:** Record the actual quantity placed in a verified destination bin.

**Authorized Users:** Assigned Put Away Worker, Supervisor, Manager

**Displayed Information:**
- Item number and description.
- Verified destination.
- Quantity assigned.
- Quantity already placed.
- Quantity remaining.
- Available bin capacity.
- Quantity confirmation field.
- Confirmation status.

**User Actions:**
- Enter actual quantity placed.
- Confirm Putaway Movement.
- Enter a smaller quantity.
- Request another location.
- Return to the current instruction.

**Validation and Behavior:**
- Require successful Item and destination verification.
- Accept only positive whole individual units.
- Reject quantities exceeding the instruction remainder.
- Reject quantities exceeding received units awaiting Put Away.
- Reject quantities exceeding available bin capacity.
- Prevent duplicate confirmation.
- Display success only after the movement and Inventory updates are committed.
- Preserve remaining quantities after partial placement.

### UI-11G: Alternative Storage Location Screen

**Purpose:** Allow a worker to request a different destination when the assigned bin cannot hold the products.

**Authorized Users:** Assigned Put Away Worker, Supervisor, Manager

**Displayed Information:**
- Current destination.
- Reason for requesting an alternative.
- Remaining quantity.
- Suggested alternative locations.
- Aisle, row, and slot.
- Available capacity.
- Storage location status.

**User Actions:**
- Request an alternative location.
- Select an offered alternative.
- Return to the current instruction.
- Report that no suitable location is available.

**Validation and Behavior:**
- Display only suitable locations within the receiving Warehouse.
- Respect capacity and storage restrictions.
- Exclude inactive or unavailable locations.
- Require barcode verification for the selected alternative.
- Recalculate the remaining sequence when necessary.
- Preserve outstanding quantities.

### UI-11H: Blocked Putaway Instruction Screen

**Purpose:** Record work that cannot currently be completed and notify a Supervisor.

**Authorized Users:** Put Away Worker, Supervisor, Manager

**Displayed Information:**
- Putaway Instruction identifier.
- Item number and description.
- Remaining quantity.
- Receiving Door.
- Last attempted destination.
- Reason for blockage.
- Instruction status.
- Supervisor notification status.

**User Actions:**
- Report blocked work.
- Enter or select a blockage reason.
- Submit the exception.
- Return to outstanding instructions.

**Validation and Behavior:**
- Preserve the remaining unplaced quantity.
- Do not mark the instruction Completed.
- Notify an authorized Supervisor.
- Preserve previously confirmed movements.
- Prevent Inventory updates for unconfirmed placement.

### UI-11I: Putaway Assignment Completion Screen

**Purpose:** Confirm that all assigned quantities have been successfully placed.

**Authorized Users:** Assigned Put Away Worker, Supervisor, Manager

**Displayed Information:**
- Assignment identifier.
- Supplier Order number.
- Receiving Record identifier.
- Assigned worker.
- Total assigned quantity.
- Total placed quantity.
- Remaining quantity.
- Completed instructions.
- Blocked instructions.
- Assignment status.

**User Actions:**
- Review assignment progress.
- Complete the assignment.
- Return to outstanding instructions.
- Request another assignment after completion.

**Validation and Behavior:**
- Allow completion only when all assigned quantities are placed.
- Prevent completion when instructions remain outstanding or Blocked.
- Prevent duplicate completion.
- Record the completion timestamp.
- Display a confirmation message after successful completion.

### UI-11J: Putaway Movement History Screen

**Purpose:** Allow authorized personnel to review confirmed movements for auditing and reconciliation.

**Authorized Users:** Supervisor, Manager, and other explicitly authorized personnel

**Displayed Information:**
- Putaway Movement identifier.
- Assignment identifier.
- Receiving Record Line.
- Supplier Order number.
- Item number and description.
- Destination Warehouse Location.
- Quantity moved.
- Worker who confirmed the movement.
- Confirmation date and time.

**User Actions:**
- View movement history.
- Filter movements by assignment.
- Filter by Item.
- Filter by date.
- Review the original receiving source.

**Validation and Behavior:**
- Display only authorized Warehouse information.
- Preserve confirmed movement records.
- Do not allow ordinary workers to modify completed movements.
- Maintain traceability to Receiving Records.

### Screen Navigation Flow

1. Available Putaway Assignments
2. Putaway Assignment Details
3. Putaway Sequence
4. Item UPC Verification
5. Destination Bin Verification
6. Confirm Putaway Quantity
7. Next Putaway Instruction or Alternative Storage Location
8. Blocked Instruction, if necessary
9. Putaway Assignment Completion
10. Return to Available Putaway Assignments

Supervisors and Managers may access Putaway Movement History and blocked work according to their permissions.

### Role-Based Screen Access

| Screen | Put Away Worker | Supervisor | Manager |
|--------|-----------------|------------|---------|
| Available Assignments | Yes | Yes | Yes |
| Assignment Details | Assigned work | Yes | Yes |
| Putaway Sequence | Assigned work | Yes | Yes |
| Item UPC Verification | Assigned work | Yes | Yes |
| Destination Verification | Assigned work | Yes | Yes |
| Confirm Quantity | Assigned work | Yes | Yes |
| Alternative Location | Assigned work | Yes | Yes |
| Blocked Instruction | Report | Review | Review |
| Assignment Completion | Assigned work | Yes | Yes |
| Movement History | Restricted | Yes | Yes |

### General UI Requirements

- All screens MUST follow the Warehouse System's shared UI style conventions.
- The interface MUST be usable on warehouse scanning devices.
- Barcode fields SHOULD support automatic focus when scanning is expected.
- Error messages MUST clearly explain the required corrective action.
- Quantity fields MUST display individual units.
- The current Item, destination, and remaining quantity MUST be clearly visible.
- Navigation SHOULD minimize unnecessary worker interaction.
- The system MUST not display a successful movement confirmation before the backend commits the update.
- Screen actions MUST respect server-side authorization.
- The UI MUST not permit workers to modify Item or Warehouse master data through Put Away screens.

### Figma Design Deliverables

The Figma design SHOULD include:
- Wireframes for UI-11A through UI-11J.
- Screen navigation connections.
- Barcode verification success and failure states.
- Quantity validation error states.
- Partial placement workflow.
- Alternative location workflow.
- Blocked instruction workflow.
- Assignment completion confirmation.
- Role-based screen visibility.
- Mobile or handheld scanner layouts.

### Screen Design Clarifications

- **[NEEDS CLARIFICATION]** Confirm the warehouse scanning device screen size and input capabilities.
- **[NEEDS CLARIFICATION]** Confirm whether barcode scanning uses a hardware scanner, camera, or both.
- **[NEEDS CLARIFICATION]** Confirm whether Supervisors may directly perform Put Away operations or only oversee and resolve exceptions.
- **[NEEDS CLARIFICATION]** Confirm whether workers may manually select alternative bins or must use system recommendations.
- **[NEEDS CLARIFICATION]** Confirm whether Figma requires separate mobile and desktop layouts.

---

## Definition of Done

Feature 11: Put Away Received Items is considered complete only when the approved requirements, design, implementation, and verification activities have been satisfied.

### Requirements and Design

- [ ] All six User Stories (US-11.1 through US-11.6) are reviewed and approved.
- [ ] All 80 Functional Requirements (FR-001 through FR-080) are reviewed and traceable to implementation and tests.
- [ ] Assumptions, Edge Cases, and Success Criteria are reviewed.
- [ ] All 45 Gherkin Acceptance Criteria are implemented and verified.
- [ ] The Initial Data Model is reviewed for consistency with related Warehouse features.
- [ ] Data ownership responsibilities are confirmed.
- [ ] API contracts are reviewed and approved.
- [ ] Required screens and navigation flows are documented in Figma.
- [ ] All outstanding design clarifications are resolved or explicitly approved for deferral.

### Putaway Assignment Management

- [ ] The system identifies Completed Receiving Records containing quantities awaiting Put Away.
- [ ] Completed receiving work can be put away even when the Supplier Order remains Partially Received.
- [ ] Authorized workers can request, accept, and reject assignments.
- [ ] Assignment acceptance records the assigned worker.
- [ ] Rejected work remains available for reassignment.
- [ ] Concurrent workers cannot claim the same assignment or allocate the same received units twice.
- [ ] Assignment statuses are maintained correctly.
- [ ] The system reports when no Put Away work is available.

### Putaway Sequencing

- [ ] The system generates Putaway Instructions for accepted assignments.
- [ ] Each instruction identifies the Item, quantity, and destination Warehouse Location.
- [ ] The system displays the destination aisle, row, and slot.
- [ ] The Receiving Door is used as the starting location for sequencing.
- [ ] Suitable primary storage bins are preferred.
- [ ] Reserve storage bins are supported when necessary.
- [ ] Inactive, unavailable, restricted, or unsuitable locations are excluded.
- [ ] Sequencing follows approved and repeatable routing rules.
- [ ] Remaining instructions are recalculated when destinations change.
- [ ] Completed movements remain unchanged after recalculation.

### Barcode Verification

- [ ] Workers can scan Item UPCs using the supported scanning devices.
- [ ] Correct Item UPCs are accepted.
- [ ] Incorrect, unknown, and unreadable Item UPCs are rejected.
- [ ] Case UPCs identify the correct Item and units per package.
- [ ] Workers must verify the destination bin barcode.
- [ ] Incorrect, unknown, and unreadable destination barcodes are rejected.
- [ ] Item and destination verification are required before movement confirmation.
- [ ] Changing the destination invalidates the previous destination verification.
- [ ] Failed verification does not modify Inventory.

### Quantity and Inventory Management

- [ ] Workers can confirm actual quantities placed in individual units.
- [ ] Zero, negative, and fractional quantities are rejected.
- [ ] Confirmed quantities cannot exceed outstanding instruction quantities.
- [ ] Quantity Putaway cannot exceed Quantity Received.
- [ ] Destination capacity is checked at confirmation time.
- [ ] Confirmations that exceed available bin capacity are rejected.
- [ ] Concurrent confirmations cannot overfill a destination bin.
- [ ] Confirmed movements increase destination Inventory exactly once.
- [ ] Quantity Putaway increases by the confirmed movement quantity.
- [ ] Original Quantity Received remains unchanged.
- [ ] Partial placements preserve the remaining outstanding quantity.
- [ ] Movement creation, Inventory updates, and Quantity Putaway updates succeed or fail together.
- [ ] Duplicate confirmation requests cannot create duplicate Inventory updates.

### Alternative Locations and Exceptions

- [ ] Workers can request alternative storage locations.
- [ ] Alternative locations satisfy Warehouse boundaries, capacity, and storage restrictions.
- [ ] Alternative destinations require new barcode verification.
- [ ] Instructions can be split between multiple suitable bins.
- [ ] The system identifies when no suitable location is available.
- [ ] Unplaceable quantities remain outstanding.
- [ ] Blocked instructions are recorded correctly.
- [ ] Authorized Supervisors are notified of blocked work.
- [ ] Previously confirmed movements remain preserved during exception handling.

### Assignment Completion

- [ ] The system identifies when all assigned instructions are complete.
- [ ] Assignments cannot be completed while quantities remain outstanding.
- [ ] Assignments containing unresolved Blocked instructions cannot be completed.
- [ ] Completed assignments record their completion timestamps.
- [ ] Duplicate completion requests are rejected.
- [ ] Completed assignments cannot be modified through ordinary Put Away operations.
- [ ] Workers can request another assignment after completion.
- [ ] Putaway Movement history remains available for auditing.

### Security and Authorization

- [ ] All Put Away APIs require authentication.
- [ ] Server-side role-based authorization is enforced.
- [ ] Unauthorized Users cannot accept, modify, or complete assignments.
- [ ] Workers cannot modify another worker's active assignment without authorization.
- [ ] Warehouse access restrictions are enforced.
- [ ] Workers cannot modify Item or Warehouse master data through Put Away operations.
- [ ] Confirmed movements record the authenticated worker.

### API Verification

- [ ] All approved Feature 11 API endpoints are implemented.
- [ ] API request and response data follow the approved contracts.
- [ ] Invalid identifiers and quantities return appropriate errors.
- [ ] Missing or unauthorized resources are handled correctly.
- [ ] Concurrent assignment and placement conflicts are handled safely.
- [ ] Movement confirmation is idempotent.
- [ ] Failed transactions do not leave inconsistent Inventory or Quantity Putaway values.
- [ ] API integration tests verify cross-feature data consistency.

### User Interface Verification

- [ ] Required screens UI-11A through UI-11J are implemented according to approved designs.
- [ ] The interface supports the approved warehouse scanning devices.
- [ ] Workers can complete the normal Put Away workflow without paper.
- [ ] Barcode success and failure messages are clear.
- [ ] Quantity validation messages are clear.
- [ ] Partial placement and alternative location workflows are supported.
- [ ] Blocked work is visible to authorized personnel.
- [ ] Assignment completion is clearly confirmed.
- [ ] Screen access follows approved role permissions.

### Testing and Quality

- [ ] Unit tests cover assignment, sequencing, barcode, quantity, capacity, and completion rules.
- [ ] Integration tests cover Receiving Record, Inventory, Item, and Warehouse Location interactions.
- [ ] Acceptance tests cover all 45 Gherkin scenarios.
- [ ] Concurrency tests verify that duplicate allocation, over-placement, and bin overfilling are prevented.
- [ ] Failure tests verify that unsuccessful updates do not partially modify Inventory.
- [ ] Regression tests verify that Feature 11 does not break Features 2, 3, 4, 9, or 10.
- [ ] All required tests pass in the approved test environment.
- [ ] No unresolved critical or high-severity defects remain.

### Documentation and Review

- [ ] Feature documentation matches the implemented behavior.
- [ ] API documentation is updated.
- [ ] Figma designs reflect the approved screens.
- [ ] Important design decisions and approved clarifications are recorded.
- [ ] Movement history and audit requirements are documented.
- [ ] Feature 11 is reviewed and approved according to the project's Definition of Done.

---

## Out of Scope

### Functionality Excluded from Feature 11

The following activities are outside the scope of Feature 11: Put Away Received Items. They are handled by other Warehouse features or require separate approval.

**1. Supplier Order Creation and Maintenance**
- Creating Supplier Orders.
- Editing Supplier Order quantities, prices, or supplier information.
- Approving or canceling Supplier Orders.
- Managing purchasing and payment terms.
- These activities belong to Feature 9 and related supplier-management features.

**2. Receiving Supplier Orders**
- Recording products as received from suppliers.
- Comparing received quantities with Supplier Order quantities.
- Reconciling receiving shortages, overages, or discrepancies.
- Recording Bill of Lading information.
- Completing Receiving Records.
- These activities belong to Feature 10.
- Feature 11 begins only after a Receiving Record has been completed.

**3. Warehouse and Location Maintenance**
- Creating or deleting Warehouses.
- Creating or modifying Receiving Doors.
- Creating, renaming, or deactivating Warehouse Locations.
- Maintaining aisle, row, and slot master information.
- Configuring Warehouse storage restrictions.
- These activities belong to Feature 2.

**4. Item and UPC Maintenance**
- Creating or modifying Individual Item records.
- Changing Item descriptions or identifying information.
- Creating or modifying UPC records.
- Changing Case UPC quantities or units per package.
- Activating or deactivating Items.
- These activities belong to Feature 4.

**5. General Inventory Maintenance**
- Performing manual Inventory adjustments unrelated to confirmed Put Away.
- Conducting physical Inventory counts.
- Correcting historical Inventory discrepancies.
- Managing Inventory outside the Put Away workflow.
- These activities belong to Feature 3 and other applicable Inventory features.
- Feature 11 only initiates Inventory updates associated with confirmed Putaway Movements.

**6. Store Order Picking and Shipping**
- Creating Store Orders.
- Selecting products for Store Orders.
- Picking products from storage locations.
- Preparing shipments.
- Loading delivery trucks.
- Confirming shipment or delivery.
- These activities belong to the applicable Store Order, Picking, and Shipping features.

**7. General Inventory Movement**
- Moving already stored Inventory between bins for reasons unrelated to receiving.
- Reorganizing existing Inventory.
- Performing routine Inventory transfers.
- These activities belong to the separate Move Inventory feature.
- Feature 11 handles only the initial placement of received products into storage.

**8. User Account and Role Administration**
- Creating User accounts.
- Changing passwords.
- Assigning or removing system roles.
- Maintaining authentication settings.
- Feature 11 uses shared authentication and authorization services but does not manage User accounts.

**9. Warehouse Hardware Administration**
- Purchasing or configuring barcode scanners.
- Installing or maintaining warehouse networking equipment.
- Repairing scanning devices.
- Printing or replacing physical bin barcode labels.
- Feature 11 assumes approved scanning devices and readable barcodes are available.

**10. Advanced Warehouse Optimization**
- Predicting future storage requirements.
- Automatically redesigning warehouse layouts.
- Using machine learning to forecast storage demand.
- Optimizing worker schedules across multiple warehouses.
- Coordinating autonomous robots or automated storage equipment.
- Feature 11 requires an approved, repeatable putaway sequencing method but does not require these advanced capabilities.

### Deferred or Pending Design Decisions

The following items require stakeholder or instructor clarification before final implementation decisions are made.

**OS-11.1: Routing Algorithm**
- Confirm whether the system must calculate a mathematically optimal route or recommend an efficient route using documented rules.
- Confirm the available warehouse travel-distance information.
- Confirm how route recalculation should work when destinations change.

**OS-11.2: Storage Capacity Measurement**
- Confirm whether capacity is measured in individual units, volume, weight, or another unit.
- Confirm whether different Items require different capacity calculations.
- Confirm how reserved storage capacity is maintained.

**OS-11.3: Damaged or Unplaceable Products**
- Confirm the approved process for damaged products.
- Confirm the process for missing or physically unavailable products.
- Confirm whether Supervisors can authorize adjustments or must use another feature.
- Until approved, Feature 11 must preserve outstanding quantities and report blocked work rather than silently adjusting received totals.

**OS-11.4: Blocked Assignment Resolution**
- Confirm which roles may reopen blocked instructions.
- Confirm whether blocked work may be reassigned to another worker.
- Confirm how the system records Supervisor decisions.
- Confirm when a blocked assignment may return to In Progress.

**OS-11.5: Barcode Verification State**
- Confirm whether successful barcode verification is stored in a server-side session or represented by short-lived verification tokens.
- Confirm whether verification expires after a period of inactivity.
- Confirm how device disconnections affect verification.

**OS-11.6: Shared Transaction Ownership**
- Confirm which backend component coordinates Putaway Movement creation, Inventory updates, and Quantity Putaway updates.
- Confirm how transaction failures and retries are handled across Features 3, 10, and 11.
- Confirm the authoritative source for Quantity Putaway.

**OS-11.7: User Roles and Permissions**
- Confirm the final Warehouse role names.
- Confirm whether Supervisors and Managers may directly perform Put Away.
- Confirm which personnel may review movement history and resolve blocked work.

**OS-11.8: Device and Screen Requirements**
- Confirm supported handheld scanning devices.
- Confirm required screen dimensions.
- Confirm whether hardware scanning, camera scanning, or both are supported.
- Confirm whether separate desktop Supervisor screens are required.

### Scope Boundary

Feature 11 is responsible for moving products from a completed Receiving Record into valid Warehouse storage locations.

Its responsibilities begin when received products become eligible for Put Away and end when all assigned products have been successfully placed, Inventory has been updated, and the Putaway Assignment has been completed.

Feature 11 MUST preserve traceability between received products, confirmed movements, and destination Inventory without modifying the original receiving quantities.

Any functionality beyond these responsibilities requires approval and must be assigned to the appropriate Warehouse feature.

---
