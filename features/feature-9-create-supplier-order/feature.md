
# Feature: Create Supplier Order

**Feature ID:** 9  
**Feature Name:** Create Supplier Order  
**Status:** Design Draft — Clarifications Pending  
**Project:** Warehouse Management System  
**Branch:** `design-draft`  
**Created:** 2026-09-28

**Description:** The Warehouse Management System assists purchasing personnel in creating Supplier Orders by identifying Items requiring replenishment, calculating quantities using minimum and maximum stock levels, accounting for inventory already on order, selecting Suppliers, and recording purchase orders for later receiving.

---

## User Stories

### US-9.1: Identify Items Needing Replenishment

**As a** Purchasing Clerk or Manager  
**I want to** identify Items whose calculated Quantity on Hand is below their minimum stock level  
**So that** the company can replenish products before shortages affect customer orders.

**Priority:** P1

**Independent Test:** Configure an Item's inventory and outstanding order quantities below its minimum stock level and verify that it appears on the replenishment list.

### US-9.2: Determine Quantity to Order

**As a** Purchasing Clerk or Manager  
**I want to** calculate the quantity required to replenish an Item toward its maximum stock level  
**So that** the company orders enough products without ignoring quantities already on order.

**Priority:** P1

**Independent Test:** Provide inventory, outstanding order quantity, minimum stock, and maximum stock; verify the recommended replenishment quantity.

### US-9.3: Create Supplier Order

**As a** Purchasing Clerk or Manager  
**I want to** create a Supplier Order containing a Supplier, ordered Items, and quantities  
**So that** the Supplier can fulfill the order and receivers can identify it when products arrive.

**Priority:** P1

**Independent Test:** Create an order with a valid Supplier and order lines and verify that its unique PO Number, quantities, and status are saved.

### US-9.4: Review and Submit Supplier Order

**As a** Purchasing Clerk or Manager  
**I want to** review and submit a prepared Supplier Order  
**So that** only valid purchasing information is recorded as an outstanding order.

**Priority:** P1

**Independent Test:** Submit a valid Draft order and verify that its status changes and outstanding quantity is included in replenishment calculations.

### US-9.5: Retrieve Supplier Order for Receiving

**As a** Receiving Clerk or Warehouse Receiver  
**I want to** find a submitted Supplier Order using its PO Number  
**So that** I can compare delivered products with the quantities originally ordered.

**Priority:** P1

**Independent Test:** Search for a submitted PO Number and verify that the Supplier, ordered Items, and original quantities are displayed without allowing receiving personnel to change them.

---

## Functional Requirements

### Replenishment Calculations

- **FR-001:** The system MUST maintain minimum and maximum stock levels for Individual Items as defined in Feature 4.
- **FR-002:** The system MUST calculate physical Inventory Quantity in individual units by summing recorded inventory balances for the Item across all eligible bins/locations within the selected Warehouse; the same physical units MUST NOT be counted more than once.
- **FR-003:** The system MUST calculate Quantity Already on Order in individual units as the sum, for the Item and selected Warehouse, of `max(0, quantityOrderedCases × unitsPerCase - quantityReceivedUnits)` across eligible Supplier Order Lines; already received units MUST NOT remain outstanding.
- **FR-004:** The system MUST use the formula **Calculated Quantity on Hand = Physical Inventory Quantity + Quantity Already on Order**. This planning value is distinct from physical stock available for picking.
- **FR-005:** The system MUST identify an Item as needing replenishment when Calculated Quantity on Hand is below its Minimum Stock Level.
- **FR-006:** The system MUST NOT identify an Item as below minimum when Calculated Quantity on Hand equals or exceeds its Minimum Stock Level.
- **FR-007:** When Calculated Quantity on Hand is below Minimum Stock Level, the system MUST calculate **Reorder Quantity (units) = max(0, Maximum Stock Level - Calculated Quantity on Hand)**. Otherwise, the recommendation MUST be zero.
- **FR-008:** The system MUST prevent negative recommended replenishment quantities.
- **FR-009:** The system MUST include outstanding quantities only from Supplier Orders in Submitted or Partially Received status. Separate Approved or Sent statuses require clarification.
- **FR-010:** The system MUST exclude Draft, Received, and Canceled Supplier Orders from Quantity Already on Order.
- **FR-011:** The system MUST avoid counting quantities already received as still outstanding.
- **FR-012:** The system MUST flag missing, negative, non-integer, or inconsistent stock thresholds and exclude those Items from automatic recommendations until corrected. Zero thresholds are valid when minimum does not exceed maximum.

### Supplier Order Creation

- **FR-013:** The system MUST allow authorized Purchasing Clerks and Managers to create Supplier Orders.
- **FR-014:** Each Supplier Order MUST be associated with one existing active Supplier.
- **FR-015:** Each Supplier Order MUST have a unique, system-generated PO Number.
- **FR-016:** Each Supplier Order MUST record its creation date and creating User.
- **FR-017:** Each Supplier Order MUST contain one or more Supplier Order Lines before submission.
- **FR-018:** Each Supplier Order Line MUST identify an existing Individual Item.
- **FR-019:** Each Supplier Order Line MUST maintain Quantity Ordered separately from Quantity Received.
- **FR-020:** The system MUST record Quantity Ordered in cases and preserve the Units Per Case used for the order line.
- **FR-021:** The system MUST calculate the corresponding ordered quantity in individual units.
- **FR-022:** Quantity Ordered MUST be a positive whole number of cases.
- **FR-023:** Authorized purchasing personnel MUST be able to review and adjust recommended quantities before submission.
- **FR-024:** The system MUST prevent the same Individual Item from appearing more than once on a Supplier Order.
- **FR-025:** The system MUST verify that every ordered Item is associated with the selected Supplier.
- **FR-026:** Items without an eligible active Supplier MUST be flagged for manual purchasing review; the system MUST NOT assign an arbitrary Supplier.
- **FR-027:** The system MUST prevent submission of an Item that is not supplied by the selected Supplier.
- **FR-028:** The system MUST support Supplier-specific purchasing prices.
- **FR-029:** The system MUST preserve the purchase price used when the order is submitted.
- **FR-030:** The system MUST support creating Supplier Orders from active Supplier Order Forms maintained in Feature 7.
- **FR-031:** The system MUST also allow orders to be created without a Supplier Order Form.

### Status and Submission

- **FR-032:** Supplier Order statuses MUST include Draft, Submitted, Partially Received, Received, and Canceled. Additional Approved or Sent statuses remain subject to clarification.
- **FR-033:** Newly created Supplier Orders MUST begin in Draft status.
- **FR-034:** Authorized purchasing personnel MUST be able to submit valid Draft orders.
- **FR-035:** The system MUST reject submission without a Supplier or at least one valid order line.
- **FR-036:** Unauthorized Users MUST NOT create or submit Supplier Orders.
- **FR-037:** Submitted order details MUST be preserved for receiving and reconciliation.
- **FR-038:** Draft orders MAY be edited by authorized purchasing personnel. After submission, original quantities and purchasing prices MUST be protected from ordinary edits. Authorized corrections require an auditable process.

### Receiving and History

- **FR-039:** Submitted and Partially Received orders MUST be retrievable by PO Number.
- **FR-040:** Authorized receiving personnel MUST be able to view Supplier Order details without changing original ordered quantities.
- **FR-041:** The system MUST maintain cumulative Quantity Received separately for every Supplier Order Line.
- **FR-042:** Receiving updates and discrepancies MUST be handled through Feature 10.
- **FR-043:** Supplier Orders and their lines MUST be preserved for purchasing and receiving history.
- **FR-044:** The system MUST maintain relationships among Supplier Orders, Suppliers, Individual Items, Supplier Order Forms, and Users.
- **FR-045:** Supplier Orders MUST be recorded even when electronic transmission to the Supplier occurs outside the system.
- **FR-046:** Canceled orders MUST NOT contribute outstanding inventory on order.
- **FR-047:** The system MUST reject attempts to retrieve or modify nonexistent Supplier Orders.

### Additional Validation and Integrity

- **FR-048:** Minimum and Maximum Stock Levels MUST be evaluated for an Item within a selected Warehouse, aggregating eligible bins without including other Warehouses. Per-Warehouse threshold policy requires confirmation.
- **FR-049:** Outstanding Supplier Order Lines MUST be associated with the receiving Warehouse so orders intended for other Warehouses are excluded.
- **FR-050:** The system MUST distinguish recommended individual units from orderable cases. Recommended cases MUST be rounded upward, and any excess units MUST be displayed for authorized review. The rounding policy requires approval.
- **FR-051:** Negative physical Inventory Quantity MUST be flagged for reconciliation rather than silently treated as zero. Zero inventory is valid.
- **FR-052:** Submission MUST be blocked when the Supplier is missing or inactive, Supplier Item relationships are invalid, or quantities and Units Per Case are invalid.
- **FR-053:** The system MUST generate persistent unique `supplierOrderId` and `supplierOrderLineId` identifiers independently of the PO Number; identifiers MUST NOT be reused.
- **FR-054:** The system MUST record `updatedAt`, `updatedBy`, and audit history for creation, edits, submission, amendments, cancellation, and receiving-related status changes.
- **FR-055:** Items with invalid stock thresholds or no eligible Supplier MUST appear in a purchasing exception list rather than being silently omitted.
- **FR-056:** Quantity Already on Order MUST include only unreceived portions of eligible order lines. Over-receipt MUST NOT produce negative outstanding quantities.

**Requirement count:** 56 recovered requirements. Earlier design notes reference FR-057–FR-060, but their original text was not available for verification.

---

## Assumptions

- **A-001:** Supplier Orders are created for one destination Warehouse.
- **A-002:** Purchasing Clerks and Managers can create, review, and submit orders.
- **A-003:** Receiving personnel have read-only access to original purchasing details.
- **A-004:** Feature 4 maintains Item master data and stock thresholds.
- **A-005:** Feature 3 maintains physical Inventory.
- **A-006:** Feature 5 maintains Suppliers.
- **A-007:** Feature 7 maintains optional Supplier Order Forms.
- **A-008:** Feature 10 handles receiving and discrepancies.
- **A-009:** Inventory quantities are calculated in individual units.
- **A-010:** Physical Inventory is counted only once.
- **A-011:** Submitted and Partially Received orders contribute outstanding quantities.
- **A-012:** Draft, Received, and Canceled orders do not contribute outstanding quantities.
- **A-013:** Calculated Quantity on Hand is a planning value, not available picking stock.
- **A-014:** Replenishment is triggered only below minimum stock.
- **A-015:** Invalid stock thresholds prevent automatic recommendations.
- **A-016:** Purchasing quantities are recorded as whole cases.
- **A-017:** Case quantities are converted to individual units for calculations.
- **A-018:** Recommended cases are rounded upward, subject to approval.
- **A-019:** Every Supplier Order references a Supplier and Warehouse.
- **A-020:** Submitted orders contain at least one valid line.
- **A-021:** Each line references an Item supplied by the selected Supplier.
- **A-022:** Submitted Units Per Case and purchase prices are preserved.
- **A-023:** Ordered and received quantities are separate.
- **A-024:** Submitted purchasing details are protected from ordinary edits.
- **A-025:** Authorized amendments and cancellations are audited.
- **A-026:** Creation information is preserved.
- **A-027:** Electronic Supplier transmission is optional.
- **A-028:** Order history is retained after receipt or cancellation.
- **A-029:** Per-Warehouse stock threshold policy requires confirmation.
- **A-030:** Final approval, amendment, over-receipt, and status rules require stakeholder confirmation.

---

## Edge Cases

- **EC-001:** Minimum or Maximum Stock Level is missing.
- **EC-002:** Stock thresholds are negative or non-integer.
- **EC-003:** Minimum Stock Level exceeds Maximum Stock Level.
- **EC-004:** Both stock thresholds are zero.
- **EC-005:** Calculated Quantity on Hand equals minimum.
- **EC-006:** Calculated Quantity on Hand exceeds maximum.
- **EC-007:** An Item exists in multiple bins within one Warehouse.
- **EC-008:** An Item exists in multiple Warehouses.
- **EC-009:** A Draft order contains outstanding-looking quantities.
- **EC-010:** A Canceled order contains ordered quantities.
- **EC-011:** A Submitted order is partially received.
- **EC-012:** Different order lines have different outstanding quantities.
- **EC-013:** Received units exceed ordered units.
- **EC-014:** Recommended units are not divisible by Units Per Case.
- **EC-015:** Case rounding creates excess units.
- **EC-016:** Units Per Case is invalid.
- **EC-017:** An Item has no Supplier.
- **EC-018:** An Item's Supplier is inactive.
- **EC-019:** The selected Supplier does not provide an Item.
- **EC-020:** The selected Supplier does not exist.
- **EC-021:** An inactive Supplier is used at submission.
- **EC-022:** Submission is attempted with no lines.
- **EC-023:** Ordered cases are zero, negative, or fractional.
- **EC-024:** An Item is added twice.
- **EC-025:** An unauthorized User attempts purchasing.
- **EC-026:** Ordinary editing is attempted after submission.
- **EC-027:** Amendment is attempted after partial receipt.
- **EC-028:** Master-data Units Per Case changes after submission.
- **EC-029:** Supplier purchasing price changes after submission.
- **EC-030:** A nonexistent order is modified.
- **EC-031:** Receiving searches for an unknown PO Number.
- **EC-032:** Receiving retrieves a Partially Received order.
- **EC-033:** Two Users generate orders simultaneously.
- **EC-034:** Cancellation occurs during outstanding-quantity calculation.
- **EC-035:** Receiving updates occur during replenishment calculation.
- **EC-036:** A Supplier becomes inactive during submission.
- **EC-037:** A Supplier Order Form becomes inactive.
- **EC-038:** Order transmission occurs outside the system.
- **EC-039:** An audit record cannot be saved.
- **EC-040:** A Warehouse has zero physical Inventory but outstanding Supplier Orders.

---

## Success Criteria

- **SC-001:** Authorized Users can identify Items requiring replenishment.
- **SC-002:** Physical Inventory is aggregated without double counting.
- **SC-003:** Other Warehouses' Inventory is excluded.
- **SC-004:** Only eligible outstanding orders are counted.
- **SC-005:** Calculated Quantity on Hand uses the required formula.
- **SC-006:** Items at or above minimum are not flagged.
- **SC-007:** Reorder quantities use maximum minus calculated stock.
- **SC-008:** Negative recommendations are prevented.
- **SC-009:** Invalid thresholds produce exceptions.
- **SC-010:** Units and cases are converted correctly.
- **SC-011:** Case-rounding excess is displayed.
- **SC-012:** Items without eligible Suppliers are flagged.
- **SC-013:** Supplier Orders receive unique IDs and PO Numbers.
- **SC-014:** Supplier and Warehouse references are valid.
- **SC-015:** Submitted orders contain valid lines.
- **SC-016:** Duplicate Items are rejected.
- **SC-017:** Line IDs and quantities are valid.
- **SC-018:** Supplier Item relationships are verified.
- **SC-019:** Supplier-specific prices are supported.
- **SC-020:** Submitted prices and Units Per Case are preserved.
- **SC-021:** Ordered and received quantities remain separate.
- **SC-022:** New orders begin as Draft.
- **SC-023:** Authorized Users can submit valid Draft orders.
- **SC-024:** Submitted and Partially Received orders are retrievable by PO Number.
- **SC-025:** Receiving cannot overwrite original purchasing data.
- **SC-026:** Feature 10 updates confirmed receiving information.
- **SC-027:** Canceled orders are excluded while history is retained.
- **SC-028:** Creation and audit information are preserved.
- **SC-029:** Invalid or unauthorized operations do not corrupt data.
- **SC-030:** All 34 recovered Gherkin scenarios are covered by tests; the earlier reference to 37 scenarios remains unverified.

---

## Key Entities

### Supplier Order

Represents a purchase order placed with a Supplier. It includes a unique PO Number, Supplier, destination Warehouse, status, creation details, and order lines.

### Supplier Order Line

Represents an Item being purchased. It stores ordered cases, Units Per Case, purchase price, and cumulative received units.

### Individual Item

Represents a product requiring replenishment. Feature 4 maintains its stock thresholds and packaging information.

### Inventory

Represents physical quantities of an Item in Warehouse Locations. Feature 3 maintains these balances.

### Supplier

Represents a business supplying products to the Warehouse. Feature 5 maintains Supplier information.

### Supplier Item

Represents the relationship between a Supplier and an Item, including supplier-specific purchasing information.

### Supplier Order Form

Represents an optional reusable template maintained through Feature 7.

### User

Represents an employee authorized to create, submit, review, or retrieve Supplier Orders.

### Supplier Order Audit Event

Records significant purchasing actions, acting Users, timestamps, and before-and-after values.

### Warehouse

Represents the destination for ordered products and the scope for inventory and replenishment calculations.

---

## Initial Data Model

### Supplier Order

| Attribute | Type | Description |
|---|---|---|
| supplierOrderId | Integer | Unique internal identifier |
| poNumber | String | Unique purchasing reference |
| supplierId | Integer | Supplier reference |
| warehouseId | Integer | Destination Warehouse reference |
| sourceFormId | Integer | Optional Supplier Order Form |
| createdAt | DateTime | Creation timestamp |
| submittedAt | DateTime | Submission timestamp |
| createdBy | Integer | Creating User |
| updatedAt | DateTime | Last update timestamp |
| updatedBy | Integer | Last modifying User |
| status | String | Draft, Submitted, Partially Received, Received, Canceled |

**Relationships:**
- One Supplier Order belongs to one Supplier.
- One Supplier Order belongs to one destination Warehouse.
- One Supplier Order has many Supplier Order Lines.
- One Supplier Order may reference one Supplier Order Form.
- One Supplier Order is created by one User.
- One Supplier Order has many Audit Events.

**Constraints:**
- Internal ID and PO Number must be unique.
- Supplier must exist and be active at submission.
- At least one valid line is required for submission.
- Submitted purchasing details are protected.

### Supplier Order Line

| Attribute | Type | Description |
|---|---|---|
| supplierOrderLineId | Integer | Unique line identifier |
| supplierOrderId | Integer | Parent order |
| itemId | Integer | Ordered Item |
| quantityOrderedCases | Integer | Ordered whole cases |
| unitsPerCase | Integer | Units per case at ordering |
| quantityReceivedUnits | Integer | Cumulative received units |
| purchasePricePerCase | Decimal | Recorded purchasing price |

**Relationships:**
- Each line belongs to one Supplier Order.
- Each line references one Individual Item.
- Each line corresponds to a Supplier Item relationship.
- Feature 10 references lines during receiving.

**Constraints:**
- Ordered cases must be positive integers.
- Units Per Case must be positive.
- Received units must not be negative.
- Item cannot be duplicated within one order.
- Submitted purchasing values are preserved.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Item identifier |
| itemNumber | String | Item Number |
| description | String | Product description |
| minimumStockLevel | Integer | Minimum stock threshold |
| maximumStockLevel | Integer | Maximum stock threshold |
| unitsPerCase | Integer | Current packaging quantity |

**Owner:** Feature 4.

**Clarification:** Whether stock thresholds are global or Warehouse-specific must be confirmed.

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Inventory record identifier |
| itemId | Integer | Item reference |
| locationId | Integer | Warehouse Location reference |
| quantity | Integer | Physical quantity in units |

**Owner:** Feature 3.

### Supplier

| Attribute | Type | Description |
|---|---|---|
| supplierId | Integer | Unique Supplier identifier |
| name | String | Supplier name |
| active | Boolean | Supplier active status |

**Owner:** Feature 5.

### Supplier Item

| Attribute | Type | Description |
|---|---|---|
| supplierId | Integer | Supplier reference |
| itemId | Integer | Item reference |
| purchasePricePerCase | Decimal | Supplier-specific price |

**Owner:** Supplier/Item master-data integration.

### Supplier Order Form

| Attribute | Type | Description |
|---|---|---|
| supplierOrderFormId | Integer | Unique form identifier |
| supplierId | Integer | Associated Supplier |
| active | Boolean | Whether form may be used |

**Owner:** Feature 7.

### Supplier Order Audit Event

| Attribute | Type | Description |
|---|---|---|
| auditEventId | Integer | Unique event ID |
| supplierOrderId | Integer | Order reference |
| action | String | Action performed |
| actorUserId | Integer | Acting User |
| occurredAt | DateTime | Event timestamp |
| previousValues | Text/JSON | Previous values |
| newValues | Text/JSON | Updated values |

**Owner:** Feature 9.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique Warehouse identifier |
| warehouseName | String | Warehouse name |

**Owner:** Feature 2.

### Derived Quantities

These are calculated rather than independently maintained purchasing balances:

- **Ordered Units** = Quantity Ordered Cases × Units Per Case.
- **Outstanding Units** = max(0, Ordered Units − Quantity Received Units).
- **Physical Inventory Quantity** = Sum of eligible Inventory balances for the Item in the selected Warehouse.
- **Quantity Already on Order** = Sum of outstanding units on eligible Supplier Orders.
- **Calculated Quantity on Hand** = Physical Inventory Quantity + Quantity Already on Order.
- **Reorder Quantity** = max(0, Maximum Stock Level − Calculated Quantity on Hand), only when below Minimum Stock Level.
- **Recommended Cases** = ceiling(Reorder Quantity / Units Per Case).

---

## Gherkin AC

### US-9.1: Identify Items Needing Replenishment

#### AC-9.1.1: Calculate Quantity on Hand

**Given** an Individual Item has 40 units in Inventory  
**And** 20 units remain outstanding on submitted Supplier Orders  
**When** the system calculates Quantity on Hand  
**Then** Calculated Quantity on Hand is 60 units.

#### AC-9.1.2: Identify Item Below Minimum

**Given** an Item has a Minimum Stock Level of 50 units  
**And** Calculated Quantity on Hand is 35 units  
**When** the system evaluates replenishment  
**Then** the Item is identified as requiring replenishment.

#### AC-9.1.3: Do Not Replenish Item at Minimum

**Given** an Item has a Minimum Stock Level of 50 units  
**And** Calculated Quantity on Hand is 50 units  
**When** the system evaluates replenishment  
**Then** the Item is not identified as below minimum.

#### AC-9.1.4: Exclude Canceled Orders

**Given** an Item has 25 units in Inventory  
**And** a Canceled Supplier Order contains 20 units  
**When** Quantity on Hand is calculated  
**Then** the canceled order contributes zero outstanding units  
**And** Calculated Quantity on Hand is 25 units.

#### AC-9.1.5: Exclude Draft Orders

**Given** an Item has 30 units in Inventory  
**And** a Draft Supplier Order contains 15 units  
**When** Quantity on Hand is calculated  
**Then** the Draft order contributes zero outstanding units  
**And** Calculated Quantity on Hand is 30 units.

#### AC-9.1.6: Aggregate Multiple Bins in One Warehouse

**Given** Item A has 10 units in Bin 1 and 15 units in Bin 2 of Warehouse W1  
**And** Item A has 30 units in Warehouse W2  
**And** 5 units are outstanding on an eligible Supplier Order destined for W1  
**When** replenishment is calculated for W1  
**Then** Physical Inventory Quantity is 25 units  
**And** Calculated Quantity on Hand is 30 units  
**And** inventory in W2 is excluded.

#### AC-9.1.7: Reject Negative Inventory Balance

**Given** an Item has a recorded physical inventory balance of -2 units  
**When** the system evaluates replenishment  
**Then** the Item is flagged for inventory reconciliation  
**And** no automatic order is generated.

### US-9.2: Determine Quantity to Order

#### AC-9.2.1: Calculate Replenishment Quantity

**Given** an Item has Minimum Stock Level 50  
**And** Maximum Stock Level 100  
**And** Calculated Quantity on Hand is 30  
**When** replenishment is calculated  
**Then** the recommended quantity is 70 units.

#### AC-9.2.2: Include Outstanding Orders

**Given** an Item has 25 physical units  
**And** 15 units remain outstanding  
**And** Minimum Stock Level is 50  
**And** Maximum Stock Level is 100  
**When** replenishment is calculated  
**Then** Calculated Quantity on Hand is 40  
**And** recommended replenishment is 60 units.

#### AC-9.2.3: Do Not Order Above Minimum

**Given** an Item has Minimum Stock Level 50  
**And** Calculated Quantity on Hand is 65  
**When** replenishment is evaluated  
**Then** the recommended quantity is zero.

#### AC-9.2.4: Reject Invalid Stock Thresholds

**Given** an Item has Minimum Stock Level 100  
**And** Maximum Stock Level 50  
**When** replenishment is calculated  
**Then** the Item is flagged for correction  
**And** no automatic recommendation is generated.

#### AC-9.2.5: Convert Recommended Units to Cases

**Given** an Item requires 60 additional units  
**And** Units Per Case is 12  
**When** recommended cases are calculated  
**Then** the system recommends 5 cases.

#### AC-9.2.6: Round Up Incomplete Cases

**Given** an Item requires 65 additional units  
**And** Units Per Case is 12  
**When** recommended cases are calculated  
**Then** the system recommends 6 cases  
**And** displays 72 resulting units  
**And** identifies 7 excess units for review.

#### AC-9.2.7: Exclude Already Received Quantities

**Given** a Supplier Order Line originally ordered 100 units  
**And** 40 units have already been received  
**When** outstanding quantity is calculated  
**Then** only 60 units remain outstanding.

#### AC-9.2.8: Exclude Orders for Another Warehouse

**Given** an Item has outstanding orders for W1 and W2  
**When** replenishment is calculated for W1  
**Then** only orders destined for W1 contribute to Quantity Already on Order.

#### AC-9.2.9: Prevent Negative Outstanding Quantity

**Given** an order line has 100 ordered units  
**And** 105 units are recorded as received  
**When** outstanding quantity is calculated  
**Then** the outstanding quantity is zero  
**And** the over-receipt remains available for discrepancy handling.

#### AC-9.2.10: Flag Item Without Eligible Supplier

**Given** an Item requires replenishment  
**And** no active Supplier provides the Item  
**When** purchasing recommendations are displayed  
**Then** the Item appears in the exception list  
**And** no Supplier is automatically assigned.

### US-9.3: Create Supplier Order

#### AC-9.3.1: Create Draft Supplier Order

**Given** a Purchasing Clerk is authorized  
**And** a valid Supplier and Warehouse are selected  
**When** the Clerk creates a Supplier Order  
**Then** a unique Supplier Order ID and PO Number are generated  
**And** the order begins in Draft status.

#### AC-9.3.2: Record Order Line

**Given** a valid Draft Supplier Order exists  
**And** an Item is supplied by the selected Supplier  
**When** the Clerk adds the Item with a positive whole-case quantity  
**Then** a Supplier Order Line is created  
**And** ordered cases and Units Per Case are recorded.

#### AC-9.3.3: Reject Invalid Quantity

**Given** a Draft Supplier Order exists  
**When** the Clerk enters zero, negative, or fractional ordered cases  
**Then** the system rejects the quantity.

#### AC-9.3.4: Prevent Duplicate Item

**Given** an Item already appears on a Supplier Order  
**When** the Clerk attempts to add the same Item again  
**Then** the duplicate line is rejected.

#### AC-9.3.5: Reject Item Not Supplied by Supplier

**Given** a Supplier Order uses Supplier A  
**And** Item B is not supplied by Supplier A  
**When** Item B is added  
**Then** the system rejects the line.

#### AC-9.3.6: Use Supplier Order Form

**Given** an active Supplier Order Form exists  
**When** an authorized Clerk selects the form  
**Then** the system uses it to prepare a Draft Supplier Order.

#### AC-9.3.7: Create Without Supplier Order Form

**Given** an authorized Clerk is creating an order  
**When** no Supplier Order Form is selected  
**Then** the Clerk can create the Draft order manually.

#### AC-9.3.8: Record Creation Information

**Given** an authorized Clerk creates a Supplier Order  
**When** the order is saved  
**Then** the creating User and creation timestamp are recorded.

#### AC-9.3.9: Reject Unauthorized Creation

**Given** a Driver does not have purchasing permissions  
**When** the Driver attempts to create a Supplier Order  
**Then** the operation is denied.

### US-9.4: Review and Submit Supplier Order

#### AC-9.4.1: Submit Valid Draft

**Given** a Draft Supplier Order has an active Supplier  
**And** at least one valid line  
**When** an authorized Purchasing Clerk submits it  
**Then** the status changes to Submitted  
**And** the submission timestamp is recorded.

#### AC-9.4.2: Reject Empty Order

**Given** a Draft Supplier Order contains no lines  
**When** submission is requested  
**Then** the system rejects submission.

#### AC-9.4.3: Reject Inactive Supplier

**Given** a Draft Supplier Order references an inactive Supplier  
**When** submission is requested  
**Then** submission is rejected.

#### AC-9.4.4: Preserve Submitted Quantities

**Given** a Supplier Order has been submitted  
**When** an ordinary edit attempts to change Quantity Ordered  
**Then** the edit is rejected  
**And** the original ordered quantity remains unchanged.

#### AC-9.4.5: Preserve Submitted Purchase Price

**Given** a Supplier Order has been submitted  
**When** the Supplier's current purchasing price changes  
**Then** the submitted order retains its original purchase price.

#### AC-9.4.6: Include Submitted Order in Outstanding Quantity

**Given** a valid Supplier Order is submitted  
**When** replenishment is recalculated  
**Then** its unreceived quantities contribute to Quantity Already on Order.

#### AC-9.4.7: Cancel Order Without Deleting History

**Given** a Supplier Order is eligible for cancellation  
**When** an authorized User cancels it  
**Then** its status becomes Canceled  
**And** its history is preserved  
**And** its remaining quantities no longer contribute to Quantity Already on Order.

#### AC-9.4.8: Record Purchasing Audit Event

**Given** an authorized User submits or changes a Supplier Order  
**When** the action succeeds  
**Then** the system records the User, timestamp, action, and relevant changes.

### US-9.5: Retrieve Supplier Order for Receiving

#### AC-9.5.1: Retrieve Submitted Order by PO Number

**Given** a Supplier Order has Submitted status  
**When** an authorized Receiving Clerk enters its PO Number  
**Then** the system displays the Supplier, destination Warehouse, ordered Items, and original ordered quantities.

#### AC-9.5.2: Retrieve Partially Received Order

**Given** a Supplier Order is Partially Received  
**When** an authorized Receiver searches its PO Number  
**Then** the order is displayed  
**And** original ordered quantities and cumulative received quantities remain separate.

#### AC-9.5.3: Reject Unknown PO Number

**Given** a PO Number does not exist  
**When** a Receiver searches for it  
**Then** the system displays a not-found message  
**And** no Supplier Order is modified.

**Acceptance Criteria Note:** This consolidated draft contains 37 numbered scenario entries above. The earlier recovered source was reported as containing 34 scenarios, so the three additional scenario wordings must be checked against the original requirements before being treated as professor-approved acceptance criteria.

---

## Data Ownership

### Feature 9 — Supplier Order and Supplier Order Line

Feature 9 owns:
- Supplier Order ID and PO Number
- Supplier and destination Warehouse references
- Optional Supplier Order Form reference
- Creation and submission details
- Order status
- Supplier Order Lines
- Original ordered cases and Units Per Case
- Submitted purchasing prices
- Purchasing audit history

Original submitted purchasing values cannot be silently overwritten.

### Feature 3 — Inventory

Feature 9 reads physical Inventory balances for replenishment. It does not change physical Inventory when creating an order.

### Feature 4 — Individual Item

Feature 9 reads Item identity, stock thresholds, Units Per Case, and relevant Supplier Item relationships.

Submitted order lines preserve the purchasing values used at submission.

### Feature 5 — Supplier

Feature 9 reads Supplier identity, active status, and Supplier eligibility.

### Feature 7 — Supplier Order Form

Feature 9 may use an active form to prepare a Draft Supplier Order. Later changes to the form must not alter submitted orders.

### Feature 10 — Receiving

Feature 10 owns receiving transactions, discrepancies, and confirmed receipt records.

Feature 9 uses confirmed receiving information to maintain cumulative received quantities and determine outstanding quantities and receiving status.

### Feature 2 — Warehouse

Feature 9 reads Warehouse information to scope replenishment and identify the destination.

### Shared Authentication

Shared services own User identity and role definitions.

Feature 9 records the User performing purchasing actions.

### Feature 9 — Audit Events

Every significant purchasing action must preserve:
- Acting User
- Timestamp
- Action
- Relevant previous values
- Relevant new values

### Data Integrity

- Supplier Order IDs and PO Numbers must be unique.
- Order Line IDs must be persistent.
- Duplicate Items within an order are prohibited.
- Ordered cases and Units Per Case must be positive integers.
- Received quantities cannot be negative.
- Purchasing prices cannot be negative.
- Foreign-key references must be valid.
- Submitted purchasing values must be preserved.
- Cancellation must not delete history.
- Status changes and audit events must be transactionally consistent.

---

## API Requirements

**Design Status:** Proposed. Final routes must follow the project's API conventions.

### API-9.1: Get Replenishment Recommendations

**Method:** GET  
**Endpoint:** `/api/warehouses/{warehouseId}/replenishment`

**Authorization:** Purchasing Clerk or Manager.

**Response:** `200 OK`

Returns:
- Item ID and Item Number
- Physical Inventory Quantity
- Quantity Already on Order
- Calculated Quantity on Hand
- Minimum and Maximum Stock Levels
- Recommended Reorder Units
- Units Per Case
- Recommended Cases
- Case-rounding excess
- Supplier eligibility or exception status

**Rules:**
- Use the selected Warehouse only.
- Count eligible outstanding orders only.
- Reject invalid thresholds.
- Flag Items without eligible Suppliers.
- Do not automatically create orders.

### API-9.2: Create Supplier Order

**Method:** POST  
**Endpoint:** `/api/supplier-orders`

**Authorization:** Purchasing Clerk or Manager.

**Example Request:**

    {
      "supplierId": 101,
      "warehouseId": 1,
      "sourceFormId": null,
      "lines": [
        {
          "itemId": 201,
          "quantityOrderedCases": 5
        }
      ]
    }

**Response:** `201 Created`

**Rules:**
- Generate unique IDs and PO Number.
- Set status to Draft.
- Record creator and timestamp.
- Validate Supplier, Warehouse, Items, and relationships.
- Store ordered cases separately from received units.

**Errors:** `400`, `401`, `403`, `404`, `409`.

### API-9.3: Get Supplier Order

**Method:** GET  
**Endpoint:** `/api/supplier-orders/{supplierOrderId}`

**Authorization:** Authorized purchasing and receiving personnel.

**Response:** `200 OK`

Returns order header, lines, purchasing values, received quantities, outstanding quantities, and status, subject to permissions.

### API-9.4: Find Supplier Order by PO Number

**Method:** GET  
**Endpoint:** `/api/supplier-orders/by-po/{poNumber}`

**Authorization:** Purchasing Clerk, Manager, Receiving Clerk, or authorized Warehouse Receiver.

**Response:** `200 OK`

**Rules:**
- Return matching order details.
- Support Submitted and Partially Received orders for receiving.
- Prevent receiving personnel from editing purchasing values.
- Return `404` for unknown PO Numbers.

### API-9.5: Update Draft Supplier Order

**Method:** PUT  
**Endpoint:** `/api/supplier-orders/{supplierOrderId}`

**Authorization:** Purchasing Clerk or Manager.

**Response:** `200 OK`

**Rules:**
- Allow ordinary edits only while Draft.
- Validate all lines.
- Reject duplicate Items.
- Preserve creation information.
- Record audit history.
- Reject ordinary edits after submission.

### API-9.6: Submit Supplier Order

**Method:** POST  
**Endpoint:** `/api/supplier-orders/{supplierOrderId}/submit`

**Authorization:** Purchasing Clerk or Manager.

**Response:** `200 OK`

**Rules:**
- Order must be Draft.
- Supplier must be active.
- At least one valid line is required.
- Quantities must be positive whole cases.
- Preserve submitted prices and Units Per Case.
- Record submission timestamp and audit event.

### API-9.7: Cancel Supplier Order

**Method:** POST  
**Endpoint:** `/api/supplier-orders/{supplierOrderId}/cancel`

**Authorization:** Authorized purchasing personnel.

**Response:** `200 OK`

**Rules:**
- Apply approved cancellation policy.
- Preserve order history.
- Record User and timestamp.
- Exclude canceled outstanding quantities.
- Do not overwrite confirmed receiving records.

### API-9.8: Request Authorized Amendment

**Method:** POST  
**Endpoint:** `/api/supplier-orders/{supplierOrderId}/amendments`

**Authorization:** To be confirmed.

**Rules:**
- Require authorization.
- Record before-and-after values.
- Preserve original submitted information.
- Apply approved rules after partial receipt.
- Prevent unauthorized purchasing changes.

### API-9.9: Receiving Confirmation Integration

**Owner:** Feature 10.

**Purpose:** Update confirmed received quantities and receiving-related Supplier Order status.

**Rules:**
- Maintain cumulative received units by line.
- Preserve original ordered quantities.
- Prevent duplicate receipt processing.
- Apply approved over-receipt rules.

### Shared API Requirements

- Authenticate requests.
- Enforce role permissions on the server.
- Validate identifiers and foreign keys.
- Use transactions for submission, cancellation, and auditing.
- Use consistent individual-unit quantities.
- Preserve historical purchasing values.
- Return clear validation and conflict errors.

---

## Screen Requirements

**Design Status:** Proposed. Mockup paths are planned, not confirmed existing files.

### UI-9A: Replenishment Recommendations

**Proposed Image:** `docs/UI/supplier-replenishment.png`

**Purpose:** Identify Items requiring purchasing.

**Displays:**
- Warehouse
- Item Number and Description
- Physical Inventory
- Outstanding Units
- Calculated Quantity on Hand
- Minimum and Maximum Stock
- Recommended Units and Cases
- Case-rounding excess
- Supplier or exception status

**Actions:** Select Warehouse, Refresh, Review Exceptions, Select Items, Start Supplier Order.

### UI-9B: Create Supplier Order

**Proposed Image:** `docs/UI/supplier-order-create.png`

**Purpose:** Prepare a Draft Supplier Order.

**Fields:**
- Supplier
- Destination Warehouse
- Optional Supplier Order Form
- Item
- Ordered Cases
- Units Per Case
- Calculated Ordered Units
- Supplier Purchase Price

**Actions:** Add Item, Remove Item, Update Quantity, Save Draft, Cancel.

**Validation:** Reject invalid Suppliers, quantities, and duplicate Items.

### UI-9C: Review and Submit Supplier Order

**Proposed Image:** `docs/UI/supplier-order-review.png`

**Purpose:** Review an order before submission.

**Displays:** PO Number, Supplier, Warehouse, status, Items, ordered cases, Units Per Case, ordered units, and prices.

**Actions:** Edit Draft, Submit Order, Return to Draft List.

### UI-9D: Supplier Order List

**Proposed Image:** `docs/UI/supplier-order-list.png`

**Purpose:** Search and review orders.

**Displays:** PO Number, Supplier, Warehouse, creation date, status, submission date.

**Actions:** Search, Filter, View, Open Draft, Create Order.

### UI-9E: Supplier Order Details

**Proposed Image:** `docs/UI/supplier-order-details.png`

**Purpose:** Display saved purchasing information.

**Displays:**
- PO Number
- Supplier and Warehouse
- Status
- Creation and submission details
- Original ordered quantities
- Cumulative received quantities
- Outstanding quantities
- Purchasing prices for authorized Users
- Audit history

**Rule:** Original submitted purchasing information is read-only through ordinary operations.

### UI-9F: Receiving PO Lookup

**Proposed Image:** `docs/UI/supplier-order-receiving-lookup.png`

**Purpose:** Allow receiving personnel to find submitted orders.

**Fields:** PO Number.

**Displays:** Supplier, Warehouse, status, ordered Items, ordered quantities, received quantities, and outstanding quantities.

**Actions:** Search, View Details, Continue to Feature 10.

### UI-9G: Supplier Order Audit History

**Proposed Image:** `docs/UI/supplier-order-audit.png`

**Purpose:** Review purchasing changes.

**Displays:** Action, User, timestamp, previous values, new values.

**Rule:** Audit history is read-only.

### UI-9H: Purchasing Exceptions

**Proposed Image:** `docs/UI/supplier-purchasing-exceptions.png`

**Purpose:** Display Items requiring manual purchasing review.

**Exceptions:**
- Missing thresholds
- Invalid thresholds
- Invalid Units Per Case
- No eligible Supplier
- Inactive Supplier
- Case-rounding excess

**Actions:** Review Exception, Open Item Details, Return to Replenishment.

### Role Permissions

| Role | View Replenishment | Create/Edit Draft | Submit | View Receiving PO |
|---|---|---|---|---|
| Purchasing Clerk | Yes | Yes | Yes | Yes |
| Manager | Yes | Yes | Yes | Yes |
| Receiving Clerk | No by default | No | No | Yes |
| Warehouse Receiver | No by default | No | No | Yes |
| Picker | No | No | No | No by default |
| Driver | No | No | No | No by default |

Submitted purchasing changes require a separately approved amendment process.

---

## Definition of Done

### Requirements and Design

- [ ] Five User Stories are documented.
- [ ] Fifty-six recovered Functional Requirements are documented.
- [ ] The discrepancy with the earlier 60-requirement count is resolved.
- [ ] Assumptions are documented.
- [ ] Edge Cases are documented.
- [ ] Success Criteria are documented.
- [ ] Ten Key Entities are documented.
- [ ] Initial Data Model is documented.
- [ ] Gherkin acceptance scenarios are reviewed against the original source.
- [ ] Data Ownership is documented.
- [ ] API Requirements are documented.
- [ ] Screen Requirements are documented.
- [ ] Out of Scope is documented.

### Replenishment

- [ ] Physical Inventory is aggregated correctly.
- [ ] Inventory is not counted twice.
- [ ] Outstanding quantities use eligible order statuses.
- [ ] Calculated Quantity on Hand uses the required formula.
- [ ] Items below minimum are identified.
- [ ] Items at or above minimum are not flagged.
- [ ] Reorder quantities are correct.
- [ ] Invalid thresholds are flagged.
- [ ] Case conversion is correct.
- [ ] Case-rounding excess is displayed.
- [ ] Items without eligible Suppliers appear in exceptions.

### Supplier Order Creation

- [ ] Authorized Users can create orders.
- [ ] IDs and PO Numbers are unique.
- [ ] Creator and timestamp are recorded.
- [ ] Destination Warehouse is recorded.
- [ ] Supplier Item relationships are validated.
- [ ] Submitted orders contain valid lines.
- [ ] Duplicate Items are rejected.
- [ ] Ordered cases are positive integers.
- [ ] Units Per Case is preserved.
- [ ] Ordered and received quantities are separate.
- [ ] Optional Supplier Order Forms are supported.

### Submission and History

- [ ] Orders begin in Draft status.
- [ ] Valid Draft orders can be submitted.
- [ ] Invalid submissions are rejected.
- [ ] Submitted values are preserved.
- [ ] Ordinary edits after submission are blocked.
- [ ] Amendments follow approved rules.
- [ ] Cancellation preserves history.
- [ ] Purchasing changes create audit events.
- [ ] Creation information remains unchanged.

### Receiving Integration

- [ ] Submitted orders are retrievable by PO Number.
- [ ] Partially Received orders are retrievable.
- [ ] Receiving personnel can view ordered and received quantities.
- [ ] Receiving personnel cannot overwrite purchasing values.
- [ ] Feature 10 provides confirmed receiving updates.
- [ ] Receiving status reflects confirmed receipts.

### Testing

- [ ] US-9.1 acceptance scenarios pass.
- [ ] US-9.2 acceptance scenarios pass.
- [ ] US-9.3 acceptance scenarios pass.
- [ ] US-9.4 acceptance scenarios pass.
- [ ] US-9.5 acceptance scenarios pass.
- [ ] Tests verify unit and case conversions.
- [ ] Tests verify Warehouse-specific calculations.
- [ ] Tests verify Supplier eligibility.
- [ ] Tests verify authorization.
- [ ] Tests verify audit history.
- [ ] Tests verify original submitted values are preserved.
- [ ] Acceptance scenario count and wording are reconciled with the original file.

### Documentation and Review

- [ ] Feature follows OC Speckit section order.
- [ ] Architecture diagrams are updated.
- [ ] Design decisions are recorded in `docs/ADRs/`.
- [ ] Non-functional requirements are addressed in `docs/NFR/`.
- [ ] UI mockups are created.
- [ ] UI paths match actual repository files.
- [ ] Feature changes are committed to `design-draft`.
- [ ] Changes are pushed to GitHub.

**Draft Note:** Unchecked tasks do not indicate completed implementation, testing, or mockups.

---

## Out of Scope

Feature 9 does not include:

- Maintaining Company or Warehouse master records.
- Maintaining physical Inventory balances (Feature 3).
- Editing Individual Item master data (Feature 4).
- Maintaining Supplier master records (Feature 5).
- Maintaining Supplier Order Forms (Feature 7).
- Physically receiving shipments (Feature 10).
- Scanning incoming products.
- Recording receiving-door assignments.
- Reconciling receiving discrepancies.
- Put Away, Picking, Shipping, or Delivery.
- Maintaining Customer Orders.
- Ordinary editing of submitted purchasing quantities.
- Allowing receiving personnel to change purchasing approval data.
- Automatically assigning arbitrary Suppliers.
- Counting Draft or Canceled orders as outstanding.
- Treating outstanding orders as physical picking stock.
- Requiring electronic transmission to Suppliers.
- Maintaining User accounts and passwords.

### Pending Design Decisions

- **PD-9.1:** Confirm whether Minimum and Maximum Stock Levels are per Warehouse or global.
- **PD-9.2:** Confirm whether Approved and Sent should be separate order statuses.
- **PD-9.3:** Confirm amendment permissions and whether amendments are allowed after partial receipt.
- **PD-9.4:** Confirm whether upward whole-case rounding is mandatory.
- **PD-9.5:** Confirm over-receipt handling and its effect on order completion.
- **PD-9.6:** Reconcile the earlier 60-functional-requirement reference with the 56 recovered requirements.
- **PD-9.7:** Verify the acceptance scenarios against the original Feature 9 source before treating revised wording as approved.

These decisions remain pending stakeholder or professor approval.
