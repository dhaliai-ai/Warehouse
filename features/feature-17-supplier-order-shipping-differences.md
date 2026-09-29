# Feature: Report Suppliers That Do Not Ship What Was Ordered

**Feature ID:** 17  
**Branch pattern:** `feature/17-supplier-order-differences`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system provides a report identifying Supplier Orders where Quantity Received differs from Quantity Ordered so that a manager can review suppliers that did not ship what was ordered.

---

## User Stories

### US-17.1: View Supplier Order Differences

**As a** manager  
**I want to** see Supplier Orders where Quantity Received differs from Quantity Ordered  
**So that** I can identify supplier delivery exceptions

**Priority:** P1  
**Independent test:** Generate the report and confirm that Supplier Order Items with differences between Quantity Ordered and Quantity Received are identified.

### US-17.2: Review Supplier Difference Details

**As a** manager  
**I want to** see the Supplier, Individual Item, Quantity Ordered, and Quantity Received  
**So that** I can understand what was not shipped as ordered

**Priority:** P1  
**Independent test:** View a reported difference and confirm that the Supplier, Individual Item, Quantity Ordered, and Quantity Received can be reviewed.

---

## Functional Requirements

- **FR-001:** The system MUST compare Quantity Ordered with Quantity Received for Supplier Order Items.
- **FR-002:** The system MUST identify Supplier Order Items where Quantity Received differs from Quantity Ordered.
- **FR-003:** The system MUST provide identified Supplier Order differences in a report.
- **FR-004:** The report MUST identify the Supplier associated with the Supplier Order.
- **FR-005:** The report MUST identify the Individual Item associated with the difference.
- **FR-006:** The report MUST provide Quantity Ordered and Quantity Received for the identified Individual Item.
- **FR-007:** The system MUST preserve Quantity Ordered separately from Quantity Received.
- **FR-008:** Supplier Order Items where Quantity Ordered equals Quantity Received MUST NOT be identified as quantity differences.
- **FR-009:** When Quantity Received is less than Quantity Ordered, the difference MUST be available for reporting.
- **FR-010:** When Quantity Received is greater than Quantity Ordered, the difference MUST be available for reporting.
- **FR-011:** If multiple Supplier Order Items have differences, each applicable difference MUST be available for reporting.
- **FR-012:** Whether Supplier Orders with incomplete receiving should appear in the report is **TBD**.
- **FR-013:** Whether the report can be filtered by Supplier is **TBD**.
- **FR-014:** Whether the report can be filtered by date is **TBD**.
- **FR-015:** Whether the report can be filtered by Individual Item is **TBD**.
- **FR-016:** Whether shortages and overages should be displayed differently is **TBD**.
- **FR-017:** The date associated with a reported Supplier Order difference is **TBD**.
- **FR-018:** The exact report sorting and grouping are **TBD**.

---

## Key Entities

- **Supplier Difference Report:** A reporting view of differences between Quantity Ordered and Quantity Received.
- **Supplier:** The Supplier associated with the Supplier Order.
- **Supplier Order:** An order placed with a Supplier.
- **Supplier Order Item:** An Individual Item on a Supplier Order with Quantity Ordered and Quantity Received.
- **Individual Item:** A product ordered from a Supplier.

---

## Initial Data Model

### Supplier Difference Report

Represents the reporting view of differences between what was ordered from Suppliers and what was received.

**Relationships:**
- A Supplier Difference Report contains Supplier Order Item differences.
- The report uses Supplier Order and receiving information.
- Only applicable differences between Quantity Ordered and Quantity Received are reported.

### Supplier

Represents the Supplier responsible for a Supplier Order.

**Relationships:**
- A Supplier may have one or more Supplier Orders.
- Supplier information identifies which Supplier is associated with an order difference.

### Supplier Order

Represents an order placed with a Supplier.

**Relevant Attributes:**
- PO Number / Order Identifier
- Status [exact values TBD]

**Relationships:**
- A Supplier Order is associated with a Supplier.
- A Supplier Order contains one or more Supplier Order Items.

### Supplier Order Item

Represents an Individual Item included in a Supplier Order.

**Attributes:**
- Individual Item
- Quantity Ordered
- Quantity Received

**Relationships:**
- A Supplier Order contains one or more Supplier Order Items.
- Each Supplier Order Item refers to an Individual Item.
- Quantity Ordered is compared with Quantity Received for reporting.
- Quantity Ordered remains separate from Quantity Received.

### Individual Item

Represents a product ordered from a Supplier.

**Relevant Attributes:**
- SKU / Item Number
- Description

**Relationships:**
- An Individual Item may appear on multiple Supplier Orders.
- An Individual Item may appear in the Supplier Difference Report when Quantity Ordered differs from Quantity Received.

---

## Gherkin AC

### US-17.1: View Supplier Order Differences

#### AC-17.1.1: Supplier shipped less than Ordered

**Given** a Supplier Order Item has a Quantity Ordered  
**And** receiving has recorded a smaller Quantity Received  
**When** the manager requests the Supplier Difference Report  
**Then** the system identifies the Supplier Order Item as a difference

#### AC-17.1.2: Supplier shipped more than Ordered

**Given** a Supplier Order Item has a Quantity Ordered  
**And** receiving has recorded a greater Quantity Received  
**When** the manager requests the Supplier Difference Report  
**Then** the system identifies the Supplier Order Item as a difference

#### AC-17.1.3: Supplier shipped the Ordered Quantity

**Given** Quantity Received equals Quantity Ordered  
**When** the manager requests the Supplier Difference Report  
**Then** that Supplier Order Item is not identified as a quantity difference

#### AC-17.1.4: No Supplier Differences exist

**Given** all applicable Quantity Received values equal their Quantity Ordered values  
**When** the manager requests the Supplier Difference Report  
**Then** the report contains no supplier quantity differences

#### AC-17.1.5: Receiving is incomplete

**Given** a Supplier Order is still being received  
**When** Quantity Received has not been finalized  
**Then** [TBD: whether the Supplier Order should appear in the report]

### US-17.2: Review Supplier Difference Details

#### AC-17.2.1: Difference Details are displayed

**Given** a Supplier Order Item has a difference between Quantity Ordered and Quantity Received  
**When** the manager reviews the reported difference  
**Then** the report identifies the Supplier  
**And** identifies the Individual Item  
**And** provides Quantity Ordered  
**And** provides Quantity Received

#### AC-17.2.2: Multiple Differences exist

**Given** multiple Supplier Order Items have differences between Quantity Ordered and Quantity Received  
**When** the manager requests the Supplier Difference Report  
**Then** each applicable difference is available for review

#### AC-17.2.3: One Item differs on a Multi-Item Order

**Given** a Supplier Order contains multiple Supplier Order Items  
**And** only one item has a difference between Quantity Ordered and Quantity Received  
**When** the manager requests the Supplier Difference Report  
**Then** the differing Supplier Order Item is identified

#### AC-17.2.4: Multiple Orders from the same Supplier have Differences

**Given** multiple Supplier Orders from the same Supplier contain quantity differences  
**When** the manager requests the Supplier Difference Report  
**Then** the applicable differences from those Supplier Orders are available for review