
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

## Assumptions

- **A-001:** Feature 14 provides finalized Shipment and Shipment Line information used by the Monthly Shipping Report.
- **A-002:** Feature 4 maintains Individual Item master data, including Item Number and description.
- **A-003:** Feature 12 maintains Customer Order information used to associate Shipments with Customers.
- **A-004:** Customer information is available through the Customer master data maintained in Feature 6.
- **A-005:** Each Shipment identifies the Warehouse responsible for fulfilling it.
- **A-006:** A Shipment is eligible for the monthly report only when it has been finalized as Ready for Delivery.
- **A-007:** A finalized Shipment has a readyAt timestamp identifying when shipping preparation was completed.
- **A-008:** The readyAt timestamp determines the Shipment's reporting month and year.
- **A-009:** The system uses a consistently configured warehouse reporting time zone to interpret Shipment timestamps.
- **A-010:** Quantity Shipped is recorded in nonnegative whole individual units.
- **A-011:** Each Shipment Line references one Individual Item.
- **A-012:** A Customer Order may be fulfilled through multiple Shipments.
- **A-013:** Each completed partial Shipment contributes to the month in which it was finalized.
- **A-014:** Delivery outcomes do not change the original Quantity Shipped recorded for a finalized Shipment.
- **A-015:** The report summarizes Quantity Shipped independently of the current Customer Order status.
- **A-016:** The Manager must select a reporting month and year before generating the report.
- **A-017:** Warehouse, Customer, and Individual Item filters are optional.
- **A-018:** The report includes only Warehouses the requesting User is authorized to review.
- **A-019:** Historical Shipment information remains available after related Customer, Item, or Warehouse records are deactivated.
- **A-020:** The Monthly Shipping Report is a generated read-only view and does not create or modify shipping transactions.
- **A-021:** Missing or invalid Shipment completion timestamps are treated as data-quality problems rather than assigned to an estimated month.
- **A-022:** Reported monthly totals can be traced back to the finalized Shipment Lines contributing to them.

**[NEEDS CLARIFICATION]** Confirm whether the configured warehouse reporting time zone is shared by all Warehouses or whether different Warehouses can have separate reporting time zones.

**[NEEDS CLARIFICATION]** Confirm whether a finalized Shipment can later change from Ready for Delivery to another status and, if so, how historical monthly totals should preserve the original finalized Shipment.

**[NEEDS CLARIFICATION]** Confirm the valid reporting-year range and whether future months may be selected.

**[NEEDS CLARIFICATION]** Confirm whether missing readyAt timestamps should be displayed in a separate data-quality list or only through a report warning.

---

## Edge Cases

### EC-19.1: No Shipments During the Selected Month

No qualifying finalized Shipments exist during the selected month.

The system displays an empty report and indicates that no matching shipping activity was found.

### EC-19.2: Same Item Appears in Multiple Shipments

An Individual Item appears in several finalized Shipment Lines during the same reporting month.

The system adds the applicable Quantity Shipped values and displays one summary row for that Item.

### EC-19.3: Same Item Appears in Different Months

An Item is shipped in September and October.

The October report includes only the applicable October Shipment quantities.

### EC-19.4: Same Month in Different Years

An Item is shipped in October 2025 and October 2026.

The October 2026 report excludes October 2025 quantities.

### EC-19.5: Shipment Is Still Preparing

A Shipment contains Items but remains in Preparing status.

Its Shipment Lines are excluded from finalized monthly totals.

### EC-19.6: Shipment Is Canceled

A Shipment is in Canceled status.

The system excludes its quantities from monthly totals.

### EC-19.7: Shipment Has Exception Status

A Shipment remains in Exception status.

The system excludes its quantities until the Shipment is successfully finalized according to Feature 14.

### EC-19.8: Shipment Is Finalized Near a Month Boundary

A Shipment is finalized near midnight on the last day of a month.

The system uses readyAt and the configured warehouse reporting time zone to determine the correct calendar month.

### EC-19.9: Shipment Completion Timestamp Is Missing

A Shipment is marked Ready for Delivery but has no valid readyAt timestamp.

The system identifies the missing timestamp and warns that monthly totals may be incomplete.

It does not assign the Shipment to an arbitrary month.

### EC-19.10: Multiple Shipments Belong to One Customer Order

One Customer Order is fulfilled through several finalized Shipments.

Each qualifying Shipment Line contributes to the monthly total exactly once.

### EC-19.11: Partial Shipment Is Completed

A Customer Order is partially fulfilled by a finalized Shipment.

The system includes the actual Quantity Shipped from that Shipment in the applicable month.

### EC-19.12: Delivery Is Incomplete or Failed

A finalized Shipment contains 40 units of an Item, but the associated Delivery is incomplete or unsuccessful.

The Monthly Shipping Report still uses the original 40 units shipped.

### EC-19.13: Shipment Has Multiple Delivery Attempts

A Shipment is associated with multiple delivery attempts.

The system counts each qualifying Shipment Line once, regardless of the number of Delivery attempts.

### EC-19.14: Item Has No Shipped Quantity During the Month

An Individual Item has no qualifying finalized Shipment Lines during the selected month.

The default report does not display a row for that Item.

### EC-19.15: Item Is Deactivated

An Individual Item was shipped during a historical month and later deactivated.

The historical report continues to identify the Item and includes its shipped quantity.

### EC-19.16: Customer Is Deactivated

A Customer associated with a historical Shipment is later deactivated.

The Shipment remains available for historical monthly reporting.

### EC-19.17: Warehouse Is Deactivated

A Warehouse associated with historical Shipments is later deactivated.

The report preserves its historical shipping activity for authorized Users.

### EC-19.18: Manager Has Access to Multiple Warehouses

A Manager has reporting permission for several Warehouses and does not select a Warehouse filter.

The report includes qualifying Shipments from all Warehouses that Manager is authorized to review.

### EC-19.19: Manager Has Limited Warehouse Access

A Manager has reporting permission for only one Warehouse.

The report does not include Shipments from unauthorized Warehouses, even when no Warehouse filter is selected.

### EC-19.20: Customer Filter Is Applied

Shipments for several Customers exist during the selected month.

When the Manager selects one Customer, only qualifying Shipments associated with that Customer contribute to the report.

### EC-19.21: Item Filter Is Applied

Several Items were shipped during the selected month.

When the Manager selects one Item, only Shipment Lines for that Item contribute to the report.

### EC-19.22: Invalid Reporting Month

The Manager enters a month outside the range 1 through 12.

The system rejects the value and requests a valid month.

### EC-19.23: Reporting Year Is Missing

The Manager attempts to generate a report without selecting a year.

The system requests a valid reporting year.

### EC-19.24: Duplicate Shipment Line Is Retrieved

The same finalized Shipment Line appears more than once during report processing.

The system counts its Quantity Shipped only once.

### EC-19.25: Quantity Shipped Is Negative

A Shipment Line contains an invalid negative Quantity Shipped value.

The system identifies the invalid data and does not silently include it in a monthly total.

### EC-19.26: Historical Shipping Information Is Incomplete

Some historical Shipment records are unavailable.

The system warns that the report may be incomplete rather than claiming no shipping occurred.

### EC-19.27: Unauthorized Report Access

A User without reporting permission attempts to generate the Monthly Shipping Report.

The system denies access and does not display restricted shipping information.

### EC-19.28: Report Is Generated Repeatedly

The Manager generates the same monthly report multiple times without changes to source data.

The system returns consistent totals without duplicating Shipment Lines or modifying shipping records.

---

## Success Criteria

- **SC-001:** Authorized Managers can generate a Monthly Shipping Report for a selected month and year.
- **SC-002:** The report uses finalized Shipment information maintained by Feature 14.
- **SC-003:** Only successfully finalized Ready for Delivery Shipments contribute to monthly totals.
- **SC-004:** Preparing, Canceled, and Exception Shipments are excluded.
- **SC-005:** Each Shipment is assigned to its reporting month using readyAt and the configured warehouse reporting time zone.
- **SC-006:** Monthly totals are calculated from Shipment Line quantityShipped values.
- **SC-007:** Quantity Ordered, Quantity Picked, and Quantity Delivered are not substituted for Quantity Shipped.
- **SC-008:** Each qualifying Shipment Line is counted exactly once.
- **SC-009:** Multiple Shipments containing the same Item are combined into one monthly Item total.
- **SC-010:** The report displays one summary row per qualifying Individual Item.
- **SC-011:** Each row identifies the Item Number, description, total Quantity Shipped, and unit of measure.
- **SC-012:** Shipments from different months and years are excluded from the selected reporting period.
- **SC-013:** All 12 calendar months are supported.
- **SC-014:** Missing or invalid reporting month and year values are rejected.
- **SC-015:** Warehouse filtering limits results to authorized Warehouses.
- **SC-016:** Customer filtering includes only applicable Customer Shipments.
- **SC-017:** Individual Item filtering includes only applicable Shipment Lines.
- **SC-018:** Optional filters may be left unselected.
- **SC-019:** Sorting by Item Number, description, or total Quantity Shipped is supported.
- **SC-020:** The Manager can review the Shipments contributing to an Item's monthly total.
- **SC-021:** Incomplete Shipment timestamps are identified without assigning quantities to an arbitrary month.
- **SC-022:** Missing historical shipping information produces a data-quality warning.
- **SC-023:** Items with no qualifying shipped quantity are omitted from the default report.
- **SC-024:** Empty results display a clear message indicating no matching shipping activity was found.
- **SC-025:** Delivery outcomes and repeated delivery attempts do not change or duplicate monthly shipped quantities.
- **SC-026:** Historical shipping information remains available after related Item, Customer, or Warehouse deactivation.
- **SC-027:** Unauthorized Users cannot access restricted report information.
- **SC-028:** Generating the report does not modify Shipment, Customer Order, or Inventory records.
- **SC-029:** Monthly totals can be traced to their contributing Shipment Lines.
- **SC-030:** All 24 original Gherkin Acceptance Criteria have corresponding tests.

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

---

## Data Ownership

### Individual Item Data

**Owning Feature:** Feature 4 - Maintain Individual Items

Feature 4 owns Individual Item master data, including:

- Item ID
- Item Number
- Item Description
- Item active or inactive status

Feature 19 reads Individual Item information to identify the products included in the Monthly Shipping Report.

Feature 19 MUST NOT create, edit, deactivate, or delete Individual Item records.

Historical Item identification MUST remain available after an Item is deactivated.

### Customer Data

**Owning Feature:** Feature 6 - Maintain Customers

Feature 6 owns Customer master data, including:

- Customer ID
- Customer Number
- Customer Name

Feature 19 reads Customer information to support filtering monthly shipping activity by Customer.

Feature 19 MUST NOT modify Customer master data.

Historical Customer identification MUST remain available after deactivation.

### Warehouse Data

**Owning Feature:** Maintain Warehouses functionality

Warehouse master data includes:

- Warehouse ID
- Warehouse Code
- Warehouse Name

Feature 19 reads Warehouse information to determine which Warehouse fulfilled each Shipment.

Feature 19 MUST NOT create, edit, deactivate, or delete Warehouse records.

Historical Warehouse identification MUST remain available after deactivation.

**[NEEDS CLARIFICATION]** Confirm the exact feature number responsible for maintaining Warehouse master data.

### Customer Order Data

**Owning Feature:** Feature 12 - Enter Customer Orders

Feature 12 maintains Customer Order information, including:

- Customer Order ID
- Customer Order Number
- Customer ID
- Customer Order Line references
- Quantity Ordered

Feature 19 reads Customer Order information to associate Shipments with Customers.

Feature 19 MUST NOT create, update, cancel, or delete Customer Orders.

Quantity Ordered MUST NOT be used to calculate monthly shipped quantities.

### Shipment Data

**Owning Feature:** Feature 14 - Ship Customer Orders

Feature 14 owns Shipment information, including:

- Shipment ID
- Shipment Number
- Customer Order ID
- Warehouse ID
- Shipment Status
- Shipment readyAt timestamp

Feature 19 reads Shipment information to determine which Shipments qualify for the selected reporting month.

A qualifying Shipment MUST:

- Have been successfully finalized as Ready for Delivery.
- Have a valid readyAt timestamp.
- Fall within the selected calendar month and year using the configured warehouse reporting time zone.
- Belong to a Warehouse the requesting User is authorized to review.
- Match any selected Warehouse or Customer filters.

Feature 19 MUST NOT modify Shipment records or their status.

### Shipment Line Data

**Owning Feature:** Feature 14 - Ship Customer Orders

Feature 14 owns Shipment Line information, including:

- Shipment Line ID
- Shipment ID
- Customer Order Line ID
- Item ID
- Quantity Shipped

Feature 19 uses finalized Shipment Line quantityShipped values to calculate monthly totals.

Each qualifying Shipment Line MUST be counted exactly once.

Feature 19 MUST NOT modify Quantity Shipped or Shipment Line records.

### Monthly Shipping Report

**Owning Feature:** Feature 19 - Report Monthly Shipped Item Quantities

Feature 19 owns:

- Monthly Shipping Report generation
- Reporting month and year selection
- Report filtering
- Report sorting
- Monthly shipped quantity calculations
- Grouping Shipment Lines by Individual Item
- Displaying one summary row per qualifying Item
- Shipment contribution details
- Data-quality warnings
- Read-only report presentation

The Monthly Shipping Report is a generated reporting view rather than a permanent business transaction.

Feature 19 MUST NOT overwrite data owned by Features 4, 6, 12, or 14.

### User and Authorization Data

**Owning Component:** Shared User and Access Control functionality

The shared authorization component maintains:

- User accounts
- User roles
- Authentication information
- Reporting permissions
- Authorized Warehouse access

Feature 19 checks whether the requesting User is authorized to generate and review Monthly Shipping Reports.

Feature 19 MUST NOT modify User accounts or permissions.

### Data Ownership Rules

- Feature 4 owns Individual Item master data.
- Feature 6 owns Customer master data.
- Feature 12 owns Customer Order entry information.
- Feature 14 owns Shipment and Shipment Line information.
- Warehouse master data ownership must be confirmed.
- Feature 19 owns monthly reporting calculations, filtering, sorting, and presentation.
- Shared authorization functionality owns User reporting permissions.
- Feature 19 MUST preserve references to original source records.
- Feature 19 MUST remain read-only.

---

## API Requirements

The following API endpoints are proposed for Feature 19.

Final endpoint names, request formats, and response structures must follow the Warehouse Management System's established API conventions.

### API-19.1: Generate Monthly Shipping Report

**Method:** GET

**Proposed Endpoint:**

`/api/reports/monthly-shipped-items`

**Purpose:**

Generate a read-only report showing total Quantity Shipped for each Individual Item during a selected calendar month and year.

**Query Parameters:**

| Parameter | Type | Required | Description |
|---|---|---|---|
| reportMonth | Integer | Yes | Selected month, 1 through 12 |
| reportYear | Integer | Yes | Selected reporting year |
| warehouseId | Integer | No | Filter by Warehouse |
| customerId | Integer | No | Filter by Customer |
| itemId | Integer | No | Filter by Individual Item |
| sortBy | String | No | Item Number, Description, or Quantity Shipped |

**Expected Response Information:**

- Reporting Month
- Reporting Year
- Reporting Time Zone
- Applied Warehouse filter
- Applied Customer filter
- Applied Item filter
- Item ID
- Item Number
- Item Description
- Total Quantity Shipped
- Unit of Measure
- Number of contributing Shipment Lines
- Data-quality warning, when applicable

**Calculation Rules:**

Monthly Quantity Shipped for an Item = Sum of quantityShipped across all qualifying finalized Shipment Lines for that Item during the selected month.

**Shipment Qualification Rules:**

- The Shipment must be finalized as Ready for Delivery.
- The Shipment must have a valid readyAt timestamp.
- The readyAt timestamp must fall within the selected reporting month and year using the configured warehouse reporting time zone.
- The Shipment must belong to an authorized Warehouse.
- The Shipment must match the selected Warehouse filter, if provided.
- The Shipment must belong to a Customer Order associated with the selected Customer, if provided.
- The Shipment Line must match the selected Item filter, if provided.

**Aggregation Rules:**

- Group qualifying Shipment Lines by Individual Item.
- Sum Quantity Shipped for each Item.
- Count each Shipment Line exactly once.
- Display one summary row per qualifying Item.
- Exclude Items with no qualifying shipped quantities from the default report.
- Do not use Quantity Ordered, Quantity Picked, or Quantity Delivered.
- Do not duplicate shipped quantities because of multiple Delivery attempts.

**Validation Rules:**

- The requesting User must be authenticated.
- The requesting User must have reporting permission.
- reportMonth must be between 1 and 12.
- reportYear must identify a valid reporting year.
- Optional filters must reference valid records.
- Warehouse access restrictions must be enforced.
- Quantity Shipped must be a nonnegative whole number.
- Missing readyAt timestamps must not be assigned to arbitrary months.
- Report generation must not modify source records.

**Possible Responses:**

- `200 OK` - Report generated successfully, including empty results.
- `400 Bad Request` - Invalid report parameters.
- `401 Unauthorized` - User is not authenticated.
- `403 Forbidden` - User lacks reporting permission or Warehouse access.
- `500 Internal Server Error` - Unexpected server failure.

**[NEEDS CLARIFICATION]** Confirm the valid reporting-year range and whether future reporting periods are permitted.

**[NEEDS CLARIFICATION]** Confirm whether the configured reporting time zone is shared by all Warehouses or may differ by Warehouse.

### API-19.2: Retrieve Monthly Item Shipment Details

**Method:** GET

**Proposed Endpoint:**

`/api/reports/monthly-shipped-items/{itemId}/shipments`

**Purpose:**

Allow an authorized Manager to review the Shipment Lines contributing to an Individual Item's monthly shipped quantity total.

**Path Parameter:**

- `itemId` - Unique identifier of the Individual Item.

**Query Parameters:**

| Parameter | Type | Required | Description |
|---|---|---|---|
| reportMonth | Integer | Yes | Selected month |
| reportYear | Integer | Yes | Selected year |
| warehouseId | Integer | No | Optional Warehouse filter |
| customerId | Integer | No | Optional Customer filter |

**Expected Response Information:**

- Reporting Month
- Reporting Year
- Item ID
- Item Number
- Item Description
- Monthly Total Quantity Shipped
- Shipment ID
- Shipment Number
- Shipment Line ID
- Customer Order Number
- Customer Number
- Customer Name
- Warehouse Code
- Warehouse Name
- Shipment readyAt timestamp
- Quantity Shipped for each contributing Shipment Line

**Processing Rules:**

- Use the same reporting period and filters as the summary report.
- Include only qualifying finalized Shipment Lines.
- Preserve the relationship between Shipment Lines and their Shipments.
- Count each Shipment Line once.
- Ensure the sum of contributing Shipment Line quantities equals the summary total.
- Restrict results to authorized Warehouses.
- Do not modify Shipment records.

**Possible Responses:**

- `200 OK` - Shipment details returned successfully.
- `400 Bad Request` - Invalid report parameters.
- `401 Unauthorized` - User is not authenticated.
- `403 Forbidden` - User lacks reporting permission.
- `404 Not Found` - Requested Item does not exist.

### API-19.3: Retrieve Monthly Shipping Data-Quality Issues

**Method:** GET

**Proposed Endpoint:**

`/api/reports/monthly-shipped-items/data-quality`

**Purpose:**

Allow authorized reporting personnel to review known incomplete Shipment information that may affect monthly report accuracy.

**Query Parameters:**

| Parameter | Type | Required | Description |
|---|---|---|---|
| reportMonth | Integer | Yes | Selected reporting month |
| reportYear | Integer | Yes | Selected reporting year |
| warehouseId | Integer | No | Optional Warehouse filter |

**Expected Response Information:**

- Shipment ID
- Shipment Number
- Warehouse ID
- Shipment Status
- readyAt timestamp, when available
- Data-quality issue type
- Description of the issue
- Potential impact on reporting

**Processing Rules:**

- Identify finalized Shipments with missing or invalid readyAt timestamps.
- Identify known incomplete historical Shipment information.
- Do not silently assign missing timestamps to the selected month.
- Clearly identify when the affected reporting period cannot be determined.
- Restrict results to authorized Warehouse information.
- Do not modify Shipment data.

**[NEEDS CLARIFICATION]** Confirm whether missing readyAt records should be displayed for every report period as unresolved date-quality issues or only in a separate general data-quality view.

### API Security Requirements

- All report endpoints MUST require authentication.
- Reporting permission MUST be checked on the server.
- Warehouse access restrictions MUST be enforced.
- Unauthorized Users MUST NOT receive restricted Shipment information.
- Drivers without reporting permission MUST be denied access.
- Report endpoints MUST be read-only.
- Report generation MUST NOT modify Shipment, Shipment Line, Customer Order, or Inventory records.
- Historical shipping information MUST remain traceable to its original Shipment Lines.

---

## Screen Requirements

### SCREEN-19.1: Monthly Shipping Report Screen

**Purpose:**

Allow authorized Managers to generate and review monthly Quantity Shipped totals for Individual Items.

**Authorized Users:**

- Warehouse Managers
- Approved reporting personnel

**Screen Elements:**

- Page title: Monthly Shipping Report
- Reporting Month selection
- Reporting Year selection
- Warehouse filter
- Customer filter
- Individual Item filter
- Sort By selection
- Generate Report button
- Clear Filters button
- Results table
- Empty-results message
- Data-quality warning, when applicable

**Results Table Columns:**

| Column | Description |
|---|---|
| Item Number | Individual Item SKU |
| Item Description | Item description |
| Total Quantity Shipped | Monthly shipped quantity |
| Unit of Measure | Individual units |
| Details | Read-only access to contributing Shipment Lines |

**Screen Behavior:**

1. The Manager opens the Monthly Shipping Report from the reporting menu.
2. The system displays the reporting period controls.
3. The Manager selects a reporting month.
4. The Manager selects a reporting year.
5. The Manager optionally selects a Warehouse.
6. The Manager optionally selects a Customer.
7. The Manager optionally selects an Individual Item.
8. The Manager optionally selects a sorting method.
9. The Manager selects Generate Report.
10. The system validates the reporting period and filters.
11. The system retrieves qualifying finalized Shipment Lines.
12. The system calculates monthly Quantity Shipped totals.
13. The system groups the totals by Individual Item.
14. The system displays one summary row per qualifying Item.
15. The system displays a data-quality warning if known incomplete Shipment information may affect the report.
16. The Manager may select an Item to review its contributing Shipments.

**Default Behavior:**

- Reporting Month and Reporting Year are required.
- Warehouse, Customer, and Individual Item filters are optional.
- Only authorized Warehouses are included.
- Only successfully finalized Ready for Delivery Shipments contribute to totals.
- Items without qualifying shipped quantities are omitted.
- The report remains read-only.

**Validation:**

- Reporting Month must be between 1 and 12.
- Reporting Year must be valid.
- Optional filters must reference valid records.
- Unauthorized Warehouse selections must be rejected.
- No matching Shipments must produce an empty-results message.
- Incomplete historical information must produce an appropriate warning.

### SCREEN-19.2: Monthly Item Shipment Details Screen

**Purpose:**

Allow an authorized Manager to review the individual Shipment Lines contributing to an Item's monthly shipped quantity total.

**Displayed Information:**

- Reporting Month
- Reporting Year
- Item Number
- Item Description
- Monthly Total Quantity Shipped
- Unit of Measure

**Shipment Details Table:**

| Column | Description |
|---|---|
| Shipment Number | Shipment reference |
| Customer Order Number | Associated Customer Order |
| Customer | Customer Number or Name |
| Warehouse | Warehouse that fulfilled the Shipment |
| Shipment Date | Shipment readyAt timestamp |
| Quantity Shipped | Finalized Shipment Line quantity |

**Screen Behavior:**

1. The Manager selects an Item from the Monthly Shipping Report.
2. The system retrieves qualifying Shipment Lines for that Item.
3. The system applies the same month, year, and optional filters.
4. The system displays the contributing Shipments.
5. The system displays Quantity Shipped for each Shipment Line.
6. The system displays the monthly total.
7. The Manager may return to the summary report.
8. No edit or delete actions are available.

**Validation:**

- Each Shipment Line must be counted once.
- The displayed Shipment Line quantities must add up to the monthly total.
- Unauthorized Warehouse information must not be displayed.
- Only finalized Shipment information may contribute to the total.

### SCREEN-19.3: Monthly Shipping Data-Quality View

**Purpose:**

Inform authorized Managers when missing or incomplete Shipment information may affect monthly totals.

**Displayed Information:**

- Shipment Number, when available
- Warehouse
- Shipment Status
- readyAt timestamp, when available
- Data-quality issue
- Potential reporting impact

**Screen Behavior:**

1. The system identifies known incomplete Shipment information.
2. The Monthly Shipping Report displays a warning.
3. The Manager may open the data-quality view.
4. The system displays the available issue details.
5. The Manager may return to the Monthly Shipping Report.
6. The view remains read-only.

**[NEEDS CLARIFICATION]** Confirm whether data-quality issues should appear in a separate screen or as a section of the Monthly Shipping Report.

### SCREEN-19.4: Empty Results and Validation Messages

**Purpose:**

Provide clear feedback when report parameters are invalid, no matching shipping activity exists, or historical information is incomplete.

**Required Messages:**

When no matching Shipments exist:

`No matching shipping activity was found for the selected month and filters.`

When the reporting month is missing:

`Please select a reporting month.`

When the reporting year is missing:

`Please select a reporting year.`

When the reporting month is invalid:

`Reporting Month must be between 1 and 12.`

When the reporting year is invalid:

`Please enter a valid reporting year.`

When a Warehouse is unauthorized:

`You do not have permission to view shipping information for this Warehouse.`

When a finalized Shipment lacks a valid readyAt timestamp:

`Some finalized Shipments have missing or invalid completion dates. Monthly totals may be incomplete.`

When historical Shipment information is unavailable:

`Historical shipping information is incomplete. The report may not include all shipping activity.`

When a User lacks reporting permission:

`You do not have permission to view this report.`

### Screen Design Requirements

- Follow the Warehouse Management System's established UI style.
- Use consistent Item, Shipment, Customer, and Warehouse labels.
- Clearly display the selected reporting month and year.
- Display shipped quantities in individual units.
- Show one summary row per qualifying Individual Item.
- Support sorting by Item Number, Item description, and Quantity Shipped.
- Provide read-only access to contributing Shipment Lines.
- Clearly identify incomplete historical information.
- Preserve historical Item, Customer, and Warehouse identification.
- Use consistent date and time formatting.
- Support readable tables containing multiple Items.
- Do not provide report-side editing controls.
- Do not require paper records to review monthly shipping activity.

**[NEEDS CLARIFICATION]** Confirm final Figma screen layouts, navigation placement, and table presentation.

---

## Definition of Done

Feature 19 is considered complete when the following conditions are satisfied.

### Requirements

- [ ] All Functional Requirements FR-001 through FR-058 are implemented or explicitly deferred.
- [ ] All User Stories US-19.1 through US-19.5 are supported.
- [ ] All 24 Gherkin Acceptance Criteria have corresponding tests.
- [ ] All clarification items have been reviewed.
- [ ] The implementation follows approved requirements.

### Data Model

- [ ] Shipment records include required identifiers and status.
- [ ] Shipment records include Warehouse references.
- [ ] Finalized Shipments include valid readyAt timestamps.
- [ ] Shipment Lines include Item references.
- [ ] Shipment Lines include Quantity Shipped.
- [ ] Customer Order relationships are preserved.
- [ ] Customer relationships are preserved.
- [ ] Warehouse relationships are preserved.
- [ ] Individual Item identification is preserved.
- [ ] Historical shipping information remains available after deactivation.

### Business Logic

- [ ] Monthly totals use finalized Shipment Line quantityShipped values.
- [ ] Only qualifying Ready for Delivery Shipments are included.
- [ ] Preparing, Canceled, and Exception Shipments are excluded.
- [ ] readyAt determines the reporting month and year.
- [ ] The configured warehouse reporting time zone is applied consistently.
- [ ] Each qualifying Shipment Line is counted exactly once.
- [ ] Multiple Shipment Lines for the same Item are summed correctly.
- [ ] One summary row is produced per qualifying Item.
- [ ] Quantity Ordered is not substituted for Quantity Shipped.
- [ ] Quantity Picked is not substituted for Quantity Shipped.
- [ ] Quantity Delivered is not substituted for Quantity Shipped.
- [ ] Multiple Delivery attempts do not duplicate shipped quantities.
- [ ] Partial Shipments contribute to the correct reporting month.
- [ ] Customer Order status does not incorrectly change finalized shipped totals.
- [ ] Items with no qualifying shipped quantities are omitted.
- [ ] Negative Quantity Shipped values are identified as invalid.
- [ ] Missing readyAt timestamps are not assigned to arbitrary months.
- [ ] Incomplete historical information is identified.
- [ ] Monthly totals remain traceable to contributing Shipment Lines.

### API

- [ ] Monthly Shipping Report API is implemented.
- [ ] Monthly Item Shipment Details API is implemented.
- [ ] Data-quality information is available through an approved API or existing reporting service.
- [ ] Month validation works.
- [ ] Year validation works.
- [ ] Warehouse filtering works.
- [ ] Customer filtering works.
- [ ] Individual Item filtering works.
- [ ] Report sorting works.
- [ ] Warehouse authorization is enforced.
- [ ] Unauthorized reporting access is denied.
- [ ] Empty results are handled correctly.
- [ ] API operations remain read-only.

### User Interface

- [ ] Monthly Shipping Report screen is implemented.
- [ ] Reporting Month selection is available.
- [ ] Reporting Year selection is available.
- [ ] Warehouse filter is available.
- [ ] Customer filter is available.
- [ ] Individual Item filter is available.
- [ ] Sorting controls are available.
- [ ] Generate Report action works.
- [ ] Clear Filters action works.
- [ ] Results display Item Number and description.
- [ ] Results display Total Quantity Shipped.
- [ ] Unit of measure is identified as individual units.
- [ ] Shipment contribution details are available.
- [ ] Empty results display a clear message.
- [ ] Invalid report parameters display clear messages.
- [ ] Incomplete historical information displays a warning.
- [ ] Screens follow the approved Figma design.
- [ ] No report-side editing controls are provided.

### Testing

- [ ] Unit tests verify monthly Quantity Shipped calculations.
- [ ] Unit tests verify grouping by Individual Item.
- [ ] Unit tests verify multiple Shipment aggregation.
- [ ] Unit tests verify exclusion of Shipments outside the selected month.
- [ ] Unit tests verify separation of the same month in different years.
- [ ] Unit tests verify Ready for Delivery status filtering.
- [ ] Unit tests verify exclusion of Preparing Shipments.
- [ ] Unit tests verify exclusion of Canceled Shipments.
- [ ] Unit tests verify exclusion of Exception Shipments.
- [ ] Unit tests verify reporting time zone behavior.
- [ ] Unit tests verify duplicate Shipment Line prevention.
- [ ] Unit tests verify partial Shipment inclusion.
- [ ] Unit tests verify that Delivery outcomes do not change shipped totals.
- [ ] Unit tests verify that multiple Delivery attempts do not duplicate totals.
- [ ] Unit tests verify Warehouse filtering.
- [ ] Unit tests verify Customer filtering.
- [ ] Unit tests verify Individual Item filtering.
- [ ] Unit tests verify report sorting.
- [ ] Unit tests verify invalid reporting month handling.
- [ ] Unit tests verify invalid reporting year handling.
- [ ] Unit tests verify missing readyAt handling.
- [ ] Unit tests verify negative Quantity Shipped handling.
- [ ] Integration tests verify Shipment and Shipment Line relationships.
- [ ] Integration tests verify Customer Order and Customer relationships.
- [ ] Integration tests verify Warehouse authorization.
- [ ] Integration tests verify Item deactivation does not remove historical quantities.
- [ ] API tests verify report generation.
- [ ] API tests verify unauthorized access is denied.
- [ ] UI tests verify report filters and detail navigation.
- [ ] All 24 original Gherkin Acceptance Criteria are covered.
- [ ] All automated tests pass.

### Code Quality and Documentation

- [ ] Code follows project conventions.
- [ ] Monthly calculation rules are documented.
- [ ] Reporting time zone behavior is documented.
- [ ] API documentation is updated.
- [ ] Data model relationships are documented.
- [ ] Validation and error messages are reviewed.
- [ ] No unrelated feature behavior is modified.
- [ ] Code is reviewed and approved.
- [ ] Changes are committed to the correct Git branch.

---

## Out of Scope

The following capabilities are not included in Feature 19.

### Individual Item Maintenance

Feature 19 does not:

- Create Individual Items.
- Edit Item descriptions.
- Change Item Numbers.
- Activate or deactivate Items.
- Delete Item records.

Individual Item maintenance belongs to Feature 4.

### Customer Maintenance

Feature 19 does not:

- Create Customers.
- Edit Customer information.
- Activate or deactivate Customers.
- Delete Customer records.

Customer maintenance belongs to Feature 6.

### Warehouse Maintenance

Feature 19 does not:

- Create Warehouses.
- Edit Warehouse information.
- Activate or deactivate Warehouses.
- Delete Warehouse records.

These operations belong to the applicable Warehouse maintenance feature.

### Customer Order Maintenance

Feature 19 does not:

- Create Customer Orders.
- Add or remove Customer Order Lines.
- Change ordered quantities.
- Cancel Customer Orders.
- Modify Customer Order status.

Customer Order entry belongs to Feature 12.

### Picking Operations

Feature 19 does not:

- Generate picking tasks.
- Pick Items from storage bins.
- Confirm picked quantities.
- Adjust picked quantities.
- Replenish picking locations.

These operations belong to the applicable warehouse picking feature.

### Shipping Operations

Feature 19 does not:

- Create Shipments.
- Add or remove Shipment Lines.
- Change Quantity Shipped.
- Finalize Shipments.
- Cancel Shipments.
- Modify readyAt timestamps.

Shipping operations belong to Feature 14.

### Delivery Operations

Feature 19 does not:

- Assign Deliveries to Drivers.
- Start delivery attempts.
- Confirm delivered quantities.
- Complete Deliveries.
- Record Delivery Discrepancies.
- Resolve Delivery Discrepancies.

Delivery operations belong to Feature 15.

### Inventory Maintenance

Feature 19 does not:

- Adjust Inventory quantities.
- Move Inventory between bins.
- Reconcile Inventory balances.
- Create replenishment tasks.
- Modify warehouse stock levels.

These activities belong to separate warehouse operations.

### Financial Processing

Feature 19 does not:

- Generate invoices.
- Calculate Customer charges.
- Process payments.
- Issue Customer refunds.
- Calculate shipping costs.
- Calculate shipping revenue.

### Advanced Reporting

The following capabilities are deferred unless separately approved:

- Weekly or daily shipping summaries.
- Year-to-date shipping summaries.
- Month-over-month trend charts.
- Predictive shipping volume analysis.
- Automatic scheduled reports.
- Email report delivery.
- Custom reporting dashboards.
- Automatic PDF or spreadsheet exports.
- Warehouse performance rankings.
- Customer shipping trend analysis.

### Historical Data Correction

Feature 19 does not provide report-screen functionality for:

- Modifying historical Shipment quantities.
- Changing Shipment completion timestamps.
- Editing historical Shipment Lines.
- Deleting finalized Shipment records.
- Reassigning Shipments to different reporting months.

Historical corrections must be handled through separately authorized workflows.

---

**End of Feature 19: Report Monthly Shipped Item Quantities**
