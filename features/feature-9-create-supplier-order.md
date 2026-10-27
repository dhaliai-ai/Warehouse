
# Feature: Create Supplier Order

**Feature ID:** 9  
**Branch pattern:** `feature/9-create-supplier-order`  
**Status:** Draft - Professor Feedback Incorporated; Clarifications Pending  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System assists purchasing personnel in creating Supplier Orders by identifying items that require replenishment, calculating quantities using minimum and maximum stock levels, considering inventory already on order, selecting appropriate suppliers, and recording purchase orders for later receiving. The system preserves ordered quantities separately from received quantities.

---

## User Stories

### US-9.1: Identify Items Needing Replenishment

**As a** Purchasing Clerk or Manager  
**I want to** identify items whose calculated Quantity on Hand is below their minimum stock level  
**So that** the company can replenish products before shortages affect customer orders.

**Priority:** P1  
**Independent test:** Set an item's inventory and outstanding supplier order quantities below its minimum stock level and verify that the item appears on the replenishment list.

### US-9.2: Determine Quantity to Order

**As a** Purchasing Clerk or Manager  
**I want to** calculate the quantity required to replenish an item toward its maximum stock level  
**So that** the company orders enough products without ignoring quantities already on order.

**Priority:** P1  
**Independent test:** Provide inventory quantity, outstanding order quantity, minimum stock, and maximum stock; verify that the calculated replenishment quantity is correct.

### US-9.3: Create Supplier Order

**As a** Purchasing Clerk or Manager  
**I want to** create a purchase order containing a Supplier, ordered items, and quantities  
**So that** the Supplier can fulfill the order and warehouse receivers can identify it when products arrive.

**Priority:** P1  
**Independent test:** Create a Supplier Order for an active Supplier with valid order lines and verify that a unique PO Number, quantities, and status are saved.

### US-9.4: Review and Submit Supplier Order

**As a** Purchasing Clerk or Manager  
**I want to** review and submit a prepared Supplier Order  
**So that** only valid, approved purchasing information is recorded as an outstanding order.

**Priority:** P1  
**Independent test:** Create a draft Supplier Order, review its lines, submit it, and verify that its status changes and the outstanding ordered quantity is included in replenishment calculations.

### US-9.5: Retrieve Supplier Order for Receiving

**As a** Receiving Clerk or Warehouse Receiver  
**I want to** find a submitted Supplier Order using its PO Number  
**So that** I can compare delivered products with the quantities originally ordered.

**Priority:** P1  
**Independent test:** Search for a submitted PO Number and verify that the Supplier, ordered items, and ordered quantities are displayed without changing them.

---

## Functional Requirements

- **FR-001:** The system MUST maintain minimum and maximum stock levels for Individual Items as defined in Feature 4.

- **FR-002:** The system MUST calculate Physical Inventory Quantity in individual units by summing recorded inventory balances for an Item across eligible bins and locations within the selected Warehouse. The same physical units MUST NOT be counted more than once.

- **FR-003:** The system MUST calculate Quantity Already on Order as the sum of outstanding individual units on eligible Supplier Order Lines for the Item and selected Warehouse.

- **FR-004:** The system MUST use the formula:

  `Calculated Quantity on Hand = Physical Inventory Quantity + Quantity Already on Order`

  This calculated value is used for replenishment planning and is distinct from physical stock currently available for picking.

- **FR-005:** The system MUST identify an Item as requiring replenishment when Calculated Quantity on Hand is below its Minimum Stock Level.

- **FR-006:** The system MUST NOT identify an Item as below minimum when Calculated Quantity on Hand equals or exceeds its Minimum Stock Level.

- **FR-007:** When replenishment is required, the system MUST use the formula:

  `Reorder Quantity (units) = max(0, Maximum Stock Level - Calculated Quantity on Hand)`

  When Calculated Quantity on Hand is not below Minimum Stock Level, the recommended Reorder Quantity MUST be zero.

- **FR-008:** The system MUST prevent negative recommended replenishment quantities.

- **FR-009:** Quantity Already on Order MUST include outstanding quantities from Supplier Orders in Submitted or Partially Received status.

- **FR-010:** The system MUST exclude Draft, Received, and Canceled Supplier Orders from Quantity Already on Order.

- **FR-011:** The system MUST calculate outstanding quantity for each eligible Supplier Order Line using:

  `Outstanding Units = max(0, Ordered Units - Quantity Received Units)`

  `Ordered Units = Quantity Ordered Cases × Units Per Case`

- **FR-012:** The system MUST flag Items with missing, negative, non-integer, or inconsistent minimum and maximum stock levels. An Item MUST be excluded from automatic replenishment recommendations until invalid values are corrected.

- **FR-013:** The system MUST allow authorized Purchasing Clerks and Managers to create Supplier Orders.

- **FR-014:** Each Supplier Order MUST be associated with one existing active Supplier.

- **FR-015:** Each Supplier Order MUST have a unique, system-generated PO Number and a unique internal Supplier Order identifier.

- **FR-016:** Each Supplier Order MUST record its creation date, creation time, and the User who created it.

- **FR-017:** Each Supplier Order MUST contain at least one valid Supplier Order Line before submission.

- **FR-018:** Each Supplier Order Line MUST reference an existing Individual Item and have a unique persistent line identifier.

- **FR-019:** Each Supplier Order Line MUST maintain Quantity Ordered separately from Quantity Received.

- **FR-020:** The system MUST record Quantity Ordered in cases and preserve the Units Per Case value used for that order line.

- **FR-021:** The system MUST calculate Ordered Units as Quantity Ordered Cases multiplied by Units Per Case.

- **FR-022:** Quantity Ordered MUST be a positive whole number of cases.

- **FR-023:** The system MUST allow authorized purchasing personnel to review and adjust recommended quantities before submission.

- **FR-024:** The system MUST prevent the same Individual Item from appearing more than once on the same Supplier Order.

- **FR-025:** The system MUST verify that each ordered Item is associated with the selected Supplier through a Supplier Item relationship.

- **FR-026:** Items requiring replenishment that have no associated active Supplier MUST be flagged for manual purchasing intervention. The system MUST NOT assign an arbitrary Supplier.

- **FR-027:** The system MUST prevent submission of an order line for an Item not supplied by the selected Supplier.

- **FR-028:** The system MUST support supplier-specific purchasing prices defined through Supplier Item relationships.

- **FR-029:** The system MUST preserve the purchase price used when the Supplier Order is submitted.

- **FR-030:** The system MUST support creating a Supplier Order from an active Supplier Order Form defined in Feature 7.

- **FR-031:** Authorized purchasing personnel MUST also be able to create a Supplier Order without selecting a reusable Supplier Order Form.

- **FR-032:** The system MUST maintain Supplier Order statuses of Draft, Submitted, Partially Received, Received, and Canceled.

- **FR-033:** A newly created Supplier Order MUST initially have Draft status.

- **FR-034:** The system MUST allow authorized purchasing personnel to submit a valid Draft Supplier Order.

- **FR-035:** The system MUST reject submission of a Supplier Order without an active Supplier or at least one valid order line.

- **FR-036:** The system MUST prevent unauthorized users from creating or submitting Supplier Orders.

- **FR-037:** The system MUST preserve submitted Supplier Order details for later receiving and reconciliation.

- **FR-038:** Authorized purchasing personnel MAY edit Draft Supplier Orders. After submission, original ordered quantities and submitted purchasing prices MUST NOT be changed through ordinary editing. Corrections MUST use an authorized, auditable amendment or cancellation process.

- **FR-039:** Submitted and Partially Received Supplier Orders MUST be available for receiving by PO Number.

- **FR-040:** Authorized receiving personnel MUST be able to view Supplier Order details without changing the original Quantity Ordered.

- **FR-041:** The system MUST record cumulative Quantity Received separately for each Supplier Order Line.

- **FR-042:** Receiving updates and discrepancies MUST be handled through Feature 10.

- **FR-043:** The system MUST preserve Supplier Orders and their order lines for purchasing and receiving history.

- **FR-044:** The system MUST maintain relationships between Supplier Orders, Suppliers, Individual Items, Supplier Order Forms, Users, and the destination Warehouse.

- **FR-045:** The system MUST record submitted Supplier Orders even when electronic transmission to the Supplier occurs outside the system.

- **FR-046:** Canceled Supplier Orders MUST NOT contribute to outstanding inventory on order.

- **FR-047:** The system MUST reject attempts to modify nonexistent Supplier Orders and MUST report when a requested PO Number does not exist.

- **FR-048:** Replenishment calculations MUST use consistent individual-unit quantities. Cases MUST be converted to units before quantities are added or compared.

- **FR-049:** When the recommended unit quantity is not divisible by Units Per Case, the system MUST calculate the recommended number of cases by rounding upward to the next whole case and display the resulting ordered units for purchasing review.

- **FR-050:** The system MUST display when rounding to whole cases causes the proposed order to exceed the calculated unit requirement.

- **FR-051:** Replenishment calculations MUST use the selected Warehouse's physical inventory and eligible outstanding Supplier Orders. [NEEDS CLARIFICATION: Confirm whether minimum and maximum stock levels are maintained separately per Warehouse or globally for each Item.]

- **FR-052:** The system MUST NOT count physical inventory twice when an Item is recorded across multiple bins or locations.

- **FR-053:** The system MUST reject automatic replenishment recommendations when required stock thresholds are missing or invalid, but MUST identify the affected Items for authorized review.

- **FR-054:** A Supplier Order MUST retain its original creation information, even after subsequent edits or status changes.

- **FR-055:** The system MUST record the User, date, time, action, and relevant before-and-after values for Supplier Order edits, submission, cancellation, and authorized amendments.

- **FR-056:** A Supplier Order Line MUST retain its original Units Per Case value after submission, even if the Item's current Units Per Case changes.

- **FR-057:** The system MUST update Supplier Order receiving status based on confirmed receiving information from Feature 10, without overwriting original ordered quantities.

- **FR-058:** The system MUST prevent ordinary receiving personnel from changing purchasing approval information or submitted purchase prices.

- **FR-059:** The system MUST preserve a canceled order's historical records and audit history.

- **FR-060:** The system MUST prevent automatic replenishment from selecting an inactive Supplier.

**Clarifications Pending Approval:**

1. Confirm whether Minimum Stock Level and Maximum Stock Level apply to each Warehouse separately or to an Item across the company.
2. Confirm whether Approved and Sent should be separate Supplier Order statuses.
3. Confirm which roles can authorize amendments and whether an order may be amended after partial receipt.
4. Confirm whether purchasing should always round up to full cases or allow another policy for exceptional Items.
5. Confirm the procedure for over-receipt and whether over-received units affect Supplier Order completion.

---

## Key Entities

### Supplier Order

Represents a purchase order created by the warehouse company to purchase products from a Supplier.

Each Supplier Order has a unique PO Number, internal identifier, Supplier, destination Warehouse, status, creation information, and associated order lines.

### Supplier Order Line

Represents an Individual Item included in a Supplier Order.

Each line records Quantity Ordered in cases, Units Per Case, Quantity Received in individual units, and the purchasing price associated with the order.

### Individual Item

Represents a product that may require replenishment.

Minimum and maximum stock levels and Units Per Case are maintained through Feature 4.

### Inventory

Represents the physical quantity of an Individual Item stored at a Warehouse Location.

Inventory quantities are maintained through Feature 3.

### Supplier

Represents a business from which the warehouse company purchases products.

Supplier information is maintained through Feature 5.

### Supplier Item

Represents the relationship between a Supplier and an Individual Item, including supplier-specific purchasing prices.

### Supplier Order Form

Represents an optional reusable form used to prepare a Supplier Order.

Supplier Order Forms are maintained through Feature 7.

### Warehouse

Represents the warehouse for which inventory is evaluated and to which the Supplier Order is intended to deliver products.

### User

Represents an employee authorized to create, submit, review, or retrieve Supplier Orders.

### Supplier Order Audit Entry

Represents a recorded change or status transition for a Supplier Order, including the acting User, timestamp, action, and relevant before-and-after values.

---

## Initial Data Model

### Supplier Order

| Attribute | Type | Description |
|---|---|---|
| supplierOrderId | Integer | Unique internal Supplier Order identifier |
| poNumber | String | Unique system-generated purchase order number |
| supplierId | Integer | Foreign key referencing Supplier |
| warehouseId | Integer | Destination Warehouse |
| sourceFormId | Integer | Optional reference to Supplier Order Form |
| createdAt | DateTime | Date and time the order was created |
| submittedAt | DateTime | Date and time the order was submitted |
| createdBy | Integer | User who created the order |
| updatedAt | DateTime | Date and time of the latest modification |
| updatedBy | Integer | User who last modified the order |
| status | String | Draft, Submitted, Partially Received, Received, or Canceled |

**Relationships:**
- Each Supplier Order belongs to one Supplier.
- Each Supplier Order is associated with one destination Warehouse.
- Each submitted Supplier Order contains one or more Supplier Order Lines.
- A Supplier Order may reference a Supplier Order Form.
- Each Supplier Order is created by a User.
- A Supplier Order may be referenced by receiving records in Feature 10.
- Each Supplier Order may have multiple audit entries.

**Constraints:**
- supplierOrderId MUST be unique.
- poNumber MUST be unique and nonempty.
- supplierId MUST reference an existing Supplier.
- warehouseId MUST reference an existing Warehouse.
- The Supplier MUST be active when the order is submitted.
- Submitted orders MUST contain at least one valid order line.

### Supplier Order Line

| Attribute | Type | Description |
|---|---|---|
| supplierOrderLineId | Integer | Unique persistent order line identifier |
| supplierOrderId | Integer | Foreign key referencing Supplier Order |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityOrderedCases | Integer | Quantity ordered in whole cases |
| unitsPerCase | Integer | Units per case preserved for the order |
| quantityReceivedUnits | Integer | Cumulative quantity received in individual units |
| purchasePricePerCase | Decimal | Purchasing price per case preserved on submission |

**Relationships:**
- Each Supplier Order Line belongs to one Supplier Order.
- Each line references one Individual Item.
- An Individual Item may appear on multiple Supplier Orders.

**Constraints:**
- quantityOrderedCases MUST be greater than zero.
- unitsPerCase MUST be greater than zero.
- quantityReceivedUnits MUST NOT be negative.
- purchasePricePerCase MUST NOT be negative.
- The combination of supplierOrderId and itemId MUST be unique.

**Derived Values:**
- Ordered Units = quantityOrderedCases × unitsPerCase.
- Outstanding Units = max(0, Ordered Units - quantityReceivedUnits).

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |
| minimumStock | Integer | Minimum stock level in individual units |
| maximumStock | Integer | Maximum stock level in individual units |
| unitsPerCase | Integer | Number of individual units per case |
| isActive | Boolean | Indicates whether the Item is active |

**Relationships:**
- An Individual Item can appear on multiple Supplier Order Lines.
- An Individual Item can have Inventory in multiple Warehouse Locations.
- Item maintenance is defined in Feature 4.

**Constraints:**
- Minimum and maximum stock levels MUST be nonnegative whole numbers.
- Minimum Stock Level MUST NOT exceed Maximum Stock Level.
- Units Per Case MUST be greater than zero.

**Pending clarification:** Whether minimumStock and maximumStock should instead be stored in a separate Item-Warehouse stock policy entity.

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique Inventory identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| locationId | Integer | Foreign key referencing Warehouse Location |
| quantity | Integer | Physical quantity in individual units |

**Relationships:**
- Inventory contributes to replenishment calculations.
- Inventory maintenance is defined in Feature 3.
- Warehouse Location identifies the Warehouse containing the Inventory.

### Supplier

| Attribute | Type | Description |
|---|---|---|
| supplierId | Integer | Unique Supplier identifier |
| name | String | Supplier business name |
| isActive | Boolean | Indicates whether the Supplier is active |

**Relationships:**
- One Supplier may have multiple Supplier Orders.
- Supplier maintenance is defined in Feature 5.

### Supplier Item

| Attribute | Type | Description |
|---|---|---|
| supplierItemId | Integer | Unique Supplier Item relationship identifier |
| supplierId | Integer | Foreign key referencing Supplier |
| itemId | Integer | Foreign key referencing Individual Item |
| purchasePricePerCase | Decimal | Supplier purchasing price per case |

**Relationships:**
- Supplier Item identifies which products may be ordered from a Supplier.
- Supplier-specific purchasing prices are maintained through Feature 4.

### Supplier Order Form

| Attribute | Type | Description |
|---|---|---|
| formId | Integer | Unique Supplier Order Form identifier |
| supplierId | Integer | Foreign key referencing Supplier |
| isActive | Boolean | Indicates whether the Form is active |

**Relationships:**
- A Supplier Order may reference a Supplier Order Form.
- Supplier Order Form maintenance is defined in Feature 7.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique Warehouse identifier |
| name | String | Warehouse name |

**Relationships:**
- A Warehouse contains Inventory Locations.
- A Supplier Order identifies its destination Warehouse.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Purchasing personnel create and submit Supplier Orders.
- Receiving personnel retrieve Supplier Orders during receiving.
- Users are referenced in Supplier Order audit entries.

### Supplier Order Audit Entry

| Attribute | Type | Description |
|---|---|---|
| auditEntryId | Integer | Unique audit entry identifier |
| supplierOrderId | Integer | Supplier Order being changed |
| userId | Integer | User performing the action |
| action | String | Edit, Submit, Cancel, or Amend |
| occurredAt | DateTime | Timestamp of the action |
| previousValues | Text | Relevant values before the action |
| newValues | Text | Relevant values after the action |

**Relationships:**
- Each audit entry belongs to one Supplier Order.
- Each audit entry references the User responsible for the action.

---

## Gherkin AC

### US-9.1: Identify Items Needing Replenishment

#### AC-9.1.1: Calculate Quantity on Hand

**Given** an Individual Item has 40 units recorded in Inventory  
**And** 20 additional units remain outstanding on submitted Supplier Orders  
**When** the system calculates Quantity on Hand for replenishment  
**Then** Calculated Quantity on Hand is 60 units.

#### AC-9.1.2: Identify Item below minimum

**Given** an Individual Item has a Minimum Stock Level of 50 units  
**And** its Calculated Quantity on Hand is 35 units  
**When** the system evaluates replenishment needs  
**Then** the system identifies the Item as requiring replenishment.

#### AC-9.1.3: Do not replenish Item at minimum

**Given** an Individual Item has a Minimum Stock Level of 50 units  
**And** its Calculated Quantity on Hand is 50 units  
**When** the system evaluates replenishment needs  
**Then** the Item is not identified as below minimum.

#### AC-9.1.4: Exclude canceled orders

**Given** an Item has 25 units in physical Inventory  
**And** a Canceled Supplier Order contains 20 units of the Item  
**When** the system calculates Quantity on Hand  
**Then** the Canceled order contributes zero outstanding units  
**And** Calculated Quantity on Hand is 25 units.

#### AC-9.1.5: Exclude unsubmitted drafts

**Given** an Item has 30 units in physical Inventory  
**And** a Draft Supplier Order contains 15 units of the Item  
**When** the system calculates Quantity on Hand  
**Then** the Draft order contributes zero outstanding units  
**And** Calculated Quantity on Hand is 30 units.

#### AC-9.1.6: Aggregate inventory across bins

**Given** an Item has 15 units in Bin A  
**And** the same Item has 25 units in Bin B  
**And** both bins belong to the selected Warehouse  
**When** the system calculates Physical Inventory Quantity  
**Then** the Physical Inventory Quantity is 40 units  
**And** neither bin balance is counted more than once.

#### AC-9.1.7: Exclude another Warehouse

**Given** an Item has 20 units in Warehouse A  
**And** the same Item has 35 units in Warehouse B  
**When** replenishment is evaluated for Warehouse A  
**Then** Physical Inventory Quantity for Warehouse A is 20 units  
**And** inventory in Warehouse B is not included.

### US-9.2: Determine Quantity to Order

#### AC-9.2.1: Calculate replenishment quantity

**Given** an Item has a Minimum Stock Level of 50 units  
**And** a Maximum Stock Level of 100 units  
**And** Calculated Quantity on Hand is 30 units  
**When** the system calculates the recommended replenishment quantity  
**Then** the recommended quantity is 70 units.

#### AC-9.2.2: Include outstanding Supplier Orders

**Given** an Item has 25 units in physical Inventory  
**And** 15 units remain outstanding on submitted Supplier Orders  
**And** its Minimum Stock Level is 50 units  
**And** its Maximum Stock Level is 100 units  
**When** the system calculates replenishment  
**Then** Calculated Quantity on Hand is 40 units  
**And** the recommended replenishment quantity is 60 units.

#### AC-9.2.3: Do not recommend negative quantities

**Given** an Item has a Maximum Stock Level of 100 units  
**And** Calculated Quantity on Hand is 120 units  
**When** the system evaluates replenishment  
**Then** the system does not recommend an additional order  
**And** no negative order quantity is generated.

#### AC-9.2.4: Handle invalid stock levels

**Given** an Item has a Minimum Stock Level greater than its Maximum Stock Level  
**When** the system evaluates replenishment  
**Then** the system identifies the stock-level configuration as invalid  
**And** no automatic replenishment recommendation is generated.

#### AC-9.2.5: Handle case quantities

**Given** an Item requires 23 additional units to reach its Maximum Stock Level  
**And** the Item is purchased in cases containing 12 units  
**When** the system prepares an order recommendation  
**Then** the system proposes 2 cases, totaling 24 units  
**And** displays the resulting quantity for purchasing review.

#### AC-9.2.6: Missing stock thresholds

**Given** an Item has no configured Minimum Stock Level  
**When** replenishment is evaluated  
**Then** the Item appears in the purchasing exception list  
**And** no automatic replenishment recommendation is generated until the value is corrected.

#### AC-9.2.7: Zero stock levels

**Given** an Item has a Minimum Stock Level of zero  
**And** a Maximum Stock Level of zero  
**And** its Physical Inventory Quantity is zero  
**When** replenishment is evaluated  
**Then** the stock-level configuration is valid  
**And** no reorder quantity is recommended.

#### AC-9.2.8: Count only outstanding quantities in eligible statuses

**Given** an Item has 10 units in physical Inventory  
**And** a Submitted order has 20 units ordered and 5 received  
**And** a Partially Received order has 12 units ordered and 4 received  
**And** a Draft order has 9 units ordered  
**And** a Canceled order has 7 units ordered  
**When** the system calculates replenishment  
**Then** Quantity Already on Order is 23 units  
**And** Calculated Quantity on Hand is 33 units.

#### AC-9.2.9: Reject negative stock thresholds

**Given** an Item has a Minimum Stock Level of -5 units  
**When** the system evaluates replenishment  
**Then** the system flags the configuration as invalid  
**And** does not generate an automatic recommendation.

#### AC-9.2.10: Show excess caused by case rounding

**Given** an Item needs 13 additional units  
**And** each case contains 10 units  
**When** the system converts the recommendation to cases  
**Then** it recommends 2 cases totaling 20 units  
**And** informs the Purchasing Clerk that the proposed order exceeds the unit requirement by 7 units.

### US-9.3: Create Supplier Order

#### AC-9.3.1: Successfully create Supplier Order

**Given** an active Supplier exists  
**And** the Supplier provides an active Individual Item  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user creates a Supplier Order containing 5 cases of the Item  
**Then** the system saves the Supplier Order  
**And** assigns a unique PO Number  
**And** records the Supplier, Item, and Quantity Ordered  
**And** sets the order status to Draft.

#### AC-9.3.2: Prevent order for nonexistent Supplier

**Given** the requested Supplier does not exist  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user attempts to create a Supplier Order  
**Then** the system rejects the request  
**And** no Supplier Order is created.

#### AC-9.3.3: Prevent order for inactive Supplier

**Given** a Supplier exists but is inactive  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user attempts to submit a Supplier Order for that Supplier  
**Then** the system rejects the submission  
**And** the order is not marked Submitted.

#### AC-9.3.4: Handle Item without Supplier

**Given** an Individual Item requires replenishment  
**And** no active Supplier is associated with the Item  
**When** the system prepares replenishment recommendations  
**Then** the system identifies that no eligible Supplier is available  
**And** does not automatically create an order line for that Item.

#### AC-9.3.5: Reject invalid order quantity

**Given** a valid Supplier and Individual Item exist  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user attempts to add an order line with zero cases  
**Then** the system rejects the order line  
**And** no invalid quantity is saved.

#### AC-9.3.6: Keep Ordered and Received quantities separate

**Given** a Supplier Order contains an Item with 10 cases ordered  
**And** each case contains 12 units  
**When** the Supplier Order is created  
**Then** the system records 10 cases ordered, equivalent to 120 units  
**And** Quantity Received is initially zero  
**And** Quantity Ordered remains separate from Quantity Received.

#### AC-9.3.7: Reject unauthorized order creation

**Given** the user is authenticated as a Driver  
**When** the user attempts to create a Supplier Order  
**Then** the system denies the operation  
**And** no Supplier Order is created.

#### AC-9.3.8: Flag inactive-only Supplier association

**Given** an Item needs replenishment  
**And** its only associated Supplier is inactive  
**When** the system prepares replenishment recommendations  
**Then** the Item appears in the purchasing exception list  
**And** no default Supplier is assigned  
**And** no Supplier Order is automatically created.

#### AC-9.3.9: Persist distinct identifiers

**Given** an authorized Purchasing Clerk creates a Supplier Order with two valid lines  
**When** the order is saved  
**Then** the Supplier Order receives a unique internal identifier and PO Number  
**And** each line receives a distinct persistent Supplier Order Line identifier.

### US-9.4: Review and Submit Supplier Order

#### AC-9.4.1: Successfully submit Supplier Order

**Given** a Draft Supplier Order exists with an active Supplier and valid order lines  
**And** the user is authenticated as a Manager  
**When** the user reviews and submits the Supplier Order  
**Then** the system changes its status to Submitted  
**And** records the submission date and time  
**And** includes its outstanding ordered quantities in replenishment calculations.

#### AC-9.4.2: Reject empty Supplier Order

**Given** a Draft Supplier Order exists without any order lines  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user attempts to submit the order  
**Then** the system rejects the submission  
**And** the order remains in Draft status.

#### AC-9.4.3: Prevent duplicate Item lines

**Given** a Draft Supplier Order already contains Item A  
**When** an authorized user attempts to add Item A as another line  
**Then** the system rejects the duplicate line  
**And** the existing order line remains unchanged.

#### AC-9.4.4: Preserve submitted quantities

**Given** a Supplier Order has been submitted with 8 cases of an Item  
**When** a Receiving Clerk retrieves the order  
**Then** the original Quantity Ordered remains 8 cases  
**And** the Receiving Clerk cannot directly overwrite that ordered quantity.

#### AC-9.4.5: Exclude canceled Supplier Order

**Given** a Submitted Supplier Order has not received any Items  
**And** an authorized Manager cancels the order  
**When** the system recalculates replenishment quantities  
**Then** the Canceled order is excluded from outstanding quantities  
**And** its historical order information remains available.

#### AC-9.4.6: Record audit history

**Given** a Draft Supplier Order exists  
**And** an authorized Purchasing Clerk updates an order line  
**When** the Clerk saves the edit and later submits the valid order  
**Then** the system records the User and timestamp for each action  
**And** preserves the relevant before-and-after values in the audit history  
**And** retains the original creation information.

#### AC-9.4.7: Prevent ordinary editing after submission

**Given** a Supplier Order is Submitted  
**When** a Purchasing Clerk attempts to directly overwrite its original ordered quantity  
**Then** the system rejects the ordinary edit  
**And** directs the User to the authorized amendment or cancellation process.

#### AC-9.4.8: Preserve original Units Per Case

**Given** a Supplier Order Line was submitted with 12 Units Per Case  
**And** the Item's current Units Per Case is later changed to 10  
**When** a Receiving Clerk retrieves the submitted Supplier Order  
**Then** the Supplier Order Line still records 12 Units Per Case  
**And** its original Ordered Units calculation remains unchanged.

### US-9.5: Retrieve Supplier Order for Receiving

#### AC-9.5.1: Find Supplier Order by PO Number

**Given** a Submitted Supplier Order exists with PO Number "PO1001"  
**And** the user is authenticated as a Receiving Clerk  
**When** the user searches for "PO1001"  
**Then** the system displays the matching Supplier Order  
**And** displays its Supplier, Items, Quantity Ordered, and Quantity Received.

#### AC-9.5.2: Reject nonexistent PO Number

**Given** no Supplier Order exists with PO Number "PO9999"  
**And** the user is authenticated as a Receiving Clerk  
**When** the user searches for "PO9999"  
**Then** the system reports that no matching Supplier Order exists  
**And** does not create or modify an order.

#### AC-9.5.3: Make partially received order available

**Given** a Supplier Order is in Partially Received status  
**And** additional ordered quantities remain outstanding  
**When** a Receiving Clerk searches for its PO Number  
**Then** the system displays the Supplier Order  
**And** shows the original ordered quantities and cumulative received quantities  
**And** makes the order available for the receiving process defined in Feature 10.
