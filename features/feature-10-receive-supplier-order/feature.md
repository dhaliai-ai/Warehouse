
# Feature: Receive Supplier Order

**Feature ID:** 10  
**Feature Name:** Receive Supplier Order  
**Project:** Warehouse Management System  
**Status:** Design Draft — Clarifications Pending  
**Branch:** `design-draft`  
**Created:** 2026-09-28

**Description:** The Warehouse Management System assists receiving workers in receiving shipments from Suppliers. The worker identifies the Supplier Order using the PO Number on the bill of lading, records the receiving door, scans delivered cases or individual items, records actual received quantities, compares those quantities with the original order, investigates discrepancies, and completes receiving. Received products remain at the receiving location until they are processed through the separate Put Away workflow in Feature 11.

---

## User Stories

### US-10.1: Identify Supplier Order

**As a** Receiving Clerk  
**I want to** enter the PO Number from the bill of lading  
**So that** I can identify the correct Supplier Order and review what was ordered.

**Priority:** P1

**Independent Test:** Enter the PO Number of an existing submitted Supplier Order and verify that the correct Supplier, Items, and ordered quantities are displayed.

### US-10.2: Record Receiving Location

**As a** Receiving Clerk  
**I want to** record the Warehouse and Receiving Door where the shipment arrived  
**So that** Put Away workers can locate the received products.

**Priority:** P1

**Independent Test:** Select a valid Receiving Door and verify that it is stored with the Receiving Record.

### US-10.3: Scan Received Items

**As a** Receiving Clerk  
**I want to** scan the delivered products and record their quantities  
**So that** the system accurately records what the Supplier actually delivered.

**Priority:** P1

**Independent Test:** Scan a known Item UPC and Case UPC and verify that the appropriate quantities are recorded in individual units.

### US-10.4: Reconcile Ordered and Received Quantities

**As a** Receiving Clerk  
**I want to** compare the quantities ordered with the quantities received  
**So that** missing, extra, or incorrect products can be identified and investigated.

**Priority:** P1

**Independent Test:** Receive fewer or more units than ordered and verify that the system displays the discrepancy and allows it to be reviewed.

### US-10.5: Complete Receiving and Prepare for Put Away

**As a** Receiving Clerk  
**I want to** complete receiving after verifying the shipment  
**So that** the received products become available for Put Away without being incorrectly recorded as already stored in Warehouse bins.

**Priority:** P1

**Independent Test:** Complete a receiving session with valid scanned quantities and a Receiving Door, then verify that the received products are available for Feature 11.

---

## Functional Requirements

### Identify Supplier Order

- **FR-001:** The system MUST allow authorized Receiving Clerks and receiving workers to enter or scan a PO Number from the bill of lading.
- **FR-002:** The system MUST locate the corresponding Supplier Order using its unique PO Number.
- **FR-003:** The system MUST display the Supplier, ordered Items, and original ordered quantities for the identified Supplier Order.
- **FR-004:** The system MUST reject a PO Number that does not identify an existing Supplier Order.
- **FR-005:** The system MUST prevent receiving against Draft or Canceled Supplier Orders.
- **FR-006:** The system MUST allow receiving against Submitted or Partially Received Supplier Orders.
- **FR-007:** The system MUST preserve the original Quantity Ordered when receiving is performed.
- **FR-008:** The system MUST identify the destination Warehouse recorded on the Supplier Order and display it during receiving. The receiving worker MUST confirm that the shipment arrived at that Warehouse. If the actual receiving Warehouse differs from the Supplier Order's destination Warehouse, the system MUST flag the mismatch for authorized review and MUST NOT silently accept the change. [NEEDS CLARIFICATION: Confirm whether authorized Managers or Supervisors may approve receiving at a different Warehouse.]

### Record Receiving Location

- **FR-009:** The system MUST allow the worker to select an existing Receiving Door within that Warehouse.
- **FR-010:** The system MUST associate the selected Receiving Door with the Receiving Record.
- **FR-011:** The system MUST require a valid Receiving Door before a receiving session can be completed.

### Scan Received Items

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

### Reconcile Ordered and Received Quantities

- **FR-025:** The system MUST display the original Quantity Ordered, previously received quantity, current session quantity, and cumulative Quantity Received for each order line.
- **FR-026:** The system MUST compare cumulative Quantity Received with Quantity Ordered.
- **FR-027:** The system MUST identify shortages when cumulative Quantity Received is less than Quantity Ordered, distinguishing an open order awaiting further deliveries from a final shortage on a closed order.
- **FR-028:** The system MUST identify overages when cumulative Quantity Received is greater than Quantity Ordered.
- **FR-029:** The system MUST identify ordered Items for which no units have been received.
- **FR-030:** The system MUST allow the receiving worker to continue scanning additional Items or cases while investigating discrepancies.
- **FR-031:** The system MUST recalculate receiving differences when additional quantities are recorded.
- **FR-032:** The system MUST identify and record quantity discrepancies during receiving. Receiving workers MUST be able to report and acknowledge discrepancies, but final approval of unresolved shortages, overages, or unexpected Items MUST be performed by an authorized Manager or Supervisor before the receiving session is completed. The system MUST record the approving User, approval date and time, and discrepancy details.
- **FR-033:** The system MUST preserve the actual received quantity even when it differs from Quantity Ordered.
- **FR-034:** The system MUST record approved discrepancies for Supplier performance reporting in Feature 17.

### Complete Receiving

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

### Security and History

- **FR-049:** The system MUST restrict receiving operations to authorized receiving personnel.
- **FR-050:** The system MUST allow authorized Managers or Supervisors to review and approve receiving discrepancies.
- **FR-051:** The system MUST preserve receiving history for later Inventory reconciliation and reporting.
- **FR-052:** The system MUST reject attempts to complete a nonexistent or already completed Receiving Record.
- **FR-053:** The system MUST prevent the same Receiving Record from being completed more than once.
- **FR-054:** The system MUST keep Supplier Order creation separate from Supplier Order receiving.

---

## Assumptions

- **A-001:** Supplier Orders are created and submitted through Feature 9.
- **A-002:** Receiving is allowed only for Submitted and Partially Received Supplier Orders.
- **A-003:** The bill of lading contains the PO Number.
- **A-004:** Every Supplier Order identifies its intended destination Warehouse.
- **A-005:** The receiving Warehouse must match the destination Warehouse unless an authorized exception is approved.
- **A-006:** Each completed Receiving Record must identify a valid Receiving Door.
- **A-007:** Receiving workers use electronic devices and barcode scanners rather than paper lists.
- **A-008:** An Individual Item UPC represents one unit.
- **A-009:** A Case UPC represents its configured number of individual units.
- **A-010:** Case packaging quantities may differ from the original Units Per Case on the order.
- **A-011:** Packaging differences are flagged without changing original purchasing data.
- **A-012:** Received quantities are stored in individual units.
- **A-013:** Original ordered quantities and actual received quantities remain separate.
- **A-014:** One Supplier Order may have multiple receiving sessions.
- **A-015:** Only completed Receiving Records contribute to cumulative received quantities.
- **A-016:** Receiving workers may report discrepancies but cannot approve unresolved discrepancies.
- **A-017:** Managers and Supervisors may approve receiving discrepancies.
- **A-018:** Approvals include the approving User, timestamp, and discrepancy details.
- **A-019:** Completing a receiving session does not necessarily close the Supplier Order.
- **A-020:** Authorized personnel may close an order when no further deliveries are expected.
- **A-021:** Completed received quantities become available to Feature 11.
- **A-022:** Received products remain associated with their Receiving Door until Put Away.
- **A-023:** Receiving does not assign final storage bins.
- **A-024:** Receiving does not mark products as put away.
- **A-025:** Completed receiving history cannot be silently overwritten.
- **A-026:** Duplicate completion must be prevented.
- **A-027:** Confirmed discrepancies support Feature 17 reporting.
- **A-028:** Shared authentication services determine permissions.

---

## Edge Cases

- **EC-001:** The entered PO Number does not exist.
- **EC-002:** The Supplier Order is Draft.
- **EC-003:** The Supplier Order is Canceled.
- **EC-004:** The Supplier Order is already Received and closed.
- **EC-005:** The Supplier Order is Partially Received.
- **EC-006:** The shipment arrives at a different Warehouse.
- **EC-007:** The selected Receiving Door does not exist.
- **EC-008:** The Receiving Door belongs to another Warehouse.
- **EC-009:** The Receiving Door is inactive.
- **EC-010:** Completion is attempted without a Receiving Door.
- **EC-011:** A scanned UPC is unknown or unreadable.
- **EC-012:** A scanned Item is not on the Supplier Order.
- **EC-013:** An Individual Item UPC is scanned repeatedly.
- **EC-014:** A Case UPC is scanned repeatedly.
- **EC-015:** Case packaging differs from the original order.
- **EC-016:** A negative quantity is entered.
- **EC-017:** An ordered Item has no received units.
- **EC-018:** Received quantity is below ordered quantity.
- **EC-019:** Received quantity exceeds ordered quantity.
- **EC-020:** Additional scans resolve a shortage.
- **EC-021:** A discrepancy remains unresolved at completion.
- **EC-022:** A Receiving Clerk attempts unauthorized approval.
- **EC-023:** A shortage is approved while additional deliveries are expected.
- **EC-024:** Multiple receiving sessions are required.
- **EC-025:** A session completes while the order remains open.
- **EC-026:** A Manager closes an order with an approved shortage.
- **EC-027:** A Manager closes an order with an approved overage.
- **EC-028:** Completion is submitted twice.
- **EC-029:** Two Users attempt simultaneous completion.
- **EC-030:** A completed Receiving Record is edited.
- **EC-031:** A Receiving Record Line references a nonexistent order line.
- **EC-032:** An unauthorized Driver attempts receiving.
- **EC-033:** Feature 11 retrieves completed receiving work.
- **EC-034:** Received products are awaiting Put Away.
- **EC-035:** The Supplier Order closes before all products are put away.
- **EC-036:** Supplier discrepancy history is requested for reporting.
- **EC-037:** A database error occurs during completion.
- **EC-038:** Multiple receiving sessions for the same Supplier Order run concurrently.

---

## Success Criteria

- **SC-001:** Authorized receiving workers can find eligible Supplier Orders by PO Number.
- **SC-002:** Invalid, Draft, Canceled, and closed orders cannot begin unauthorized receiving.
- **SC-003:** Original ordered Items and quantities are displayed.
- **SC-004:** Destination Warehouse is displayed and validated.
- **SC-005:** Warehouse mismatches are flagged.
- **SC-006:** Every completed Receiving Record has a valid Receiving Door.
- **SC-007:** Individual UPC scans record correct unit quantities.
- **SC-008:** Case UPC scans correctly convert cases to individual units.
- **SC-009:** Packaging mismatches are detected.
- **SC-010:** Unknown UPCs and unexpected Items are not silently accepted.
- **SC-011:** Original ordered quantities remain unchanged.
- **SC-012:** Session and cumulative received quantities remain separate.
- **SC-013:** Shortages, overages, and missing Items are detected.
- **SC-014:** Discrepancies are recalculated after additional scans.
- **SC-015:** Unresolved discrepancies require authorized approval.
- **SC-016:** Approval details are preserved.
- **SC-017:** Multiple receiving sessions are supported.
- **SC-018:** Completed quantities update cumulative received quantities exactly once.
- **SC-019:** Supplier Orders remain Partially Received when additional deliveries are expected.
- **SC-020:** Final closure preserves confirmed differences and closing information.
- **SC-021:** Completed received products become available for Put Away.
- **SC-022:** Receiving does not assign final storage bins.
- **SC-023:** Completed records cannot be silently overwritten.
- **SC-024:** Unauthorized operations are rejected.
- **SC-025:** Receiving history is available for reconciliation and reporting.
- **SC-026:** All 31 Gherkin acceptance scenarios have corresponding verification tests.

---

## Key Entities

### Supplier Order

Represents an existing purchase order placed with a Supplier. It provides the PO Number, Supplier, destination Warehouse, original ordered Items, and ordered quantities.

### Supplier Order Line

Represents an Individual Item ordered from a Supplier. Each line maintains Quantity Ordered and cumulative Quantity Received separately.

### Receiving Record

Represents one receiving session. It identifies the Supplier Order, Warehouse, Receiving Door, receiving worker, and session status.

### Receiving Record Line

Represents an Item and the quantity received during a particular receiving session.

### Individual Item

Represents a product received from a Supplier. An Item may have UPCs for individual units and cases.

### UPC

Represents a barcode identifying an Individual Item or a case containing multiple units.

### Warehouse

Represents the Warehouse receiving the shipment. Warehouse maintenance is defined in Feature 2.

### Receiving Door

Represents a designated Warehouse location where incoming products are unloaded and await Put Away.

### Receiving Discrepancy

Represents a difference between ordered and received quantities, including its review and approval information.

### User

Represents an employee authorized to receive Supplier Orders or review discrepancies.

---

## Initial Data Model

### Supplier Order

| Attribute | Type | Description |
|---|---|---|
| supplierOrderId | Integer | Unique Supplier Order ID |
| poNumber | String | Unique PO Number |
| supplierId | Integer | Supplier reference |
| warehouseId | Integer | Destination Warehouse |
| status | String | Draft, Submitted, Partially Received, Received, Canceled |

**Relationships:**
- One Supplier Order belongs to one Supplier.
- One Supplier Order contains one or more Supplier Order Lines.
- One Supplier Order may have multiple Receiving Records.

**Constraints:**
- PO Number is unique.
- Only Submitted and Partially Received orders may begin receiving.
- Original ordered quantities must remain unchanged.

### Supplier Order Line

| Attribute | Type | Description |
|---|---|---|
| supplierOrderLineId | Integer | Unique line ID |
| supplierOrderId | Integer | Parent Supplier Order |
| itemId | Integer | Ordered Item |
| quantityOrderedCases | Integer | Original cases ordered |
| unitsPerCase | Integer | Units per case at ordering |
| quantityReceivedUnits | Integer | Cumulative received units |

**Derived Values:**

`Ordered Units = quantityOrderedCases × unitsPerCase`

`Quantity Difference = quantityReceivedUnits - Ordered Units`

`Outstanding Units = max(0, Ordered Units - quantityReceivedUnits)`

**Constraints:**
- Ordered quantities remain unchanged during receiving.
- Cumulative received quantities come from completed receiving sessions.

### Receiving Record

| Attribute | Type | Description |
|---|---|---|
| receivingRecordId | Integer | Unique receiving session ID |
| supplierOrderId | Integer | Supplier Order reference |
| warehouseId | Integer | Actual receiving Warehouse |
| receivingDoorId | Integer | Receiving Door reference |
| receivedBy | Integer | Receiving worker |
| startedAt | DateTime | Start timestamp |
| completedAt | DateTime | Completion timestamp |
| status | String | In Progress or Completed |
| discrepanciesConfirmed | Boolean | Whether required approvals exist |

**Relationships:**
- One Receiving Record belongs to one Supplier Order.
- One Receiving Record identifies one Warehouse and Receiving Door.
- One Receiving Record contains multiple Receiving Record Lines.
- Completed records provide work to Feature 11.

**Constraints:**
- Receiving Door must belong to the receiving Warehouse.
- A valid Receiving Door is required before completion.
- Warehouse mismatches require authorized review.
- Completed records cannot be completed again.

### Receiving Record Line

| Attribute | Type | Description |
|---|---|---|
| receivingRecordLineId | Integer | Unique line ID |
| receivingRecordId | Integer | Parent Receiving Record |
| supplierOrderLineId | Integer | Original ordered line |
| itemId | Integer | Received Item |
| quantityReceivedUnits | Integer | Units received this session |

**Constraints:**
- Received quantities cannot be negative.
- The Item must match the referenced order line.
- Only completed lines contribute to cumulative received quantities.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Item ID |
| itemNumber | String | Item Number |
| description | String | Item description |
| unitsPerCase | Integer | Current configured packaging |

**Owner:** Feature 4.

### UPC

| Attribute | Type | Description |
|---|---|---|
| upcId | Integer | Unique UPC ID |
| itemId | Integer | Item reference |
| upcCode | String | Barcode |
| barcodeType | String | Individual Unit or Case |
| unitsRepresented | Integer | Units represented by one scan |

**Constraints:**
- Individual UPC represents one unit.
- Case UPC represents its configured unit count.
- UPC codes uniquely identify configured Items and package types.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique Warehouse ID |
| name | String | Warehouse name |

**Owner:** Feature 2.

### Receiving Door

| Attribute | Type | Description |
|---|---|---|
| receivingDoorId | Integer | Unique Door ID |
| warehouseId | Integer | Parent Warehouse |
| doorCode | String | Door identifier |
| isActive | Boolean | Active status |

**Constraints:**
- Door code is unique within its Warehouse.
- Inactive Doors cannot be selected for new receiving sessions.

### Receiving Discrepancy

| Attribute | Type | Description |
|---|---|---|
| discrepancyId | Integer | Unique discrepancy ID |
| receivingRecordId | Integer | Receiving session |
| supplierOrderLineId | Integer | Related ordered line, if applicable |
| discrepancyType | String | Shortage, Overage, Unexpected Item, Packaging Mismatch |
| quantityDifferenceUnits | Integer | Quantity difference |
| details | String | Explanation |
| confirmedBy | Integer | Approving User |
| confirmedAt | DateTime | Approval timestamp |
| status | String | Pending or Approved |

**Constraints:**
- Approval requires an authorized Manager or Supervisor.
- Actual received quantities must be preserved.
- Approved discrepancies remain available for reporting.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User ID |
| role | String | Authorized role |

**Owner:** Shared authentication services.

---

## Gherkin AC

### US-10.1: Identify Supplier Order

#### AC-10.1.1: Identify Valid Supplier Order

**Given** a Supplier Order exists with Submitted status  
**And** the receiving worker has its PO Number from the bill of lading  
**When** the worker enters the PO Number  
**Then** the system displays the Supplier, ordered Items, and original ordered quantities.

#### AC-10.1.2: Reject Nonexistent PO Number

**Given** no Supplier Order exists for the entered PO Number  
**When** the worker searches for the order  
**Then** the system displays a not-found message  
**And** no receiving session is started.

#### AC-10.1.3: Reject Canceled Supplier Order

**Given** a Supplier Order has Canceled status  
**When** the worker attempts to begin receiving  
**Then** the system rejects the operation.

#### AC-10.1.4: Allow Partially Received Supplier Order

**Given** a Supplier Order has Partially Received status  
**And** additional quantities remain outstanding  
**When** an authorized worker starts another receiving session  
**Then** the system permits receiving  
**And** displays previously received and outstanding quantities.

### US-10.2: Record Receiving Location

#### AC-10.2.1: Record Valid Receiving Door

**Given** a Receiving Record is In Progress  
**And** an active Receiving Door exists in the receiving Warehouse  
**When** the worker selects that Door  
**Then** the Door is saved with the Receiving Record.

#### AC-10.2.2: Reject Nonexistent Receiving Door

**Given** a Receiving Door identifier does not exist  
**When** the worker attempts to select it  
**Then** the system rejects the selection.

#### AC-10.2.3: Reject Receiving Door from Another Warehouse

**Given** the receiving Warehouse is W1  
**And** a selected Door belongs to W2  
**When** the worker attempts to use that Door  
**Then** the system rejects the selection.

#### AC-10.2.3a: Identify Destination Warehouse Mismatch

**Given** a Supplier Order is destined for Warehouse W1  
**And** the shipment arrives at Warehouse W2  
**When** the worker starts receiving  
**Then** the system displays the mismatch  
**And** flags it for authorized review  
**And** does not silently change the Supplier Order destination.

#### AC-10.2.4: Require Receiving Door Before Completion

**Given** a Receiving Record has no valid Receiving Door  
**When** the worker attempts to complete receiving  
**Then** the system blocks completion.

#### AC-10.2.5: Make Receiving Door Available for Put Away

**Given** a Receiving Record has a valid Receiving Door  
**When** the record is completed  
**Then** Feature 11 can identify that Door as the location of received products awaiting Put Away.

### US-10.3: Scan Received Items

#### AC-10.3.1: Scan Individual Item UPC

**Given** an Item has an Individual UPC representing one unit  
**When** the worker scans the UPC  
**Then** the system identifies the Item  
**And** records one received unit.

#### AC-10.3.2: Scan Case UPC

**Given** an Item has a Case UPC representing 12 units  
**When** the worker scans one case  
**Then** the system identifies the Item  
**And** records 12 received units.

#### AC-10.3.2a: Flag Case Packaging Mismatch

**Given** a submitted Supplier Order Line records 12 units per case  
**And** the scanned Case UPC represents 10 units  
**When** the worker scans the Case UPC  
**Then** the system records 10 actual received units  
**And** flags the packaging difference  
**And** preserves the original order quantities.

#### AC-10.3.3: Scan Multiple Cases

**Given** a Case UPC represents 12 units  
**When** the worker scans three physical cases  
**Then** the system records 36 received units.

#### AC-10.3.4: Reject Unknown Barcode

**Given** a scanned UPC is not configured  
**When** the worker scans it  
**Then** the system displays an error  
**And** does not record an unidentified Item.

#### AC-10.3.5: Identify Unexpected Item

**Given** a scanned Item is not on the selected Supplier Order  
**When** the worker scans its UPC  
**Then** the system flags the Item as unexpected  
**And** does not silently add it to the order.

#### AC-10.3.6: Preserve Quantity Ordered

**Given** a Supplier Order Line originally ordered 100 units  
**When** the worker records 95 received units  
**Then** Quantity Ordered remains 100  
**And** Quantity Received is recorded separately.

#### AC-10.3.7: Reject Unauthorized Receiving

**Given** a User does not have receiving permission  
**When** the User attempts to record received products  
**Then** the system rejects the operation.

### US-10.4: Reconcile Ordered and Received Quantities

#### AC-10.4.1: Received Quantity Matches Ordered Quantity

**Given** an order line contains 100 ordered units  
**And** cumulative received quantity is 100 units  
**When** the system compares the quantities  
**Then** the quantity difference is zero.

#### AC-10.4.2: Identify Shortage

**Given** an order line contains 100 ordered units  
**And** cumulative received quantity is 90 units  
**When** the system compares the quantities  
**Then** the system identifies a shortage of 10 units  
**And** distinguishes whether additional deliveries are expected.

#### AC-10.4.3: Identify Overage

**Given** an order line contains 100 ordered units  
**And** cumulative received quantity is 110 units  
**When** the system compares the quantities  
**Then** the system identifies an overage of 10 units.

#### AC-10.4.4: Update Quantity After Finding Missing Case

**Given** a receiving session shows a shortage of 12 units  
**And** the worker finds and scans one additional 12-unit case  
**When** quantities are recalculated  
**Then** the shortage is resolved.

#### AC-10.4.5: Confirm Actual Shortage

**Given** a receiving session has an unresolved shortage  
**And** an authorized Supervisor has reviewed it  
**When** the Supervisor approves the discrepancy  
**Then** the actual received quantity is preserved  
**And** the Supervisor and approval timestamp are recorded.

#### AC-10.4.6: Prevent Unapproved Discrepancy

**Given** a receiving session has an unresolved discrepancy requiring approval  
**When** a Receiving Clerk attempts to complete the session  
**Then** completion is blocked until an authorized Manager or Supervisor approves it.

#### AC-10.4.7: Preserve Cumulative Received Quantity

**Given** a Supplier Order Line has 40 units previously received  
**And** a new completed receiving session contains 30 units  
**When** cumulative received quantity is updated  
**Then** cumulative Quantity Received becomes 70 units  
**And** original Quantity Ordered remains unchanged.

### US-10.5: Complete Receiving and Prepare for Put Away

#### AC-10.5.1: Complete Receiving Session

**Given** a Receiving Record has a valid Receiving Door  
**And** all required discrepancy approvals exist  
**When** the worker completes the session  
**Then** its status becomes Completed  
**And** its completion timestamp is recorded  
**And** its received quantities are confirmed exactly once.

#### AC-10.5.2: Mark Order Partially Received

**Given** an order has outstanding quantities  
**And** further deliveries are expected  
**When** a receiving session is completed  
**Then** the Supplier Order status becomes Partially Received  
**And** the order remains available for additional receiving.

#### AC-10.5.3: Mark Order Received

**Given** all ordered quantities have been received  
**Or** an authorized Manager or Supervisor confirms that no further deliveries are expected and required discrepancies are approved  
**When** receiving is finally closed  
**Then** the Supplier Order status becomes Received  
**And** actual quantities and confirmed discrepancies are preserved.

#### AC-10.5.4: Make Received Products Available for Put Away

**Given** a Receiving Record has been completed  
**When** Feature 11 requests available Put Away work  
**Then** the system provides the received Items, quantities, and Receiving Door  
**And** does not mark the products as already put away.

#### AC-10.5.5: Prevent Duplicate Completion

**Given** a Receiving Record is already Completed  
**When** a worker attempts to complete it again  
**Then** the system rejects the duplicate completion  
**And** cumulative received quantities are not increased again.

#### AC-10.5.6: Preserve Receiving History

**Given** a Receiving Record is Completed  
**When** an authorized User reviews receiving history  
**Then** the system displays the Supplier Order, received Items, quantities, Receiving Door, worker, timestamps, and confirmed discrepancies.

---

## Data Ownership

### Feature 9 — Supplier Order

Feature 9 owns:
- Supplier Order ID
- PO Number
- Supplier reference
- Destination Warehouse
- Original ordered Items
- Original ordered cases
- Original Units Per Case
- Original purchasing information

Feature 10 reads these values and does not overwrite original purchasing quantities.

Confirmed receiving information is integrated with the Supplier Order's cumulative received quantities and receiving-related status.

### Feature 10 — Receiving Record

Feature 10 owns:
- Receiving Record ID
- Supplier Order reference
- Actual receiving Warehouse
- Receiving Door
- Receiving worker
- Start timestamp
- Completion timestamp
- Receiving status
- Discrepancy confirmation state

### Feature 10 — Receiving Record Line

Feature 10 owns:
- Receiving Record Line ID
- Receiving Record reference
- Supplier Order Line reference
- Item reference
- Quantity received during the session

Only completed receiving sessions contribute confirmed quantities.

### Feature 10 — Receiving Discrepancy

Feature 10 owns:
- Discrepancy ID
- Discrepancy type
- Receiving Record reference
- Related order line
- Quantity difference
- Explanation
- Approving User
- Approval timestamp
- Approval status

Confirmed discrepancies are available to Feature 17.

### Feature 4 — Individual Item and UPC

Feature 4 owns Item and barcode master data.

Feature 10 reads UPC identity, barcode type, and units represented.

Feature 10 does not edit Item master data.

### Feature 2 — Warehouse and Receiving Door

Feature 2 owns Warehouse and Receiving Door definitions.

Feature 10 validates the selected receiving location.

### Feature 11 — Put Away

Feature 11 owns:
- Putaway Assignments
- Putaway Instructions
- Putaway Movements
- Final storage-bin placement

Feature 10 provides completed receiving work and the original Receiving Door.

### Feature 3 — Inventory

Feature 3 owns physical Inventory records.

Receiving and Put Away updates must not count the same products twice.

### Shared Authentication

Shared services own User accounts and roles.

Feature 10 records the receiving worker and discrepancy approver.

### Data Integrity Rules

- Original ordered quantities remain unchanged.
- Received quantities are nonnegative.
- Case conversions use configured UPC units.
- Receiving Doors must belong to the receiving Warehouse.
- Required discrepancy approvals must exist before completion.
- Receiving completion and cumulative updates must be atomic.
- Duplicate completion must not double-count quantities.
- Completed receiving history must be preserved.
- Receiving completion and Put Away completion remain separate.

---

## API Requirements

**Design Status:** Proposed API contracts. Final naming must follow project conventions.

### API-10.1: Find Supplier Order by PO Number

**Method:** GET  
**Endpoint:** `/api/supplier-orders/by-po/{poNumber}`

**Authorization:** Authorized receiving personnel.

**Response:** `200 OK`

**Returns:**
- Supplier Order ID
- PO Number
- Supplier
- Destination Warehouse
- Status
- Ordered Items
- Original ordered quantities
- Previously received quantities
- Outstanding quantities

**Validation:**
- Reject unknown PO Numbers.
- Allow receiving only for Submitted or Partially Received orders.
- Preserve original purchasing data.

### API-10.2: Start Receiving Session

**Method:** POST  
**Endpoint:** `/api/receiving-records`

**Authorization:** Authorized receiving personnel.

**Example Request:**

    {
      "supplierOrderId": 1001,
      "warehouseId": 1
    }

**Response:** `201 Created`

**Rules:**
- Supplier Order must be eligible.
- Validate the actual Warehouse.
- Flag Warehouse mismatches.
- Create an In Progress Receiving Record.
- Record the worker and start time.

### API-10.3: Select Receiving Door

**Method:** PATCH  
**Endpoint:** `/api/receiving-records/{receivingRecordId}/door`

**Authorization:** Authorized receiving personnel.

**Example Request:**

    {
      "receivingDoorId": 3
    }

**Response:** `200 OK`

**Rules:**
- Record must be In Progress.
- Door must exist and be active.
- Door must belong to the receiving Warehouse.
- Preserve the selected Door.

### API-10.4: Scan Received Barcode

**Method:** POST  
**Endpoint:** `/api/receiving-records/{receivingRecordId}/scans`

**Authorization:** Authorized receiving personnel.

**Example Request:**

    {
      "upcCode": "012345678905",
      "scanCount": 1
    }

**Response:** `200 OK`

**Returns:**
- Identified Item
- Barcode type
- Units represented
- Quantity recorded
- Session quantity
- Cumulative quantity preview
- Original ordered quantity
- Detected exceptions

**Rules:**
- Convert case scans into individual units.
- Reject unknown UPCs.
- Flag unexpected Items.
- Flag packaging differences.
- Preserve original ordered quantities.
- Reject scans against completed records.

### API-10.5: Get Receiving Session

**Method:** GET  
**Endpoint:** `/api/receiving-records/{receivingRecordId}`

**Authorization:** Authorized receiving personnel or Manager/Supervisor.

**Response:** `200 OK`

**Returns:**
- Receiving Record details
- Supplier Order
- Warehouse and Door
- Session status
- Received Items and quantities
- Original ordered quantities
- Previous receipts
- Cumulative quantities
- Discrepancies

### API-10.6: Review Discrepancies

**Method:** GET  
**Endpoint:** `/api/receiving-records/{receivingRecordId}/discrepancies`

**Authorization:** Authorized receiving personnel and Managers/Supervisors.

**Response:** `200 OK`

**Rules:**
- Compare ordered and cumulative quantities.
- Identify shortages, overages, and missing Items.
- Identify unexpected Items and packaging differences.
- Recalculate differences after additional scans.

### API-10.7: Approve Receiving Discrepancy

**Method:** POST  
**Endpoint:** `/api/receiving-records/{receivingRecordId}/discrepancies/{discrepancyId}/approve`

**Authorization:** Manager or Supervisor.

**Example Request:**

    {
      "notes": "Confirmed shortage after recount"
    }

**Response:** `200 OK`

**Rules:**
- Record approving User and timestamp.
- Preserve actual received quantities.
- Preserve original ordered quantities.
- Reject unauthorized approval.
- Retain discrepancies for reporting.

### API-10.8: Complete Receiving Session

**Method:** POST  
**Endpoint:** `/api/receiving-records/{receivingRecordId}/complete`

**Authorization:** Authorized receiving personnel.

**Response:** `200 OK`

**Rules:**
- Record must be In Progress.
- Valid Receiving Door is required.
- Required discrepancy approvals must exist.
- Record completion timestamp.
- Update cumulative received quantities exactly once.
- Update Supplier Order receiving status.
- Preserve Receiving Door for Put Away.
- Make completed quantities available to Feature 11.
- Do not assign final storage bins.
- Do not automatically close the order when further deliveries are expected.
- Prevent duplicate completion.

### API-10.9: Close Supplier Order Receiving

**Method:** POST  
**Endpoint:** `/api/supplier-orders/{supplierOrderId}/close-receiving`

**Authorization:** Manager or Supervisor.

**Example Request:**

    {
      "noFurtherDeliveriesExpected": true,
      "notes": "Final delivery confirmed"
    }

**Response:** `200 OK`

**Rules:**
- Confirm no further deliveries are expected.
- Require approval of unresolved discrepancies.
- Set Supplier Order status to Received.
- Preserve actual received quantities and differences.
- Record closing User and timestamp.
- Do not alter Put Away status.

### API-10.10: Get Receiving Work Awaiting Put Away

**Method:** GET  
**Endpoint:** `/api/putaway/available-receiving`

**Owner:** Feature 11, consuming Feature 10 data.

**Response:** `200 OK`

**Returns:**
- Completed Receiving Record
- Supplier Order
- Receiving Door
- Item
- Received quantity
- Quantity already put away
- Quantity remaining for Put Away

**Rules:**
- Include only confirmed receiving work.
- Preserve Receiving Door location.
- Do not treat products as already stored in final bins.
- Exclude completed Put Away quantities from remaining work.

### Shared API Requirements

- Authenticate every request.
- Enforce role-based authorization.
- Validate identifiers.
- Reject invalid quantities.
- Prevent duplicate receiving completion.
- Use database transactions for confirmed receiving updates.
- Preserve original purchasing values.
- Preserve receiving and discrepancy history.
- Follow established security and API conventions.

---

## Screen Requirements

**Design Status:** Proposed. The image paths below are planned mockups, not confirmed existing files.

### UI-10A: Supplier Order Lookup

**Proposed Image:** `docs/UI/receive-supplier-order-lookup.png`

**Purpose:** Identify a shipment using the PO Number on the bill of lading.

**Fields:**
- PO Number

**Displays:**
- Supplier
- Order status
- Destination Warehouse
- Ordered Items
- Original ordered quantities

**Actions:** Search, Start Receiving, Cancel.

**Rules:** Reject unknown PO Numbers and ineligible orders.

### UI-10B: Receiving Warehouse and Door

**Proposed Image:** `docs/UI/receive-supplier-order-door.png`

**Purpose:** Record the actual receiving location.

**Fields:**
- Destination Warehouse (read-only)
- Actual receiving Warehouse
- Receiving Door selector

**Actions:** Confirm Location, Return.

**Rules:**
- Flag Warehouse mismatches.
- Require an active Door in the correct Warehouse.
- Require a valid Door before completion.

### UI-10C: Scan Received Items

**Proposed Image:** `docs/UI/receive-supplier-order-scan.png`

**Purpose:** Record delivered products through scanning.

**Displays:**
- PO Number
- Receiving Door
- Scanned UPC
- Item Number and Description
- Barcode type
- Units represented
- Original ordered units
- Previously received units
- Current session units
- Cumulative received units
- Difference

**Actions:** Scan Item, Scan Case, Enter Quantity, Review Discrepancies, Complete Receiving.

**Rules:**
- Support Individual and Case UPCs.
- Convert cases into units.
- Flag unknown barcodes and unexpected Items.
- Flag packaging mismatches.
- Preserve original quantities.

### UI-10D: Receiving Discrepancy Review

**Proposed Image:** `docs/UI/receive-supplier-order-discrepancies.png`

**Purpose:** Investigate differences.

**Displays:**
- Item
- Ordered quantity
- Previous receipts
- Current session quantity
- Cumulative quantity
- Difference
- Discrepancy type
- Approval status
- Notes

**Actions:** Continue Scanning, Report Discrepancy, Request Approval, Approve Discrepancy, Return.

**Rules:**
- Only Managers or Supervisors may approve unresolved discrepancies.
- Record approval details.
- Block completion when approval is missing.

### UI-10E: Complete Receiving

**Proposed Image:** `docs/UI/receive-supplier-order-complete.png`

**Purpose:** Confirm completion of a Receiving Record.

**Displays:**
- PO Number
- Warehouse
- Receiving Door
- Received quantities
- Discrepancy approval status
- Receiving worker

**Actions:** Complete Session, Cancel, Return to Scanning.

**Rules:**
- Require valid Door and approvals.
- Complete only once.
- Make received quantities available to Put Away.
- Do not automatically close the order if more deliveries are expected.

### UI-10F: Supplier Order Receiving Closure

**Proposed Image:** `docs/UI/receive-supplier-order-close.png`

**Purpose:** Allow authorized final closure.

**Displays:**
- PO Number
- Ordered quantities
- Cumulative received quantities
- Outstanding quantities
- Confirmed discrepancies
- Current status

**Actions:** Confirm No Further Deliveries, Close Receiving, Cancel.

**Rules:**
- Manager or Supervisor authorization required.
- Preserve approved discrepancies.
- Record closing User and timestamp.
- Do not change Put Away status.

### UI-10G: Receiving History

**Proposed Image:** `docs/UI/receive-supplier-order-history.png`

**Purpose:** Review previous receiving sessions.

**Displays:**
- Receiving Record ID
- PO Number
- Warehouse
- Receiving Door
- Worker
- Start and completion timestamps
- Received quantities
- Confirmed discrepancies

**Actions:** Search, Filter, View Details.

**Rules:** Completed records are read-only for ordinary receiving workers.

### Role Permissions

| Role | Start Receiving | Scan Items | Complete Session | Approve Discrepancies | Close Supplier Order |
|---|---|---|---|---|---|
| Receiving Clerk | Yes | Yes | Yes | No | No |
| Authorized Receiving Worker | Yes | Yes | Yes | No | No |
| Supervisor | If authorized | If authorized | If authorized | Yes | Yes |
| Manager | If authorized | If authorized | If authorized | Yes | Yes |
| Picker | No by default | No | No | No | No |
| Driver | No | No | No | No | No |

### Proposed UI Deliverables

- `docs/UI/receive-supplier-order-lookup.png`
- `docs/UI/receive-supplier-order-door.png`
- `docs/UI/receive-supplier-order-scan.png`
- `docs/UI/receive-supplier-order-discrepancies.png`
- `docs/UI/receive-supplier-order-complete.png`
- `docs/UI/receive-supplier-order-close.png`
- `docs/UI/receive-supplier-order-history.png`

---

## Definition of Done

### Requirements and Design

- [ ] All 5 User Stories are documented.
- [ ] All 54 Functional Requirements are documented.
- [ ] Assumptions are documented.
- [ ] Edge Cases are documented.
- [ ] Success Criteria are documented.
- [ ] All 10 Key Entities are documented.
- [ ] Initial Data Model is documented.
- [ ] All 31 Gherkin acceptance scenarios are documented.
- [ ] Data Ownership is documented.
- [ ] API Requirements are documented.
- [ ] Screen Requirements are documented.
- [ ] Out of Scope is documented.
- [ ] Pending clarifications are identified.

### Receiving Workflow

- [ ] Authorized Users can identify Supplier Orders by PO Number.
- [ ] Only eligible orders can begin receiving.
- [ ] Destination Warehouse is displayed.
- [ ] Warehouse mismatches are flagged.
- [ ] Receiving Doors are validated.
- [ ] Individual UPC scans record correct units.
- [ ] Case UPC scans record correct units.
- [ ] Packaging differences are identified.
- [ ] Unknown UPCs are rejected.
- [ ] Unexpected Items are flagged.
- [ ] Original ordered quantities remain unchanged.
- [ ] Multiple receiving sessions are supported.

### Discrepancies and Completion

- [ ] Shortages are identified.
- [ ] Overages are identified.
- [ ] Missing Items are identified.
- [ ] Differences are recalculated after additional scans.
- [ ] Required approvals are enforced.
- [ ] Approver and timestamp are preserved.
- [ ] Valid Receiving Door is required.
- [ ] Completed quantities update cumulative receipts exactly once.
- [ ] Duplicate completion is prevented.
- [ ] Partial receipt and final closure remain separate.
- [ ] Receiving history is preserved.

### Put Away Integration

- [ ] Completed receiving products are available to Feature 11.
- [ ] Receiving Door is preserved.
- [ ] Received and put-away quantities remain distinct.
- [ ] Receiving does not assign final storage bins.
- [ ] Receiving does not mark products as already put away.

### Acceptance Testing

- [ ] AC-10.1.1 through AC-10.1.4 pass.
- [ ] AC-10.2.1 through AC-10.2.5, including AC-10.2.3a, pass.
- [ ] AC-10.3.1 through AC-10.3.7, including AC-10.3.2a, pass.
- [ ] AC-10.4.1 through AC-10.4.7 pass.
- [ ] AC-10.5.1 through AC-10.5.6 pass.
- [ ] Tests cover authorization.
- [ ] Tests cover barcode conversion.
- [ ] Tests cover discrepancies.
- [ ] Tests cover partial receiving and closure.
- [ ] Tests cover duplicate completion.
- [ ] Tests cover Put Away integration.

### Documentation and Review

- [ ] Feature follows OC Speckit section order.
- [ ] Architecture diagrams reflect receiving data flows.
- [ ] Design decisions are documented in `docs/ADRs/`.
- [ ] Non-functional requirements are addressed in `docs/NFR/`.
- [ ] UI mockups are created.
- [ ] UI paths match actual repository files.
- [ ] Changes are committed to `design-draft`.
- [ ] Changes are pushed to GitHub.

**Draft Note:** Unchecked items do not mean implementation, testing, or UI mockups have already been completed.

---

## Out of Scope

Feature 10 does not include:

- Creating or submitting Supplier Orders (Feature 9).
- Maintaining Supplier master data (Feature 5).
- Maintaining Individual Item or UPC master data (Feature 4).
- Maintaining Warehouse master data (Feature 2).
- Changing original submitted purchasing quantities.
- Changing submitted Supplier purchase prices.
- Automatically accepting Warehouse mismatches without approval.
- Allowing unauthorized discrepancy approval.
- Assigning received products to final storage bins.
- Physically performing Put Away (Feature 11).
- Marking received products as already put away.
- Picking Customer Orders.
- Shipping or delivering products.
- Maintaining Customer Orders.
- Implementing Supplier performance reporting (Feature 17).
- Maintaining User accounts or roles.
- Deleting or silently overwriting completed receiving history.

### Pending Clarifications

- **CL-10.1:** May a Manager or Supervisor approve receiving at a Warehouse different from the Supplier Order destination?
- **CL-10.2:** If a mismatch is approved, should the original destination remain unchanged while the actual receiving Warehouse is recorded separately?
- **CL-10.3:** How should unexpected Items be physically held while approval is pending?
- **CL-10.4:** May a Supervisor correct a completed Receiving Record through an audited adjustment process?
- **CL-10.5:** What Inventory staging update occurs at receiving completion versus Put Away completion?
- **CL-10.6:** How should concurrent receiving sessions for the same Supplier Order be controlled?
- **CL-10.7:** How should approved overages be handled when they exceed the original ordered quantity?

These decisions require stakeholder approval before implementation rules are finalized.
