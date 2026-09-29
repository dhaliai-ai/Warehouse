# Feature: Ship Customer Orders

**Feature ID:** 14  
**Branch pattern:** `feature/14-ship-customer-orders`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system assists a shipping clerk in shipping a picked Customer Order by verifying the items prepared for shipment, recording the Quantity Shipped, and preparing the order for delivery.

---

## User Stories

### US-14.1: Select Picked Customer Order for Shipping

**As a** shipping clerk  
**I want to** select a Customer Order that has been picked  
**So that** I can prepare it for shipment

**Priority:** P1  
**Independent test:** Select a picked Customer Order and confirm that its picked items and quantities are available for shipping.

### US-14.2: Verify Items for Shipment

**As a** shipping clerk  
**I want to** verify the items prepared for shipment  
**So that** I can confirm what is actually being shipped

**Priority:** P1  
**Independent test:** Verify the items prepared for a Customer Order and confirm that the system records the shipment information.

### US-14.3: Record Quantity Shipped

**As a** shipping clerk  
**I want to** record Quantity Shipped for each item  
**So that** the system can distinguish what was shipped from what was ordered and picked

**Priority:** P1  
**Independent test:** Record Quantity Shipped for an item and confirm that it remains separate from Quantity Ordered and Quantity Picked.

### US-14.4: Prepare Customer Order for Delivery

**As a** shipping clerk  
**I want to** prepare the Customer Order for delivery  
**So that** the shipped order can move to the delivery process

**Priority:** P1  
**Independent test:** Complete shipping for a Customer Order and confirm that the order is available for the delivery process.

---

## Functional Requirements

- **FR-001:** The system MUST identify Customer Orders that have been picked and are ready for shipping.
- **FR-002:** The system MUST allow the shipping clerk to select a picked Customer Order for shipping.
- **FR-003:** The system MUST provide the items and quantities associated with the picked Customer Order.
- **FR-004:** The system MUST allow the shipping clerk to verify the items being prepared for shipment.
- **FR-005:** The system MUST record Quantity Shipped for each item.
- **FR-006:** The system MUST keep Quantity Shipped separate from Quantity Ordered, Quantity Picked, and Quantity Delivered.
- **FR-007:** The system MUST allow Quantity Shipped to be compared with Quantity Picked.
- **FR-008:** The system MUST preserve differences between Quantity Picked and Quantity Shipped for later reporting.
- **FR-009:** The shipping process MUST support preparing the Customer Order for delivery, including verification, shrink-wrapping, and labeling.
- **FR-010:** The system MUST identify when shipping for the Customer Order has been completed.
- **FR-011:** After shipping is completed, the Customer Order MUST be available for the delivery process.
- **FR-012:** The exact Customer Order and Shipment status values used before, during, and after shipping are **TBD**.
- **FR-013:** The exact system behavior when Quantity Shipped differs from Quantity Picked is **TBD**.
- **FR-014:** Behavior when an incorrect item is discovered during shipping verification is **TBD**.
- **FR-015:** Whether a Customer Order may be partially shipped is **TBD**.
- **FR-016:** If partial shipments are allowed, how they are represented is **TBD**.
- **FR-017:** The exact information that must be recorded for shipment verification, shrink-wrapping, and labeling is **TBD**.
- **FR-018:** Behavior when the shipping process cannot be completed is **TBD**.

---

## Key Entities

- **Shipment:** Shipping information for a picked Customer Order.
- **Shipment Item:** An Individual Item included in a Shipment with Quantity Picked and Quantity Shipped.
- **Customer Order:** An order that has been picked and is being prepared for shipment.
- **Customer Order Item:** An Individual Item requested on a Customer Order with quantities maintained across the warehouse processes.
- **Individual Item:** A product included in the Customer Order and Shipment.

---

## Initial Data Model

### Shipment

Represents the shipping information for a picked Customer Order.

**Attributes:**
- [TBD: Shipment identifier]
- Status [exact values TBD]

**Relationships:**
- A Shipment is associated with a Customer Order.
- A Shipment contains one or more Shipment Items.
- A completed Shipment becomes available for the delivery process.

### Shipment Item

Represents an Individual Item included in a Shipment.

**Attributes:**
- Individual Item
- Quantity Picked
- Quantity Shipped

**Relationships:**
- A Shipment contains one or more Shipment Items.
- Each Shipment Item refers to an Individual Item.
- Quantity Shipped is compared with Quantity Picked.
- Quantity Shipped remains separate from Quantity Ordered, Quantity Picked, and Quantity Delivered.

### Customer Order

Represents an order received from a Customer.

**Relevant Attributes:**
- [TBD: Customer Order identifier]
- Status [exact values TBD]

**Relationships:**
- A Customer Order contains one or more Customer Order Items.
- A Customer Order is picked before shipping.
- A Customer Order may have a Shipment.
- After shipping, the Customer Order becomes available for delivery.

### Customer Order Item

Represents an Individual Item requested on a Customer Order.

**Relevant Attributes:**
- Individual Item
- Quantity Ordered
- Quantity Picked
- Quantity Shipped
- Quantity Delivered

**Relationships:**
- A Customer Order contains one or more Customer Order Items.
- Each Customer Order Item refers to an Individual Item.
- The different quantities are preserved so differences between ordering, picking, shipping, and delivery can be identified.

### Individual Item

Represents a product included in the Customer Order and Shipment.

**Relevant Attributes:**
- SKU / Item Number
- Description

**Relationships:**
- An Individual Item may appear on multiple Customer Orders.
- An Individual Item may appear on multiple Shipments.

---

## Gherkin AC

### US-14.1: Select Picked Customer Order for Shipping

#### AC-14.1.1: Picked Customer Order is available for Shipping

**Given** a Customer Order has been picked  
**When** the shipping clerk starts the shipping process  
**Then** the system identifies the Customer Order as available for shipping  
**And** provides the picked items and quantities

### US-14.2: Verify Items for Shipment

#### AC-14.2.1: Shipping Clerk verifies Items

**Given** a picked Customer Order has been selected for shipping  
**When** the shipping clerk reviews the items prepared for shipment  
**Then** the system allows the items being shipped to be verified

#### AC-14.2.2: Incorrect Item is discovered

**Given** the shipping clerk is verifying the items prepared for shipment  
**When** an incorrect item is discovered  
**Then** [TBD: correction process not specified in the interview or class notes]

### US-14.3: Record Quantity Shipped

#### AC-14.3.1: Quantity Shipped equals Quantity Picked

**Given** an item has a recorded Quantity Picked  
**When** the shipping clerk records the same Quantity Shipped  
**Then** the system records Quantity Shipped separately from Quantity Picked

#### AC-14.3.2: Quantity Shipped is less than Quantity Picked

**Given** an item has a recorded Quantity Picked  
**When** the shipping clerk records a smaller Quantity Shipped  
**Then** the system records the actual Quantity Shipped  
**And** preserves the difference between Quantity Picked and Quantity Shipped

#### AC-14.3.3: Quantity Shipped is greater than Quantity Picked

**Given** an item has a recorded Quantity Picked  
**When** the shipping clerk attempts to record a greater Quantity Shipped  
**Then** [TBD: behavior not specified in the interview or class notes]

### US-14.4: Prepare Customer Order for Delivery

#### AC-14.4.1: Order is prepared for Delivery

**Given** the items and quantities for the Shipment have been verified  
**When** the shipping clerk prepares the order for delivery  
**Then** the order can be verified, shrink-wrapped, and labeled for delivery

#### AC-14.4.2: Shipping is completed

**Given** the Customer Order has been prepared for delivery  
**When** the shipping clerk completes the shipping process  
**Then** the system records the Shipment as completed  
**And** makes the Customer Order available for the delivery process

#### AC-14.4.3: Order cannot be completely prepared

**Given** the Customer Order is being prepared for delivery  
**When** the shipping process cannot be completed  
**Then** [TBD: behavior not specified in the interview or class notes]