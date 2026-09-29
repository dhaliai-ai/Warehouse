# Feature: Report Deliveries That Do Not Match What Was Shipped

**Feature ID:** 18  
**Branch pattern:** `feature/18-delivery-shipment-differences`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system provides a report identifying Customer Order Items where Quantity Delivered differs from Quantity Shipped so that a manager can review delivery exceptions.

---

## User Stories

### US-18.1: View Delivery Differences

**As a** manager  
**I want to** see deliveries where Quantity Delivered differs from Quantity Shipped  
**So that** I can identify delivery exceptions

**Priority:** P1  
**Independent test:** Generate the report and confirm that Customer Order Items with differences between Quantity Shipped and Quantity Delivered are identified.

### US-18.2: Review Delivery Difference Details

**As a** manager  
**I want to** see the Customer Order, Individual Item, Quantity Shipped, and Quantity Delivered  
**So that** I can understand what did not match during delivery

**Priority:** P1  
**Independent test:** View a reported delivery difference and confirm that the Customer Order, Individual Item, Quantity Shipped, and Quantity Delivered can be reviewed.

---

## Functional Requirements

- **FR-001:** The system MUST compare Quantity Shipped with Quantity Delivered for Customer Order Items.
- **FR-002:** The system MUST identify Customer Order Items where Quantity Delivered differs from Quantity Shipped.
- **FR-003:** The system MUST provide identified delivery differences in a report.
- **FR-004:** The report MUST identify the Customer Order associated with each difference.
- **FR-005:** The report MUST identify the Individual Item associated with each difference.
- **FR-006:** The report MUST provide Quantity Shipped and Quantity Delivered for each identified difference.
- **FR-007:** The system MUST preserve Quantity Shipped separately from Quantity Delivered.
- **FR-008:** Customer Order Items where Quantity Shipped equals Quantity Delivered MUST NOT be identified as delivery quantity differences.
- **FR-009:** When Quantity Delivered is less than Quantity Shipped, the difference MUST be available for reporting.
- **FR-010:** When Quantity Delivered is greater than Quantity Shipped, the difference MUST be available for reporting.
- **FR-011:** If multiple Customer Order Items have delivery differences, each applicable difference MUST be available for reporting.
- **FR-012:** The system MUST preserve the relationship between the Delivery and its Delivery Route.
- **FR-013:** Whether incomplete Deliveries should appear in the report is **TBD**.
- **FR-014:** Whether the report can be filtered by Customer is **TBD**.
- **FR-015:** Whether the report can be filtered by Delivery Route is **TBD**.
- **FR-016:** Whether the report can be filtered by date is **TBD**.
- **FR-017:** Whether the report can be filtered by Individual Item is **TBD**.
- **FR-018:** Whether shortages and over-deliveries should be displayed differently is **TBD**.
- **FR-019:** The date associated with a delivery difference is **TBD**.
- **FR-020:** How unsuccessful Deliveries appear in the report is **TBD**.
- **FR-021:** The exact report format, grouping, and sorting are **TBD**.

---

## Key Entities

- **Delivery Difference Report:** A reporting view of differences between Quantity Shipped and Quantity Delivered.
- **Customer Order:** The Customer Order associated with the Shipment and Delivery.
- **Customer Order Item:** An Individual Item with Quantity Shipped and Quantity Delivered.
- **Shipment:** Shipping information for a Customer Order.
- **Delivery:** Delivery information for a shipped Customer Order.
- **Delivery Route:** The route associated with delivery of Customer Orders.
- **Individual Item:** A product included in the Shipment and Delivery.

---

## Initial Data Model

### Delivery Difference Report

Represents the reporting view of differences between what was shipped and what was delivered.

**Relationships:**
- A Delivery Difference Report contains delivery differences.
- The report uses Shipment and Delivery information.
- Only applicable differences between Quantity Shipped and Quantity Delivered are reported.

### Customer Order

Represents the Customer Order associated with the Shipment and Delivery.

**Relevant Attributes:**
- [TBD: Customer Order identifier]

**Relationships:**
- A Customer Order contains one or more Customer Order Items.
- A Customer Order may have Shipment and Delivery information.

### Customer Order Item

Represents an Individual Item included in a Customer Order.

**Attributes:**
- Individual Item
- Quantity Shipped
- Quantity Delivered

**Relationships:**
- A Customer Order contains one or more Customer Order Items.
- Each Customer Order Item refers to an Individual Item.
- Quantity Shipped is compared with Quantity Delivered for reporting.
- Quantity Shipped remains separate from Quantity Delivered.

### Shipment

Represents the shipping information for a Customer Order.

**Relationships:**
- A Shipment is associated with a Customer Order.
- Shipment information provides Quantity Shipped.

### Delivery

Represents the delivery of a shipped Customer Order.

**Relevant Attributes:**
- Status [exact values TBD]

**Relationships:**
- A Delivery is associated with a Customer Order.
- A Delivery may be associated with a Delivery Route.
- Delivery information provides Quantity Delivered.

### Delivery Route

Represents the route used to deliver Customer Orders.

**Relevant Attributes:**
- [TBD: Route identifier]

**Relationships:**
- A Delivery Route may contain Customer Orders to be delivered.
- Delivery differences may be associated with orders on a Delivery Route.

### Individual Item

Represents a product included in a Shipment and Delivery.

**Relevant Attributes:**
- SKU / Item Number
- Description

**Relationships:**
- An Individual Item may appear on multiple Customer Orders.
- An Individual Item may appear in the Delivery Difference Report when Quantity Shipped differs from Quantity Delivered.

---

## Gherkin AC

### US-18.1: View Delivery Differences

#### AC-18.1.1: Quantity Delivered is less than Quantity Shipped

**Given** a Customer Order Item has a recorded Quantity Shipped  
**And** Delivery records a smaller Quantity Delivered  
**When** the manager requests the Delivery Difference Report  
**Then** the system identifies the Customer Order Item as a delivery difference

#### AC-18.1.2: Quantity Delivered is greater than Quantity Shipped

**Given** a Customer Order Item has a recorded Quantity Shipped  
**And** Delivery records a greater Quantity Delivered  
**When** the manager requests the Delivery Difference Report  
**Then** the system identifies the Customer Order Item as a delivery difference

#### AC-18.1.3: Quantity Delivered matches Quantity Shipped

**Given** Quantity Delivered equals Quantity Shipped  
**When** the manager requests the Delivery Difference Report  
**Then** that Customer Order Item is not identified as a delivery quantity difference

#### AC-18.1.4: No Delivery Differences exist

**Given** all applicable Quantity Delivered values equal their Quantity Shipped values  
**When** the manager requests the Delivery Difference Report  
**Then** the report contains no delivery quantity differences

#### AC-18.1.5: Delivery is incomplete

**Given** a Customer Order is still being delivered  
**When** Quantity Delivered has not been finalized  
**Then** [TBD: whether the Customer Order should appear in the report]

### US-18.2: Review Delivery Difference Details

#### AC-18.2.1: Difference Details are displayed

**Given** a Customer Order Item has a difference between Quantity Shipped and Quantity Delivered  
**When** the manager reviews the reported difference  
**Then** the report identifies the Customer Order  
**And** identifies the Individual Item  
**And** provides Quantity Shipped  
**And** provides Quantity Delivered

#### AC-18.2.2: Multiple Delivery Differences exist

**Given** multiple Customer Order Items have differences between Quantity Shipped and Quantity Delivered  
**When** the manager requests the Delivery Difference Report  
**Then** each applicable difference is available for review

#### AC-18.2.3: One Item differs on a Multi-Item Customer Order

**Given** a Customer Order contains multiple Customer Order Items  
**And** only one item has a difference between Quantity Shipped and Quantity Delivered  
**When** the manager requests the Delivery Difference Report  
**Then** the differing Customer Order Item is identified

#### AC-18.2.4: No Quantity of a Shipped Item is delivered

**Given** an Individual Item has a recorded Quantity Shipped  
**And** no quantity of that Individual Item is delivered  
**When** the manager requests the Delivery Difference Report  
**Then** the system identifies the difference between Quantity Shipped and Quantity Delivered

#### AC-18.2.5: Multiple Deliveries contain Differences

**Given** multiple Deliveries contain differences between Quantity Shipped and Quantity Delivered  
**When** the manager requests the Delivery Difference Report  
**Then** the applicable delivery differences are available for review