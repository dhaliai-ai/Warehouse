# Feature: Receive Customer Orders

**Feature ID:** 12  
**Branch pattern:** `feature/12-receive-customer-orders`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system receives and records a Customer Order, including the customer, items, and Quantity Ordered, so that the order can later proceed to the picking process.

---

## User Stories

### US-12.1: Record Customer Order

**As a** warehouse office worker  
**I want to** record a Customer Order  
**So that** the warehouse can fulfill the customer's order

**Priority:** P1  
**Independent test:** Enter a Customer Order and confirm that the order is recorded in the system.

### US-12.2: Record Ordered Items and Quantities

**As a** warehouse office worker  
**I want to** record the items and Quantity Ordered for a Customer Order  
**So that** the warehouse knows what the customer requested

**Priority:** P1  
**Independent test:** Add items and quantities to a Customer Order and confirm that Quantity Ordered is recorded for each item.

### US-12.3: Make Customer Order Available for Picking

**As a** warehouse office worker  
**I want to** complete the Customer Order entry  
**So that** the order can proceed to the picking process

**Priority:** P1  
**Independent test:** Complete entry of a Customer Order and confirm that it becomes available for the picking process.

---

## Functional Requirements

- **FR-001:** The system MUST allow a warehouse office worker to record a Customer Order.
- **FR-002:** The system MUST associate the Customer Order with a Customer.
- **FR-003:** The system MUST allow one or more Individual Items to be recorded on a Customer Order.
- **FR-004:** The system MUST record Quantity Ordered for each item on the Customer Order.
- **FR-005:** The system MUST keep Quantity Ordered separate from Quantity Picked, Quantity Shipped, and Quantity Delivered.
- **FR-006:** The system MUST preserve the items and Quantity Ordered so they are available to the picking process.
- **FR-007:** The system MUST identify when Customer Order entry has been completed.
- **FR-008:** After Customer Order entry is completed, the Customer Order MUST be available for the picking process.
- **FR-009:** The exact Customer Order status values are **TBD**.
- **FR-010:** The exact method by which Customer Orders are received or entered into the system is **TBD**.
- **FR-011:** Behavior when the Customer does not already exist in the system is **TBD**.
- **FR-012:** Behavior when an Individual Item on the Customer Order does not exist in the system is **TBD**.
- **FR-013:** Whether the same Individual Item may appear more than once on a Customer Order is **TBD**.
- **FR-014:** How zero or negative Quantity Ordered values are handled is **TBD**.
- **FR-015:** The Customer Order information required before an order can proceed to picking is **TBD**.
- **FR-016:** Whether an incomplete Customer Order can be saved before it is ready for picking is **TBD**.

---

## Key Entities

- **Customer Order:** An order received from a Customer.
- **Customer Order Item:** An Individual Item requested on a Customer Order with quantities recorded for the different warehouse stages.
- **Customer:** The customer who places the Customer Order.
- **Individual Item:** A product requested on the Customer Order.

---

## Initial Data Model

### Customer Order

Represents an order received from a Customer.

**Attributes:**
- [TBD: Customer Order identifier]
- Status [exact values TBD]

**Relationships:**
- A Customer Order is associated with a Customer.
- A Customer Order contains one or more Customer Order Items.
- A completed Customer Order becomes available for the picking process.

### Customer Order Item

Represents an Individual Item requested on a Customer Order.

**Attributes:**
- Individual Item
- Quantity Ordered
- Quantity Picked
- Quantity Shipped
- Quantity Delivered

**Relationships:**
- A Customer Order contains one or more Customer Order Items.
- Each Customer Order Item refers to an Individual Item.
- Quantity Ordered is recorded when the Customer Order is received.
- Quantity Picked, Quantity Shipped, and Quantity Delivered are recorded during later processes.
- Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered remain separate so differences between stages can be identified.

### Customer

Represents a Customer that places Customer Orders.

**Relevant Attributes:**
- [TBD: Customer identifier]
- [TBD: Customer information defined by Maintain Customers]

**Relationships:**
- A Customer may have one or more Customer Orders.
- Each Customer Order is associated with a Customer.

### Individual Item

Represents a product requested on a Customer Order.

**Relevant Attributes:**
- SKU / Item Number
- UPC
- Description

**Relationships:**
- An Individual Item may appear on multiple Customer Orders.
- An Individual Item may be included in one or more Customer Order Items.

---

## Gherkin AC

### US-12.1: Record Customer Order

#### AC-12.1.1: Customer Order is recorded

**Given** a Customer exists in the system  
**When** the warehouse office worker records a Customer Order for that Customer  
**Then** the system associates the Customer Order with the Customer

#### AC-12.1.2: Customer does not exist

**Given** a Customer Order is being recorded  
**When** the Customer does not exist in the system  
**Then** [TBD: behavior not specified in the interview or class notes]

### US-12.2: Record Ordered Items and Quantities

#### AC-12.2.1: Item is added to Customer Order

**Given** a Customer Order is being recorded  
**When** the warehouse office worker adds an Individual Item and Quantity Ordered  
**Then** the system records the Individual Item and Quantity Ordered on the Customer Order

#### AC-12.2.2: Multiple Items are ordered

**Given** a Customer Order contains multiple Individual Items  
**When** the items and quantities are recorded  
**Then** the system records Quantity Ordered for each item

#### AC-12.2.3: Item does not exist

**Given** a Customer Order is being recorded  
**When** an Individual Item does not exist in the system  
**Then** [TBD: behavior not specified in the interview or class notes]

#### AC-12.2.4: Invalid Quantity is entered

**Given** an Individual Item is being added to a Customer Order  
**When** a zero or negative Quantity Ordered is entered  
**Then** [TBD: behavior not specified in the interview or class notes]

### US-12.3: Make Customer Order Available for Picking

#### AC-12.3.1: Customer Order entry is completed

**Given** the Customer Order information, items, and Quantity Ordered have been recorded  
**When** the warehouse office worker completes the Customer Order entry  
**Then** the system records the Customer Order as ready to proceed to the picking process

#### AC-12.3.2: Quantities remain separate

**Given** a Customer Order has been recorded  
**When** the order proceeds to later warehouse processes  
**Then** Quantity Ordered remains separate from Quantity Picked, Quantity Shipped, and Quantity Delivered

#### AC-12.3.3: Customer Order entry is incomplete

**Given** a Customer Order is being recorded  
**When** required Customer Order information is incomplete  
**Then** [TBD: behavior for incomplete orders not specified in the interview or class notes]