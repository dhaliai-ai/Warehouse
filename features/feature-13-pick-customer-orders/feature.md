
# Feature: Pick Customer Orders

**Feature ID:** 13  
**Branch pattern:** `feature/13-pick-customer-orders`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  

**Input:** The Warehouse Management System assists warehouse pickers in fulfilling Customer Orders that are ready for picking. The system assigns orders, determines an efficient picking sequence, directs workers to storage bins, verifies locations and products through barcode scanning, records actual quantities picked, updates Inventory, and records shortages electronically. Quantity Picked remains separate from Quantity Ordered, Quantity Shipped, and Quantity Delivered.

---

## User Stories

### US-13.1: Start Picking a Customer Order

**As a** Picker  
**I want to** receive a Customer Order that is ready for picking  
**So that** I know which order I am responsible for fulfilling.

**Priority:** P1  
**Independent test:** Request picking work when a Customer Order is Ready for Picking and verify that an assignment identifies the correct order.

### US-13.2: Follow Picking Sequence

**As a** Picker  
**I want to** receive picking instructions in an efficient sequence  
**So that** I can move through the warehouse without unnecessary travel.

**Priority:** P1  
**Independent test:** Begin an assignment containing multiple items and verify that the system provides an ordered sequence of items, locations, and quantities.

### US-13.3: Verify Pick Location and Product

**As a** Picker  
**I want to** scan the assigned storage bin and product  
**So that** I can confirm that I am picking the correct product from the correct location.

**Priority:** P1  
**Independent test:** Scan a correct and incorrect bin and product barcode and verify that only the correct combination allows picking confirmation.

### US-13.4: Record Quantity Picked

**As a** Picker  
**I want to** confirm the actual quantity removed from each storage bin  
**So that** Inventory and the Customer Order accurately reflect the products picked.

**Priority:** P1  
**Independent test:** Pick a valid quantity from a verified bin and confirm that Inventory decreases and Quantity Picked increases by the same amount.

### US-13.5: Record Picking Shortage

**As a** Picker  
**I want to** report when the assigned bin does not contain enough product  
**So that** the shortage can be handled electronically without using a paper pick ticket.

**Priority:** P1  
**Independent test:** Report fewer units than required at an assigned location and verify that the system records the shortage and preserves the actual Quantity Picked.

### US-13.6: Complete Picking Assignment

**As a** Picker  
**I want to** finish a picking assignment after all instructions have been resolved  
**So that** the system can identify the order as fully or partially picked and make its picked products available for the shipping process.

**Priority:** P1  
**Independent test:** Complete an assignment with all quantities picked, then repeat with a confirmed shortage and verify that the resulting order statuses differ.

---

## Functional Requirements

- **FR-001:** The system MUST identify Customer Orders in Ready for Picking status.
- **FR-002:** The system MUST make only eligible Customer Orders available for new picking assignments.
- **FR-003:** The system MUST allow authorized Pickers to request available picking work.
- **FR-004:** The system MUST associate each Picking Assignment with a Customer Order and an assigned Picker.
- **FR-005:** The system MUST prevent the same Customer Order from being assigned to multiple active picking assignments without an explicit reassignment process.
- **FR-006:** The system MUST identify when no Customer Orders are ready for picking.
- **FR-007:** The system MUST determine a sequence of Picking Instructions for an assigned Customer Order.
- **FR-008:** Each Picking Instruction MUST identify the Customer Order Line, Individual Item, quantity to pick, and source Warehouse Location.
- **FR-009:** Each Picking Instruction MUST identify the aisle, row, and slot of the source location.
- **FR-010:** The system MUST direct the Picker to the next location in the picking sequence.
- **FR-011:** The system MUST prefer eligible primary picking bins when sufficient Inventory is available.
- **FR-012:** The system MUST support selecting additional eligible locations when the required quantity cannot be picked from one bin.
- **FR-013:** The system MUST prevent inactive or unavailable Warehouse Locations from being selected for new picking instructions.
- **FR-014:** The system MUST allow the Picker to scan the source Warehouse Location barcode.
- **FR-015:** The system MUST verify that the scanned Warehouse Location matches the assigned source location.
- **FR-016:** The system MUST allow the Picker to scan the product UPC.
- **FR-017:** The system MUST verify that the scanned product corresponds to the expected Individual Item.
- **FR-018:** The system MUST reject confirmation of a pick when the source location has not been verified.
- **FR-019:** The system MUST reject confirmation of a pick when the scanned product does not match the expected Item.
- **FR-020:** The system MUST identify unreadable or unknown location and product barcodes without recording an unverified pick.
- **FR-021:** The system MUST allow the Picker to record the actual quantity removed from the verified source bin.
- **FR-022:** The system MUST record picked quantities in individual units.
- **FR-023:** The system MUST require confirmed picked quantities to be positive whole numbers.
- **FR-024:** The system MUST prevent a confirmed pick quantity from exceeding the quantity remaining on its Picking Instruction.
- **FR-025:** The system MUST prevent a confirmed pick quantity from exceeding the available Inventory at the source location.
- **FR-026:** The system MUST decrease Inventory at the verified source Warehouse Location after a successful pick confirmation.
- **FR-027:** The system MUST increase Quantity Picked on the corresponding Customer Order Line by the same confirmed quantity.
- **FR-028:** The system MUST preserve Quantity Ordered separately from Quantity Picked.
- **FR-029:** The system MUST preserve Quantity Shipped and Quantity Delivered separately from Quantity Picked.
- **FR-030:** The system MUST maintain a record of each confirmed Picking Movement.
- **FR-031:** The system MUST prevent the same Picking Movement from being applied to Inventory more than once.
- **FR-032:** The system MUST allow the Picker to record a shortage when fewer products are available than required.
- **FR-033:** The system MUST allow a shortage of the full assigned quantity to be recorded when no product is available at the assigned location.
- **FR-034:** The system MUST calculate the difference between the required quantity and actual Quantity Picked.
- **FR-035:** The system MUST preserve confirmed shortages electronically.
- **FR-036:** The system MUST NOT require paper pick tickets to record picking quantities or shortages.
- **FR-037:** The system MUST support requesting replenishment or another eligible picking location when a shortage occurs.
- **FR-038:** The system MUST notify an authorized Supervisor when a shortage cannot be resolved through available Inventory.
- **FR-039:** The system MUST preserve unresolved shortages for later review.
- **FR-040:** The system MUST provide the next outstanding Picking Instruction after the current instruction is completed or resolved.
- **FR-041:** The system MUST identify when all Picking Instructions have been completed or resolved.
- **FR-042:** The system MUST mark a Customer Order as Picked when all ordered quantities have been successfully picked.
- **FR-043:** The system MUST mark a Customer Order as Partially Picked when picking is finished but at least one ordered quantity remains unpicked.
- **FR-044:** The system MUST mark a Customer Order as Picking while active picking work is in progress.
- **FR-045:** The system MUST preserve the actual Quantity Picked when the Customer Order is partially picked.
- **FR-046:** The system MUST make completed picking information available to the shipping process in Feature 14.
- **FR-047:** The system MUST prevent the same Picking Assignment from being completed more than once.
- **FR-048:** The system MUST preserve Picking Assignment history, including the Picker, source locations, quantities, and shortages.
- **FR-049:** The system MUST restrict picking operations to authorized warehouse personnel.
- **FR-050:** The system MUST reject attempts to pick a nonexistent or canceled Customer Order.
- **FR-051:** The system MUST preserve the relationships between Customer Orders, Picking Assignments, Picking Instructions, Warehouse Locations, and Inventory.
- **FR-052:** The system MUST keep picking separate from shipping and delivery.
- **FR-053:** The system MUST NOT automatically mark picked products as shipped or delivered.

---

## Assumptions

- **A-001:** Feature 12 creates and releases Customer Orders for picking.
- **A-002:** Only Customer Orders in Ready for Picking status are eligible for new picking assignments.
- **A-003:** Pickers must be authenticated and authorized before receiving picking work.
- **A-004:** Each Picking Assignment identifies one Customer Order and an assigned Picker.
- **A-005:** A Customer Order cannot have multiple active Picking Assignments without an approved reassignment process.
- **A-006:** The Warehouse System maintains scannable Warehouse Locations with aisle, row, and slot identifiers.
- **A-007:** Warehouse Locations identify whether they are primary or reserve storage locations.
- **A-008:** The system maintains Inventory quantities for Individual Items at specific Warehouse Locations.
- **A-009:** Inventory quantities are recorded in individual units.
- **A-010:** Individual Items have associated UPCs that can be used for barcode verification.
- **A-011:** Picking Instructions are generated from released Customer Order Lines and eligible Inventory locations.
- **A-012:** The system determines an efficient sequence for visiting assigned picking locations.
- **A-013:** Eligible primary picking bins are preferred when sufficient Inventory is available.
- **A-014:** Additional eligible locations may be used when a single bin cannot satisfy the required quantity.
- **A-015:** Inactive or unavailable Warehouse Locations cannot be selected for new picking instructions.
- **A-016:** Pickers use an electronic device to view instructions and scan locations and products.
- **A-017:** Paper pick tickets are not required.
- **A-018:** Both the source location and product must be verified before confirming a pick.
- **A-019:** Confirmed picking quantities must be positive whole numbers.
- **A-020:** A confirmed pick cannot exceed the remaining instruction quantity or available source Inventory.
- **A-021:** Every successful pick decreases source Inventory and increases Quantity Picked by the same amount.
- **A-022:** Quantity Ordered remains unchanged during ordinary picking.
- **A-023:** Quantity Shipped and Quantity Delivered remain separate from Quantity Picked.
- **A-024:** Confirmed Picking Movements are recorded for historical tracking.
- **A-025:** The system prevents duplicate application of the same Picking Movement.
- **A-026:** Pickers can electronically report partial or complete shortages at assigned locations.
- **A-027:** Shortages may be resolved through another eligible location or a replenishment request.
- **A-028:** Unresolved shortages are made available for Supervisor review.
- **A-029:** A Picking Assignment can be completed only when all instructions have been completed or resolved.
- **A-030:** Fully picked orders receive Picked status.
- **A-031:** Orders with confirmed remaining shortages receive Partially Picked status when picking is finished.
- **A-032:** Completed picking information is available to Feature 14.
- **A-033:** Picking does not automatically complete shipping or delivery.
- **A-034:** Picking Assignment history remains available for authorized review.
- **A-035:** Shared authentication and role-based permissions are provided by the Warehouse System.
- **A-036:** Replenishment and reassignment workflows may require coordination with other warehouse features.

---

## Edge Cases

### EC-13.1: No Customer Orders Ready for Picking

**Condition:** A Picker requests picking work when no eligible Customer Orders exist.

**Expected Behavior:**
- The system reports that no picking work is available.
- No empty Picking Assignment is created.
- Existing Customer Orders remain unchanged.

### EC-13.2: Duplicate Active Picking Assignment

**Condition:** Two Pickers request the same available Customer Order.

**Expected Behavior:**
- The system prevents duplicate active assignments.
- Only one eligible assignment is created unless an approved reassignment process is used.
- The system preserves assignment consistency.

### EC-13.3: Nonexistent or Canceled Customer Order

**Condition:** A Picker attempts to begin picking a Customer Order that does not exist or has been canceled.

**Expected Behavior:**
- The system rejects the request.
- No Picking Assignment or Inventory change is created.

### EC-13.4: No Eligible Inventory Location

**Condition:** An ordered Item has no eligible Warehouse Location with available Inventory.

**Expected Behavior:**
- The system does not generate an invalid picking instruction.
- The outstanding quantity is identified for exception handling.
- **[NEEDS CLARIFICATION]** Confirm whether an immediate shortage record, replenishment request, or blocked assignment is created.

### EC-13.5: Insufficient Inventory in Primary Bin

**Condition:** The primary picking bin contains fewer units than required.

**Expected Behavior:**
- The system identifies the available quantity.
- Another eligible location may be selected for the remaining quantity.
- The system does not permit picking more units than are available.

### EC-13.6: Incorrect Source Location Scan

**Condition:** The Picker scans a bin other than the assigned source location.

**Expected Behavior:**
- The system reports a location mismatch.
- Picking confirmation remains unavailable.
- Inventory and Quantity Picked remain unchanged.

### EC-13.7: Incorrect Product Scan

**Condition:** The Picker scans a UPC associated with the wrong Individual Item.

**Expected Behavior:**
- The system rejects product verification.
- The Picker cannot confirm the incorrect product.
- No Inventory or Customer Order quantity is changed.

### EC-13.8: Unknown or Unreadable Barcode

**Condition:** The device cannot read a location or product barcode, or the scanned code is unknown.

**Expected Behavior:**
- The system reports unsuccessful verification.
- No unverified pick is recorded.
- The Picker may retry or request Supervisor assistance.

### EC-13.9: Zero or Negative Confirmed Pick Quantity

**Condition:** The Picker attempts to confirm zero or a negative number of units.

**Expected Behavior:**
- The system rejects the pick confirmation.
- No Picking Movement is recorded.
- A zero-availability situation is handled through the shortage workflow.

### EC-13.10: Pick Quantity Exceeds Instruction

**Condition:** The Picker attempts to confirm more units than remain on the Picking Instruction.

**Expected Behavior:**
- The system rejects the confirmation.
- Inventory and Quantity Picked remain unchanged.

### EC-13.11: Pick Quantity Exceeds Available Inventory

**Condition:** The Picker attempts to confirm more units than exist at the source location.

**Expected Behavior:**
- The system rejects the confirmation.
- Inventory does not become negative.
- The Picker may report a shortage.

### EC-13.12: Partial Pick from Assigned Location

**Condition:** A Picking Instruction requires more units than the Picker can physically remove.

**Expected Behavior:**
- The system records only the actual confirmed quantity.
- The system records the shortage separately.
- The outstanding quantity remains available for resolution.

### EC-13.13: Assigned Bin Is Empty

**Condition:** The Picker finds no units of the required Item at the assigned location.

**Expected Behavior:**
- The Picker can report the full assigned quantity as a shortage.
- No Inventory decrease is recorded.
- The shortage remains available for resolution or Supervisor review.

### EC-13.14: Replenishment Required

**Condition:** A primary bin is short but eligible reserve Inventory exists.

**Expected Behavior:**
- The Picker can request replenishment.
- The system records the request electronically.
- The outstanding quantity remains tracked.
- **[NEEDS CLARIFICATION]** Confirm which feature owns replenishment task creation and completion.

### EC-13.15: Unresolved Shortage

**Condition:** No eligible additional Inventory is available to complete a required quantity.

**Expected Behavior:**
- The system preserves the shortage.
- The Supervisor is notified.
- Missing units are not recorded as picked.
- The assignment may be completed as partially picked when all instructions are otherwise resolved.

### EC-13.16: Duplicate Picking Confirmation

**Condition:** A previously successful picking confirmation is submitted again.

**Expected Behavior:**
- The system prevents duplicate application.
- Inventory is not decreased a second time.
- Quantity Picked is not increased a second time.
- The original Picking Movement remains recorded.

### EC-13.17: Inventory Changes During Picking

**Condition:** Another warehouse operation changes source Inventory before the Picker confirms a pick.

**Expected Behavior:**
- The system validates available Inventory at confirmation time.
- The system prevents negative Inventory.
- **[NEEDS CLARIFICATION]** Confirm the inventory locking or concurrency-control strategy.

### EC-13.18: Incomplete Picking Assignment

**Condition:** A Picker attempts to complete an assignment while unresolved instructions remain.

**Expected Behavior:**
- The system rejects premature completion.
- Outstanding instructions are identified.
- Confirmed Picking Movements remain preserved.

### EC-13.19: Duplicate Assignment Completion

**Condition:** A Picker attempts to complete an already completed Picking Assignment.

**Expected Behavior:**
- The system rejects duplicate completion.
- Inventory and Quantity Picked are not changed again.
- Completed assignment history remains unchanged.

### EC-13.20: Unauthorized Picking Operation

**Condition:** A Driver or another user without picking permission attempts to confirm a pick.

**Expected Behavior:**
- The system denies the operation.
- No Inventory or Quantity Picked update occurs.

### EC-13.21: Picking Device Connection Failure

**Condition:** The Picker loses network connectivity while performing an assignment.

**Expected Behavior:**
- The system must not record unverified or duplicate movements.
- Previously confirmed server-side movements remain preserved.
- **[NEEDS CLARIFICATION]** Confirm whether offline picking is supported or whether the device must reconnect before confirming additional movements.

### EC-13.22: Partially Picked Order

**Condition:** Picking ends with one or more confirmed shortages.

**Expected Behavior:**
- The system preserves actual Quantity Picked.
- The Customer Order receives Partially Picked status.
- Shortages remain available for review.
- Completed picking information becomes available to Feature 14.

### EC-13.23: Case UPC Scanned

**Condition:** A Picker scans a case UPC rather than an individual-unit UPC.

**Expected Behavior:**
- The system identifies the associated Individual Item.
- Recorded quantities remain expressed in individual units.
- **[NEEDS CLARIFICATION]** Confirm whether case scans automatically propose a quantity based on units per case or require explicit quantity entry.

### EC-13.24: Picker Cannot Continue Assignment

**Condition:** An assigned Picker becomes unavailable before completing the work.

**Expected Behavior:**
- Confirmed Picking Movements and outstanding instructions remain preserved.
- The system prevents another Picker from taking the active assignment without authorization.
- **[NEEDS CLARIFICATION]** Define the authorized reassignment, suspension, and resumption process.

---

## Success Criteria

- **SC-001:** Authorized Pickers can request and receive eligible Customer Orders ready for picking.
- **SC-002:** The system prevents duplicate active Picking Assignments for the same Customer Order.
- **SC-003:** The system reports when no eligible picking work is available.
- **SC-004:** Each Picking Assignment identifies its Customer Order and assigned Picker.
- **SC-005:** The system generates ordered Picking Instructions with Item, quantity, and source location details.
- **SC-006:** Picking Instructions identify the aisle, row, and slot for each source location.
- **SC-007:** Eligible primary picking bins are preferred when sufficient Inventory is available.
- **SC-008:** Additional eligible locations can be selected when one bin cannot satisfy the required quantity.
- **SC-009:** Inactive or unavailable locations are excluded from new picking instructions.
- **SC-010:** The Picker must verify the assigned location barcode before confirming a pick.
- **SC-011:** The Picker must verify a UPC associated with the expected Individual Item.
- **SC-012:** Incorrect or unreadable barcodes cannot produce confirmed Picking Movements.
- **SC-013:** Confirmed pick quantities are positive whole numbers expressed in individual units.
- **SC-014:** Confirmed quantities cannot exceed remaining instruction quantities.
- **SC-015:** Confirmed quantities cannot exceed available source Inventory.
- **SC-016:** Successful picking decreases source Inventory and increases Customer Order Line Quantity Picked by the same amount.
- **SC-017:** Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered remain separate.
- **SC-018:** Every confirmed pick has a recorded Picking Movement.
- **SC-019:** Duplicate confirmations cannot apply the same Inventory movement more than once.
- **SC-020:** Pickers can report partial and complete shortages electronically.
- **SC-021:** Shortage reporting does not require paper pick tickets.
- **SC-022:** The system supports alternate eligible locations or replenishment requests when shortages occur.
- **SC-023:** Unresolved shortages are preserved and available to Supervisors.
- **SC-024:** The system advances to the next outstanding Picking Instruction after the current instruction is resolved.
- **SC-025:** Assignments cannot be completed while outstanding instructions remain unresolved.
- **SC-026:** Fully picked Customer Orders receive Picked status.
- **SC-027:** Orders with confirmed remaining shortages receive Partially Picked status when picking is finished.
- **SC-028:** Completed picking information is available to Feature 14.
- **SC-029:** Picking does not automatically mark orders as Shipped or Delivered.
- **SC-030:** Unauthorized users cannot perform picking operations.
- **SC-031:** Picking Assignment history preserves workers, source locations, actual quantities, and shortages.
- **SC-032:** All 28 original Gherkin Acceptance Criteria have corresponding verification tests.
- **SC-033:** Inventory and Customer Order quantities remain consistent when confirmations are repeated or concurrent operations occur.

---

## Key Entities

### Picking Assignment

Represents a Customer Order assigned to a Picker for fulfillment.

The assignment identifies the order, assigned worker, and picking status.

### Picking Instruction

Represents one step in the system-directed picking sequence.

Each instruction identifies the Item, source Warehouse Location, required quantity, and sequence number.

### Customer Order

Represents an order received from a Customer and released for picking.

Customer Order entry is defined in Feature 12.

### Customer Order Line

Represents an Individual Item requested on a Customer Order.

Each line maintains Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered separately.

### Warehouse Location

Represents a scannable storage bin or slot from which Inventory is picked.

### Inventory

Represents the quantity of an Individual Item stored in a Warehouse Location.

### Individual Item

Represents a product included in a Customer Order.

### UPC

Represents a barcode identifying an Individual Item during picking.

### Picking Movement

Represents a confirmed removal of an Item quantity from a source Warehouse Location.

### Picking Shortage

Represents a recorded difference between the required quantity and the actual quantity available or picked.

### User

Represents an employee authorized to perform picking or review shortages.

---

## Initial Data Model

### Picking Assignment

| Attribute | Type | Description |
|---|---|---|
| pickingAssignmentId | Integer | Unique Picking Assignment identifier |
| customerOrderId | Integer | Foreign key referencing Customer Order |
| assignedUserId | Integer | Foreign key referencing the assigned Picker |
| status | String | Assigned, In Progress, Completed, or Blocked |
| assignedAt | DateTime | Date and time the assignment was created |
| startedAt | DateTime | Date and time picking began |
| completedAt | DateTime | Date and time picking finished |

**Relationships:**
- Each Picking Assignment belongs to one Customer Order.
- Each Picking Assignment is assigned to one Picker.
- Each Picking Assignment contains one or more Picking Instructions.

**Constraints:**
- A Customer Order cannot have multiple active assignments without an authorized reassignment process.
- A completed assignment cannot be completed again.

### Picking Instruction

| Attribute | Type | Description |
|---|---|---|
| pickingInstructionId | Integer | Unique Picking Instruction identifier |
| pickingAssignmentId | Integer | Foreign key referencing Picking Assignment |
| customerOrderLineId | Integer | Foreign key referencing Customer Order Line |
| itemId | Integer | Foreign key referencing Individual Item |
| sourceLocationId | Integer | Foreign key referencing Warehouse Location |
| sequenceNumber | Integer | Position in the picking sequence |
| quantityToPick | Integer | Required quantity for this instruction |
| quantityPicked | Integer | Quantity confirmed picked from this location |
| status | String | Pending, In Progress, Completed, or Shortage |

**Relationships:**
- Each Picking Instruction belongs to one Picking Assignment.
- Each instruction references one Customer Order Line.
- Each instruction identifies a source Warehouse Location.
- Each instruction may have one or more Picking Movements.

**Constraints:**
- quantityToPick must be greater than zero.
- quantityPicked cannot be negative.
- quantityPicked cannot exceed quantityToPick.

**Derived Value:**
- Remaining Quantity = quantityToPick - quantityPicked.

### Customer Order

| Attribute | Type | Description |
|---|---|---|
| customerOrderId | Integer | Unique Customer Order identifier |
| orderNumber | String | Unique Customer Order Number |
| customerId | Integer | Foreign key referencing Customer |
| status | String | Current Customer Order status |

**Relationships:**
- A Customer Order contains one or more Customer Order Lines.
- A Customer Order can have Picking Assignments.
- Customer Order entry is defined in Feature 12.

### Customer Order Line

| Attribute | Type | Description |
|---|---|---|
| customerOrderLineId | Integer | Unique Customer Order Line identifier |
| customerOrderId | Integer | Foreign key referencing Customer Order |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityOrdered | Integer | Quantity requested by Customer |
| quantityPicked | Integer | Cumulative quantity picked |
| quantityShipped | Integer | Cumulative quantity shipped |
| quantityDelivered | Integer | Cumulative quantity delivered |

**Relationships:**
- Each Customer Order Line belongs to one Customer Order.
- Each line references one Individual Item.
- Picking Movements contribute to Quantity Picked.

**Constraints:**
- quantityOrdered must be positive.
- quantityPicked cannot be negative.
- Quantity Ordered remains unchanged through ordinary picking operations.

### Warehouse Location

| Attribute | Type | Description |
|---|---|---|
| locationId | Integer | Unique Warehouse Location identifier |
| warehouseId | Integer | Foreign key referencing Warehouse |
| locationCode | String | Scannable location identifier |
| aisle | String | Aisle identifier |
| row | String | Row identifier |
| slot | String | Slot or bin identifier |
| locationType | String | Primary or Reserve |
| isActive | Boolean | Indicates whether the location is active |

**Relationships:**
- A Warehouse Location belongs to a Warehouse.
- A Warehouse Location contains Inventory.
- Picking Instructions identify source Warehouse Locations.

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique Inventory identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| locationId | Integer | Foreign key referencing Warehouse Location |
| quantity | Integer | Current quantity in individual units |

**Relationships:**
- Each Inventory record references an Item and Warehouse Location.
- Confirmed Picking Movements decrease Inventory at the source location.

**Constraints:**
- Inventory quantity cannot become negative.
- The combination of itemId and locationId must be unique.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |

**Relationships:**
- One Individual Item can appear on multiple Customer Order Lines.
- One Individual Item can exist in multiple Inventory locations.

### UPC

| Attribute | Type | Description |
|---|---|---|
| upcId | Integer | Unique UPC identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| upcCode | String | Unique product barcode |
| barcodeType | String | Individual Unit or Case |

**Relationships:**
- Each UPC identifies one Individual Item.
- An Individual Item may have multiple UPCs.

### Picking Movement

| Attribute | Type | Description |
|---|---|---|
| pickingMovementId | Integer | Unique Picking Movement identifier |
| pickingInstructionId | Integer | Foreign key referencing Picking Instruction |
| customerOrderLineId | Integer | Foreign key referencing Customer Order Line |
| itemId | Integer | Foreign key referencing Individual Item |
| sourceLocationId | Integer | Verified source Warehouse Location |
| quantityPicked | Integer | Confirmed quantity removed |
| pickedBy | Integer | User who confirmed the pick |
| pickedAt | DateTime | Date and time of confirmation |

**Relationships:**
- Each Picking Movement belongs to a Picking Instruction.
- Each movement updates Inventory and Quantity Picked.
- Each movement is associated with the Picker who performed it.

**Constraints:**
- quantityPicked must be positive.
- A Picking Movement cannot be applied more than once.

### Picking Shortage

| Attribute | Type | Description |
|---|---|---|
| pickingShortageId | Integer | Unique Picking Shortage identifier |
| pickingInstructionId | Integer | Foreign key referencing Picking Instruction |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityShort | Integer | Quantity not available at the assigned location |
| reportedBy | Integer | User who reported the shortage |
| reportedAt | DateTime | Date and time shortage was reported |
| status | String | Open, Replenishment Requested, or Resolved |

**Relationships:**
- Each Picking Shortage belongs to a Picking Instruction.
- A Picking Shortage may result in a replenishment request or alternate location.
- Shortages are available for Supervisor review.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Pickers complete Picking Assignments.
- Supervisors review unresolved shortages.

---

## Gherkin Acceptance Criteria

### US-13.1: Start Picking a Customer Order

#### AC-13.1.1: Assign available Customer Order

**Given** a Customer Order exists in Ready for Picking status  
**And** the user is authenticated as a Picker  
**When** the Picker requests available picking work  
**Then** the system assigns an eligible Customer Order  
**And** creates a Picking Assignment linked to that order.

#### AC-13.1.2: No Customer Orders ready

**Given** no Customer Orders are in Ready for Picking status  
**When** the Picker requests picking work  
**Then** the system reports that no picking work is available  
**And** does not create an empty Picking Assignment.

#### AC-13.1.3: Prevent duplicate active assignment

**Given** a Customer Order already has an active Picking Assignment  
**When** another Picker requests work  
**Then** the system does not assign the same Customer Order again.

#### AC-13.1.4: Reject canceled Customer Order

**Given** a Customer Order is in Canceled status  
**When** a Picker attempts to begin picking it  
**Then** the system rejects the request  
**And** does not create a Picking Assignment.

### US-13.2: Follow Picking Sequence

#### AC-13.2.1: Generate first Picking Instruction

**Given** a Picker has started an assigned Customer Order  
**And** eligible Inventory locations exist for the ordered Items  
**When** the system generates the picking sequence  
**Then** the system provides the first Picking Instruction  
**And** displays the Item, required quantity, aisle, row, and slot.

#### AC-13.2.2: Provide next Picking Instruction

**Given** the Picker has completed the current Picking Instruction  
**And** more instructions remain  
**When** the system continues the picking process  
**Then** the system displays the next Picking Instruction.

#### AC-13.2.3: Select alternate picking location

**Given** an Item requires 20 units  
**And** its primary picking bin contains only 12 units  
**And** another eligible bin contains at least 8 units  
**When** the system prepares picking instructions  
**Then** the system may allocate 12 units from the primary bin  
**And** 8 units from the alternate bin  
**And** identifies both locations for verification.

### US-13.3: Verify Pick Location and Product

#### AC-13.3.1: Verify correct Warehouse Location

**Given** a Picking Instruction identifies bin "A1-R2-S3"  
**When** the Picker scans barcode "A1-R2-S3"  
**Then** the system verifies the source location.

#### AC-13.3.2: Reject incorrect Warehouse Location

**Given** a Picking Instruction identifies bin "A1-R2-S3"  
**When** the Picker scans barcode "A1-R2-S4"  
**Then** the system reports that the source location is incorrect  
**And** does not allow picking confirmation from that bin.

#### AC-13.3.3: Verify correct product

**Given** the Picker has verified the assigned source location  
**And** the Picking Instruction requires Item A  
**When** the Picker scans a UPC associated with Item A  
**Then** the system verifies the product  
**And** allows the Picker to enter the quantity picked.

#### AC-13.3.4: Reject incorrect product

**Given** the Picking Instruction requires Item A  
**When** the Picker scans a UPC associated with Item B  
**Then** the system identifies the wrong product  
**And** prevents confirmation of the pick.

#### AC-13.3.5: Handle unreadable barcode

**Given** the Picker is attempting to verify a location or product  
**When** the barcode cannot be read  
**Then** the system reports that verification failed  
**And** does not update Inventory or Quantity Picked  
**And** allows the Picker to retry or request Supervisor assistance.

### US-13.4: Record Quantity Picked

#### AC-13.4.1: Successfully pick full quantity

**Given** a Picking Instruction requires 20 units of Item A  
**And** the source bin contains 30 units of Item A  
**And** the Picker has verified the bin and product  
**When** the Picker confirms picking 20 units  
**Then** the system reduces source Inventory to 10 units  
**And** increases Quantity Picked on the Customer Order Line by 20  
**And** records the Picking Movement.

#### AC-13.4.2: Reject quantity exceeding Inventory

**Given** a Picking Instruction requires 20 units  
**And** the source bin contains only 12 units  
**When** the Picker attempts to confirm 20 units from that bin  
**Then** the system rejects the confirmation  
**And** Inventory and Quantity Picked remain unchanged.

#### AC-13.4.3: Reject quantity exceeding instruction

**Given** a Picking Instruction requires 10 units  
**And** the source bin contains 30 units  
**When** the Picker attempts to confirm picking 15 units  
**Then** the system rejects the confirmation  
**And** Inventory remains unchanged.

#### AC-13.4.4: Prevent duplicate picking update

**Given** a Picking Movement for 10 units has already been confirmed  
**When** the same confirmation is submitted again  
**Then** the system rejects the duplicate operation  
**And** does not decrease Inventory or increase Quantity Picked again.

#### AC-13.4.5: Preserve separate quantities

**Given** a Customer Order Line contains 30 units ordered  
**And** 25 units have been picked  
**When** the system displays the order line  
**Then** Quantity Ordered remains 30  
**And** Quantity Picked is 25  
**And** Quantity Shipped and Quantity Delivered remain unchanged.

### US-13.5: Record Picking Shortage

#### AC-13.5.1: Record partial picking shortage

**Given** a Picking Instruction requires 20 units  
**And** the assigned bin contains only 12 units  
**When** the Picker confirms 12 units picked  
**And** reports that 8 units are unavailable at that bin  
**Then** the system records Quantity Picked as 12 for that instruction  
**And** records a shortage of 8 units  
**And** preserves the remaining quantity for resolution.

#### AC-13.5.2: Record zero quantity available

**Given** a Picking Instruction requires 15 units  
**And** no product is available in the assigned bin  
**When** the Picker reports that no quantity could be picked  
**Then** the system records a shortage of 15 units  
**And** does not decrease Inventory.

#### AC-13.5.3: Request replenishment

**Given** a Picker reports a shortage in the assigned primary bin  
**And** eligible reserve Inventory is available  
**When** the Picker requests replenishment  
**Then** the system records a replenishment request  
**And** makes the request available to authorized warehouse personnel  
**And** preserves the outstanding picking quantity.

#### AC-13.5.4: No additional Inventory available

**Given** a Picking Instruction has an unresolved shortage  
**And** no eligible alternate Inventory is available  
**When** the Picker reports the shortage  
**Then** the system records the unresolved quantity  
**And** makes the shortage available for Supervisor review  
**And** does not record the missing units as picked.

### US-13.6: Complete Picking Assignment

#### AC-13.6.1: Complete fully picked order

**Given** all Picking Instructions for a Customer Order are resolved  
**And** Quantity Picked equals Quantity Ordered for every Customer Order Line  
**When** the Picker completes the assignment  
**Then** the system marks the Picking Assignment as Completed  
**And** changes the Customer Order status to Picked  
**And** makes the picked quantities available for Feature 14.

#### AC-13.6.2: Complete partially picked order

**Given** all Picking Instructions have been resolved or shortages have been confirmed  
**And** at least one Customer Order Line has Quantity Picked less than Quantity Ordered  
**When** the Picker completes the assignment  
**Then** the system marks the Picking Assignment as Completed  
**And** changes the Customer Order status to Partially Picked  
**And** preserves the confirmed shortage information.

#### AC-13.6.3: Prevent premature completion

**Given** a Picking Assignment still contains instructions that have not been completed or resolved  
**When** the Picker attempts to complete the assignment  
**Then** the system rejects completion  
**And** identifies the outstanding instructions.

#### AC-13.6.4: Prevent duplicate completion

**Given** a Picking Assignment is already Completed  
**When** the Picker attempts to complete it again  
**Then** the system rejects the duplicate completion  
**And** does not update Inventory again.

#### AC-13.6.5: Preserve picking history

**Given** a Picking Assignment has been completed  
**When** an authorized Manager reviews the assignment  
**Then** the system displays the Customer Order, Picker, source locations, actual quantities picked, and recorded shortages.

#### AC-13.6.6: Reject unauthorized picking

**Given** the user is authenticated as a Driver without picking permission  
**When** the user attempts to confirm a Picking Instruction  
**Then** the system denies the operation  
**And** Inventory and Quantity Picked remain unchanged.

---

## Data Ownership

### Feature 13 — Pick Customer Orders

Feature 13 owns the picking workflow, including Picking Assignments, Picking Instructions, Picking Movements, and Picking Shortages.

**Owned Data:**
- Picking Assignment
- Picking Assignment status
- Assigned Picker
- Assignment creation, start, and completion timestamps
- Picking Instruction
- Picking Instruction sequence
- Picking Instruction status
- Quantity to Pick
- Quantity Picked per instruction
- Picking Movement
- Picking Shortage
- Shortage quantity and status
- Picking confirmation history

**Responsibilities:**
- Identify Customer Orders eligible for picking.
- Assign eligible Customer Orders to authorized Pickers.
- Prevent duplicate active assignments.
- Generate efficient picking sequences.
- Identify source Warehouse Locations and required quantities.
- Verify source location and product barcodes.
- Record confirmed picking quantities.
- Record Picking Movements.
- Coordinate Inventory decreases for confirmed picks.
- Update Quantity Picked on Customer Order Lines.
- Record shortages electronically.
- Support alternate locations and replenishment requests.
- Make unresolved shortages available to Supervisors.
- Complete Picking Assignments.
- Update Customer Order picking status.
- Provide completed picking information to Feature 14.
- Preserve picking history.

### Feature 12 — Receive Customer Orders

**Owned Data:**
- Customer Order
- Customer Order Line
- Customer Order Number
- Customer association
- Quantity Ordered
- Original order entry information
- Order creation and release information

**Feature 13 Responsibilities:**
- Retrieve Customer Orders in Ready for Picking status.
- Reference the existing Customer Order and its lines.
- Preserve Quantity Ordered.
- Update Quantity Picked through the approved Customer Order interface.
- Update picking-related Customer Order statuses.
- Never modify the original ordered quantities through ordinary picking.

### Warehouse Location Maintenance

**Owned Data:**
- Warehouse Location ID
- Warehouse association
- Location Code
- Aisle
- Row
- Slot
- Primary or Reserve location classification
- Location active status

**Feature 13 Responsibilities:**
- Retrieve eligible Warehouse Locations.
- Use location information to generate picking instructions.
- Verify scanned location barcodes.
- Exclude inactive or unavailable locations.
- Never modify Warehouse Location master data.

### Inventory Management

**Owned Data:**
- Inventory ID
- Individual Item reference
- Warehouse Location reference
- Current Inventory quantity

**Feature 13 Responsibilities:**
- Read available Inventory at eligible locations.
- Validate Inventory before confirming a pick.
- Decrease source Inventory by the confirmed quantity through the approved Inventory update operation.
- Prevent negative Inventory.
- Ensure each confirmed movement is applied only once.
- Preserve Inventory consistency during concurrent operations.

### Feature 4 — Maintain Individual Items

**Owned Data:**
- Individual Item ID
- Item Number
- Item description
- Item master information

**Feature 13 Responsibilities:**
- Retrieve Individual Item information.
- Verify that scanned product UPCs identify the expected Item.
- Never modify Individual Item master data.

### UPC Maintenance

**Owned Data:**
- UPC ID
- UPC Code
- Associated Individual Item
- Barcode Type

**Feature 13 Responsibilities:**
- Read UPC information for product verification.
- Confirm that the scanned UPC identifies the expected Individual Item.
- Never modify UPC master data.

### Feature 14 — Ship Customer Orders

**Responsibilities:**
- Retrieve completed picking information.
- Use actual Quantity Picked during shipping.
- Record Quantity Shipped.
- Manage shipping activities and shipping status.

**Feature 13 Responsibilities:**
- Make completed Picking Assignments available to Feature 14.
- Preserve actual Quantity Picked.
- Keep picking separate from shipping.

### Feature 15 — Deliver Customer Orders

**Responsibilities:**
- Manage delivery operations.
- Record Quantity Delivered.
- Maintain delivery-related status.

**Feature 13 Responsibilities:**
- Preserve picking history.
- Never automatically mark picked products as delivered.

### Shared Authentication and Authorization

**Owned Data:**
- User ID
- User role
- Authentication information
- Authorization permissions

**Feature 13 Responsibilities:**
- Require authentication before picking.
- Restrict picking operations to authorized warehouse personnel.
- Associate confirmed movements with the authenticated Picker.
- Allow authorized Supervisors to review shortages.
- Deny unauthorized picking operations.

### Cross-Feature Data Rules

- Feature 13 owns Picking Assignments, Picking Instructions, Picking Movements, and Picking Shortages.
- Feature 12 maintains the original Customer Order and Quantity Ordered.
- Feature 13 updates Quantity Picked through the approved shared interface.
- Feature 14 updates Quantity Shipped.
- Feature 15 updates Quantity Delivered.
- Inventory quantities are maintained through the approved Inventory operation.
- Warehouse Location and Item master data remain owned by their respective maintenance features.
- Confirmed picking must update Inventory and Quantity Picked consistently.
- A Picking Movement must never be applied more than once.
- Picking must not automatically perform shipping or delivery.

**[NEEDS CLARIFICATION]** Confirm the exact owner and API for Inventory updates.

**[NEEDS CLARIFICATION]** Confirm which warehouse feature owns replenishment requests and their completion.

**[NEEDS CLARIFICATION]** Confirm how Feature 13 updates Customer Order status and Quantity Picked without allowing unrelated changes to Feature 12 data.

---

## API Requirements

The following endpoints are proposed interfaces for the Feature 13 design draft. Final route naming and service boundaries require architecture approval.

### API-13.1: Request Available Picking Work

**Endpoint:** `POST /api/picking-assignments`

**Purpose:** Assign an eligible Customer Order to an authorized Picker.

**Authorized Roles:**
- Picker
- Other authorized warehouse personnel

**Request Data:**
- customerOrderId (optional, if selecting a specific eligible order)

**System-Generated Data:**
- pickingAssignmentId
- assignedUserId
- assignedAt
- status = Assigned

**Validation and Behavior:**
- Require authentication and picking permission.
- Identify a Customer Order in Ready for Picking status.
- Reject nonexistent or canceled Customer Orders.
- Prevent duplicate active assignments for the same order.
- Associate the assignment with the authenticated Picker.
- Return a message when no eligible orders are available.

**Successful Response:**
- Picking Assignment ID
- Customer Order ID
- Order Number
- Assigned Picker
- Assignment status

**Error Conditions:**
- Unauthorized user
- No eligible Customer Orders
- Customer Order not found
- Customer Order not eligible
- Duplicate active assignment

### API-13.2: Retrieve Picking Assignment

**Endpoint:** `GET /api/picking-assignments/{pickingAssignmentId}`

**Purpose:** Retrieve an existing Picking Assignment and its progress.

**Authorized Roles:**
- Assigned Picker
- Authorized Supervisor
- Manager

**Response Data:**
- Picking Assignment ID
- Customer Order Number
- Assigned Picker
- Assignment status
- Assignment timestamps
- Picking Instructions
- Confirmed quantities
- Recorded shortages

**Validation and Behavior:**
- Verify the assignment exists.
- Verify the user has permission to view it.
- Return current assignment information.
- Do not modify Inventory or picking quantities.

**Error Conditions:**
- Assignment not found
- Unauthorized access

### API-13.3: Start Picking Assignment

**Endpoint:** `POST /api/picking-assignments/{pickingAssignmentId}/start`

**Purpose:** Begin an assigned picking task.

**Authorized Roles:**
- Assigned Picker
- Authorized warehouse personnel

**Validation and Behavior:**
- Confirm the assignment exists.
- Confirm the assignment is eligible to start.
- Verify the assigned Picker.
- Record the start timestamp.
- Change the assignment status to In Progress.
- Change the Customer Order status to Picking.
- Prepare the ordered Picking Instructions.

**Successful Response:**
- Picking Assignment ID
- In Progress status
- First Picking Instruction

**Error Conditions:**
- Unauthorized user
- Assignment not found
- Assignment already completed
- Invalid assignment status

### API-13.4: Retrieve Picking Instructions

**Endpoint:** `GET /api/picking-assignments/{pickingAssignmentId}/instructions`

**Purpose:** Retrieve the system-generated picking sequence.

**Authorized Roles:**
- Assigned Picker
- Authorized Supervisor
- Manager

**Response Data:**
- Picking Instruction ID
- Sequence Number
- Customer Order Line
- Individual Item
- Quantity to Pick
- Quantity Picked
- Remaining Quantity
- Source Warehouse Location
- Aisle
- Row
- Slot
- Instruction status

**Validation and Behavior:**
- Return instructions in the assigned sequence.
- Identify the next outstanding instruction.
- Prefer eligible primary picking bins when sufficient Inventory exists.
- Support additional eligible locations when required.
- Exclude inactive or unavailable locations.

**Error Conditions:**
- Assignment not found
- Unauthorized access

### API-13.5: Verify Source Location

**Endpoint:** `POST /api/picking-instructions/{pickingInstructionId}/verify-location`

**Purpose:** Verify that the Picker is at the assigned source Warehouse Location.

**Authorized Role:**
- Assigned Picker

**Request Data:**
- scannedLocationCode

**Validation and Behavior:**
- Confirm the instruction exists.
- Confirm the Picker is authorized for the assignment.
- Resolve the scanned location barcode.
- Compare it with the assigned source location.
- Reject incorrect or unknown locations.
- Do not modify Inventory.

**Successful Response:**
- Verification result
- Verified Warehouse Location
- Picking Instruction ID

**Error Conditions:**
- Unauthorized user
- Instruction not found
- Unknown barcode
- Incorrect source location

### API-13.6: Verify Product UPC

**Endpoint:** `POST /api/picking-instructions/{pickingInstructionId}/verify-product`

**Purpose:** Verify that the scanned product matches the expected Individual Item.

**Authorized Role:**
- Assigned Picker

**Request Data:**
- scannedUpcCode

**Validation and Behavior:**
- Confirm the source location has been verified.
- Resolve the scanned UPC.
- Compare the associated Item with the expected Item.
- Reject incorrect or unknown UPCs.
- Do not modify Inventory or Quantity Picked.

**Successful Response:**
- Verification result
- Verified Individual Item
- Picking Instruction ID

**Error Conditions:**
- Unauthorized user
- Instruction not found
- Location not verified
- Unknown UPC
- Incorrect product

### API-13.7: Confirm Picking Movement

**Endpoint:** `POST /api/picking-instructions/{pickingInstructionId}/confirm-pick`

**Purpose:** Record the actual quantity removed from a verified source location.

**Authorized Role:**
- Assigned Picker

**Request Data:**
- quantityPicked
- confirmationRequestId (unique identifier used to prevent duplicate application)

**Validation and Behavior:**
- Confirm the instruction exists and is active.
- Confirm the source location and product have been verified.
- Require a positive whole-number quantity.
- Prevent picking more than the remaining instruction quantity.
- Prevent picking more than available source Inventory.
- Decrease Inventory by the confirmed quantity.
- Increase Customer Order Line Quantity Picked by the same amount.
- Record a Picking Movement.
- Prevent duplicate application of the same confirmation.
- Update instruction progress.
- Apply Inventory and Quantity Picked changes consistently.

**Successful Response:**
- Picking Movement ID
- Confirmed quantity
- Updated instruction quantity
- Updated source Inventory
- Updated Customer Order Line Quantity Picked

**Error Conditions:**
- Unauthorized user
- Instruction not found
- Location or product not verified
- Invalid quantity
- Quantity exceeds instruction
- Insufficient Inventory
- Duplicate confirmation
- Concurrent Inventory conflict

### API-13.8: Report Picking Shortage

**Endpoint:** `POST /api/picking-instructions/{pickingInstructionId}/shortages`

**Purpose:** Record a partial or complete shortage at an assigned source location.

**Authorized Role:**
- Assigned Picker

**Request Data:**
- quantityShort
- shortageReason (optional)

**Validation and Behavior:**
- Confirm the instruction exists.
- Confirm the Picker is authorized.
- Validate the reported shortage quantity.
- Preserve the actual Quantity Picked.
- Record the shortage electronically.
- Preserve the outstanding quantity for resolution.
- Do not decrease Inventory for missing units.

**Successful Response:**
- Picking Shortage ID
- Quantity Short
- Shortage status
- Remaining picking quantity

**Error Conditions:**
- Unauthorized user
- Instruction not found
- Invalid shortage quantity
- Duplicate shortage report

### API-13.9: Request Replenishment

**Endpoint:** `POST /api/picking-shortages/{pickingShortageId}/request-replenishment`

**Purpose:** Request additional stock for an unresolved picking shortage.

**Authorized Roles:**
- Picker
- Supervisor

**Validation and Behavior:**
- Confirm the shortage exists.
- Confirm the shortage is eligible for replenishment.
- Record the replenishment request.
- Make the request available to authorized warehouse personnel.
- Preserve the outstanding picking quantity.
- Prevent duplicate active replenishment requests for the same shortage.

**Successful Response:**
- Picking Shortage ID
- Replenishment request reference
- Updated shortage status

**Error Conditions:**
- Unauthorized user
- Shortage not found
- Invalid shortage status
- Duplicate active request

**[NEEDS CLARIFICATION]** Confirm whether the replenishment task is created directly by Feature 13 or delegated to another inventory movement feature.

### API-13.10: Request Alternate Picking Location

**Endpoint:** `POST /api/picking-shortages/{pickingShortageId}/alternate-location`

**Purpose:** Identify another eligible source location for outstanding picking quantities.

**Authorized Roles:**
- Picker
- Supervisor

**Validation and Behavior:**
- Confirm the shortage exists.
- Identify eligible Inventory locations.
- Exclude inactive or unavailable locations.
- Preserve previously confirmed Picking Movements.
- Generate or update the appropriate Picking Instruction.
- Require barcode verification at the new source location.

**Successful Response:**
- Alternate Warehouse Location
- Updated or additional Picking Instruction
- Remaining quantity to pick

**Error Conditions:**
- Unauthorized user
- Shortage not found
- No eligible alternate location
- Invalid request

### API-13.11: Complete Picking Assignment

**Endpoint:** `POST /api/picking-assignments/{pickingAssignmentId}/complete`

**Purpose:** Finish a Picking Assignment after all instructions have been completed or resolved.

**Authorized Role:**
- Assigned Picker

**Validation and Behavior:**
- Confirm the assignment exists.
- Confirm all instructions are completed or resolved.
- Reject premature completion.
- Prevent duplicate completion.
- Compare Quantity Picked with Quantity Ordered for each Customer Order Line.
- Set Customer Order status to Picked when all quantities are fully picked.
- Set Customer Order status to Partially Picked when confirmed shortages remain.
- Record the assignment completion timestamp.
- Make completed picking information available to Feature 14.
- Preserve all movements and shortages.

**Successful Response:**
- Picking Assignment ID
- Completed status
- Customer Order ID
- Final Customer Order picking status
- Completion timestamp

**Error Conditions:**
- Unauthorized user
- Assignment not found
- Outstanding unresolved instructions
- Assignment already completed

### API-13.12: Retrieve Picking Shortages

**Endpoint:** `GET /api/picking-shortages`

**Purpose:** Allow authorized Supervisors to review picking shortages.

**Authorized Roles:**
- Supervisor
- Manager

**Optional Filters:**
- Picking Assignment
- Customer Order
- Shortage status
- Individual Item

**Response Data:**
- Picking Shortage ID
- Customer Order reference
- Picking Instruction
- Individual Item
- Quantity Short
- Reporting Picker
- Report timestamp
- Shortage status

**Validation and Behavior:**
- Return matching shortage records.
- Preserve unresolved shortages for review.
- Do not modify Inventory or picking quantities.

**Error Conditions:**
- Unauthorized access
- Invalid filter values

### API-13.13: Retrieve Picking History

**Endpoint:** `GET /api/picking-assignments/{pickingAssignmentId}/history`

**Purpose:** Review confirmed Picking Movements and shortages for an assignment.

**Authorized Roles:**
- Supervisor
- Manager
- Other users with approved read permissions

**Response Data:**
- Customer Order
- Assigned Picker
- Picking Instructions
- Source Warehouse Locations
- Confirmed quantities
- Movement timestamps
- Recorded shortages
- Assignment completion status

**Validation and Behavior:**
- Retrieve preserved historical records.
- Do not modify existing Picking Movements.
- Restrict access according to role permissions.

**Error Conditions:**
- Unauthorized access
- Assignment not found

### General API Requirements

- All picking write operations MUST enforce server-side authorization.
- Picking Assignments MUST reference valid Customer Orders and Users.
- Picking Instructions MUST reference valid Items and Warehouse Locations.
- The system MUST prevent duplicate active assignments.
- Location and product barcode verification MUST precede picking confirmation.
- Confirmed quantities MUST be positive whole numbers.
- Confirmed quantities MUST NOT exceed the remaining instruction quantity.
- Confirmed quantities MUST NOT exceed available source Inventory.
- Inventory decreases and Quantity Picked increases MUST be committed consistently.
- Duplicate confirmation requests MUST NOT apply Inventory movements more than once.
- Inventory quantities MUST NOT become negative.
- The system MUST preserve Picking Movement history.
- Shortages MUST be recorded electronically.
- Assignment completion MUST validate all outstanding instructions.
- API operations MUST enforce valid assignment and order status transitions.
- API responses MUST preserve Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered as separate values.
- Picking operations MUST NOT automatically perform shipping or delivery.

**[NEEDS CLARIFICATION]** Confirm the final API route conventions, barcode verification state handling, concurrency-control method, and approved reassignment workflow.

---

## Screen Requirements

### SCREEN-13.1: Available Picking Work

**Purpose:** Allow an authorized Picker to request available Customer Orders.

**Authorized Users:**
- Picker
- Other authorized warehouse personnel

**Displayed Information:**
- Available Customer Order Number
- Customer reference
- Order status
- Assignment availability
- Message when no picking work is available

**Controls:**
- Request Picking Work
- Open Assigned Order
- Refresh Available Work

**Behavior:**
- Show only eligible Customer Orders.
- Exclude Draft, Canceled, and already assigned orders.
- Prevent duplicate active assignments.
- Display a message when no work is available.
- Require an authorized user.

### SCREEN-13.2: Picking Assignment Overview

**Purpose:** Show the Picker the assigned Customer Order and picking progress.

**Authorized Users:**
- Assigned Picker
- Authorized Supervisor

**Displayed Information:**
- Customer Order Number
- Picking Assignment ID
- Assigned Picker
- Assignment status
- Total Picking Instructions
- Completed Instructions
- Outstanding Instructions
- Recorded shortages

**Controls:**
- Start Picking
- Continue Picking
- View Instructions
- Complete Assignment, when eligible

**Behavior:**
- Show the current assignment.
- Allow the Picker to start or resume eligible work.
- Identify outstanding instructions.
- Prevent completion while instructions remain unresolved.
- Preserve assignment progress.

### SCREEN-13.3: Picking Instruction

**Purpose:** Direct the Picker to the next assigned Item and source Warehouse Location.

**Authorized User:**
- Assigned Picker

**Displayed Information:**
- Customer Order Number
- Item Number
- Item Description
- Quantity to Pick
- Quantity Already Picked
- Remaining Quantity
- Source Warehouse Location
- Aisle
- Row
- Slot
- Instruction sequence
- Instruction status

**Controls:**
- Scan Location
- Scan Product UPC
- Enter Quantity Picked
- Confirm Pick
- Report Shortage
- Request Alternate Location
- Request Replenishment
- Next Instruction, when eligible

**Behavior:**
- Display instructions in the assigned sequence.
- Require verification of the source location.
- Require verification of the expected product.
- Prevent confirmation before both verifications succeed.
- Reject invalid or excessive quantities.
- Record confirmed picking movements.
- Advance to the next instruction when the current instruction is completed or resolved.

### SCREEN-13.4: Barcode Verification

**Purpose:** Confirm the correct Warehouse Location and Individual Item before picking.

**Authorized User:**
- Assigned Picker

**Displayed Information:**
- Expected Warehouse Location
- Expected Item
- Scanned Location Code
- Scanned Product UPC
- Location verification result
- Product verification result

**Controls:**
- Scan Location Barcode
- Scan Product Barcode
- Retry Scan
- Request Supervisor Assistance

**Behavior:**
- Compare the scanned location with the assigned source location.
- Compare the scanned UPC with the expected Item.
- Display clear verification results.
- Reject incorrect, unknown, or unreadable barcodes.
- Prevent unverified picking confirmation.
- Do not update Inventory during verification alone.

### SCREEN-13.5: Picking Shortage

**Purpose:** Record insufficient Inventory at the assigned picking location.

**Authorized User:**
- Assigned Picker

**Displayed Information:**
- Customer Order Number
- Individual Item
- Assigned Source Location
- Required Quantity
- Actual Quantity Picked
- Quantity Short
- Shortage status
- Available resolution options

**Controls:**
- Report Shortage
- Request Replenishment
- Request Alternate Location
- Return to Picking Instruction

**Behavior:**
- Allow partial or full shortages to be reported.
- Preserve actual confirmed quantities.
- Record shortages electronically.
- Keep missing units separate from picked units.
- Make unresolved shortages available for Supervisor review.
- Do not require paper pick tickets.

### SCREEN-13.6: Picking Completion

**Purpose:** Review and complete a Picking Assignment.

**Authorized User:**
- Assigned Picker

**Displayed Information:**
- Customer Order Number
- Picking Assignment ID
- Assigned Picker
- Total Quantity Ordered
- Total Quantity Picked
- Completed Instructions
- Outstanding Instructions
- Confirmed shortages
- Expected final order status

**Controls:**
- Review Outstanding Instructions
- Confirm Completion
- Return to Picking

**Behavior:**
- Validate that all instructions are completed or resolved.
- Reject premature completion.
- Set the order to Picked when all ordered quantities are picked.
- Set the order to Partially Picked when confirmed shortages remain.
- Prevent duplicate completion.
- Make completed picking information available to Feature 14.

### SCREEN-13.7: Supervisor Shortage Review

**Purpose:** Allow authorized Supervisors to review unresolved picking shortages.

**Authorized Users:**
- Supervisor
- Manager

**Displayed Information:**
- Customer Order Number
- Picking Assignment
- Individual Item
- Assigned Picker
- Source Warehouse Location
- Quantity Short
- Shortage status
- Report timestamp

**Controls:**
- View Shortage Details
- View Picking Assignment
- Review Replenishment Request
- Refresh Shortage List

**Behavior:**
- Display unresolved shortages.
- Allow Supervisors to review recorded details.
- Preserve Picking Movement and shortage history.
- Do not automatically mark missing units as picked.

### SCREEN-13.8: Picking History

**Purpose:** Allow authorized personnel to review completed Picking Assignments.

**Authorized Users:**
- Supervisor
- Manager
- Other users with approved read permissions

**Displayed Information:**
- Customer Order Number
- Assigned Picker
- Assignment status
- Start and completion timestamps
- Source Warehouse Locations
- Confirmed Picking Movements
- Actual quantities picked
- Recorded shortages

**Controls:**
- Search by Customer Order
- Open Picking Assignment
- View Picking Movements
- View Shortages
- Return to Assignment List

**Behavior:**
- Display preserved picking records.
- Keep historical movements read-only.
- Show actual picked quantities and shortages.
- Restrict access according to user permissions.

### General Screen Requirements

- Screens MUST follow the approved Warehouse System UI style conventions.
- Picking screens MUST support electronic, paperless workflows.
- Picking instructions MUST clearly display the next location and Item.
- Location and product scanning controls MUST be easy to access on warehouse devices.
- The system MUST provide clear success and error messages after scans.
- Invalid barcode scans MUST NOT confirm a pick.
- Quantity fields MUST accept only valid whole-number quantities.
- Quantity Ordered and Quantity Picked MUST remain distinguishable.
- Shortage reporting MUST be available from the picking workflow.
- Assignment progress MUST remain visible.
- Screens MUST prevent unauthorized actions.
- UI validation MUST be reinforced by server-side validation.
- Screen designs MUST be documented in Figma or the approved design tool before implementation.

**[NEEDS CLARIFICATION]** Confirm the required handheld scanner screen size, device operating system, and whether offline operation is supported.

---

## Definition of Done

Feature 13 is considered complete when all approved requirements and acceptance criteria have been implemented and verified.

### Requirements and Design

- [ ] All six User Stories are implemented.
- [ ] Functional Requirements FR-001 through FR-053 are satisfied.
- [ ] Assumptions and unresolved clarifications have been reviewed.
- [ ] Edge Cases have corresponding handling and verification.
- [ ] Success Criteria have been evaluated.
- [ ] Data ownership boundaries are documented and followed.
- [ ] Initial Data Model has been reviewed and approved.
- [ ] Picking Assignment and Picking Instruction status rules are approved.
- [ ] API contracts have been reviewed.
- [ ] Screen designs have been prepared and reviewed.

### Implementation

- [ ] Authorized Pickers can request available picking work.
- [ ] Only eligible Customer Orders can be assigned.
- [ ] Duplicate active Picking Assignments are prevented.
- [ ] The system generates efficient picking sequences.
- [ ] Picking Instructions identify Items, quantities, and source locations.
- [ ] Primary picking bins are preferred when sufficient Inventory exists.
- [ ] Additional eligible locations are supported.
- [ ] Inactive or unavailable locations are excluded.
- [ ] Pickers can scan and verify source Warehouse Locations.
- [ ] Pickers can scan and verify product UPCs.
- [ ] Incorrect or unknown barcodes are rejected.
- [ ] Picking confirmation requires successful verification.
- [ ] Confirmed quantities are positive whole numbers.
- [ ] Confirmed quantities cannot exceed instruction limits.
- [ ] Confirmed quantities cannot exceed available Inventory.
- [ ] Confirmed picking decreases source Inventory correctly.
- [ ] Confirmed picking increases Customer Order Line Quantity Picked correctly.
- [ ] Inventory and Quantity Picked changes remain consistent.
- [ ] Every confirmed pick creates a Picking Movement.
- [ ] Duplicate Picking Movements are not applied.
- [ ] Partial and complete shortages can be reported electronically.
- [ ] Replenishment requests or alternate locations are supported.
- [ ] Unresolved shortages are available for Supervisor review.
- [ ] Picking Instructions advance after completion or resolution.
- [ ] Incomplete assignments cannot be completed prematurely.
- [ ] Fully picked orders receive Picked status.
- [ ] Partially picked orders receive Partially Picked status.
- [ ] Duplicate assignment completion is prevented.
- [ ] Completed picking information is available to Feature 14.
- [ ] Picking does not automatically update Quantity Shipped or Quantity Delivered.
- [ ] Picking Assignment history is preserved.
- [ ] Unauthorized users cannot perform picking operations.

### Testing and Verification

- [ ] All 28 Gherkin Acceptance Criteria have corresponding verification tests.
- [ ] Unit tests cover picking eligibility.
- [ ] Unit tests cover duplicate assignment prevention.
- [ ] Unit tests cover picking sequence generation.
- [ ] Unit tests cover location verification.
- [ ] Unit tests cover UPC verification.
- [ ] Unit tests cover quantity validation.
- [ ] Unit tests cover Inventory availability checks.
- [ ] Unit tests cover shortage calculations.
- [ ] Unit tests cover assignment completion rules.
- [ ] API tests verify successful picking operations.
- [ ] API tests verify unauthorized access is denied.
- [ ] API tests verify invalid barcode scans are rejected.
- [ ] API tests verify invalid quantities are rejected.
- [ ] API tests verify duplicate confirmations do not update Inventory twice.
- [ ] Integration tests verify Customer Order retrieval from Feature 12.
- [ ] Integration tests verify Item and UPC references.
- [ ] Integration tests verify Warehouse Location and Inventory references.
- [ ] Integration tests verify Inventory decreases and Quantity Picked increases consistently.
- [ ] Integration tests verify shortage handling and Supervisor review.
- [ ] Integration tests verify completed picking information is available to Feature 14.
- [ ] Tests verify that Quantity Ordered remains unchanged.
- [ ] Tests verify that Quantity Shipped and Quantity Delivered remain unchanged by picking.
- [ ] Tests verify concurrent Inventory operations do not produce negative quantities.
- [ ] Regression tests confirm existing warehouse features continue to operate correctly.

### Documentation and Review

- [ ] API documentation is updated.
- [ ] Data model documentation is updated.
- [ ] Screen documentation is updated.
- [ ] Picking workflow and barcode verification rules are documented.
- [ ] Role permissions are documented.
- [ ] Picking status transition rules are documented.
- [ ] Shortage and replenishment procedures are documented.
- [ ] Known limitations and approved deferrals are recorded.
- [ ] Code has been reviewed.
- [ ] Required tests pass.
- [ ] The feature is approved for integration.

---

## Out of Scope

The following activities are not implemented as part of Feature 13.

### Customer Order Entry

Creating Customer Orders, selecting Customers, adding original order lines, and maintaining Quantity Ordered belong to Feature 12.

Feature 13 only processes Customer Orders that have been released for picking.

### Customer Master Data Maintenance

Creating, editing, or deactivating Customers is not part of Feature 13.

Customer information is maintained through Feature 6.

### Individual Item and UPC Master Data Maintenance

Creating or editing Individual Items and UPC definitions is outside Feature 13.

Feature 13 uses existing Item and UPC records for product identification.

### Warehouse Location Maintenance

Creating, editing, activating, or deactivating Warehouse Locations is not part of Feature 13.

Feature 13 uses existing eligible locations for picking instructions.

### General Inventory Maintenance

General Inventory corrections, stock adjustments unrelated to confirmed picking, and physical inventory counts are outside Feature 13.

Feature 13 records Inventory decreases only as part of confirmed Picking Movements.

### Physical Replenishment and Inventory Transfers

Feature 13 supports requesting replenishment or another eligible picking location.

Physically transferring Inventory between bins and completing replenishment movements belong to the appropriate inventory movement workflow.

**[NEEDS CLARIFICATION]** Confirm which feature owns replenishment task execution.

### Receiving and Putaway

Receiving Supplier Orders and placing incoming Inventory into storage locations are outside Feature 13.

These activities belong to the receiving and putaway features.

### Shipping

Packing, loading, shipment confirmation, and recording Quantity Shipped belong to Feature 14.

Feature 13 makes completed picking information available to shipping but does not ship products.

### Delivery

Transporting Customer Orders, confirming delivery, and recording Quantity Delivered belong to Feature 15.

Feature 13 does not perform delivery operations.

### Customer Order Pricing and Billing

Calculating invoices, processing payments, and managing Customer billing are not part of Feature 13.

### Advanced Warehouse Optimization

The feature requires an efficient picking sequence, but advanced warehouse-wide optimization, predictive workload balancing, and complex multi-Picker coordination are not included unless separately approved.

### Offline Picking

Offline scanning, local Inventory updates, and synchronization after reconnection are not included in the current draft.

**[NEEDS CLARIFICATION]** Confirm whether offline device support is required.

### Picking Reassignment

The system prevents duplicate active assignments.

A complete reassignment workflow for unavailable Pickers requires separate approval.

**[NEEDS CLARIFICATION]** Confirm the authorized reassignment and resumption rules.

### Final Deferrals and Clarifications

The following decisions remain open for review:

- **[NEEDS CLARIFICATION]** Exact Inventory update ownership and API.
- **[NEEDS CLARIFICATION]** Replenishment request ownership and completion workflow.
- **[NEEDS CLARIFICATION]** Customer Order status update mechanism across Features 12–15.
- **[NEEDS CLARIFICATION]** Handling an Item with no eligible Inventory location.
- **[NEEDS CLARIFICATION]** Concurrency control for Inventory updates.
- **[NEEDS CLARIFICATION]** Barcode verification state and retry behavior.
- **[NEEDS CLARIFICATION]** Case UPC quantity handling.
- **[NEEDS CLARIFICATION]** Picking Assignment reassignment and resumption.
- **[NEEDS CLARIFICATION]** Offline picking support.
- **[NEEDS CLARIFICATION]** Required handheld scanner specifications.
- **[NEEDS CLARIFICATION]** Final API conventions and audit requirements.

These decisions must be reviewed before implementation. They do not prevent Feature 13 from being maintained as a design draft.
