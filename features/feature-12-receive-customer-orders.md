
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

## Gherkin AC

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
