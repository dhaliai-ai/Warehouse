
# Feature: Report Monthly Shipped Item Quantities

**Feature ID:** 19  
**Branch pattern:** `feature/19-monthly-shipped-item-quantities`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System provides authorized Managers with a monthly report showing the total Quantity Shipped for each Individual Item. The system uses finalized Shipment Lines from the shipping process, groups shipped quantities by Individual Item and calendar month, and supports review of shipping activity by reporting period. Monthly totals use Quantity Shipped rather than Quantity Ordered, Quantity Picked, or Quantity Delivered.

---

## User Stories

### US-19.1: View Monthly Shipped Quantities

**As a** Warehouse Manager  
**I want to** generate a report showing quantities of Individual Items shipped during a selected month  
**So that** I can review monthly warehouse shipping activity.

**Priority:** P1  
**Independent test:** Generate a report for a month containing completed Shipments and verify that shipped quantities are grouped and totaled by Individual Item.

### US-19.2: Review Shipped Quantity by Item

**As a** Warehouse Manager  
**I want to** see the total Quantity Shipped for each Individual Item  
**So that** I can determine how much of each product was shipped during the month.

**Priority:** P1  
**Independent test:** Record multiple completed Shipments containing the same Item and verify that the report calculates the correct monthly total.

### US-19.3: Select Reporting Month and Year

**As a** Warehouse Manager  
**I want to** select the month and year for the Monthly Shipping Report  
**So that** I can review shipping activity for a specific reporting period.

**Priority:** P1  
**Independent test:** Generate reports for the same calendar month in two different years and verify that their totals are calculated separately.

### US-19.4: Filter Monthly Shipping Activity

**As a** Warehouse Manager  
**I want to** filter the report by Warehouse, Customer, or Individual Item  
**So that** I can investigate shipping activity relevant to a particular part of the business.

**Priority:** P2  
**Independent test:** Generate a report with a Customer filter and verify that only Shipments associated with that Customer contribute to the totals.

### US-19.5: Review Missing or Incomplete Shipping Data

**As a** Warehouse Manager  
**I want to** know when Shipment information is incomplete  
**So that** I do not rely on incorrect monthly shipping totals.

**Priority:** P2  
**Independent test:** Generate a report when a finalized Shipment has no valid shipping completion timestamp and verify that the system identifies the data-quality issue.

---

## Functional Requirements

- **FR-001:** The system MUST use Quantity Shipped information recorded during the shipping process defined in Feature 14.
- **FR-002:** The system MUST associate shipped quantities with the correct Individual Items.
- **FR-003:** The system MUST associate each finalized Shipment with a calendar month and year.
- **FR-004:** The system MUST calculate the total Quantity Shipped for each Individual Item during the selected reporting month.
- **FR-005:** The system MUST provide monthly shipped Item quantities in a Monthly Shipping Report.
- **FR-006:** The report MUST identify each applicable Individual Item by Item Number and description.
- **FR-007:** The report MUST display the total Quantity Shipped for each applicable Individual Item.
- **FR-008:** The system MUST add together applicable Quantity Shipped values when an Individual Item appears in multiple completed Shipments during the same month.
- **FR-009:** The system MUST exclude Shipments finalized outside the selected reporting month.
- **FR-010:** The system MUST use Quantity Shipped rather than Quantity Ordered, Quantity Picked, or Quantity Delivered.
- **FR-011:** The system MUST require a reporting month and year.
- **FR-012:** The system MUST support all 12 calendar months.
- **FR-013:** The system MUST distinguish the same calendar month in different years.
- **FR-014:** The system MUST use the Shipment's readyAt timestamp to determine the month in which the Shipment was finalized for delivery.
- **FR-015:** The system MUST use one consistent configured warehouse reporting time zone when assigning Shipment timestamps to calendar months.
- **FR-016:** The system MUST include only Shipments that have been successfully finalized as Ready for Delivery.
- **FR-017:** The system MUST exclude Shipments in Preparing, Canceled, or Exception status.
- **FR-018:** The system MUST calculate monthly totals from Shipment Line quantityShipped values.
- **FR-019:** The system MUST NOT calculate monthly totals from Customer Order Line quantityOrdered values.
- **FR-020:** The system MUST NOT calculate monthly totals from Picking Movement quantities.
- **FR-021:** The system MUST NOT calculate monthly totals from Delivery Line quantityDelivered values.
- **FR-022:** The system MUST count each finalized Shipment Line exactly once.
- **FR-023:** The system MUST prevent repeated report generation from changing or duplicating shipped quantities.
- **FR-024:** The system MUST preserve the original finalized Quantity Shipped when the associated Delivery is incomplete or unsuccessful.
- **FR-025:** The system MUST support multiple Shipments associated with one Customer Order.
- **FR-026:** The system MUST include each applicable completed partial Shipment in the month in which that Shipment was finalized.
- **FR-027:** The system MUST calculate Item totals independently of Customer Order status.
- **FR-028:** The system MUST exclude Individual Items with no completed Shipments during the selected month from the default report.
- **FR-029:** The system MUST display an empty result when no Items were shipped during the selected month.
- **FR-030:** The system MUST identify that no matching shipping activity was found when the report is empty.
- **FR-031:** The system MUST allow a Manager to filter the report by Warehouse.
- **FR-032:** The system MUST allow a Manager to filter the report by Customer.
- **FR-033:** The system MUST allow a Manager to filter the report by Individual Item.
- **FR-034:** The system MUST allow the report to be generated without selecting optional filters.
- **FR-035:** When no Warehouse filter is selected, the report MUST include matching Shipments from all Warehouses the Manager is authorized to review.
- **FR-036:** When a Warehouse filter is selected, the report MUST include only Shipments fulfilled by that Warehouse.
- **FR-037:** When a Customer filter is selected, the report MUST include only Shipments associated with that Customer's Orders.
- **FR-038:** When an Individual Item filter is selected, the report MUST include only matching Shipment Lines.
- **FR-039:** The report MUST display the selected reporting month and year.
- **FR-040:** The report MUST identify the unit of measure as individual units.
- **FR-041:** The system MUST support sorting the report by Item Number, Item description, or total Quantity Shipped.
- **FR-042:** The system MUST allow a Manager to review the Shipments contributing to an Item's monthly total.
- **FR-043:** The system MUST preserve the relationship between Shipment Lines, Shipments, Customer Orders, Customers, Warehouses, and Individual Items.
- **FR-044:** The system MUST identify finalized Shipments that lack a valid shipping completion timestamp.
- **FR-045:** The system MUST NOT silently assign a missing Shipment completion timestamp to an arbitrary reporting month.
- **FR-046:** The system MUST identify when missing or incomplete Shipment information could affect report accuracy.
- **FR-047:** The system MUST NOT interpret unavailable historical Shipment information as proof that no shipping occurred.
- **FR-048:** The system MUST preserve historical shipping information when an Individual Item is deactivated.
- **FR-049:** The system MUST preserve historical shipping information when a Customer is deactivated.
- **FR-050:** The system MUST preserve historical shipping information when a Warehouse is deactivated.
- **FR-051:** The system MUST restrict Monthly Shipping Report access to authorized Managers and approved reporting personnel.
- **FR-052:** The Monthly Shipping Report MUST be read-only.
- **FR-053:** Generating the report MUST NOT modify Shipments, Shipment Lines, Customer Orders, or Inventory quantities.
- **FR-054:** The system MUST preserve finalized Shipment history so monthly totals can be reproduced for historical reporting.
- **FR-055:** The system MUST calculate totals using nonnegative whole-unit Quantity Shipped values.
- **FR-056:** The system MUST NOT count an Item more than once merely because the same Shipment is associated with multiple delivery attempts.
- **FR-057:** The system MUST display one summary row per Individual Item for the selected month and filters.
- **FR-058:** The system MUST provide sufficient information to trace each monthly total back to its contributing Shipment Lines.

---

## Key Entities

### Monthly Shipping Report

Represents a read-only reporting view showing total Quantity Shipped for each Individual Item during a selected month and year.

### Shipment

Represents shipping information for a Customer Order, including the date and time shipping was finalized.

Shipment preparation is defined in Feature 14.

### Shipment Line

Represents an Individual Item included in a Shipment with its finalized Quantity Shipped.

### Individual Item

Represents a product whose shipped quantities are totaled for monthly reporting.

Individual Item maintenance is defined in Feature 4.

### Customer Order

Represents an order associated with one or more Shipments.

### Customer

Represents the business receiving products from the warehouse.

### Warehouse

Represents the Warehouse that fulfilled the Shipment.

### User

Represents an authorized Manager or reporting employee.

---

## Initial Data Model

### Monthly Shipping Report

The Monthly Shipping Report is a generated reporting view rather than a permanent business transaction.

**Report Parameters:**

| Parameter | Type | Description |
|---|---|---|
| reportMonth | Integer | Selected month, 1 through 12 |
| reportYear | Integer | Selected four-digit year |
| warehouseId | Integer | Optional Warehouse filter |
| customerId | Integer | Optional Customer filter |
| itemId | Integer | Optional Individual Item filter |
| sortBy | String | Item Number, Description, or Quantity Shipped |

**Displayed Information:**

| Field | Description |
|---|---|
| Reporting Month | Selected calendar month |
| Reporting Year | Selected year |
| Item Number | Individual Item SKU |
| Item Description | Individual Item description |
| Total Quantity Shipped | Sum of applicable finalized Shipment Line quantities |
| Unit of Measure | Individual units |

**Relationships:**
- The report uses completed Shipment and Shipment Line information.
- The report groups applicable Shipment Lines by Individual Item.
- The report may be filtered using Warehouse, Customer, and Individual Item information.

**Derived Value:**
- Monthly Quantity Shipped for an Item = Sum of quantityShipped across qualifying finalized Shipment Lines for that Item during the selected month.

**Constraints:**
- reportMonth must be between 1 and 12.
- reportYear must identify a valid reporting year.
- Optional filters must reference valid records.
- One summary row must be produced per qualifying Individual Item.
- The report must not change underlying shipping records.

### Shipment

| Attribute | Type | Description |
|---|---|---|
| shipmentId | Integer | Unique Shipment identifier |
| shipmentNumber | String | Unique Shipment Number |
| customerOrderId | Integer | Foreign key referencing Customer Order |
| warehouseId | Integer | Foreign key referencing fulfilling Warehouse |
| status | String | Preparing, Ready for Delivery, Canceled, or Exception |
| readyAt | DateTime | Date and time the Shipment was finalized for delivery |

**Relationships:**
- Each Shipment belongs to one Customer Order.
- Each Shipment contains one or more Shipment Lines.
- Each Shipment is associated with the Warehouse that fulfilled it.
- A Customer Order may have multiple Shipments.

**Constraints:**
- shipmentId must be unique.
- shipmentNumber must be unique.
- A finalized Shipment must have a valid readyAt timestamp.
- Only finalized Ready for Delivery Shipments contribute to monthly totals.

### Shipment Line

| Attribute | Type | Description |
|---|---|---|
| shipmentLineId | Integer | Unique Shipment Line identifier |
| shipmentId | Integer | Foreign key referencing Shipment |
| customerOrderLineId | Integer | Foreign key referencing Customer Order Line |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityShipped | Integer | Actual finalized quantity shipped |

**Relationships:**
- Each Shipment Line belongs to one Shipment.
- Each Shipment Line references one Individual Item.
- Each Shipment Line references the related Customer Order Line.
- Shipment Lines contribute to monthly totals for their Individual Items.

**Constraints:**
- quantityShipped must be nonnegative.
- A finalized Shipment Line must not be counted more than once.
- A Shipment Line contributes only to the month determined by its Shipment's readyAt timestamp.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |
| isActive | Boolean | Indicates whether the Item is active |

**Relationships:**
- One Individual Item may appear on multiple Shipment Lines.
- All qualifying Shipment Lines for the same Item contribute to its monthly total.
- Deactivated Items remain identifiable in historical reports.

### Customer Order

| Attribute | Type | Description |
|---|---|---|
| customerOrderId | Integer | Unique Customer Order identifier |
| orderNumber | String | Unique Customer Order Number |
| customerId | Integer | Foreign key referencing Customer |

**Relationships:**
- A Customer Order belongs to one Customer.
- A Customer Order may have multiple Shipments.
- Customer Order entry is defined in Feature 12.

### Customer

| Attribute | Type | Description |
|---|---|---|
| customerId | Integer | Unique Customer identifier |
| customerNumber | String | Unique Customer Number |
| name | String | Customer business name |

**Relationships:**
- A Customer may have multiple Customer Orders.
- A Customer filter limits which associated Shipments contribute to the report.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique Warehouse identifier |
| warehouseCode | String | Unique Warehouse Code |
| name | String | Warehouse name |

**Relationships:**
- A Warehouse may fulfill multiple Shipments.
- A Warehouse filter limits which Shipments contribute to the report.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Authorized Managers generate and review Monthly Shipping Reports.

---

## Gherkin AC

### US-19.1: View Monthly Shipped Quantities

#### AC-19.1.1: Items were shipped during selected month

**Given** completed Shipments contain Individual Items shipped during October 2026  
**And** the User is authenticated as a Manager  
**When** the Manager generates the Monthly Shipping Report for October 2026  
**Then** the system identifies the applicable Individual Items  
**And** displays their total Quantity Shipped for October 2026.

#### AC-19.1.2: No Items were shipped during selected month

**Given** no finalized Shipments contain shipped quantities during February 2026  
**When** the Manager generates the report for February 2026  
**Then** the report contains no shipped Item rows  
**And** displays a message indicating that no matching shipping activity was found.

#### AC-19.1.3: Exclude Shipment from another month

**Given** Item A was shipped in September 2026  
**And** Item A was also shipped in October 2026  
**When** the Manager generates the report for October 2026  
**Then** the system includes only the October Shipment quantities.

#### AC-19.1.4: Exclude unfinished Shipment

**Given** a Shipment contains 20 units of Item A  
**And** the Shipment remains in Preparing status  
**When** the Manager generates the Monthly Shipping Report  
**Then** those 20 units are not included in finalized monthly shipping totals.

### US-19.2: Review Shipped Quantity by Item

#### AC-19.2.1: Item shipped once

**Given** Item A appears in one finalized Shipment during October 2026  
**And** its Quantity Shipped is 25 units  
**When** the Manager generates the report for October 2026  
**Then** Item A appears with a monthly total of 25 units.

#### AC-19.2.2: Item shipped multiple times

**Given** Item A appears in a finalized Shipment containing 20 units on October 5  
**And** Item A appears in another finalized Shipment containing 30 units on October 20  
**When** the Manager generates the report for October 2026  
**Then** Item A appears once  
**And** its total Quantity Shipped is 50 units.

#### AC-19.2.3: Item was not shipped

**Given** Item B has no completed Shipments during October 2026  
**When** the Manager generates the report for October 2026  
**Then** Item B is omitted from the default report.

#### AC-19.2.4: Multiple Items shipped

**Given** Item A has 50 units shipped during October 2026  
**And** Item B has 35 units shipped during October 2026  
**When** the Manager generates the report  
**Then** the report displays Item A with 50 units  
**And** Item B with 35 units  
**And** keeps their totals separate.

#### AC-19.2.5: Multiple Shipments from one Customer Order

**Given** Customer Order CO100 has two finalized Shipments in October 2026  
**And** both Shipments contain Item A  
**When** the Manager generates the October report  
**Then** the system includes Item A's shipped quantities from both Shipments  
**And** counts each Shipment Line exactly once.

### US-19.3: Select Reporting Month and Year

#### AC-19.3.1: Select valid month and year

**Given** the Manager opens the Monthly Shipping Report  
**When** the Manager selects October and 2026  
**Then** the system generates the report for October 2026  
**And** displays the selected reporting period.

#### AC-19.3.2: Distinguish years

**Given** Item A has Shipments in October 2025 and October 2026  
**When** the Manager generates the report for October 2026  
**Then** the report excludes quantities shipped in October 2025.

#### AC-19.3.3: Reject invalid month

**Given** the Manager is selecting the reporting period  
**When** the Manager enters month 13  
**Then** the system rejects the invalid month  
**And** requests a value from 1 through 12.

#### AC-19.3.4: Assign month using Shipment completion time

**Given** Shipment S100 was finalized on October 31, 2026  
**And** Shipment S101 was finalized on November 1, 2026  
**When** the Manager generates the October 2026 report  
**Then** Shipment S100 contributes to October totals  
**And** Shipment S101 does not contribute to October totals.

### US-19.4: Filter Monthly Shipping Activity

#### AC-19.4.1: Filter by Warehouse

**Given** finalized Shipments exist for Warehouses W1 and W2  
**When** the Manager selects Warehouse W1  
**Then** the report includes only applicable Shipments fulfilled by W1.

#### AC-19.4.2: Filter by Customer

**Given** finalized Shipments exist for Customer A and Customer B  
**When** the Manager selects Customer A  
**Then** the report includes only applicable Shipments associated with Customer A.

#### AC-19.4.3: Filter by Individual Item

**Given** Item A and Item B were shipped during the selected month  
**When** the Manager selects Item A  
**Then** the report displays only Item A's applicable shipped quantity total.

#### AC-19.4.4: Generate report without optional filters

**Given** the Manager selects a valid month and year  
**And** no Warehouse, Customer, or Item filter is selected  
**When** the Manager generates the report  
**Then** the system includes all qualifying Shipments the Manager is authorized to review.

#### AC-19.4.5: Sort by shipped quantity

**Given** the report contains multiple Individual Items  
**When** the Manager selects sorting by Quantity Shipped  
**Then** the system orders the report rows by their monthly shipped totals.

### US-19.5: Review Missing or Incomplete Shipping Data

#### AC-19.5.1: Shipment completion timestamp is missing

**Given** a finalized Shipment has Quantity Shipped recorded  
**And** its readyAt timestamp is missing  
**When** the Manager generates the Monthly Shipping Report  
**Then** the system identifies the Shipment as having incomplete date information  
**And** does not silently assign its quantities to an arbitrary month  
**And** warns that the report may be incomplete.

#### AC-19.5.2: Historical shipping information is unavailable

**Given** some historical Shipment records are unavailable for the selected month  
**When** the Manager generates the report  
**Then** the system identifies that the report may be incomplete  
**And** does not claim that no shipping occurred during the missing period.

#### AC-19.5.3: Delivery does not change monthly shipped total

**Given** Item A has 40 units recorded as shipped in October 2026  
**And** only 35 units were delivered to the Customer  
**When** the Manager generates the October report  
**Then** Item A contributes 40 units to the monthly shipped total  
**And** the 35 delivered units do not replace Quantity Shipped.

#### AC-19.5.4: Prevent duplicate counting from delivery attempts

**Given** Shipment S100 contains 20 units of Item A  
**And** the Shipment has two separate Delivery attempts  
**When** the Manager generates the Monthly Shipping Report  
**Then** the system counts the 20 shipped units only once.

#### AC-19.5.5: Preserve historical report after Item deactivation

**Given** Item A was shipped during September 2026  
**And** Item A was later deactivated  
**When** the Manager generates the September report  
**Then** Item A remains identifiable  
**And** its historical shipped quantity remains included.

#### AC-19.5.6: Reject unauthorized report access

**Given** a User is authenticated as a Driver without reporting permission  
**When** the User attempts to generate the Monthly Shipping Report  
**Then** the system denies access  
**And** does not display restricted shipping information.
