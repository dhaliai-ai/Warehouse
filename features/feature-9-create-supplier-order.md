
# Feature: Create Supplier Order

**Feature ID:** 9  
**Branch pattern:** `feature/9-create-supplier-order`  
**Status:** Draft - Proposed Rules Pending Approval  
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
- **FR-002:** The system MUST calculate an item's Inventory Quantity from its recorded inventory balances.
- **FR-003:** The system MUST calculate the quantity already on order from outstanding Supplier Order quantities not yet received.
- **FR-004:** For replenishment calculations, the system MUST define calculated Quantity on Hand as Inventory Quantity plus quantity already on order.
- **FR-005:** The system MUST identify an item as needing replenishment when calculated Quantity on Hand is below its minimum stock level.
- **FR-006:** The system MUST NOT identify an item as below minimum when calculated Quantity on Hand equals or exceeds its minimum stock level.
- **FR-007:** The system MUST calculate the recommended replenishment quantity as Maximum Stock Level minus calculated Quantity on Hand when replenishment is required.
- **FR-008:** The system MUST prevent negative recommended replenishment quantities.
- **FR-009:** The system MUST include outstanding quantities from submitted Supplier Orders in replenishment calculations.
- **FR-010:** The system MUST exclude canceled Supplier Orders and unsubmitted draft orders from quantities already on order.
- **FR-011:** The system MUST avoid counting quantities already received as still outstanding.
- **FR-012:** The system MUST identify items with missing or invalid minimum and maximum stock levels and exclude them from automatic replenishment recommendations until corrected.
- **FR-013:** The system MUST allow authorized Purchasing Clerks and Managers to create Supplier Orders.
- **FR-014:** Each Supplier Order MUST be associated with one existing active Supplier.
- **FR-015:** Each Supplier Order MUST have a unique, system-generated PO Number.
- **FR-016:** Each Supplier Order MUST record its creation date and the User who created it.
- **FR-017:** Each Supplier Order MUST contain one or more Supplier Order Lines before submission.
- **FR-018:** Each Supplier Order Line MUST identify an existing Individual Item.
- **FR-019:** Each Supplier Order Line MUST maintain Quantity Ordered separately from Quantity Received.
- **FR-020:** The system MUST record Quantity Ordered in cases and preserve the number of units per case used for that order line.
- **FR-021:** The system MUST support calculating the corresponding ordered quantity in individual units.
- **FR-022:** The system MUST require Quantity Ordered to be a positive whole number of cases.
- **FR-023:** The system MUST allow authorized purchasing personnel to review and adjust recommended order quantities before submission.
- **FR-024:** The system MUST prevent the same Individual Item from appearing more than once on the same Supplier Order.
- **FR-025:** The system MUST verify that each ordered Item is associated with the selected Supplier through a Supplier Item relationship.
- **FR-026:** The system MUST identify items requiring replenishment that have no associated active Supplier.
- **FR-027:** The system MUST prevent submission of an order line for an Item that is not supplied by the selected Supplier.
- **FR-028:** The system MUST support using supplier-specific purchasing prices defined through Supplier Item relationships.
- **FR-029:** The system MUST preserve the purchase price used when the Supplier Order is submitted.
- **FR-030:** The system MUST support creating a Supplier Order from an active Supplier Order Form defined in Feature 7.
- **FR-031:** The system MUST allow authorized purchasing personnel to create a Supplier Order without selecting a reusable Supplier Order Form.
- **FR-032:** The system MUST maintain Supplier Order statuses of Draft, Submitted, Partially Received, Received, and Canceled.
- **FR-033:** A newly created Supplier Order MUST initially have Draft status.
- **FR-034:** The system MUST allow authorized purchasing personnel to submit a valid Draft Supplier Order.
- **FR-035:** The system MUST reject submission of an order without a Supplier or at least one valid order line.
- **FR-036:** The system MUST prevent unauthorized users from creating or submitting Supplier Orders.
- **FR-037:** The system MUST preserve submitted Supplier Order details for later receiving and reconciliation.
- **FR-038:** The system MUST prevent ordinary editing of submitted ordered quantities; corrections MUST use a separately authorized order amendment or cancellation process.
- **FR-039:** The system MUST make submitted and partially received Supplier Orders available for receiving by PO Number.
- **FR-040:** The system MUST allow authorized receiving personnel to view Supplier Order details without changing the original Quantity Ordered.
- **FR-041:** The system MUST record cumulative Quantity Received separately for each Supplier Order Line.
- **FR-042:** Receiving updates and discrepancies MUST be handled through Feature 10.
- **FR-043:** The system MUST preserve Supplier Orders and their order lines for purchasing and receiving history.
- **FR-044:** The system MUST maintain the relationship between Supplier Orders, Suppliers, Individual Items, Supplier Order Forms, and Users.
- **FR-045:** The system MUST record the submitted order and its lines even when electronic transmission to the Supplier is handled outside the system.
- **FR-046:** The system MUST prevent canceled orders from being treated as outstanding inventory on order.
- **FR-047:** The system MUST reject attempts to retrieve or modify nonexistent Supplier Orders.

---

## Key Entities

### Supplier Order

Represents a purchase order created by the warehouse company to purchase products from a Supplier.

Each Supplier Order has a unique PO Number, Supplier, status, creation date, and associated order lines.

### Supplier Order Line

Represents an Individual Item included in a Supplier Order.

Each line records the quantity ordered, the quantity received, and the purchasing price associated with the order.

### Individual Item

Represents a product that may require replenishment.

Minimum and maximum stock levels and units per case are maintained in Feature 4.

### Inventory

Represents the quantity of an Individual Item stored in a particular warehouse location.

Inventory quantities are maintained in Feature 3.

### Supplier

Represents a business from which the warehouse company purchases products.

Supplier information is maintained in Feature 5.

### Supplier Item

Represents the relationship between a Supplier and an Individual Item, including supplier-specific purchasing prices.

### Supplier Order Form

Represents an optional reusable form used to prepare a Supplier Order.

Supplier Order Forms are maintained in Feature 7.

### User

Represents an employee authorized to create, submit, or view Supplier Orders.

---

## Initial Data Model

### Supplier Order

| Attribute | Type | Description |
|---|---|---|
| supplierOrderId | Integer | Unique internal Supplier Order identifier |
| poNumber | String | Unique purchase order number used during receiving |
| supplierId | Integer | Foreign key referencing Supplier |
| sourceFormId | Integer | Optional reference to Supplier Order Form |
| createdAt | DateTime | Date and time the order was created |
| submittedAt | DateTime | Date and time the order was submitted, if applicable |
| createdBy | Integer | User who created the order |
| status | String | Draft, Submitted, Partially Received, Received, or Canceled |

**Relationships:**
- Each Supplier Order belongs to one Supplier.
- Each Supplier Order contains one or more Supplier Order Lines before submission.
- A Supplier Order may be created using a Supplier Order Form.
- Each Supplier Order is created by a User.
- A Supplier Order can be referenced by receiving records in Feature 10.

**Constraints:**
- supplierOrderId must be unique.
- poNumber must be unique and nonempty.
- supplierId must reference an existing Supplier.
- A Supplier must be active when the order is submitted.
- Submitted orders must contain at least one valid order line.

### Supplier Order Line

| Attribute | Type | Description |
|---|---|---|
| supplierOrderLineId | Integer | Unique order line identifier |
| supplierOrderId | Integer | Foreign key referencing Supplier Order |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityOrderedCases | Integer | Quantity ordered in cases |
| unitsPerCase | Integer | Units per case recorded when the order was created |
| quantityReceivedUnits | Integer | Cumulative quantity received in individual units |
| purchasePricePerCase | Decimal | Supplier purchasing price per case recorded on the order |

**Relationships:**
- Each Supplier Order Line belongs to one Supplier Order.
- Each line references one Individual Item.
- One Individual Item can appear on multiple Supplier Orders.

**Constraints:**
- quantityOrderedCases must be greater than zero.
- unitsPerCase must be greater than zero.
- quantityReceivedUnits cannot be negative.
- purchasePricePerCase cannot be negative.
- The combination of supplierOrderId and itemId must be unique.

**Derived Values:**
- Ordered Units = quantityOrderedCases × unitsPerCase.
- Outstanding Units = maximum of zero and (Ordered Units - quantityReceivedUnits).

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |
| minimumStock | Integer | Minimum stock level |
| maximumStock | Integer | Maximum stock level |
| unitsPerCase | Integer | Number of individual units per case |
| isActive | Boolean | Indicates whether the Item is active |

**Relationships:**
- An Individual Item can appear on multiple Supplier Order Lines.
- An Individual Item can have Inventory in multiple Warehouse Locations.
- Item maintenance is defined in Feature 4.

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique Inventory identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| locationId | Integer | Foreign key referencing Warehouse Location |
| quantity | Integer | Recorded quantity in individual units |

**Relationships:**
- Inventory quantities contribute to replenishment calculations.
- Inventory maintenance is defined in Feature 3.

### Supplier

| Attribute | Type | Description |
|---|---|---|
| supplierId | Integer | Unique Supplier identifier |
| name | String | Supplier business name |
| isActive | Boolean | Indicates whether the Supplier is active |

**Relationships:**
- One Supplier can have multiple Supplier Orders.
- Supplier maintenance is defined in Feature 5.

### Supplier Item

| Attribute | Type | Description |
|---|---|---|
| supplierItemId | Integer | Unique Supplier Item relationship identifier |
| supplierId | Integer | Foreign key referencing Supplier |
| itemId | Integer | Foreign key referencing Individual Item |
| purchasePricePerCase | Decimal | Supplier purchasing price per case |

**Relationships:**
- Supplier Item identifies which products can be ordered from a Supplier.
- Supplier-specific purchasing prices are maintained in Feature 4.

### Supplier Order Form

| Attribute | Type | Description |
|---|---|---|
| formId | Integer | Unique Supplier Order Form identifier |
| supplierId | Integer | Foreign key referencing Supplier |
| isActive | Boolean | Indicates whether the Form is active |

**Relationships:**
- A Supplier Order may reference a Supplier Order Form.
- Supplier Order Form maintenance is defined in Feature 7.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Purchasing personnel create and submit Supplier Orders.
- Receiving personnel retrieve Supplier Orders during receiving.

---

## Gherkin AC

### US-9.1: Identify Items Needing Replenishment

#### AC-9.1.1: Calculate Quantity on Hand

**Given** an Individual Item has 40 units recorded in Inventory  
**And** 20 additional units remain outstanding on submitted Supplier Orders  
**When** the system calculates Quantity on Hand for replenishment  
**Then** the calculated Quantity on Hand is 60 units.

#### AC-9.1.2: Identify Item below minimum

**Given** an Individual Item has a minimum stock level of 50 units  
**And** its calculated Quantity on Hand is 35 units  
**When** the system evaluates replenishment needs  
**Then** the system identifies the Item as requiring replenishment.

#### AC-9.1.3: Do not replenish Item at minimum

**Given** an Individual Item has a minimum stock level of 50 units  
**And** its calculated Quantity on Hand is 50 units  
**When** the system evaluates replenishment needs  
**Then** the Item is not identified as below minimum.

#### AC-9.1.4: Exclude canceled orders

**Given** an Individual Item has 25 units in Inventory  
**And** a canceled Supplier Order contains 20 units of the Item  
**When** the system calculates Quantity on Hand  
**Then** the canceled order contributes zero outstanding units  
**And** the calculated Quantity on Hand is 25 units.

#### AC-9.1.5: Exclude unsubmitted drafts

**Given** an Individual Item has 30 units in Inventory  
**And** a Draft Supplier Order contains 15 units of the Item  
**When** the system calculates Quantity on Hand  
**Then** the Draft order contributes zero outstanding units  
**And** the calculated Quantity on Hand is 30 units.

### US-9.2: Determine Quantity to Order

#### AC-9.2.1: Calculate replenishment quantity

**Given** an Item has a minimum stock level of 50 units  
**And** a maximum stock level of 100 units  
**And** calculated Quantity on Hand is 30 units  
**When** the system calculates the recommended replenishment quantity  
**Then** the recommended quantity is 70 units.

#### AC-9.2.2: Include outstanding Supplier Orders

**Given** an Item has 25 units in Inventory  
**And** 15 units remain outstanding on submitted Supplier Orders  
**And** its minimum stock level is 50 units  
**And** its maximum stock level is 100 units  
**When** the system calculates replenishment  
**Then** calculated Quantity on Hand is 40 units  
**And** the recommended replenishment quantity is 60 units.

#### AC-9.2.3: Do not recommend negative quantities

**Given** an Item has a maximum stock level of 100 units  
**And** calculated Quantity on Hand is 120 units  
**When** the system evaluates replenishment  
**Then** the system does not recommend an additional order  
**And** no negative order quantity is generated.

#### AC-9.2.4: Handle invalid stock levels

**Given** an Item has a minimum stock level greater than its maximum stock level  
**When** the system evaluates replenishment  
**Then** the system identifies the stock-level configuration as invalid  
**And** does not generate an automatic replenishment recommendation for that Item.

#### AC-9.2.5: Handle case quantities

**Given** an Item requires 23 additional units to reach its maximum stock level  
**And** the Item is purchased in cases containing 12 units  
**When** the system prepares an order recommendation  
**Then** the system identifies that 23 units do not form a whole number of cases  
**And** proposes 2 cases, totaling 24 units  
**And** displays the resulting quantity for purchasing review.

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
**And** the Quantity Received is initially zero  
**And** Quantity Ordered remains separate from Quantity Received.

#### AC-9.3.7: Reject unauthorized order creation

**Given** the user is authenticated as a Driver  
**When** the user attempts to create a Supplier Order  
**Then** the system denies the operation  
**And** no Supplier Order is created.

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

**Given** a submitted Supplier Order has not received any items  
**And** an authorized Manager cancels the order  
**When** the system recalculates replenishment quantities  
**Then** the canceled order is excluded from outstanding quantities  
**And** its historical order information remains available.

### US-9.5: Retrieve Supplier Order for Receiving

#### AC-9.5.1: Find Supplier Order by PO Number

**Given** a submitted Supplier Order exists with PO Number "PO1001"  
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
