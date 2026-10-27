
# Feature: Receive Supplier Order

**Feature ID:** 10  
**Branch pattern:** `feature/10-receive-supplier-order`  
**Status:** Draft - Professor Feedback Incorporated; Clarifications Pending  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System assists receiving workers in receiving shipments from Suppliers. The worker identifies the Supplier Order using the PO Number on the bill of lading, records the receiving door, scans delivered cases or individual items, records actual received quantities, compares those quantities with the original order, investigates discrepancies, and completes receiving. Received products remain at the receiving location until they are processed through the separate Put Away workflow in Feature 11.

---

## User Stories

### US-10.1: Identify Supplier Order

**As a** Receiving Clerk  
**I want to** enter the PO Number from the bill of lading  
**So that** I can identify the correct Supplier Order and review what was ordered.

**Priority:** P1  
**Independent test:** Enter the PO Number of an existing submitted Supplier Order and verify that the correct Supplier, items, and ordered quantities are displayed.

### US-10.2: Record Receiving Location

**As a** Receiving Clerk  
**I want to** record the warehouse and receiving door where the shipment arrived  
**So that** Put Away workers can locate the received products.

**Priority:** P1  
**Independent test:** Select a valid receiving door and verify that it is stored with the Receiving Record.

### US-10.3: Scan Received Items

**As a** Receiving Clerk  
**I want to** scan the delivered products and record their quantities  
**So that** the system accurately records what the Supplier actually delivered.

**Priority:** P1  
**Independent test:** Scan a known Item UPC and a known Case UPC and verify that the appropriate quantities are recorded in individual units.

### US-10.4: Reconcile Ordered and Received Quantities

**As a** Receiving Clerk  
**I want to** compare the quantities ordered with the quantities received  
**So that** missing, extra, or incorrect products can be identified and investigated.

**Priority:** P1  
**Independent test:** Receive fewer or more units than ordered and verify that the system displays the discrepancy and allows it to be reviewed.

### US-10.5: Complete Receiving and Prepare for Put Away

**As a** Receiving Clerk  
**I want to** complete receiving after verifying the shipment  
**So that** the received products become available for Put Away without being incorrectly recorded as already stored in warehouse bins.

**Priority:** P1  
**Independent test:** Complete a receiving session with valid scanned quantities and a receiving door, then verify that the received products are available for Feature 11.

---

## Functional Requirements

- **FR-001:** The system MUST allow authorized Receiving Clerks and receiving workers to enter or scan a PO Number from the bill of lading.
- **FR-002:** The system MUST locate the corresponding Supplier Order using its unique PO Number.
- **FR-003:** The system MUST display the Supplier, ordered items, and original ordered quantities for the identified Supplier Order.
- **FR-004:** The system MUST reject a PO Number that does not identify an existing Supplier Order.
- **FR-005:** The system MUST prevent receiving against Draft or Canceled Supplier Orders.
- **FR-006:** The system MUST allow receiving against Submitted or Partially Received Supplier Orders.
- **FR-007:** The system MUST preserve the original Quantity Ordered when receiving is performed.
- **FR-008:** The system MUST identify the destination Warehouse recorded on the Supplier Order and display it during receiving. The receiving worker MUST confirm that the shipment arrived at that Warehouse. If the actual receiving Warehouse differs from the Supplier Order's destination Warehouse, the system MUST flag the mismatch for authorized review and MUST NOT silently accept the change. [NEEDS CLARIFICATION: Confirm whether authorized Managers or Supervisors may approve receiving at a different Warehouse.]
- **FR-009:** The system MUST allow the worker to select an existing Receiving Door within that Warehouse.
- **FR-010:** The system MUST associate the selected Receiving Door with the Receiving Record.
- **FR-011:** The system MUST require a valid Receiving Door before a receiving session can be completed.
- **FR-012:** The system MUST allow a receiving worker to scan Individual Item UPCs.
- **FR-013:** The system MUST allow a receiving worker to scan Case UPCs when case-level barcodes are configured for an Item.
- **FR-014:** The system MUST identify the Individual Item associated with a scanned UPC.
- **FR-015:** The system MUST determine whether the scanned barcode represents an individual unit or a case.
- **FR-016:** When a Case UPC is scanned, the system MUST convert the scanned case quantity into individual units using the units represented by that barcode. The system MUST compare this quantity with the Units Per Case preserved on the submitted Supplier Order Line. If the values differ, the system MUST flag the packaging difference for review and preserve the actual quantity received without changing the original Quantity Ordered.
- **FR-017:** When an Individual Item UPC is scanned, the system MUST record the corresponding quantity in individual units.
- **FR-018:** The system MUST support recording multiple scans of the same Item during one receiving session.
- **FR-019:** The system MUST maintain a running Quantity Received for each Supplier Order Line.
- **FR-020:** The system MUST record received quantities separately from the original ordered quantities.
- **FR-021:** The system MUST prevent negative received quantities.
- **FR-022:** The system MUST reject an unreadable or unknown barcode without recording an unidentified Item as received.
- **FR-023:** The system MUST identify when a scanned Item does not appear on the selected Supplier Order.
- **FR-024:** The system MUST prevent an unexpected Item from being silently added to the Supplier Order.
- **FR-025:** The system MUST display the original Quantity Ordered, previously received quantity, current session quantity, and cumulative Quantity Received for each order line.
- **FR-026:** The system MUST compare cumulative Quantity Received with Quantity Ordered.
- **FR-027:** The system MUST identify shortages when cumulative Quantity Received is less than Quantity Ordered.
- **FR-028:** The system MUST identify overages when cumulative Quantity Received is greater than Quantity Ordered.
- **FR-029:** The system MUST identify ordered items for which no units have been received.
- **FR-030:** The system MUST allow the receiving worker to continue scanning additional items or cases while investigating discrepancies.
- **FR-031:** The system MUST recalculate receiving differences when additional quantities are recorded.
- **FR-032:** The system MUST identify and record quantity discrepancies during receiving. Receiving workers MUST be able to report and acknowledge discrepancies, but final approval of unresolved shortages, overages, or unexpected items MUST be performed by an authorized Manager or Supervisor before the receiving session is completed. The system MUST record the approving User, approval date and time, and discrepancy details.
- **FR-033:** The system MUST preserve the actual received quantity even when it differs from Quantity Ordered.
- **FR-034:** The system MUST record confirmed discrepancies for supplier performance reporting in Feature 17.
- **FR-035:** The system MUST maintain a Receiving Record for each receiving session.
- **FR-036:** Each Receiving Record MUST identify the Supplier Order, Warehouse, Receiving Door, receiving worker, and receiving date and time.
- **FR-037:** The system MUST maintain individual Receiving Record Lines identifying the Items and quantities received during the session.
- **FR-038:** The system MUST support multiple receiving sessions for a Supplier Order that has not been fully received.
- **FR-039:** The system MUST update the cumulative Quantity Received for each Supplier Order Line after a receiving session is completed.
- **FR-040:** The system MUST set a Supplier Order to Partially Received when receiving has occurred but at least one ordered quantity remains outstanding and further receiving is expected.
- **FR-041:** The system MUST distinguish completion of an individual Receiving Record from final closure of the Supplier Order. Completing a Receiving Record MUST NOT automatically close the Supplier Order when additional deliveries are expected. The system MUST set the Supplier Order status to Received when all ordered quantities have been received or when an authorized Manager or Supervisor confirms that no further deliveries are expected. If the order is closed with shortages or overages, the system MUST preserve the actual received quantities, confirmed discrepancies, closing User, and closing date and time.
- **FR-042:** The system MUST preserve confirmed shortages or overages when an order is closed as Received.
- **FR-043:** The system MUST prevent completed receiving sessions from being silently overwritten.
- **FR-044:** The system MUST make completed receiving quantities available to the Put Away process.
- **FR-045:** The system MUST associate received products awaiting Put Away with the Receiving Door where they were unloaded.
- **FR-046:** Completing receiving MUST NOT automatically assign received products to final storage bins.
- **FR-047:** Completing receiving MUST NOT mark products as already put away.
- **FR-048:** The system MUST maintain the distinction between Quantity Ordered, Quantity Received, and quantity physically put away.
- **FR-049:** The system MUST restrict receiving operations to authorized receiving personnel.
- **FR-050:** The system MUST allow authorized Managers or Supervisors to review receiving discrepancies.
- **FR-051:** The system MUST preserve receiving history for later inventory reconciliation and reporting.
- **FR-052:** The system MUST reject attempts to complete a nonexistent or already completed Receiving Record.
- **FR-053:** The system MUST prevent the same Receiving Record from being completed more than once.
- **FR-054:** The system MUST keep Supplier Order creation separate from Supplier Order receiving.

---

## Key Entities

### Supplier Order

Represents an existing purchase order placed with a Supplier.

The Supplier Order provides the original PO Number, Supplier, destination Warehouse, ordered Items, and ordered quantities.

### Supplier Order Line

Represents an Individual Item ordered from a Supplier.

Each line maintains Quantity Ordered, original Units Per Case, and cumulative Quantity Received separately.

### Receiving Record

Represents a receiving session for an incoming shipment.

A Receiving Record identifies the Supplier Order, Warehouse, Receiving Door, receiving worker, and session status.

### Receiving Record Line

Represents an Item and quantity received during a particular receiving session.

### Individual Item

Represents a product received from a Supplier.

Each Item may have UPCs for individual units and cases.

### UPC

Represents a barcode used to identify an Individual Item or a case containing multiple units.

### Warehouse

Represents the warehouse receiving the shipment.

Warehouse maintenance is defined in Feature 2.

### Receiving Door

Represents a designated warehouse location where an incoming shipment is unloaded and awaits Put Away.

### Receiving Discrepancy

Represents a confirmed difference between ordered and received quantities, including approval information.

### User

Represents an employee authorized to receive Supplier Orders or review and approve discrepancies.

---

## Initial Data Model

### Supplier Order

| Attribute | Type | Description |
|---|---|---|
| supplierOrderId | Integer | Unique Supplier Order identifier |
| poNumber | String | Unique purchase order number |
| supplierId | Integer | Foreign key referencing Supplier |
| warehouseId | Integer | Destination Warehouse recorded on the Supplier Order |
| status | String | Draft, Submitted, Partially Received, Received, or Canceled |
| closedAt | DateTime | Date and time receiving was finally closed |
| closedBy | Integer | User who authorized final closure |

**Relationships:**
- Each Supplier Order belongs to one Supplier.
- Each Supplier Order is associated with one destination Warehouse.
- Each Supplier Order contains one or more Supplier Order Lines before submission.
- One Supplier Order may have multiple Receiving Records.

**Constraints:**
- PO Number must be unique.
- Only Submitted and Partially Received orders may begin a new receiving session.
- Original ordered quantities must remain preserved.
- A Supplier Order cannot be finally closed with unresolved discrepancies.

### Supplier Order Line

| Attribute | Type | Description |
|---|---|---|
| supplierOrderLineId | Integer | Unique Supplier Order Line identifier |
| supplierOrderId | Integer | Foreign key referencing Supplier Order |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityOrderedCases | Integer | Original quantity ordered in cases |
| unitsPerCase | Integer | Units per case preserved on the submitted order |
| quantityReceivedUnits | Integer | Cumulative quantity received in individual units |

**Derived Values:**
- Ordered Units = quantityOrderedCases × unitsPerCase.
- Quantity Difference = quantityReceivedUnits - Ordered Units.
- Outstanding Units = max(0, Ordered Units - quantityReceivedUnits).

**Relationships:**
- Each Supplier Order Line belongs to one Supplier Order.
- Each line references one Individual Item.
- Receiving Record Lines contribute to cumulative Quantity Received.

### Receiving Record

| Attribute | Type | Description |
|---|---|---|
| receivingRecordId | Integer | Unique Receiving Record identifier |
| supplierOrderId | Integer | Foreign key referencing Supplier Order |
| warehouseId | Integer | Warehouse where shipment was received |
| receivingDoorId | Integer | Foreign key referencing Receiving Door |
| receivedBy | Integer | User who performed receiving |
| startedAt | DateTime | Date and time receiving started |
| completedAt | DateTime | Date and time receiving completed |
| status | String | In Progress or Completed |
| discrepanciesConfirmed | Boolean | Indicates whether identified discrepancies were approved |

**Relationships:**
- Each Receiving Record belongs to one Supplier Order.
- Each Receiving Record is associated with one Warehouse.
- Each Receiving Record identifies one Receiving Door.
- Each Receiving Record contains Receiving Record Lines.
- A completed Receiving Record can provide products for Put Away.

**Constraints:**
- receivingDoorId must reference a Receiving Door in the selected Warehouse.
- A Receiving Record cannot be completed without a valid Receiving Door.
- A Receiving Record with unresolved discrepancies cannot be completed without Manager or Supervisor approval.
- A completed Receiving Record cannot be completed again.

### Receiving Record Line

| Attribute | Type | Description |
|---|---|---|
| receivingRecordLineId | Integer | Unique Receiving Record Line identifier |
| receivingRecordId | Integer | Foreign key referencing Receiving Record |
| supplierOrderLineId | Integer | Foreign key referencing Supplier Order Line |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityReceivedUnits | Integer | Quantity received during this session in individual units |

**Relationships:**
- Each Receiving Record Line belongs to one Receiving Record.
- Each Receiving Record Line references an ordered Item.
- Completed Receiving Record Lines contribute to cumulative received quantities.

**Constraints:**
- quantityReceivedUnits cannot be negative.
- The Item must be associated with the selected Supplier Order Line.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique Item Number or SKU |
| description | String | Item description |
| unitsPerCase | Integer | Current number of individual units per case |

**Relationships:**
- One Individual Item can appear on multiple Supplier Order Lines.
- One Individual Item can have multiple UPCs.
- Item maintenance is defined in Feature 4.

### UPC

| Attribute | Type | Description |
|---|---|---|
| upcId | Integer | Unique UPC identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| upcCode | String | Barcode value |
| barcodeType | String | Individual Unit or Case |
| unitsRepresented | Integer | Number of individual units represented by one scan |

**Relationships:**
- Each UPC identifies one Individual Item.
- An Item may have an individual-unit UPC and a case UPC.

**Constraints:**
- An individual-unit UPC represents one unit.
- A case UPC represents the configured number of units in the case.
- Each UPC code must uniquely identify its configured Item and package type.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique Warehouse identifier |
| name | String | Warehouse name |

**Relationships:**
- A Warehouse contains one or more Receiving Doors.
- Warehouse maintenance is defined in Feature 2.

### Receiving Door

| Attribute | Type | Description |
|---|---|---|
| receivingDoorId | Integer | Unique Receiving Door identifier |
| warehouseId | Integer | Foreign key referencing Warehouse |
| doorCode | String | Receiving Door identifier, such as "DOOR-3" |
| isActive | Boolean | Indicates whether the Receiving Door can be used |

**Relationships:**
- Each Receiving Door belongs to one Warehouse.
- One Receiving Door may be referenced by multiple Receiving Records.

**Constraints:**
- doorCode must be unique within its Warehouse.
- A Receiving Door must be active to be selected for a new receiving session.

### Receiving Discrepancy

| Attribute | Type | Description |
|---|---|---|
| discrepancyId | Integer | Unique Discrepancy identifier |
| receivingRecordId | Integer | Foreign key referencing Receiving Record |
| supplierOrderLineId | Integer | Foreign key referencing Supplier Order Line |
| quantityDifferenceUnits | Integer | Difference between received and expected quantities |
| confirmedBy | Integer | Manager or Supervisor who approved the discrepancy |
| confirmedAt | DateTime | Date and time of approval |
| discrepancyType | String | Shortage, Overage, Unexpected Item, or Packaging Mismatch |
| notes | String | Explanation or resolution of discrepancy |

**Relationships:**
- Each Receiving Discrepancy belongs to a Receiving Record.
- Each Discrepancy may reference a Supplier Order Line.
- Each Discrepancy references the approving User.
- Discrepancy information supports Feature 17.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Receiving personnel create and complete Receiving Records.
- Managers or Supervisors approve receiving discrepancies and may close Supplier Orders.

---

## Gherkin AC

### US-10.1: Identify Supplier Order

#### AC-10.1.1: Identify valid Supplier Order

**Given** a Supplier Order exists with PO Number "PO1001"  
**And** its status is Submitted  
**And** the user is authenticated as a Receiving Clerk  
**When** the user enters "PO1001" from the bill of lading  
**Then** the system identifies the Supplier Order  
**And** displays the Supplier, Items, and original Quantity Ordered.

#### AC-10.1.2: Reject nonexistent PO Number

**Given** no Supplier Order exists with PO Number "PO9999"  
**When** the receiving worker enters "PO9999"  
**Then** the system reports that no matching Supplier Order exists  
**And** does not create a Receiving Record for that PO Number.

#### AC-10.1.3: Reject canceled Supplier Order

**Given** a Supplier Order exists with status Canceled  
**When** the receiving worker attempts to begin receiving against it  
**Then** the system rejects the request  
**And** no Receiving Record is started.

#### AC-10.1.4: Allow partially received Supplier Order

**Given** a Supplier Order exists with status Partially Received  
**And** additional quantities remain outstanding  
**When** an authorized receiving worker enters its PO Number  
**Then** the system displays the original ordered quantities  
**And** displays the quantities already received  
**And** allows a new receiving session to begin.

### US-10.2: Record Receiving Location

#### AC-10.2.1: Record valid Receiving Door

**Given** a Supplier Order has been identified  
**And** Warehouse A contains an active Receiving Door "DOOR-3"  
**When** the receiving worker selects Warehouse A and "DOOR-3"  
**Then** the system associates that Receiving Door with the Receiving Record.

#### AC-10.2.2: Reject nonexistent Receiving Door

**Given** the receiving worker has identified a Supplier Order  
**When** the worker selects a Receiving Door that does not exist  
**Then** the system rejects the selection  
**And** does not save an invalid Receiving Door.

#### AC-10.2.3: Reject Receiving Door from another Warehouse

**Given** a Receiving Record is associated with Warehouse A  
**And** Receiving Door "DOOR-2" belongs to Warehouse B  
**When** the worker attempts to select "DOOR-2" for the record  
**Then** the system rejects the selection  
**And** requires a Receiving Door belonging to Warehouse A.

#### AC-10.2.3a: Identify destination Warehouse mismatch

**Given** a Submitted Supplier Order identifies Warehouse A as its destination  
**And** a Receiving Clerk begins receiving the shipment at Warehouse B  
**When** the Receiving Clerk attempts to select Warehouse B  
**Then** the system identifies that the receiving Warehouse differs from the Supplier Order's destination Warehouse  
**And** flags the mismatch for authorized review  
**And** does not silently accept Warehouse B as the receiving Warehouse  
**And** preserves the original destination Warehouse on the Supplier Order.

#### AC-10.2.4: Require Receiving Door before completion

**Given** a Receiving Record contains scanned items  
**And** no Receiving Door has been selected  
**When** the receiving worker attempts to complete receiving  
**Then** the system rejects completion  
**And** requires a valid Receiving Door.

#### AC-10.2.5: Make Receiving Door available for Put Away

**Given** a Receiving Record has been completed at "DOOR-3"  
**When** a Put Away worker retrieves the completed Receiving Record  
**Then** the system displays "DOOR-3" as the location of the received products.

### US-10.3: Scan Received Items

#### AC-10.3.1: Scan individual Item UPC

**Given** a Supplier Order contains Item A  
**And** Item A has an individual-unit UPC  
**When** the receiving worker scans that UPC once  
**Then** the system identifies Item A  
**And** records one individual unit received.

#### AC-10.3.2: Scan Case UPC

**Given** a Supplier Order contains Item A  
**And** Item A has a Case UPC representing 12 units  
**When** the receiving worker scans the Case UPC once  
**Then** the system identifies Item A  
**And** records 12 individual units received.

#### AC-10.3.3: Scan multiple cases

**Given** a Supplier Order contains Item A  
**And** each case of Item A contains 12 units  
**When** the receiving worker scans the Case UPC three times  
**Then** the system records 36 individual units received during the session.

#### AC-10.3.4: Reject unknown barcode

**Given** the receiving worker has started a valid receiving session  
**When** the worker scans a barcode that does not match any configured UPC  
**Then** the system reports that the barcode is unknown  
**And** does not add an unidentified Item to the received quantities.

#### AC-10.3.5: Identify unexpected Item

**Given** a Supplier Order contains Item A but not Item B  
**When** the receiving worker scans Item B  
**Then** the system identifies Item B as unexpected  
**And** does not silently add Item B to the Supplier Order  
**And** flags the issue for review.

#### AC-10.3.6: Preserve Quantity Ordered

**Given** a Supplier Order Line contains 5 cases ordered  
**When** the receiving worker records received quantities  
**Then** the original Quantity Ordered remains 5 cases  
**And** the system records Quantity Received separately.

#### AC-10.3.7: Reject unauthorized receiving

**Given** the user is authenticated as a Driver without receiving permission  
**When** the user attempts to start a receiving session  
**Then** the system denies the request  
**And** no Receiving Record is created.

#### AC-10.3.8: Identify Case UPC packaging mismatch

**Given** a Supplier Order Line preserves 12 Units Per Case  
**And** the delivered Case UPC represents 10 units  
**When** the receiving worker scans the delivered case  
**Then** the system identifies the packaging mismatch  
**And** records 10 actual received units  
**And** flags the discrepancy for Manager or Supervisor review  
**And** preserves the original Units Per Case and Quantity Ordered.

### US-10.4: Reconcile Ordered and Received Quantities

#### AC-10.4.1: Received quantity matches ordered quantity

**Given** a Supplier Order Line contains 60 units ordered  
**And** the cumulative Quantity Received is 60 units  
**When** the receiving worker reviews the line  
**Then** the system displays a quantity difference of zero  
**And** does not identify a quantity discrepancy.

#### AC-10.4.2: Identify shortage

**Given** a Supplier Order Line contains 60 units ordered  
**And** the cumulative Quantity Received is 48 units  
**When** the receiving worker reviews the line  
**Then** the system identifies a shortage of 12 units.

#### AC-10.4.3: Identify overage

**Given** a Supplier Order Line contains 60 units ordered  
**And** the cumulative Quantity Received is 72 units  
**When** the receiving worker reviews the line  
**Then** the system identifies an overage of 12 units.

#### AC-10.4.4: Update quantity after finding missing case

**Given** a Supplier Order Line contains 60 units ordered  
**And** the worker has scanned 48 units  
**And** a missing case containing 12 units is found  
**When** the worker scans the additional case  
**Then** the session's received quantity increases to 60 units  
**And** the system recalculates the difference to zero.

#### AC-10.4.5: Confirm actual shortage

**Given** a Supplier Order Line contains 60 units ordered  
**And** only 48 units were delivered  
**And** the Receiving Clerk has investigated and reported the shortage  
**When** an authorized Manager or Supervisor reviews and approves the discrepancy  
**Then** the system records a confirmed shortage of 12 units  
**And** preserves the original Quantity Ordered  
**And** records the approving User and approval date and time  
**And** allows the receiving session to proceed to completion.

#### AC-10.4.6: Prevent unapproved discrepancy

**Given** a Receiving Record contains a shortage of 12 units  
**And** the Receiving Clerk has reported the shortage  
**And** no authorized Manager or Supervisor has approved the discrepancy  
**When** the Receiving Clerk attempts to complete the Receiving Record  
**Then** the system rejects completion  
**And** identifies the discrepancy requiring approval  
**And** preserves the recorded received quantities  
**And** does not change the Receiving Record status to Completed.

#### AC-10.4.7: Preserve cumulative received quantity

**Given** a Supplier Order Line contains 100 units ordered  
**And** 40 units were recorded in a previous completed receiving session  
**When** another receiving session records 30 additional units  
**And** that session is completed  
**Then** the cumulative Quantity Received becomes 70 units  
**And** the original Quantity Ordered remains 100 units.

### US-10.5: Complete Receiving and Prepare for Put Away

#### AC-10.5.1: Complete receiving session

**Given** a valid Receiving Record contains scanned quantities  
**And** a valid Receiving Door has been selected  
**And** all identified discrepancies have been approved by an authorized Manager or Supervisor  
**When** the authorized receiving worker completes the session  
**Then** the system marks the Receiving Record as Completed  
**And** records the completion date and time  
**And** preserves the actual received quantities  
**And** makes the received products available for Put Away  
**And** does not automatically close the Supplier Order when additional deliveries are expected.

#### AC-10.5.2: Mark order Partially Received

**Given** a Supplier Order contains 100 units ordered  
**And** 60 units have been received in completed sessions  
**And** the Supplier Order remains open for further deliveries  
**When** the receiving session is completed  
**Then** the system sets the Supplier Order status to Partially Received  
**And** records 40 units as still outstanding.

#### AC-10.5.3: Mark order Received

**Given** all expected receiving sessions for a Supplier Order are finished  
**And** any receiving discrepancies have been approved by an authorized Manager or Supervisor  
**And** no additional deliveries are expected for the order  
**When** an authorized Manager or Supervisor closes receiving for the Supplier Order  
**Then** the system sets the Supplier Order status to Received  
**And** preserves the original ordered quantities and actual received quantities  
**And** preserves any confirmed shortages or overages  
**And** records the closing User and closing date and time.

#### AC-10.5.4: Make received products available for Put Away

**Given** a Receiving Record has been completed  
**And** its products are located at Receiving Door "DOOR-3"  
**When** a Put Away worker requests available receiving work  
**Then** the system makes the received products available for Put Away  
**And** identifies "DOOR-3" as their current location  
**And** does not mark the products as already stored in destination bins.

#### AC-10.5.5: Prevent duplicate completion

**Given** a Receiving Record has already been completed  
**When** the receiving worker attempts to complete the same record again  
**Then** the system rejects the duplicate completion  
**And** does not add the received quantities a second time.

#### AC-10.5.6: Preserve receiving history

**Given** a Receiving Record has been completed  
**When** an authorized Manager reviews the Supplier Order history  
**Then** the system displays the Receiving Record  
**And** identifies the Receiving Door, receiving worker, quantities, and confirmed discrepancies  
**And** preserves the original Supplier Order information.
