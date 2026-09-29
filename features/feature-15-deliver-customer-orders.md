# Feature: Deliver Customer Orders

**Feature ID:** 15  
**Branch pattern:** `feature/15-deliver-customer-orders`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system assists a driver in delivering shipped Customer Orders by identifying the orders on the delivery route, recording the Quantity Delivered, and preserving differences between what was shipped and what was actually delivered.

---

## User Stories

### US-15.1: Identify Customer Orders for Delivery

**As a** driver  
**I want to** see the Customer Orders assigned to my delivery route  
**So that** I know which orders must be delivered

**Priority:** P1  
**Independent test:** Start the delivery process and confirm that the driver can identify the Customer Orders on the delivery route.

### US-15.2: Deliver Customer Order

**As a** driver  
**I want to** deliver a shipped Customer Order to the Customer  
**So that** the Customer's order can be completed

**Priority:** P1  
**Independent test:** Select a shipped Customer Order on the route and confirm that it can be processed for delivery.

### US-15.3: Record Quantity Delivered

**As a** driver  
**I want to** record Quantity Delivered for each item  
**So that** the system knows what was actually delivered to the Customer

**Priority:** P1  
**Independent test:** Record Quantity Delivered and confirm that it remains separate from Quantity Shipped.

### US-15.4: Identify Delivery Difference

**As a** driver  
**I want to** record when Quantity Delivered differs from Quantity Shipped  
**So that** the system preserves the delivery difference for reporting

**Priority:** P1  
**Independent test:** Record a Quantity Delivered that differs from Quantity Shipped and confirm that the difference is preserved.

---

## Functional Requirements

- **FR-001:** The system MUST identify Customer Orders assigned to the driver's Delivery Route.
- **FR-002:** The system MUST allow the driver to select a Customer Order on the Delivery Route for delivery.
- **FR-003:** The system MUST provide the shipped items and Quantity Shipped for the selected Customer Order.
- **FR-004:** The system MUST allow the driver to record Quantity Delivered for each item.
- **FR-005:** The system MUST keep Quantity Delivered separate from Quantity Shipped.
- **FR-006:** The system MUST compare Quantity Delivered with Quantity Shipped.
- **FR-007:** The system MUST preserve differences between Quantity Shipped and Quantity Delivered for later reporting.
- **FR-008:** The system MUST allow delivery information to be recorded for each Customer Order on the route.
- **FR-009:** The system MUST identify when delivery of a Customer Order has been completed.
- **FR-010:** The system MUST preserve the relationship between the delivered Customer Order and its Delivery Route.
- **FR-011:** The exact behavior when Quantity Delivered differs from Quantity Shipped is **TBD**.
- **FR-012:** The exact Customer Order and Delivery status values are **TBD**.
- **FR-013:** How Customer Orders are assigned to a Delivery Route is **TBD**.
- **FR-014:** How a partially delivered Customer Order is represented is **TBD**.
- **FR-015:** Behavior when a Customer cannot receive a delivery is **TBD**.
- **FR-016:** Whether a driver can deliver a Customer Order that is not assigned to the driver's Delivery Route is **TBD**.
- **FR-017:** Whether a Customer Order that has not completed shipping can enter the delivery process is **TBD**.
- **FR-018:** The process for loading the truck and driving the route is outside the defined scope of this feature.

---

## Key Entities

- **Delivery:** The delivery of a shipped Customer Order to a Customer.
- **Delivery Item:** An Individual Item included in a Delivery with Quantity Shipped and Quantity Delivered.
- **Delivery Route:** A route used by a driver to deliver Customer Orders.
- **Customer Order:** An order that has been shipped and is being delivered to a Customer.
- **Customer Order Item:** An Individual Item on a Customer Order with quantities recorded across warehouse processes.
- **Driver:** An employee who delivers Customer Orders.
- **Individual Item:** A product included in a Customer Order and Delivery.

---

## Initial Data Model

### Delivery

Represents the delivery of a shipped Customer Order to a Customer.

**Attributes:**
- [TBD: Delivery identifier]
- Status [exact values TBD]

**Relationships:**
- A Delivery is associated with a Customer Order.
- A Delivery is associated with a Delivery Route.
- A Delivery contains one or more Delivery Items.
- A Driver performs the Delivery.

### Delivery Item

Represents an Individual Item included in a Delivery.

**Attributes:**
- Individual Item
- Quantity Shipped
- Quantity Delivered

**Relationships:**
- A Delivery contains one or more Delivery Items.
- Each Delivery Item refers to an Individual Item.
- Quantity Delivered is compared with Quantity Shipped.
- Differences between Quantity Shipped and Quantity Delivered are preserved for reporting.

### Delivery Route

Represents a route used by a Driver to deliver Customer Orders.

**Relevant Attributes:**
- [TBD: Route identifier]

**Relationships:**
- A Delivery Route is associated with a Driver.
- A Delivery Route contains Customers and Customer Orders to be delivered.
- A Delivery is associated with a Delivery Route.

### Customer Order

Represents an order being delivered to a Customer.

**Relevant Attributes:**
- [TBD: Customer Order identifier]
- Status [exact values TBD]

**Relationships:**
- A Customer Order is associated with a Customer.
- A Customer Order is shipped before delivery.
- A Customer Order may have a Delivery.
- A Customer Order contains one or more Customer Order Items.

### Customer Order Item

Represents an Individual Item included in a Customer Order.

**Relevant Attributes:**
- Individual Item
- Quantity Ordered
- Quantity Picked
- Quantity Shipped
- Quantity Delivered

**Relationships:**
- A Customer Order contains one or more Customer Order Items.
- Each Customer Order Item refers to an Individual Item.
- Quantity Shipped and Quantity Delivered remain separate so delivery differences can be identified.

### Driver

Represents an employee who delivers Customer Orders.

**Relationships:**
- A Driver may be associated with a Delivery Route.
- A Driver performs Deliveries for Customer Orders on the route.

### Individual Item

Represents a product included in a Customer Order and Delivery.

**Relevant Attributes:**
- SKU / Item Number
- Description

**Relationships:**
- An Individual Item may appear on multiple Customer Orders.
- An Individual Item may appear on multiple Deliveries.

---

## Gherkin AC

### US-15.1: Identify Customer Orders for Delivery

#### AC-15.1.1: Customer Orders are available on the Route

**Given** a Driver has a Delivery Route  
**When** the Driver starts the delivery process  
**Then** the system identifies the Customer Orders assigned to that Delivery Route

#### AC-15.1.2: Customer Order is selected

**Given** the Driver has Customer Orders assigned to the Delivery Route  
**When** the Driver selects a Customer Order for delivery  
**Then** the system provides the shipped items and Quantity Shipped for that order

### US-15.2: Deliver Customer Order

#### AC-15.2.1: Shipped Customer Order is delivered

**Given** a shipped Customer Order is assigned to the Driver's Delivery Route  
**When** the Driver performs the Delivery  
**Then** the system allows delivery information to be recorded for that Customer Order

#### AC-15.2.2: Customer cannot receive the Delivery

**Given** the Driver attempts to deliver a Customer Order  
**When** the Customer cannot receive the Delivery  
**Then** [TBD: behavior not specified in the interview or class notes]

### US-15.3: Record Quantity Delivered

#### AC-15.3.1: Quantity Delivered equals Quantity Shipped

**Given** an item has a recorded Quantity Shipped  
**When** the Driver records the same Quantity Delivered  
**Then** the system records Quantity Delivered separately from Quantity Shipped  
**And** identifies no quantity difference

#### AC-15.3.2: Quantity Delivered is less than Quantity Shipped

**Given** an item has a recorded Quantity Shipped  
**When** the Driver records a smaller Quantity Delivered  
**Then** the system records the actual Quantity Delivered  
**And** preserves the difference between Quantity Shipped and Quantity Delivered

#### AC-15.3.3: Quantity Delivered is greater than Quantity Shipped

**Given** an item has a recorded Quantity Shipped  
**When** the Driver records a greater Quantity Delivered  
**Then** the system preserves the difference  
**And** [TBD: additional handling not specified in the interview or class notes]

### US-15.4: Identify Delivery Difference

#### AC-15.4.1: Delivery Difference is recorded

**Given** Quantity Delivered differs from Quantity Shipped  
**When** the Driver records the actual Quantity Delivered  
**Then** the system identifies and preserves the difference for reporting

#### AC-15.4.2: Delivery is completed

**Given** the Driver has recorded Quantity Delivered for the Customer Order  
**When** the Driver completes the Delivery  
**Then** the system records the Delivery as completed  
**And** preserves its relationship with the Delivery Route

#### AC-15.4.3: Customer Order is partially delivered

**Given** one or more items have a Quantity Delivered less than Quantity Shipped  
**When** the Driver completes the delivery information  
**Then** the actual delivered quantities are preserved  
**And** [TBD: Customer Order and Delivery status handling not specified in the interview or class notes]