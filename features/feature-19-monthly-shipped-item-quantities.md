# Feature: Report Monthly Shipped Item Quantities

**Feature ID:** 19  
**Branch pattern:** `feature/19-monthly-shipped-item-quantities`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system provides a report showing how many quantities of Individual Items have been shipped each month so that a manager can review monthly shipping activity.

---

## User Stories

### US-19.1: View Monthly Shipped Quantities

**As a** manager  
**I want to** see the quantities of items shipped each month  
**So that** I can review monthly shipping activity

**Priority:** P1  
**Independent test:** Generate the report for a month and confirm that shipped quantities are grouped by Individual Item.

### US-19.2: Review Shipped Quantity by Item

**As a** manager  
**I want to** see the total Quantity Shipped for each Individual Item  
**So that** I can understand how much of each item was shipped during the month

**Priority:** P1  
**Independent test:** View an Individual Item in the monthly report and confirm that its shipped quantities are included in the monthly total.

---

## Functional Requirements

- **FR-001:** The system MUST use Quantity Shipped information recorded during the shipping process.
- **FR-002:** The system MUST associate shipped quantities with Individual Items.
- **FR-003:** The system MUST associate shipping information with a month.
- **FR-004:** The system MUST calculate the total Quantity Shipped for each Individual Item during the applicable month.
- **FR-005:** The system MUST provide monthly shipped item quantities in a report.
- **FR-006:** The report MUST identify each applicable Individual Item.
- **FR-007:** The report MUST provide the total Quantity Shipped for each applicable Individual Item.
- **FR-008:** If an Individual Item is shipped multiple times during the same month, the applicable Quantity Shipped values MUST contribute to that item's monthly total.
- **FR-009:** Quantities from Shipments outside the applicable month MUST NOT be included in that month's total.
- **FR-010:** If no quantities were shipped during the applicable month, the report MUST contain no shipped quantities for that month.
- **FR-011:** Monthly reporting MUST use Quantity Shipped rather than Quantity Ordered, Quantity Picked, or Quantity Delivered.
- **FR-012:** The exact Shipment date/time field used to determine the applicable month is **TBD**.
- **FR-013:** Whether both month and year are required for the reporting period is **TBD**.
- **FR-014:** Whether Individual Items with no Shipments during the selected month should appear with a zero total or be omitted is **TBD**.
- **FR-015:** Whether the report can be filtered by Warehouse is **TBD**.
- **FR-016:** Whether the report can be filtered by Customer is **TBD**.
- **FR-017:** Whether the report can be filtered by Individual Item is **TBD**.
- **FR-018:** The exact report sorting and grouping are **TBD**.
- **FR-019:** Behavior when Shipment date/time information is unavailable is **TBD**.

---

## Key Entities

- **Monthly Shipping Report:** A reporting view of quantities of Individual Items shipped during a month.
- **Shipment:** Shipping information for a Customer Order.
- **Shipment Item:** An Individual Item included in a Shipment with its Quantity Shipped.
- **Individual Item:** A product whose shipped quantities are totaled for monthly reporting.
- **Customer Order:** The Customer Order associated with a Shipment.

---

## Initial Data Model

### Monthly Shipping Report

Represents the reporting view of quantities of Individual Items shipped during a month.

**Attributes:**
- Month
- [TBD: Year or other reporting-period information]

**Relationships:**
- A Monthly Shipping Report contains shipped quantity information for Individual Items.
- The report uses Shipment and Shipment Item information.

### Shipment

Represents shipping information for a Customer Order.

**Relevant Attributes:**
- [TBD: Shipment identifier]
- [TBD: Shipment date/time]
- Status [exact values TBD]

**Relationships:**
- A Shipment is associated with a Customer Order.
- A Shipment contains one or more Shipment Items.
- Shipment date/time information is used to associate shipped quantities with a month.

### Shipment Item

Represents an Individual Item included in a Shipment.

**Attributes:**
- Individual Item
- Quantity Shipped

**Relationships:**
- A Shipment contains one or more Shipment Items.
- Each Shipment Item refers to an Individual Item.
- Quantity Shipped contributes to the monthly total for the Individual Item.

### Individual Item

Represents a product included in a Shipment.

**Relevant Attributes:**
- SKU / Item Number
- Description

**Relationships:**
- An Individual Item may appear on multiple Shipments.
- Shipped quantities for an Individual Item are totaled for monthly reporting.

### Customer Order

Represents the Customer Order associated with a Shipment.

**Relationships:**
- A Customer Order may have a Shipment.
- Shipment information for the Customer Order contributes to monthly shipping data.

---

## Gherkin AC

### US-19.1: View Monthly Shipped Quantities

#### AC-19.1.1: Items were shipped during the Month

**Given** one or more Individual Items have recorded Quantity Shipped during the applicable month  
**When** the manager requests the Monthly Shipping Report  
**Then** the system identifies the applicable Individual Items  
**And** provides their monthly Quantity Shipped totals

#### AC-19.1.2: No Items were shipped during the Month

**Given** no Quantity Shipped was recorded during the applicable month  
**When** the manager requests the Monthly Shipping Report  
**Then** the report contains no shipped quantities for that month

#### AC-19.1.3: Shipment occurred outside the applicable Month

**Given** a Shipment occurred outside the applicable month  
**When** the manager requests the report for the applicable month  
**Then** the Quantity Shipped from that Shipment is not included in the month's totals

### US-19.2: Review Shipped Quantity by Item

#### AC-19.2.1: Individual Item was shipped once

**Given** an Individual Item was shipped once during the applicable month  
**When** the manager reviews that Individual Item in the report  
**Then** the item's monthly total includes its recorded Quantity Shipped

#### AC-19.2.2: Individual Item was shipped multiple times

**Given** an Individual Item appears in multiple Shipments during the applicable month  
**When** the manager reviews that Individual Item in the report  
**Then** the applicable Quantity Shipped values are included in the item's monthly total

#### AC-19.2.3: Individual Item was not shipped

**Given** an Individual Item has no Quantity Shipped during the applicable month  
**When** the manager requests the Monthly Shipping Report  
**Then** [TBD: whether the Individual Item is omitted or displayed with a zero total]

#### AC-19.2.4: Shipment Date Information is unavailable

**Given** a Shipment does not contain enough date/time information to determine its month  
**When** the system prepares the Monthly Shipping Report  
**Then** [TBD: behavior not specified in the interview or class notes]

#### AC-19.2.5: Multiple Shipments contribute to the Monthly Total

**Given** the same Individual Item has Quantity Shipped recorded on multiple Shipments during the applicable month  
**When** the manager requests the Monthly Shipping Report  
**Then** the system includes the applicable Quantity Shipped values in the Individual Item's monthly total

#### AC-19.2.6: Shipment belongs to a different Month

**Given** an Individual Item has Quantity Shipped recorded in more than one month  
**When** the manager requests the report for one applicable month  
**Then** only Quantity Shipped associated with that month is included in the monthly total