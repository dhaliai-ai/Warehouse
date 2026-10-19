
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

## Gherkin AC

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
