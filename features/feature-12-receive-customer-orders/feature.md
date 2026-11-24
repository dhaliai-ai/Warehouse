
# Feature: Receive Customer Orders

**Feature ID:** 12  
**Branch pattern:** `feature/12-receive-customer-orders`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  

**Input:** The Warehouse Management System allows authorized office personnel to receive and record orders from retail store customers. The system identifies the Customer, records the requested Individual Items and quantities, validates order information, and releases completed orders for the picking process. Quantity Ordered remains separate from Quantity Picked, Quantity Shipped, and Quantity Delivered so that differences can be tracked throughout fulfillment.

---

## User Stories

### US-12.1: Record Customer Order

**As a** Customer Service Clerk or Manager  
**I want to** record an order received from a Customer  
**So that** the warehouse can identify the Customer's request and prepare to fulfill it.

**Priority:** P1  
**Independent test:** Create an order for an active Customer and verify that the system saves the Customer association, unique Order Number, and order status.

### US-12.2: Record Ordered Items and Quantities

**As a** Customer Service Clerk or Manager  
**I want to** record the Individual Items and quantities requested by a Customer  
**So that** the warehouse knows exactly which products and quantities must be picked.

**Priority:** P1  
**Independent test:** Add multiple Items with valid quantities and verify that each Item and Quantity Ordered is saved correctly.

### US-12.3: Make Customer Order Available for Picking

**As a** Customer Service Clerk or Manager  
**I want to** complete and release a valid Customer Order  
**So that** warehouse pickers can begin fulfilling the Customer's request.

**Priority:** P1  
**Independent test:** Release a valid Customer Order and verify that it becomes available to the picking process defined in Feature 13.

### US-12.4: Save and Update Draft Customer Order

**As a** Customer Service Clerk or Manager  
**I want to** save an incomplete Customer Order and finish entering it later  
**So that** I do not lose information while waiting for missing order details.

**Priority:** P2  
**Independent test:** Save an incomplete draft, reopen it, add the missing information, and verify that it can be released only after validation succeeds.

### US-12.5: Review Customer Order Information

**As a** Customer Service Clerk or Manager  
**I want to** retrieve a Customer Order and review its recorded details  
**So that** I can verify what the Customer requested and check its fulfillment status.

**Priority:** P2  
**Independent test:** Search for an existing Customer Order Number and verify that the Customer, ordered Items, quantities, and current status are displayed.

---

## Functional Requirements

- **FR-001:** The system MUST allow authorized Customer Service Clerks and Managers to create Customer Orders.
- **FR-002:** The system MUST assign a unique, system-generated Customer Order ID to each Customer Order.
- **FR-003:** The system MUST maintain a unique Customer Order Number that can be used to identify and retrieve an order.
- **FR-004:** The system MUST associate each Customer Order with an existing Customer.
- **FR-005:** The system MUST prevent a Customer Order from being released when its Customer does not exist.
- **FR-006:** The system MUST prevent new Customer Orders from being released for inactive Customers.
- **FR-007:** The system MUST record the date and time a Customer Order was created.
- **FR-008:** The system MUST record the User who entered the Customer Order.
- **FR-009:** The system MUST allow a Customer Order to contain one or more Customer Order Lines.
- **FR-010:** Each Customer Order Line MUST reference an existing Individual Item.
- **FR-011:** The system MUST prevent nonexistent Individual Items from being added to Customer Orders.
- **FR-012:** The system MUST prevent inactive Individual Items from being added to new Customer Orders.
- **FR-013:** The system MUST record Quantity Ordered for each Customer Order Line.
- **FR-014:** Quantity Ordered MUST be a positive whole number of individual units.
- **FR-015:** The system MUST reject zero, negative, or non-integer ordered quantities.
- **FR-016:** The system MUST prevent duplicate Customer Order Lines for the same Individual Item within one order.
- **FR-017:** The system MUST allow authorized office personnel to update Item quantities while an order remains in Draft status.
- **FR-018:** The system MUST allow authorized office personnel to add or remove order lines while an order remains in Draft status.
- **FR-019:** The system MUST preserve Quantity Ordered separately from Quantity Picked, Quantity Shipped, and Quantity Delivered.
- **FR-020:** The system MUST initialize Quantity Picked, Quantity Shipped, and Quantity Delivered to zero when a new Customer Order Line is created.
- **FR-021:** The system MUST maintain Customer Order statuses of Draft, Ready for Picking, Picking, Picked, Partially Picked, Shipped, Partially Shipped, Delivered, Partially Delivered, and Canceled.
- **FR-022:** A newly created Customer Order MUST initially have Draft status.
- **FR-023:** The system MUST allow authorized office personnel to save an incomplete Customer Order as Draft.
- **FR-024:** The system MUST NOT make Draft Customer Orders available for picking.
- **FR-025:** The system MUST validate required order information before releasing an order.
- **FR-026:** A Customer Order MUST have an active Customer and at least one valid Customer Order Line before it can be released.
- **FR-027:** The system MUST reject release of an order containing invalid Item references or quantities.
- **FR-028:** The system MUST allow authorized office personnel to release a valid Draft Customer Order.
- **FR-029:** The system MUST change the status of a successfully released Customer Order to Ready for Picking.
- **FR-030:** The system MUST record the date and time an order is released for picking.
- **FR-031:** The system MUST make Ready for Picking orders available to Feature 13.
- **FR-032:** The system MUST preserve the Customer, Items, and original Quantity Ordered after an order is released.
- **FR-033:** The system MUST prevent ordinary editing of released Quantity Ordered while picking or later fulfillment activities are in progress.
- **FR-034:** The system MUST maintain an optional reference to a Customer Order Form used to prepare the order.
- **FR-035:** The system MUST allow a Customer Order to be entered without selecting a Customer Order Form.
- **FR-036:** When a Customer Order Form is selected, the system MUST copy applicable default Customer and Item information into the draft order.
- **FR-037:** The system MUST allow authorized office personnel to review and adjust copied quantities before releasing the order.
- **FR-038:** Changes to a Customer Order Form MUST NOT automatically modify previously created Customer Orders.
- **FR-039:** The system MUST allow authorized personnel to retrieve Customer Orders by Customer Order Number.
- **FR-040:** The system MUST display the Customer, ordered Items, Quantity Ordered, and current order status when an order is retrieved.
- **FR-041:** The system MUST reject attempts to retrieve or modify nonexistent Customer Orders.
- **FR-042:** The system MUST prevent unauthorized users from creating, editing, or releasing Customer Orders.
- **FR-043:** Warehouse pickers and drivers MUST NOT modify the original Customer Order entry information through this feature.
- **FR-044:** The system MUST preserve released Customer Orders for picking, shipping, delivery, and reporting.
- **FR-045:** The system MUST maintain relationships between Customer Orders, Customers, Individual Items, Customer Order Forms, and Users.
- **FR-046:** The system MUST keep Customer Order entry separate from the picking process.
- **FR-047:** The system MUST keep Customer Order entry separate from shipping and delivery.
- **FR-048:** The system MUST allow authorized Managers to cancel a Draft or Ready for Picking order that has not begun fulfillment.
- **FR-049:** The system MUST preserve canceled Customer Orders for historical reference.
- **FR-050:** Canceled Customer Orders MUST NOT be available for new picking assignments.

---

## Assumptions

- **A-001:** Customer Orders are entered by authorized Customer Service Clerks or Managers.
- **A-002:** Customers are maintained through Feature 6.
- **A-003:** Individual Items are maintained through Feature 4.
- **A-004:** Customer Order Forms are maintained through Feature 8.
- **A-005:** Customer Order entry is separate from picking, shipping, and delivery.
- **A-006:** Each Customer Order has a unique system-generated identifier and a unique Order Number.
- **A-007:** Each Customer Order belongs to an existing Customer.
- **A-008:** Only orders for active Customers may be released for picking.
- **A-009:** A Customer Order may contain multiple Individual Items.
- **A-010:** Each Individual Item may appear only once within the same Customer Order.
- **A-011:** Quantity Ordered is expressed as a positive whole number of individual units.
- **A-012:** Inactive Individual Items cannot be added to new Customer Orders.
- **A-013:** Newly created Customer Orders begin in Draft status.
- **A-014:** Incomplete Customer Orders may be saved as Draft.
- **A-015:** Draft Customer Orders are not available for picking.
- **A-016:** Authorized office personnel may add, remove, or modify order lines while the order is Draft.
- **A-017:** An order must have an active Customer and at least one valid order line before release.
- **A-018:** A successfully released Customer Order becomes Ready for Picking.
- **A-019:** Feature 13 retrieves Customer Orders that are Ready for Picking.
- **A-020:** Quantity Ordered remains separate from Quantity Picked, Quantity Shipped, and Quantity Delivered.
- **A-021:** Quantity Picked, Quantity Shipped, and Quantity Delivered are initialized to zero for new order lines.
- **A-022:** Quantity Ordered is maintained by Feature 12, while later fulfillment quantities are updated by their respective features.
- **A-023:** Released Quantity Ordered cannot be modified through ordinary Draft editing.
- **A-024:** A Customer Order Form is optional when entering an order.
- **A-025:** Information copied from a Customer Order Form may be reviewed and adjusted before release.
- **A-026:** Later changes to a Customer Order Form do not automatically modify existing Customer Orders.
- **A-027:** Authorized users can retrieve Customer Orders using their Order Numbers.
- **A-028:** Managers may cancel Draft or Ready for Picking orders before fulfillment begins.
- **A-029:** Canceled Customer Orders remain available for historical reference but cannot be picked.
- **A-030:** Warehouse Pickers and Drivers cannot modify original Customer Order entry information.
- **A-031:** Customer Order records remain available for later fulfillment and reporting.
- **A-032:** The Warehouse System provides shared authentication and role-based authorization.

---

## Edge Cases

### EC-12.1: Customer Does Not Exist

**Condition:** An authorized user selects a Customer identifier that does not exist.

**Expected Behavior:**
- The system rejects the invalid Customer reference.
- The system does not create an order associated with a nonexistent Customer.
- The user receives an appropriate validation message.

### EC-12.2: Customer Becomes Inactive

**Condition:** A Customer is inactive when an existing Draft order is submitted for release.

**Expected Behavior:**
- The system prevents release.
- The order remains in Draft status.
- The order is not made available to Feature 13.

### EC-12.3: No Order Lines

**Condition:** A user attempts to release a Customer Order containing no order lines.

**Expected Behavior:**
- The system rejects release.
- The order remains in Draft status.
- The user is informed that at least one valid order line is required.

### EC-12.4: Invalid Individual Item

**Condition:** A user attempts to add an Individual Item that does not exist.

**Expected Behavior:**
- The system rejects the order line.
- No invalid Item reference is stored.

### EC-12.5: Inactive Individual Item

**Condition:** A user attempts to add an inactive Individual Item to a new order.

**Expected Behavior:**
- The system rejects the addition.
- The existing Draft order remains available for correction.

### EC-12.6: Invalid Quantity Ordered

**Condition:** A user enters zero, a negative quantity, or a non-integer quantity.

**Expected Behavior:**
- The system rejects the invalid quantity.
- The user must provide a positive whole number before the order line is valid.

### EC-12.7: Duplicate Item on the Same Order

**Condition:** A user attempts to add the same Individual Item to an order more than once.

**Expected Behavior:**
- The system prevents the duplicate Customer Order Line.
- The existing order line remains unchanged unless the user explicitly edits it.

### EC-12.8: Incomplete Draft Order

**Condition:** A user has not finished entering all required order information.

**Expected Behavior:**
- The system allows the available information to be saved as Draft.
- The order is not available for picking.
- The user may return to complete the order.

### EC-12.9: Attempt to Edit Released Quantity Ordered

**Condition:** A user attempts ordinary Draft editing after the Customer Order has been released.

**Expected Behavior:**
- The system rejects changes to the released Quantity Ordered.
- The original order information is preserved.
- Any exceptional post-release correction process requires separate authorization and design clarification.

### EC-12.10: Nonexistent Customer Order Number

**Condition:** A user searches for a Customer Order Number that does not exist.

**Expected Behavior:**
- The system reports that no matching order was found.
- No Customer Order is created or modified.

### EC-12.11: Unauthorized User

**Condition:** A Picker, Driver, or other unauthorized user attempts to create, edit, release, or cancel a Customer Order.

**Expected Behavior:**
- The system denies the unauthorized operation.
- Customer Order information remains unchanged.

### EC-12.12: Customer Order Form Is Not Selected

**Condition:** A user creates a Customer Order without choosing a Customer Order Form.

**Expected Behavior:**
- The system permits manual order entry.
- The user may select the Customer and enter order lines directly.
- The order must still pass release validation.

### EC-12.13: Customer Order Form Changes After Copying

**Condition:** A Customer Order Form is modified after a Customer Order has already been created from it.

**Expected Behavior:**
- The existing Customer Order retains its recorded information.
- Form changes do not automatically overwrite order lines or quantities.

### EC-12.14: Cancellation Before Fulfillment

**Condition:** A Manager cancels a Draft or Ready for Picking Customer Order before fulfillment begins.

**Expected Behavior:**
- The system changes the order status to Canceled.
- The order is excluded from new picking assignments.
- The canceled order remains available for historical reference.

### EC-12.15: Cancellation After Fulfillment Starts

**Condition:** A Manager attempts to cancel an order after picking has begun.

**Expected Behavior:**
- The system rejects cancellation through the ordinary pre-fulfillment cancellation operation.
- Existing picking and fulfillment records are preserved.
- **[NEEDS CLARIFICATION]** Define the authorized workflow for canceling or stopping an order after fulfillment begins.

### EC-12.16: Simultaneous Draft Updates

**Condition:** Two authorized users attempt to modify the same Draft Customer Order at approximately the same time.

**Expected Behavior:**
- The system must not silently overwrite valid changes.
- **[NEEDS CLARIFICATION]** Confirm whether optimistic version checking or another concurrency-control method will be used.

### EC-12.17: Repeated Release Request

**Condition:** The system receives a repeated release request for an order that is already Ready for Picking.

**Expected Behavior:**
- The system must not create duplicate picking work or duplicate Customer Orders.
- **[NEEDS CLARIFICATION]** Confirm whether repeated release requests return the existing released state or a validation error.

### EC-12.18: Customer Order Form Contains Invalid Defaults

**Condition:** A selected Customer Order Form references an Item that is inactive or no longer exists.

**Expected Behavior:**
- The system must not release an order containing invalid Item references.
- The user must resolve invalid copied information before release.
- **[NEEDS CLARIFICATION]** Confirm whether invalid template lines are skipped during copying or shown for correction.

---

## Success Criteria

- **SC-001:** Authorized Customer Service Clerks and Managers can create Customer Orders associated with existing Customers.
- **SC-002:** Every saved Customer Order has a unique Customer Order ID and Order Number.
- **SC-003:** The system records the creation date, time, and creating User.
- **SC-004:** Customer Orders support multiple valid Individual Items and their requested quantities.
- **SC-005:** Every Customer Order Line records Quantity Ordered as a positive whole number of individual units.
- **SC-006:** The system rejects nonexistent or inactive Items when they are added to new orders.
- **SC-007:** The system prevents duplicate Item lines within the same Customer Order.
- **SC-008:** New Customer Order Lines initialize Quantity Picked, Quantity Shipped, and Quantity Delivered to zero.
- **SC-009:** Incomplete Customer Orders can be saved and retrieved in Draft status.
- **SC-010:** Draft orders remain unavailable to the picking process.
- **SC-011:** Authorized office personnel can update order lines and quantities while an order is Draft.
- **SC-012:** Orders without an active Customer or at least one valid order line cannot be released.
- **SC-013:** Valid Draft Customer Orders can be released successfully.
- **SC-014:** Successfully released orders change to Ready for Picking and record a release timestamp.
- **SC-015:** Feature 13 can identify Customer Orders that are Ready for Picking.
- **SC-016:** Original Quantity Ordered is preserved separately from fulfillment quantities.
- **SC-017:** Ordinary Draft editing cannot change released Quantity Ordered.
- **SC-018:** Customer Orders can be created with or without an optional Customer Order Form.
- **SC-019:** Copied Customer Order Form information can be reviewed and adjusted before release.
- **SC-020:** Changes to Customer Order Forms do not automatically alter previously created Customer Orders.
- **SC-021:** Authorized users can retrieve orders by Customer Order Number and review Customer, Items, quantities, and status.
- **SC-022:** Unauthorized users cannot create, edit, release, or cancel Customer Orders.
- **SC-023:** Managers can cancel eligible Draft or Ready for Picking orders before fulfillment begins.
- **SC-024:** Canceled orders are retained for history and excluded from new picking assignments.
- **SC-025:** Customer Order entry remains separate from picking, shipping, and delivery operations.
- **SC-026:** All original 24 Gherkin acceptance scenarios are retained and can be used to verify the corresponding behaviors.
- **SC-027:** Customer Order data remains available for subsequent fulfillment processes and reporting.

---

## Key Entities

### Customer Order

Represents an order received from a retail store Customer.

Each Customer Order has a unique Order Number, Customer, creation date, status, and associated order lines.

### Customer Order Line

Represents an Individual Item requested on a Customer Order.

Each line maintains Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered as separate values.

### Customer

Represents a retail store or business that purchases products from the warehouse.

Customer information is maintained in Feature 6.

### Individual Item

Represents a product requested by a Customer.

Individual Item information is maintained in Feature 4.

### Customer Order Form

Represents an optional reusable template used when preparing a Customer Order.

Customer Order Forms are maintained in Feature 8.

### User

Represents an authenticated employee whose role determines whether Customer Orders can be created, updated, released, or reviewed.

---

## Initial Data Model

### Customer Order

| Attribute | Type | Description |
|---|---|---|
| customerOrderId | Integer | Unique, system-generated Customer Order identifier |
| orderNumber | String | Unique Customer Order Number |
| customerId | Integer | Foreign key referencing Customer |
| sourceFormId | Integer | Optional foreign key referencing Customer Order Form |
| createdAt | DateTime | Date and time the order was created |
| releasedAt | DateTime | Date and time the order was released for picking |
| createdBy | Integer | User who created the order |
| status | String | Current Customer Order status |

**Proposed Status Values:**
- Draft
- Ready for Picking
- Picking
- Picked
- Partially Picked
- Shipped
- Partially Shipped
- Delivered
- Partially Delivered
- Canceled

**Relationships:**
- Each Customer Order belongs to one Customer.
- Each Customer Order contains one or more Customer Order Lines before release.
- A Customer Order may reference a Customer Order Form.
- Each Customer Order is created by a User.
- Released Customer Orders are available to the picking process.

**Constraints:**
- customerOrderId must be unique.
- orderNumber must be unique and nonempty.
- customerId must reference an existing Customer.
- A Customer must be active before a new order can be released.
- A released Customer Order must contain at least one valid order line.
- Canceled orders cannot be released for picking.

### Customer Order Line

| Attribute | Type | Description |
|---|---|---|
| customerOrderLineId | Integer | Unique Customer Order Line identifier |
| customerOrderId | Integer | Foreign key referencing Customer Order |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityOrdered | Integer | Quantity requested by the Customer |
| quantityPicked | Integer | Quantity physically picked |
| quantityShipped | Integer | Quantity shipped to the Customer |
| quantityDelivered | Integer | Quantity confirmed delivered |
| sellingPrice | Decimal | Selling price per individual unit recorded for the order |

**Relationships:**
- Each Customer Order Line belongs to one Customer Order.
- Each Customer Order Line references one Individual Item.
- One Individual Item may appear on multiple Customer Orders.

**Constraints:**
- quantityOrdered must be a positive integer before order release.
- quantityPicked cannot be negative.
- quantityShipped cannot be negative.
- quantityDelivered cannot be negative.
- The combination of customerOrderId and itemId must be unique.
- Quantity Ordered remains unchanged during ordinary picking, shipping, and delivery operations.

**Quantity Responsibilities:**
- Quantity Ordered is recorded in Feature 12.
- Quantity Picked is updated in Feature 13.
- Quantity Shipped is updated in Feature 14.
- Quantity Delivered is updated in Feature 15.

### Customer

| Attribute | Type | Description |
|---|---|---|
| customerId | Integer | Unique Customer identifier |
| customerNumber | String | Unique Customer Number |
| name | String | Customer business name |
| deliveryAddress | String | Customer delivery address |
| isActive | Boolean | Indicates whether the Customer is active |

**Relationships:**
- One Customer can have multiple Customer Orders.
- Customer maintenance is defined in Feature 6.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |
| sellingPrice | Decimal | Current selling price per individual unit |
| isActive | Boolean | Indicates whether the Item is active |

**Relationships:**
- One Individual Item can appear on multiple Customer Order Lines.
- Individual Item maintenance is defined in Feature 4.

### Customer Order Form

| Attribute | Type | Description |
|---|---|---|
| formId | Integer | Unique Customer Order Form identifier |
| customerId | Integer | Foreign key referencing Customer |
| isActive | Boolean | Indicates whether the Form is active |

**Relationships:**
- A Customer Order may reference a Customer Order Form.
- Customer Order Form maintenance is defined in Feature 8.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Customer Service Clerks and Managers enter Customer Orders.
- Managers may cancel eligible Customer Orders.
- Warehouse workers access released orders through later fulfillment features.

---

## Gherkin Acceptance Criteria

### US-12.1: Record Customer Order

#### AC-12.1.1: Successfully create Customer Order

**Given** an active Customer exists  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user creates a new Customer Order for that Customer  
**Then** the system creates the Customer Order  
**And** assigns a unique Customer Order ID and Order Number  
**And** associates the order with the selected Customer  
**And** sets the status to Draft.

#### AC-12.1.2: Reject nonexistent Customer

**Given** the selected Customer does not exist  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user attempts to create a Customer Order for that Customer  
**Then** the system rejects the request  
**And** does not create a Customer Order with an invalid Customer reference.

#### AC-12.1.3: Reject inactive Customer at release

**Given** a Draft Customer Order references an inactive Customer  
**And** the user is authenticated as a Manager  
**When** the user attempts to release the order  
**Then** the system rejects the release  
**And** the order remains unavailable for picking.

#### AC-12.1.4: Reject unauthorized order creation

**Given** the user is authenticated as a Driver  
**When** the user attempts to create a Customer Order  
**Then** the system denies the operation  
**And** no Customer Order is created.

### US-12.2: Record Ordered Items and Quantities

#### AC-12.2.1: Add Item to Customer Order

**Given** a Draft Customer Order exists  
**And** an active Individual Item exists  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user adds the Item with Quantity Ordered of 20 units  
**Then** the system records the Item and Quantity Ordered of 20  
**And** initializes Quantity Picked, Quantity Shipped, and Quantity Delivered to zero.

#### AC-12.2.2: Record multiple Items

**Given** a Draft Customer Order exists  
**And** two active Individual Items exist  
**When** the authorized user adds 12 units of Item A and 24 units of Item B  
**Then** the system records a separate Customer Order Line for each Item  
**And** preserves the corresponding Quantity Ordered for each line.

#### AC-12.2.3: Reject nonexistent Item

**Given** a Draft Customer Order exists  
**When** the user attempts to add an Individual Item that does not exist  
**Then** the system rejects the order line  
**And** does not save an invalid Item reference.

#### AC-12.2.4: Reject inactive Item

**Given** a Draft Customer Order exists  
**And** an Individual Item is inactive  
**When** the user attempts to add that Item  
**Then** the system rejects the request  
**And** does not create the order line.

#### AC-12.2.5: Reject zero Quantity Ordered

**Given** a Draft Customer Order exists  
**And** an active Individual Item is selected  
**When** the user enters Quantity Ordered of zero  
**Then** the system rejects the quantity  
**And** does not save the invalid order line.

#### AC-12.2.6: Reject negative Quantity Ordered

**Given** a Draft Customer Order exists  
**And** an active Individual Item is selected  
**When** the user enters Quantity Ordered of -5  
**Then** the system rejects the quantity  
**And** does not save the invalid order line.

#### AC-12.2.7: Prevent duplicate Item lines

**Given** a Draft Customer Order already contains Item A  
**When** the user attempts to add another order line for Item A  
**Then** the system rejects the duplicate line  
**And** preserves the existing Item A order line.

#### AC-12.2.8: Preserve separate quantities

**Given** a Customer Order Line contains 30 units ordered  
**When** the Customer Order is saved  
**Then** Quantity Ordered remains 30  
**And** Quantity Picked is zero  
**And** Quantity Shipped is zero  
**And** Quantity Delivered is zero.

### US-12.3: Make Customer Order Available for Picking

#### AC-12.3.1: Successfully release Customer Order

**Given** a Draft Customer Order exists  
**And** it references an active Customer  
**And** it contains at least one valid order line  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user releases the Customer Order  
**Then** the system changes its status to Ready for Picking  
**And** records the release date and time  
**And** makes the order available to Feature 13.

#### AC-12.3.2: Reject order without Items

**Given** a Draft Customer Order exists without any order lines  
**When** the user attempts to release the order  
**Then** the system rejects the release  
**And** the order remains in Draft status.

#### AC-12.3.3: Reject order with invalid Item quantity

**Given** a Draft Customer Order contains an invalid Quantity Ordered  
**When** the user attempts to release the order  
**Then** the system rejects the release  
**And** identifies the invalid quantity  
**And** does not make the order available for picking.

#### AC-12.3.4: Keep Draft order unavailable for picking

**Given** a Customer Order exists in Draft status  
**When** a Picker requests orders ready for picking  
**Then** the Draft Customer Order is not included in the available picking work.

#### AC-12.3.5: Preserve Quantity Ordered for picking

**Given** a Customer Order has been released with 40 units of Item A ordered  
**When** a Picker retrieves the order in Feature 13  
**Then** the system displays 40 units as Quantity Ordered  
**And** preserves the original ordered quantity separately from Quantity Picked.

### US-12.4: Save and Update Draft Customer Order

#### AC-12.4.1: Save incomplete Draft order

**Given** an authorized Customer Service Clerk is entering a Customer Order  
**And** the order does not yet contain all required order lines  
**When** the Clerk saves the order as Draft  
**Then** the system preserves the available order information  
**And** keeps the status as Draft  
**And** does not release the order for picking.

#### AC-12.4.2: Update Draft order

**Given** a Draft Customer Order exists  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user adds a valid Item and Quantity Ordered  
**And** saves the changes  
**Then** the system updates the Draft Customer Order  
**And** preserves its Order Number.

#### AC-12.4.3: Prevent ordinary editing after release

**Given** a Customer Order has been released for picking  
**When** a Customer Service Clerk attempts to change the original Quantity Ordered through ordinary Draft editing  
**Then** the system rejects the change  
**And** preserves the released order information.

#### AC-12.4.4: Cancel eligible Customer Order

**Given** a Customer Order is in Ready for Picking status  
**And** picking has not started  
**And** the user is authenticated as a Manager  
**When** the Manager cancels the order  
**Then** the system changes the status to Canceled  
**And** removes the order from available picking work  
**And** preserves the order history.

### US-12.5: Review Customer Order Information

#### AC-12.5.1: Retrieve Customer Order by Order Number

**Given** a Customer Order exists with Order Number "CO1001"  
**And** the user is authorized to review Customer Orders  
**When** the user searches for "CO1001"  
**Then** the system displays the matching Customer Order  
**And** shows the Customer, Items, Quantity Ordered, and current status.

#### AC-12.5.2: Reject nonexistent Order Number

**Given** no Customer Order exists with Order Number "CO9999"  
**When** an authorized user searches for "CO9999"  
**Then** the system reports that no matching Customer Order exists  
**And** does not create or modify any Customer Order.

#### AC-12.5.3: Display separate fulfillment quantities

**Given** a Customer Order Line contains 50 units ordered  
**And** 45 units have been picked  
**And** 40 units have been shipped  
**And** 38 units have been confirmed delivered  
**When** an authorized user reviews the Customer Order  
**Then** the system displays Quantity Ordered as 50  
**And** Quantity Picked as 45  
**And** Quantity Shipped as 40  
**And** Quantity Delivered as 38.

---

## Data Ownership

### Feature 12 — Receive Customer Orders

Feature 12 owns the creation, maintenance, validation, release, and eligible cancellation of Customer Orders.

**Owned Data:**
- Customer Order
- Customer Order Line
- Customer Order ID
- Customer Order Number
- Customer association on the order
- Source Customer Order Form reference
- Quantity Ordered
- Order creation timestamp
- Order release timestamp
- Creating User reference
- Draft order details
- Initial Customer Order status

**Responsibilities:**
- Create Customer Orders in Draft status.
- Add, update, and remove valid Customer Order Lines while the order is Draft.
- Validate Customer and Item references.
- Validate Quantity Ordered.
- Prevent duplicate Item lines.
- Release valid Customer Orders for picking.
- Preserve original ordered quantities after release.
- Allow authorized Managers to cancel eligible orders before fulfillment begins.
- Preserve Customer Order history.
- Provide order information to later fulfillment features.

### Feature 6 — Maintain Customers

**Owned Data:**
- Customer ID
- Customer Number
- Customer name
- Delivery address
- Customer active status

**Feature 12 Responsibilities:**
- Reference existing Customers.
- Validate Customer existence.
- Check Customer active status before release.
- Never directly modify Customer master data.

### Feature 4 — Maintain Individual Items

**Owned Data:**
- Individual Item ID
- Item Number
- Item description
- Current Item selling price
- Item active status

**Feature 12 Responsibilities:**
- Reference existing Individual Items.
- Validate Item existence and active status.
- Record the Item and Quantity Ordered on each Customer Order Line.
- Preserve the selling price recorded for the order, where applicable.
- Never directly modify Item master data.

### Feature 8 — Maintain Customer Order Forms

**Owned Data:**
- Customer Order Form ID
- Form Customer association
- Form active status
- Reusable Customer Order Form details and defaults

**Feature 12 Responsibilities:**
- Optionally reference a Customer Order Form.
- Copy applicable Customer and Item information into a new Draft order.
- Allow authorized users to adjust copied quantities before release.
- Keep previously created Customer Orders independent of later Form changes.
- Never directly modify Customer Order Form master data.

### Feature 13 — Pick Customer Orders

**Responsibilities:**
- Retrieve Customer Orders released by Feature 12.
- Perform picking activities.
- Record Quantity Picked.
- Maintain picking-related progress and status.

**Feature 12 Responsibilities:**
- Make Ready for Picking orders available to Feature 13.
- Preserve Quantity Ordered.
- Prevent ordinary Draft editing after release.

### Feature 14 — Ship Customer Orders

**Responsibilities:**
- Process Customer Orders through shipping.
- Record Quantity Shipped.
- Maintain shipping-related progress and status.

**Feature 12 Responsibilities:**
- Preserve original Customer Order information.
- Allow authorized users to review shipping quantities and status.

### Feature 15 — Deliver Customer Orders

**Responsibilities:**
- Record Customer Order delivery progress.
- Record Quantity Delivered.
- Maintain delivery-related status.

**Feature 12 Responsibilities:**
- Preserve original Customer Order information.
- Allow authorized users to review delivery quantities and status.

### Shared Authentication and Authorization

**Owned Data:**
- User ID
- User authentication information
- Assigned role
- Authorization permissions

**Feature 12 Responsibilities:**
- Require authentication for Customer Order operations.
- Permit Customer Service Clerks and Managers to create, edit, and release orders.
- Restrict eligible cancellation to Managers.
- Prevent unauthorized changes by Pickers, Drivers, and other roles.

### Cross-Feature Data Rules

- Customer Order and Customer Order Line records are maintained by Feature 12.
- Customer and Item master records remain owned by their respective maintenance features.
- Quantity Ordered is established by Feature 12.
- Quantity Picked is updated through Feature 13.
- Quantity Shipped is updated through Feature 14.
- Quantity Delivered is updated through Feature 15.
- Original Quantity Ordered must not be overwritten by fulfillment quantities.
- Released and canceled Customer Orders must remain available for historical reference.
- Fulfillment features must not modify the original Customer Order through ordinary Draft editing.

**[NEEDS CLARIFICATION]** Confirm whether later fulfillment features update their quantity and status fields directly through a shared Customer Order service or through dedicated feature APIs.

**[NEEDS CLARIFICATION]** Confirm the complete Customer Order status transition rules when an order is partially picked, shipped, or delivered.

---

## API Requirements

### API-12.1: Create Customer Order

**Endpoint:** `POST /api/customer-orders`

**Purpose:** Create a new Customer Order in Draft status.

**Authorized Roles:**
- Customer Service Clerk
- Manager

**Request Data:**
- customerId
- sourceFormId (optional)

**System-Generated Data:**
- customerOrderId
- orderNumber
- createdAt
- createdBy
- status = Draft

**Validation and Behavior:**
- Require an authenticated, authorized user.
- Validate that the selected Customer exists.
- Generate a unique Customer Order ID and Order Number.
- Record the creating User and creation timestamp.
- Create the Customer Order in Draft status.
- If a Customer Order Form is selected, copy applicable defaults into the Draft order.
- Do not release the order automatically.

**Successful Response:**
- Created Customer Order ID
- Order Number
- Customer reference
- Draft status
- Creation timestamp

**Error Conditions:**
- Unauthorized user
- Nonexistent Customer
- Invalid Customer Order Form reference
- Invalid request data
- Internal processing failure

### API-12.2: Retrieve Customer Order

**Endpoint:** `GET /api/customer-orders/{customerOrderId}`

**Purpose:** Retrieve a Customer Order and its recorded details.

**Authorized Roles:**
- Authorized office personnel
- Other authenticated roles with approved read permissions

**Response Data:**
- Customer Order ID
- Order Number
- Customer information
- Source Form reference, if applicable
- Creation and release timestamps
- Current status
- Customer Order Lines
- Quantity Ordered
- Quantity Picked
- Quantity Shipped
- Quantity Delivered
- Recorded selling prices, where applicable

**Validation and Behavior:**
- Verify that the requesting user has permission to view the order.
- Return the requested Customer Order if it exists.
- Preserve all stored information during retrieval.
- Do not modify the order.

**Error Conditions:**
- Unauthorized access
- Customer Order not found

### API-12.3: Find Customer Order by Order Number

**Endpoint:** `GET /api/customer-orders?orderNumber={orderNumber}`

**Purpose:** Retrieve a Customer Order using its unique Order Number.

**Authorized Roles:**
- Authorized office personnel
- Other authenticated roles with approved read permissions

**Validation and Behavior:**
- Validate the supplied Order Number.
- Search for the matching Customer Order.
- Return its Customer, Items, quantities, and status.
- Do not create or modify an order during lookup.

**Error Conditions:**
- Missing or invalid Order Number
- No matching Customer Order
- Unauthorized access

### API-12.4: Update Draft Customer Order

**Endpoint:** `PATCH /api/customer-orders/{customerOrderId}`

**Purpose:** Update permitted Customer Order information while the order remains Draft.

**Authorized Roles:**
- Customer Service Clerk
- Manager

**Request Data:**
- customerId, if a Customer change is permitted
- sourceFormId, if applicable
- Other permitted Draft header information

**Validation and Behavior:**
- Verify authorization.
- Confirm that the Customer Order exists.
- Require Draft status.
- Validate any updated Customer reference.
- Preserve the Customer Order ID and Order Number.
- Do not modify fulfillment quantities.
- Reject ordinary Draft updates after release or cancellation.

**Error Conditions:**
- Unauthorized user
- Customer Order not found
- Invalid Customer reference
- Order is not Draft
- Invalid request data

**[NEEDS CLARIFICATION]** Confirm whether changing the Customer on an existing Draft order is permitted after order lines have been entered.

### API-12.5: Add Customer Order Line

**Endpoint:** `POST /api/customer-orders/{customerOrderId}/lines`

**Purpose:** Add an Individual Item and Quantity Ordered to a Draft Customer Order.

**Authorized Roles:**
- Customer Service Clerk
- Manager

**Request Data:**
- itemId
- quantityOrdered

**Validation and Behavior:**
- Confirm the order exists and remains Draft.
- Validate the Item exists and is active.
- Require a positive whole-number Quantity Ordered.
- Prevent duplicate Item lines within the same order.
- Initialize Quantity Picked, Quantity Shipped, and Quantity Delivered to zero.
- Record the applicable selling price if required by the approved pricing design.

**Successful Response:**
- Customer Order Line ID
- Item reference
- Quantity Ordered
- Initial fulfillment quantities

**Error Conditions:**
- Unauthorized user
- Order not found
- Order is not Draft
- Item not found
- Inactive Item
- Invalid quantity
- Duplicate Item line

### API-12.6: Update Customer Order Line

**Endpoint:** `PATCH /api/customer-orders/{customerOrderId}/lines/{customerOrderLineId}`

**Purpose:** Update Quantity Ordered on an existing Draft order line.

**Authorized Roles:**
- Customer Service Clerk
- Manager

**Request Data:**
- quantityOrdered

**Validation and Behavior:**
- Confirm the order and line exist.
- Require Draft status.
- Require a positive whole-number Quantity Ordered.
- Preserve the associated Item unless an approved replacement workflow exists.
- Do not change fulfillment quantities.
- Reject updates after the order has been released or canceled.

**Error Conditions:**
- Unauthorized user
- Order or line not found
- Order is not Draft
- Invalid quantity

### API-12.7: Remove Customer Order Line

**Endpoint:** `DELETE /api/customer-orders/{customerOrderId}/lines/{customerOrderLineId}`

**Purpose:** Remove an Item line from a Draft Customer Order.

**Authorized Roles:**
- Customer Service Clerk
- Manager

**Validation and Behavior:**
- Confirm the order and line exist.
- Require Draft status.
- Remove the selected line from the Draft order.
- Preserve the Customer Order header.
- Allow the Draft order to contain no lines until release.
- Reject removal after release or cancellation.

**Error Conditions:**
- Unauthorized user
- Order or line not found
- Order is not Draft

### API-12.8: Release Customer Order

**Endpoint:** `POST /api/customer-orders/{customerOrderId}/release`

**Purpose:** Validate and release a completed Draft Customer Order for picking.

**Authorized Roles:**
- Customer Service Clerk
- Manager

**Validation and Behavior:**
- Confirm the Customer Order exists.
- Require Draft status.
- Confirm the associated Customer exists and is active.
- Require at least one valid Customer Order Line.
- Confirm every Item exists and is active.
- Confirm every Quantity Ordered is a positive whole number.
- Confirm that no duplicate Item lines exist.
- Change the order status to Ready for Picking.
- Record the release timestamp.
- Make the order available to Feature 13.
- Preserve the original Customer, Items, and Quantity Ordered.
- Ensure a repeated request does not create duplicate picking work.

**Successful Response:**
- Customer Order ID
- Order Number
- Ready for Picking status
- Release timestamp

**Error Conditions:**
- Unauthorized user
- Order not found
- Order is not Draft
- Inactive or nonexistent Customer
- Missing order lines
- Invalid Item reference
- Invalid Quantity Ordered

### API-12.9: Cancel Customer Order

**Endpoint:** `POST /api/customer-orders/{customerOrderId}/cancel`

**Purpose:** Cancel an eligible Customer Order before fulfillment begins.

**Authorized Role:**
- Manager

**Validation and Behavior:**
- Confirm the Customer Order exists.
- Permit cancellation only when the order is Draft or Ready for Picking.
- Confirm that fulfillment has not started.
- Change the status to Canceled.
- Remove the order from available picking work.
- Preserve the order and its lines for historical reference.
- Reject cancellation through this operation after picking has begun.

**Successful Response:**
- Customer Order ID
- Canceled status

**Error Conditions:**
- Unauthorized user
- Order not found
- Order is not eligible for cancellation
- Fulfillment has already started

### API-12.10: Retrieve Orders Ready for Picking

**Endpoint:** `GET /api/customer-orders?status=Ready%20for%20Picking`

**Purpose:** Provide released Customer Orders to the picking process in Feature 13.

**Authorized Roles:**
- Authorized picking personnel
- Managers
- Other roles with approved read permissions

**Response Data:**
- Customer Order ID
- Order Number
- Customer reference
- Order lines
- Individual Item references
- Quantity Ordered
- Current order status

**Validation and Behavior:**
- Return only orders eligible for picking.
- Exclude Draft and Canceled orders.
- Preserve Quantity Ordered.
- Do not assign picking work or modify inventory through this endpoint.

**Error Conditions:**
- Unauthorized access
- Invalid query parameters

### API-12.11: Apply Customer Order Form to Draft

**Endpoint:** `POST /api/customer-orders/{customerOrderId}/apply-form`

**Purpose:** Copy applicable Customer Order Form information into an existing Draft order.

**Authorized Roles:**
- Customer Service Clerk
- Manager

**Request Data:**
- sourceFormId

**Validation and Behavior:**
- Confirm the Customer Order exists and is Draft.
- Confirm the Customer Order Form exists.
- Validate applicable copied Customer and Item references.
- Copy permitted default information into the Draft order.
- Allow the user to review and adjust quantities before release.
- Preserve the source Form reference.
- Do not change the original Customer Order Form.
- Do not automatically release the Customer Order.

**Error Conditions:**
- Unauthorized user
- Order not found
- Order is not Draft
- Form not found
- Invalid copied information

**[NEEDS CLARIFICATION]** Define whether applying a Form replaces existing Draft lines, merges them, or requires an empty Draft order.

### API-12.12: Retrieve Customer Orders by Customer

**Endpoint:** `GET /api/customer-orders?customerId={customerId}`

**Purpose:** Allow authorized users to review Customer Orders associated with a Customer.

**Authorized Roles:**
- Customer Service Clerk
- Manager
- Other roles with approved read permissions

**Validation and Behavior:**
- Validate the Customer reference.
- Return matching Customer Orders.
- Include Order Number, creation date, and status in the results.
- Do not modify Customer Order data.

**Error Conditions:**
- Unauthorized access
- Invalid Customer reference

### General API Requirements

- All write operations MUST enforce server-side authorization.
- Customer Order IDs and Order Numbers MUST remain unique.
- All references to Customers, Items, Forms, and Users MUST be validated.
- Draft-only operations MUST reject orders that are no longer Draft.
- Release and cancellation operations MUST enforce permitted status transitions.
- API errors MUST provide meaningful validation information without exposing sensitive system details.
- Database operations MUST preserve referential integrity.
- Repeated requests MUST NOT create duplicate Customer Orders, order lines, or picking work unintentionally.
- Customer Order data MUST remain consistent when concurrent requests occur.
- API responses MUST preserve the separation between ordered and fulfillment quantities.
- The API MUST NOT allow Feature 12 users to directly alter Quantity Picked, Quantity Shipped, or Quantity Delivered.

**[NEEDS CLARIFICATION]** Confirm the final API naming conventions, pagination rules, audit requirements, and concurrency-control approach during architecture approval.

---

## Screen Requirements

### SCREEN-12.1: Customer Order List

**Purpose:** Allow authorized office personnel to find, review, and open Customer Orders.

**Authorized Users:**
- Customer Service Clerk
- Manager

**Displayed Information:**
- Order Number
- Customer Number
- Customer Name
- Creation Date
- Current Order Status
- Release Date, when applicable

**Controls:**
- Search by Order Number
- Filter by Customer
- Filter by Order Status
- Open selected Customer Order
- Create New Customer Order
- Refresh results

**Behavior:**
- Display matching Customer Orders.
- Allow authorized users to open an order for review.
- Allow creation of a new Draft Customer Order.
- Show a meaningful message when no matching orders exist.
- Prevent unauthorized users from accessing editing operations.

### SCREEN-12.2: Customer Order Entry and Edit

**Purpose:** Create and maintain Customer Orders while they are Draft.

**Authorized Users:**
- Customer Service Clerk
- Manager

**Displayed Fields:**
- Order Number (read-only, system-generated)
- Customer
- Customer Number
- Customer Order Form (optional)
- Creation Date
- Created By
- Order Status
- Individual Item
- Item Number
- Item Description
- Quantity Ordered
- Selling Price, where applicable

**Controls:**
- Select Customer
- Select Optional Customer Order Form
- Add Item
- Update Item Quantity
- Remove Item
- Save Draft
- Release for Picking
- Cancel Editing
- Return to Order List

**Behavior:**
- Create new orders in Draft status.
- Allow valid order lines to be entered and maintained.
- Reject nonexistent or inactive Items.
- Reject zero, negative, or non-integer quantities.
- Prevent duplicate Item lines.
- Allow incomplete orders to be saved as Draft.
- Validate all required information before release.
- Prevent ordinary editing of released or canceled orders.

### SCREEN-12.3: Customer Order Detail

**Purpose:** Display a Customer Order and its fulfillment progress.

**Authorized Users:**
- Customer Service Clerk
- Manager
- Other users with approved read permissions

**Displayed Information:**
- Order Number
- Customer Name and Number
- Creation Date
- Release Date
- Created By
- Current Order Status
- Item Number
- Item Description
- Quantity Ordered
- Quantity Picked
- Quantity Shipped
- Quantity Delivered
- Selling Price, where applicable

**Controls:**
- Return to Order List
- Edit Draft, when permitted
- Release Draft, when permitted
- Cancel Eligible Order, when permitted
- Refresh Order Details

**Behavior:**
- Display original Quantity Ordered separately from fulfillment quantities.
- Display current order status.
- Allow editing only when permitted.
- Preserve read-only access to released and historical order details.
- Hide or disable actions the user is not authorized to perform.

### SCREEN-12.4: Release Customer Order Confirmation

**Purpose:** Allow authorized office personnel to review a completed Draft order before releasing it for picking.

**Authorized Users:**
- Customer Service Clerk
- Manager

**Displayed Information:**
- Order Number
- Customer
- List of Individual Items
- Quantity Ordered for each Item
- Validation results
- Current status

**Controls:**
- Confirm Release
- Return to Draft
- Cancel Confirmation

**Behavior:**
- Validate the Customer and all order lines.
- Display validation errors when information is incomplete or invalid.
- Require user confirmation before release.
- Change the order to Ready for Picking after successful release.
- Display confirmation of successful release.
- Prevent repeated release from creating duplicate picking work.

### SCREEN-12.5: Cancel Customer Order Confirmation

**Purpose:** Allow a Manager to cancel an eligible Customer Order before fulfillment begins.

**Authorized User:**
- Manager

**Displayed Information:**
- Order Number
- Customer
- Current Order Status
- Eligibility for cancellation

**Controls:**
- Confirm Cancellation
- Return Without Canceling

**Behavior:**
- Permit cancellation only for Draft or Ready for Picking orders that have not begun fulfillment.
- Require confirmation before cancellation.
- Change the status to Canceled after successful cancellation.
- Preserve order history.
- Remove the canceled order from available picking work.
- Reject cancellation when fulfillment has already begun.

### General Screen Requirements

- Screens MUST use the approved Warehouse System UI style conventions.
- Screens MUST display understandable field labels and validation messages.
- Required fields MUST be identified clearly.
- Read-only fields MUST not appear editable.
- Role-based permissions MUST determine which actions are available.
- Invalid input MUST be identified before an order is released.
- Customer and Item selection MUST use existing master data.
- Order statuses MUST be displayed consistently across screens.
- Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered MUST be clearly distinguished.
- Screen behavior MUST support keyboard entry and the approved office workstation interface.
- UI validation MUST be reinforced by server-side validation.
- Screen designs MUST be documented in Figma or the approved design tool before implementation.

**[NEEDS CLARIFICATION]** Confirm whether Customer Order entry is intended for desktop office workstations only or also for handheld/mobile devices.

---

## Definition of Done

Feature 12 is considered complete when all approved requirements and acceptance criteria have been implemented and verified.

### Requirements and Design

- [ ] All approved User Stories are implemented.
- [ ] Functional Requirements FR-001 through FR-050 are satisfied.
- [ ] Assumptions and unresolved clarifications have been reviewed.
- [ ] Edge Cases have corresponding handling and verification.
- [ ] Success Criteria have been evaluated.
- [ ] Data ownership boundaries are documented and followed.
- [ ] Initial Data Model has been reviewed and approved.
- [ ] Customer Order status transitions have been approved.
- [ ] API contracts have been reviewed.
- [ ] Screen designs have been prepared and reviewed.

### Implementation

- [ ] Authorized users can create Customer Orders.
- [ ] Unique Customer Order IDs and Order Numbers are generated.
- [ ] Customer references are validated.
- [ ] Individual Item references are validated.
- [ ] Customer Order Lines can be added, updated, and removed in Draft status.
- [ ] Invalid quantities and duplicate Item lines are rejected.
- [ ] Incomplete Customer Orders can be saved as Draft.
- [ ] Valid Draft orders can be released for picking.
- [ ] Released orders become Ready for Picking.
- [ ] Feature 13 can retrieve orders available for picking.
- [ ] Quantity Ordered remains separate from fulfillment quantities.
- [ ] Original order details are protected after release.
- [ ] Optional Customer Order Form information can be copied into a Draft order.
- [ ] Customer Orders can be retrieved by Order Number.
- [ ] Authorized Managers can cancel eligible orders.
- [ ] Canceled orders are excluded from new picking assignments.
- [ ] Released and canceled order records remain available for historical reference.

### Testing and Verification

- [ ] All 24 Gherkin Acceptance Criteria have corresponding verification tests.
- [ ] Unit tests cover Customer Order validation.
- [ ] Unit tests cover order-line quantity validation.
- [ ] Unit tests cover duplicate Item prevention.
- [ ] Unit tests cover Draft editing restrictions.
- [ ] Unit tests cover release eligibility and status changes.
- [ ] Unit tests cover cancellation eligibility.
- [ ] API tests verify successful creation, retrieval, updates, release, and cancellation.
- [ ] API tests verify unauthorized access is denied.
- [ ] API tests verify invalid Customer and Item references are rejected.
- [ ] Integration tests verify Customer data from Feature 6.
- [ ] Integration tests verify Individual Item data from Feature 4.
- [ ] Integration tests verify optional Customer Order Form data from Feature 8.
- [ ] Integration tests verify released orders are available to Feature 13.
- [ ] Tests verify Quantity Ordered is preserved during later fulfillment.
- [ ] Tests verify repeated release requests do not create duplicate picking work.
- [ ] Tests verify concurrent updates do not silently overwrite valid order information.
- [ ] Regression tests confirm existing warehouse features continue to operate correctly.

### Documentation and Review

- [ ] API documentation is updated.
- [ ] Data model documentation is updated.
- [ ] Screen documentation is updated.
- [ ] Role permissions are documented.
- [ ] Customer Order status rules are documented.
- [ ] Known limitations and approved deferrals are recorded.
- [ ] Code has been reviewed.
- [ ] Required tests pass.
- [ ] The feature is approved for integration.

---

## Out of Scope

The following activities are not implemented as part of Feature 12.

### Customer Master Data Maintenance

Creating, updating, deactivating, or otherwise maintaining Customer master records belongs to Feature 6.

Feature 12 only references and validates existing Customers.

### Individual Item Master Data Maintenance

Creating, updating, deactivating, or maintaining Individual Item master records belongs to Feature 4.

Feature 12 only references and validates existing Items.

### Customer Order Form Maintenance

Creating and maintaining reusable Customer Order Forms belongs to Feature 8.

Feature 12 may use an existing Form to populate a Draft Customer Order.

### Physical Picking

Selecting warehouse locations, directing Pickers, scanning picked Items, and recording physical picking activity belong to Feature 13.

Feature 12 only releases eligible Customer Orders for picking.

### Shipping

Preparing shipments, confirming shipped quantities, and managing shipping operations belong to Feature 14.

Feature 12 preserves Customer Order information but does not perform shipping.

### Delivery

Transporting Customer Orders, confirming delivery, and recording delivered quantities belong to Feature 15.

Feature 12 does not perform delivery operations.

### Inventory Movement

Feature 12 does not directly move inventory between warehouse locations or record physical inventory movements.

Inventory changes are handled by the appropriate inventory and fulfillment features.

### Post-Release Order Corrections

Ordinary editing of Quantity Ordered after release is not supported by this feature.

**[NEEDS CLARIFICATION]** Any exceptional correction, amendment, or cancellation workflow after fulfillment begins requires a separately approved design.

### Payment and Billing Processing

Collecting Customer payments, generating invoices, processing refunds, and managing accounts receivable are not included in this feature unless separately specified.

### Automated Customer Ordering

Direct Customer self-service ordering, external e-commerce integration, and automatic electronic order import are not included in the current Feature 12 draft.

### Advanced Pricing and Discounts

Customer-specific discount agreements, promotions, tax calculation, and complex pricing rules are not defined by this feature.

The recorded selling price must follow the approved Item and pricing design.

### Advanced Fulfillment Planning

Inventory reservation, allocation optimization, picking-route generation, and shipping-route planning are outside Feature 12.

These activities belong to their respective fulfillment features.

### Final Deferrals and Clarifications

The following design decisions remain open for review:

- **[NEEDS CLARIFICATION]** Exact Customer Order status transition rules across Features 12–15.
- **[NEEDS CLARIFICATION]** Cross-feature ownership and update mechanism for fulfillment quantities and statuses.
- **[NEEDS CLARIFICATION]** Whether a Draft Customer Order may change Customers after order lines have been entered.
- **[NEEDS CLARIFICATION]** Whether applying a Customer Order Form replaces or merges existing Draft lines.
- **[NEEDS CLARIFICATION]** Handling invalid Item defaults copied from a Customer Order Form.
- **[NEEDS CLARIFICATION]** Concurrency control for simultaneous Draft updates.
- **[NEEDS CLARIFICATION]** Response behavior for repeated release requests.
- **[NEEDS CLARIFICATION]** Post-release correction and cancellation workflow.
- **[NEEDS CLARIFICATION]** Final API conventions and audit requirements.
- **[NEEDS CLARIFICATION]** Whether order entry must support mobile or handheld devices.

These decisions must be reviewed before implementation. They do not prevent Feature 12 from being maintained as a design draft.
