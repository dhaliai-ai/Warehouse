
# Feature: Report Deliveries That Do Not Match What Was Shipped

**Feature ID:** 18  
**Branch pattern:** `feature/18-delivery-shipment-differences`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System provides authorized Managers with a report identifying differences between Quantity Shipped and Quantity Delivered for Customer Orders. The report uses completed Shipment and Delivery information, identifies shortages and reported apparent over-deliveries, preserves Delivery Route information, and supports investigation of unsuccessful or partially completed deliveries. The system distinguishes confirmed quantity differences from pending deliveries and preserves historical delivery discrepancies.

---

## User Stories

### US-18.1: View Delivery Differences

**As a** Warehouse Manager  
**I want to** generate a report of Customer Order Items where Quantity Delivered differs from Quantity Shipped  
**So that** I can identify delivery exceptions.

**Priority:** P1  
**Independent test:** Generate a report containing a finalized Delivery with fewer units delivered than shipped and verify that the difference appears.

### US-18.2: Review Delivery Difference Details

**As a** Warehouse Manager  
**I want to** review the Customer, Customer Order, Shipment, Item, Quantity Shipped, and Quantity Delivered  
**So that** I can understand which products did not reach the Customer as expected.

**Priority:** P1  
**Independent test:** Open a reported discrepancy and verify that the Customer Order, Item, Shipment, shipped quantity, delivered quantity, and difference are displayed.

### US-18.3: Distinguish Delivery Shortages and Over-Delivery Reports

**As a** Warehouse Manager  
**I want to** distinguish confirmed delivery shortages from apparent over-deliveries  
**So that** I can investigate each type of delivery exception appropriately.

**Priority:** P1  
**Independent test:** Record a delivery shortage and an apparent over-delivery exception, then verify that the report identifies the two issues separately.

### US-18.4: Filter Delivery Difference Report

**As a** Warehouse Manager  
**I want to** filter delivery differences by Customer, Delivery Route, Individual Item, and date range  
**So that** I can investigate specific Customers, routes, products, or reporting periods.

**Priority:** P2  
**Independent test:** Apply a Customer and Delivery Route filter and verify that only matching report records appear.

### US-18.5: Review Incomplete and Failed Deliveries

**As a** Warehouse Manager  
**I want to** distinguish pending Deliveries from completed delivery exceptions  
**So that** I do not incorrectly treat undelivered products still in transit as confirmed shortages.

**Priority:** P2  
**Independent test:** Generate the report while a Delivery is In Progress and verify that it is excluded from finalized shortage results but can be viewed separately as pending.

### US-18.6: Review Historical Delivery Discrepancies

**As a** Warehouse Manager  
**I want to** review discrepancies from earlier delivery attempts even after a later attempt resolves the outstanding quantity  
**So that** I can identify recurring delivery problems.

**Priority:** P2  
**Independent test:** Record a partial delivery, complete a later delivery attempt, and verify that the original discrepancy remains available in historical reporting.

---

## Functional Requirements

- **FR-001:** The system MUST compare Quantity Shipped with Quantity Delivered for Customer Order Items.
- **FR-002:** The system MUST identify Customer Order Items where finalized delivery information shows a difference between Quantity Shipped and Quantity Delivered.
- **FR-003:** The system MUST provide applicable differences in a Delivery Difference Report.
- **FR-004:** The report MUST identify the Customer Order associated with each difference.
- **FR-005:** The report MUST identify the Customer associated with the Customer Order.
- **FR-006:** The report MUST identify the Shipment associated with the delivery difference.
- **FR-007:** The report MUST identify the Individual Item by Item Number and description.
- **FR-008:** The report MUST display Quantity Shipped and Quantity Delivered in individual units.
- **FR-009:** The system MUST preserve Quantity Shipped separately from Quantity Delivered.
- **FR-010:** The system MUST calculate Difference Units as Quantity Delivered minus Quantity Shipped for finalized shipment-level comparisons.
- **FR-011:** The system MUST identify a negative Difference Units value as a delivery shortage.
- **FR-012:** The system MUST identify matching Quantity Shipped and Quantity Delivered values as having no outstanding shipment-level quantity difference.
- **FR-013:** The system MUST preserve reported apparent over-deliveries as exceptions requiring authorized review.
- **FR-014:** The system MUST NOT automatically increase confirmed Quantity Delivered above Quantity Shipped when a Driver reports an apparent over-delivery.
- **FR-015:** The report MUST distinguish confirmed shortages from unverified apparent over-delivery exceptions.
- **FR-016:** The system MUST include each applicable Individual Item difference in the report.
- **FR-017:** The system MUST support reporting multiple differing Items from one Customer Order.
- **FR-018:** The system MUST support reporting differences from multiple Shipments belonging to the same Customer Order.
- **FR-019:** The system MUST preserve the relationship between each Delivery and its Delivery Route.
- **FR-020:** The report MUST identify the Delivery Route associated with each reported delivery discrepancy.
- **FR-021:** The report MUST identify the Driver associated with each finalized Delivery.
- **FR-022:** The report MUST display the date associated with each finalized delivery discrepancy.
- **FR-023:** The report date for a finalized delivery discrepancy MUST be the date and time the relevant delivery attempt was finalized.
- **FR-024:** The default report MUST include finalized Delivery attempts in Delivered, Partially Delivered, or Failed Attempt status when they contain reportable discrepancies.
- **FR-025:** The default report MUST exclude Deliveries still in Assigned or In Progress status from finalized discrepancy results.
- **FR-026:** The system MUST allow a Manager to optionally include pending delivery information.
- **FR-027:** Pending delivery information MUST be identified as Pending Delivery rather than a confirmed shortage.
- **FR-028:** The system MUST include unsuccessful delivery attempts that have been finalized as Failed Attempt.
- **FR-029:** A Failed Attempt with zero units delivered MUST preserve the undelivered quantity for reporting.
- **FR-030:** The system MUST allow a Manager to filter the report by Customer.
- **FR-031:** The system MUST allow a Manager to filter the report by Delivery Route.
- **FR-032:** The system MUST allow a Manager to filter the report by Individual Item.
- **FR-033:** The system MUST allow a Manager to filter the report by date range.
- **FR-034:** The system MUST allow a Manager to filter the report by discrepancy type.
- **FR-035:** Supported discrepancy filters MUST include All, Shortage, Apparent Over-Delivery, and Failed Delivery.
- **FR-036:** The system MUST allow the report to be generated without selecting a specific Customer, Route, or Item.
- **FR-037:** The system MUST validate that the report start date is not later than the end date.
- **FR-038:** The system MUST display an empty result when no delivery differences match the selected criteria.
- **FR-039:** The system MUST distinguish an empty report from unavailable or incomplete historical delivery information.
- **FR-040:** The system MUST NOT report matching finalized Shipment and Delivery quantities as outstanding shipment-level shortages.
- **FR-041:** The system MUST preserve historical Delivery Discrepancy records even when later delivery attempts resolve the outstanding quantity.
- **FR-042:** The system MUST distinguish historical delivery-attempt discrepancies from currently outstanding shipment-level differences.
- **FR-043:** The system MUST calculate cumulative Quantity Delivered for a Shipment Line from its finalized Delivery Lines.
- **FR-044:** The system MUST NOT count the same finalized Delivery Line more than once.
- **FR-045:** The system MUST preserve original Quantity Shipped even when subsequent deliveries occur.
- **FR-046:** The system MUST NOT use Quantity Picked as a substitute for Quantity Shipped.
- **FR-047:** The system MUST NOT use Quantity Ordered as a substitute for Quantity Delivered.
- **FR-048:** The system MUST use Shipment information maintained in Feature 14.
- **FR-049:** The system MUST use Delivery information maintained in Feature 15.
- **FR-050:** The system MUST preserve the Customer Order Line quantities maintained in Features 12 through 15.
- **FR-051:** The system MUST provide access to the associated Shipment and Delivery history for each reported difference.
- **FR-052:** The report MUST be read-only.
- **FR-053:** The system MUST restrict report access to authorized Managers and approved reporting personnel.
- **FR-054:** The system MUST preserve Customer, Item, Shipment, Delivery, and Delivery Route identification even when related master records are later deactivated.
- **FR-055:** The system MUST support sorting report results by Customer, Delivery Route, Customer Order Number, Item Number, report date, or difference magnitude.
- **FR-056:** The system MUST preserve the relationships between Customer Orders, Customer Order Lines, Shipments, Shipment Lines, Deliveries, Delivery Lines, Delivery Routes, and Delivery Discrepancies.
- **FR-057:** The system MUST NOT modify shipping or delivery quantities when generating the report.
- **FR-058:** The system MUST make confirmed delivery discrepancy information available for management review without requiring paper records.

---

## Assumptions

- **A-001:** Feature 6 owns Customer master data, including Customer identification.
- **A-002:** Feature 4 owns Individual Item master data, including Item Number and description.
- **A-003:** Customer Order and Customer Order Line information is maintained by the applicable Customer Order features, including Features 12 through 15.
- **A-004:** Feature 14 owns Shipment and Shipment Line information, including Quantity Shipped.
- **A-005:** Feature 15 owns Delivery, Delivery Line, Delivery Route references, and Delivery Discrepancy information used by this report.
- **A-006:** Quantity Shipped represents the quantity recorded for a Shipment Line, not the quantity originally ordered or picked.
- **A-007:** Quantity Delivered is calculated using confirmed quantities from finalized Delivery Lines.
- **A-008:** A Shipment may have multiple delivery attempts before all shipped units are delivered.
- **A-009:** A Delivery in Delivered, Partially Delivered, or Failed Attempt status is treated as a finalized delivery attempt.
- **A-010:** A Delivery in Assigned or In Progress status is treated as pending rather than finalized.
- **A-011:** A reported apparent over-delivery is preserved as an exception and does not automatically increase confirmed Quantity Delivered.
- **A-012:** Historical Delivery Discrepancy records remain available after later deliveries resolve the outstanding quantity.
- **A-013:** The default report focuses on current outstanding differences and reportable finalized delivery exceptions.
- **A-014:** Managers may optionally include pending delivery information and resolved historical discrepancies.
- **A-015:** Report date filtering uses the relevant delivery finalization or exception date.
- **A-016:** The report is read-only and does not modify shipping, delivery, or Customer Order quantities.
- **A-017:** Historical Customer, Item, Shipment, Delivery, and Route identification remains available after related master records are deactivated.
- **A-018:** Only authorized Managers and approved reporting personnel can access the report.

**[NEEDS CLARIFICATION]** Confirm whether a Shipment may have more than one active Delivery attempt at the same time.

**[NEEDS CLARIFICATION]** Confirm how a pending Delivery without a finalized delivery date should be handled when a date-range filter is applied.

**[NEEDS CLARIFICATION]** Confirm whether the report should display a separate current outstanding quantity for a Shipment that has both a finalized partial delivery and a later pending delivery attempt.

**[NEEDS CLARIFICATION]** Confirm the workflow for reviewing and resolving an Apparent Over-Delivery exception. Feature 18 reports the exception but does not define how the delivery quantity is corrected or approved.

---

## Edge Cases

### EC-18.1: Delivered Quantity Is Less Than Shipped Quantity

A Shipment Line contains more Quantity Shipped than cumulative confirmed Quantity Delivered.

The report identifies the outstanding quantity as a Shortage when the applicable delivery attempt is finalized.

### EC-18.2: Delivered Quantity Matches Shipped Quantity

Cumulative confirmed Quantity Delivered equals Quantity Shipped.

The system does not report an outstanding shipment-level shortage.

Historical discrepancies from earlier attempts remain available when historical reporting is requested.

### EC-18.3: Driver Reports Apparent Over-Delivery

A Driver reports that more units appear to have been delivered than were recorded as shipped.

The system preserves the Apparent Over-Delivery exception for review without automatically increasing confirmed Quantity Delivered above Quantity Shipped.

### EC-18.4: Delivery Is Still In Progress

A Delivery is In Progress and its quantities are not finalized.

The default report excludes the Delivery from finalized discrepancy results.

If pending information is requested, the system identifies the Delivery as Pending Delivery.

### EC-18.5: Delivery Has Been Assigned but Not Started

A Shipment has an Assigned Delivery that has not started.

The default report does not classify the undelivered quantity as a confirmed shortage.

### EC-18.6: Failed Delivery Attempt

A Delivery is finalized as Failed Attempt and no units were delivered.

The report preserves the undelivered quantity and identifies the unsuccessful delivery attempt.

### EC-18.7: Partial Delivery

A Shipment contains 30 shipped units, but a finalized Delivery Attempt confirms only 20 units delivered.

The report identifies 10 outstanding units and associates the discrepancy with the correct Shipment and Delivery Route.

### EC-18.8: Multiple Delivery Attempts

A Shipment Line is associated with several finalized Delivery Lines from separate attempts.

The system sums each applicable finalized Delivery Line exactly once.

### EC-18.9: Later Delivery Resolves Earlier Shortage

An earlier Delivery Attempt produced a shortage, but a later authorized attempt delivered the remaining units.

The default current outstanding report excludes the resolved shortage.

Historical reporting continues to show the original discrepancy, its Delivery Route, date, and resolution status.

### EC-18.10: Multiple Differing Items

A Shipment contains several Items, and more than one Item has a delivery difference.

The report displays each applicable Item difference separately.

### EC-18.11: Multiple Shipments for One Customer Order

A Customer Order has multiple Shipments with different delivery outcomes.

The report preserves the association between each difference and its corresponding Shipment.

### EC-18.12: Delivery Route Changes Between Attempts

A Shipment has multiple delivery attempts using different Delivery Routes.

Historical discrepancies retain the Delivery Route associated with the original attempt.

### EC-18.13: Driver Changes Between Attempts

Different Drivers perform separate delivery attempts for the same Shipment.

Each finalized Delivery retains the Driver associated with that attempt.

### EC-18.14: Invalid Date Range

The report start date is later than the end date.

The system rejects the filter and requests valid dates.

### EC-18.15: No Matching Differences

No delivery differences match the selected report filters.

The system displays an empty result with an appropriate message.

### EC-18.16: Incomplete Historical Information

Required historical Shipment or Delivery information is unavailable.

The report identifies the incomplete information and does not present an unverified quantity comparison as a confirmed zero discrepancy.

### EC-18.17: Customer or Item Is Deactivated

A Customer or Individual Item is deactivated after a Delivery.

Historical delivery discrepancies remain identifiable.

### EC-18.18: Unauthorized Report Access

A User without reporting permission attempts to generate the report.

The system denies access and does not display restricted delivery information.

### EC-18.19: Quantity Picked Differs From Quantity Shipped

A Customer Order Line has more units picked than were actually shipped.

The report uses Quantity Shipped rather than Quantity Picked for delivery comparisons.

### EC-18.20: Quantity Ordered Differs From Quantity Delivered

A Customer originally ordered more units than were included in a particular Shipment.

The report compares the Shipment Line's Quantity Shipped with confirmed Quantity Delivered, rather than using Quantity Ordered as a substitute.

### EC-18.21: Duplicate Delivery Confirmation

A finalized Delivery Line is processed or retrieved more than once.

The system counts that Delivery Line only once when calculating cumulative Quantity Delivered.

### EC-18.22: Historical Discrepancy Remains Open

A Delivery Discrepancy has been recorded and has not been resolved.

The report preserves its Open status and provides access to the associated Delivery information.

### EC-18.23: Failed Attempt Followed by Successful Delivery

A Shipment has a finalized Failed Attempt followed by a successful delivery attempt.

The original Failed Attempt remains available in historical reporting even when the current outstanding quantity becomes zero.

### EC-18.24: Report Is Generated Repeatedly

A Manager generates the same report multiple times without changes to source records.

The report returns consistent results without modifying Shipment or Delivery quantities.

---

## Success Criteria

- **SC-001:** Authorized Managers can generate a Delivery Difference Report using finalized Shipment and Delivery information.
- **SC-002:** Each applicable difference identifies the Customer, Customer Order, Shipment, Individual Item, and Delivery Route.
- **SC-003:** The report displays Quantity Shipped and Quantity Delivered in individual units.
- **SC-004:** Difference Units are calculated as cumulative Quantity Delivered minus Quantity Shipped.
- **SC-005:** Negative finalized shipment-level differences are identified as Shortages.
- **SC-006:** Apparent Over-Delivery exceptions are displayed separately from confirmed quantities.
- **SC-007:** Reported apparent over-deliveries do not automatically increase confirmed Quantity Delivered.
- **SC-008:** Matching shipped and delivered quantities are excluded from current outstanding shortage results.
- **SC-009:** Multiple differing Items and Shipments are reported with their correct references.
- **SC-010:** Each finalized Delivery discrepancy preserves its Driver, Delivery Route, and finalization date.
- **SC-011:** Finalized Delivered, Partially Delivered, and Failed Attempt outcomes are included when reportable discrepancies exist.
- **SC-012:** Assigned and In Progress Deliveries are excluded from finalized discrepancy results.
- **SC-013:** Optional pending reporting identifies unfinished Deliveries as Pending Delivery.
- **SC-014:** Failed Attempts with zero delivered units preserve the undelivered quantity.
- **SC-015:** Cumulative Quantity Delivered includes each finalized Delivery Line exactly once.
- **SC-016:** Historical Delivery Discrepancy records remain available after later deliveries resolve the outstanding quantity.
- **SC-017:** Resolved historical shortages are excluded from current outstanding shortage results.
- **SC-018:** Customer, Delivery Route, Individual Item, date-range, and discrepancy-type filters return applicable results.
- **SC-019:** Invalid date ranges are rejected with a clear message.
- **SC-020:** Report results can be sorted by Customer, Route, Customer Order Number, Item Number, report date, or difference magnitude.
- **SC-021:** No matching results produce a clear empty-results message.
- **SC-022:** Incomplete historical information is distinguished from a verified absence of discrepancies.
- **SC-023:** Historical identification remains available after related master records are deactivated.
- **SC-024:** Unauthorized Users cannot access restricted report information.
- **SC-025:** Report generation does not modify Shipment, Delivery, or Customer Order quantities.
- **SC-026:** Each reported difference provides access to the associated Shipment and Delivery history.
- **SC-027:** All 28 original Gherkin Acceptance Criteria have corresponding tests.

---

## Key Entities

### Delivery Difference Report

Represents a read-only reporting view of differences between Quantity Shipped and Quantity Delivered.

### Customer

Represents the business receiving the Customer Order.

### Customer Order

Represents an order placed by a Customer.

### Customer Order Line

Represents an Individual Item requested on a Customer Order, including cumulative shipped and delivered quantities.

### Shipment

Represents a set of products prepared for delivery in Feature 14.

### Shipment Line

Represents an Individual Item and its Quantity Shipped within a Shipment.

### Delivery

Represents a delivery attempt recorded in Feature 15.

### Delivery Line

Represents the actual quantity of an Item delivered during a specific attempt.

### Delivery Route

Represents the route associated with a Delivery.

### Delivery Discrepancy

Represents a recorded delivery shortage, apparent over-delivery, or unsuccessful delivery exception.

### Individual Item

Represents a product included in a Shipment or Delivery.

### User

Represents an authorized Manager or reporting employee.

---

## Initial Data Model

### Delivery Difference Report

The Delivery Difference Report is a generated reporting view rather than a separate business transaction.

**Report Parameters:**

| Parameter | Type | Description |
|---|---|---|
| customerId | Integer | Optional Customer filter |
| deliveryRouteId | Integer | Optional Delivery Route filter |
| itemId | Integer | Optional Individual Item filter |
| startDate | Date | Optional start date |
| endDate | Date | Optional end date |
| discrepancyType | String | All, Shortage, Apparent Over-Delivery, or Failed Delivery |
| includePending | Boolean | Whether pending delivery information is included |
| includeHistorical | Boolean | Whether resolved historical discrepancies are included |

**Displayed Information:**

| Field | Description |
|---|---|
| Customer | Customer name and number |
| Customer Order Number | Order associated with the Shipment |
| Shipment Number | Shipment reference |
| Delivery Route | Route associated with the Delivery |
| Driver | Driver who recorded the Delivery |
| Item Number | Individual Item SKU |
| Item Description | Item description |
| Quantity Shipped | Units included in the Shipment |
| Quantity Delivered | Cumulative confirmed units delivered |
| Difference Units | Delivered Units minus Shipped Units |
| Difference Type | Shortage, Apparent Over-Delivery, Failed Delivery, or Pending Delivery |
| Delivery Status | Current or finalized delivery outcome |
| Report Date | Relevant delivery finalization or exception date |

**Relationships:**
- The report uses Shipment Lines and finalized Delivery Lines.
- The report includes recorded Delivery Discrepancies.
- Each result identifies the related Customer Order, Shipment, Item, and Delivery Route.

### Customer

| Attribute | Type | Description |
|---|---|---|
| customerId | Integer | Unique Customer identifier |
| customerNumber | String | Unique Customer Number |
| name | String | Customer business name |

**Relationships:**
- A Customer may have multiple Customer Orders.
- Customer information is defined in Feature 6.

### Customer Order

| Attribute | Type | Description |
|---|---|---|
| customerOrderId | Integer | Unique Customer Order identifier |
| orderNumber | String | Unique Customer Order Number |
| customerId | Integer | Foreign key referencing Customer |

**Relationships:**
- Each Customer Order belongs to one Customer.
- Each Customer Order contains one or more Customer Order Lines.
- A Customer Order may have multiple Shipments.

### Customer Order Line

| Attribute | Type | Description |
|---|---|---|
| customerOrderLineId | Integer | Unique Customer Order Line identifier |
| customerOrderId | Integer | Foreign key referencing Customer Order |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityOrdered | Integer | Quantity ordered |
| quantityPicked | Integer | Cumulative quantity picked |
| quantityShipped | Integer | Cumulative quantity shipped |
| quantityDelivered | Integer | Cumulative quantity delivered |

**Relationships:**
- Each Customer Order Line belongs to one Customer Order.
- Shipment Lines reference Customer Order Lines.
- Finalized Delivery Lines contribute to cumulative Quantity Delivered.

### Shipment

| Attribute | Type | Description |
|---|---|---|
| shipmentId | Integer | Unique Shipment identifier |
| shipmentNumber | String | Unique Shipment Number |
| customerOrderId | Integer | Foreign key referencing Customer Order |
| status | String | Preparing, Ready for Delivery, Canceled, or Exception |

**Relationships:**
- A Shipment belongs to one Customer Order.
- A Shipment contains one or more Shipment Lines.
- A Shipment may have multiple Delivery attempts over time.

### Shipment Line

| Attribute | Type | Description |
|---|---|---|
| shipmentLineId | Integer | Unique Shipment Line identifier |
| shipmentId | Integer | Foreign key referencing Shipment |
| customerOrderLineId | Integer | Foreign key referencing Customer Order Line |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityShipped | Integer | Quantity included in the finalized Shipment |

**Relationships:**
- Each Shipment Line belongs to one Shipment.
- Each Shipment Line references one Customer Order Line.
- A Shipment Line may be referenced by multiple Delivery Lines across different delivery attempts.

### Delivery

| Attribute | Type | Description |
|---|---|---|
| deliveryId | Integer | Unique Delivery identifier |
| shipmentId | Integer | Foreign key referencing Shipment |
| deliveryRouteId | Integer | Foreign key referencing Delivery Route |
| driverId | Integer | Foreign key referencing User |
| status | String | Assigned, In Progress, Partially Delivered, Delivered, or Failed Attempt |
| completedAt | DateTime | Date and time delivery outcome was finalized |

**Relationships:**
- Each Delivery belongs to one Shipment.
- Each Delivery is associated with one Delivery Route.
- Each Delivery is performed by one Driver.
- Each Delivery contains one or more Delivery Lines.

### Delivery Line

| Attribute | Type | Description |
|---|---|---|
| deliveryLineId | Integer | Unique Delivery Line identifier |
| deliveryId | Integer | Foreign key referencing Delivery |
| shipmentLineId | Integer | Foreign key referencing Shipment Line |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityShipped | Integer | Original Shipment Line quantity |
| quantityDelivered | Integer | Quantity confirmed delivered during this attempt |

**Relationships:**
- Each Delivery Line belongs to one Delivery.
- Each Delivery Line references one Shipment Line.
- Multiple Delivery Lines may contribute to cumulative delivered quantity across attempts.

**Derived Values:**
- Cumulative Delivered = Sum of finalized Delivery Line quantities for the Shipment Line.
- Difference Units = Cumulative Delivered - Quantity Shipped.
- Outstanding Units = max(0, Quantity Shipped - Cumulative Delivered).

### Delivery Route

| Attribute | Type | Description |
|---|---|---|
| deliveryRouteId | Integer | Unique Delivery Route identifier |
| routeCode | String | Unique Route Code |
| routeName | String | Delivery Route name |

**Relationships:**
- A Delivery Route may be associated with multiple Deliveries.
- Each Delivery records the route used for that attempt.

### Delivery Discrepancy

| Attribute | Type | Description |
|---|---|---|
| deliveryDiscrepancyId | Integer | Unique discrepancy identifier |
| deliveryId | Integer | Foreign key referencing Delivery |
| deliveryLineId | Integer | Optional foreign key referencing Delivery Line |
| discrepancyType | String | Short Delivery, Apparent Over-Delivery, or Failed Delivery |
| quantityDifference | Integer | Reported difference in individual units |
| reason | String | Explanation recorded during delivery |
| reportedAt | DateTime | Date and time discrepancy was recorded |
| status | String | Open or Resolved |

**Relationships:**
- Each Delivery Discrepancy belongs to one Delivery.
- Each discrepancy may reference one Delivery Line.
- Historical discrepancy records remain available after resolution.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |

**Relationships:**
- One Individual Item may appear on multiple Customer Order Lines.
- One Individual Item may appear on multiple Shipment and Delivery Lines.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Drivers record Delivery information in Feature 15.
- Authorized Managers review Delivery Difference Reports.

---

## Gherkin AC

### US-18.1: View Delivery Differences

#### AC-18.1.1: Quantity Delivered is less than Quantity Shipped

**Given** a Shipment Line contains 30 units shipped  
**And** finalized Deliveries confirm 25 units delivered  
**When** the Manager generates the Delivery Difference Report  
**Then** the report identifies a Shortage of 5 units  
**And** displays 30 Quantity Shipped and 25 Quantity Delivered.

#### AC-18.1.2: Apparent over-delivery is reported

**Given** a Shipment Line contains 20 units shipped  
**And** the Driver reported that 23 units appeared to have been delivered  
**And** an Apparent Over-Delivery exception was recorded  
**When** the Manager generates the Delivery Difference Report  
**Then** the report identifies an Apparent Over-Delivery of 3 units  
**And** distinguishes the reported exception from confirmed Quantity Delivered.

#### AC-18.1.3: Quantity Delivered matches Quantity Shipped

**Given** a Shipment Line contains 20 units shipped  
**And** finalized Deliveries confirm 20 units delivered  
**And** no unresolved delivery exception exists  
**When** the Manager generates the default current-difference report  
**Then** that Shipment Line does not appear as an outstanding quantity difference.

#### AC-18.1.4: No delivery differences exist

**Given** all applicable completed Shipments have matching shipped and delivered quantities  
**And** no reportable delivery exceptions exist  
**When** the Manager generates the Delivery Difference Report  
**Then** the system displays no delivery quantity differences  
**And** indicates that no matching discrepancies were found.

#### AC-18.1.5: Delivery is incomplete

**Given** a Delivery is In Progress  
**And** its delivered quantities have not been finalized  
**When** the Manager generates the default report  
**Then** the system excludes the Delivery from finalized discrepancy results.

#### AC-18.1.6: Pending Delivery is requested

**Given** a Shipment has been released for delivery  
**And** its assigned Delivery is still In Progress  
**When** the Manager includes pending delivery information  
**Then** the system identifies the Shipment as Pending Delivery  
**And** does not classify its outstanding quantities as confirmed shortages.

### US-18.2: Review Delivery Difference Details

#### AC-18.2.1: Display difference details

**Given** a finalized Delivery contains a quantity difference  
**When** the Manager reviews the report  
**Then** the report identifies the Customer and Customer Order Number  
**And** identifies the Shipment Number and Individual Item  
**And** displays Quantity Shipped, Quantity Delivered, and Difference Units.

#### AC-18.2.2: Multiple Items differ

**Given** a Shipment contains three Items  
**And** two Items have finalized delivery differences  
**And** one Item has matching shipped and delivered quantities  
**When** the Manager generates the report  
**Then** the report displays the two differing Items  
**And** excludes the matching Item from outstanding difference results.

#### AC-18.2.3: One Item differs on a multi-item Customer Order

**Given** a Customer Order contains several Items  
**And** only one Item has a delivery shortage  
**When** the Manager generates the report  
**Then** the report identifies the differing Item  
**And** associates it with the correct Customer Order and Shipment.

#### AC-18.2.4: No quantity of shipped Item is delivered

**Given** a finalized Failed Attempt is recorded for a Shipment containing 15 units of Item A  
**And** no units of Item A have been delivered  
**When** the Manager generates the report  
**Then** the report identifies 15 units as undelivered  
**And** identifies the unsuccessful delivery outcome.

#### AC-18.2.5: Multiple Deliveries contain differences

**Given** several Shipments have finalized delivery discrepancies  
**When** the Manager generates the report  
**Then** the report displays the applicable differences  
**And** preserves the Shipment and Delivery Route associated with each discrepancy.

### US-18.3: Distinguish Delivery Shortages and Over-Delivery Reports

#### AC-18.3.1: Identify confirmed shortage

**Given** a Shipment Line contains 100 units shipped  
**And** finalized Delivery Lines confirm 90 units delivered  
**When** the Manager reviews the report  
**Then** the system identifies a Shortage  
**And** displays Difference Units as -10.

#### AC-18.3.2: Identify apparent over-delivery

**Given** a Driver reports 5 units more than the recorded Quantity Shipped  
**And** the system records an Apparent Over-Delivery exception  
**When** the Manager reviews the report  
**Then** the system displays the apparent over-delivery separately  
**And** identifies the exception as requiring review.

#### AC-18.3.3: Preserve Quantity Shipped

**Given** a Shipment contains 40 units shipped  
**And** only 38 units are confirmed delivered  
**When** the system records the discrepancy  
**Then** Quantity Shipped remains 40  
**And** Quantity Delivered remains 38  
**And** the report identifies a Shortage of 2 units.

### US-18.4: Filter Delivery Difference Report

#### AC-18.4.1: Filter by Customer

**Given** delivery differences exist for Customer A and Customer B  
**When** the Manager selects Customer A  
**Then** the report includes only applicable differences associated with Customer A.

#### AC-18.4.2: Filter by Delivery Route

**Given** delivery differences exist on Routes R1 and R2  
**When** the Manager filters the report to Route R1  
**Then** the report includes only applicable differences associated with Route R1.

#### AC-18.4.3: Filter by Individual Item

**Given** delivery differences exist for Item A and Item B  
**When** the Manager filters the report to Item A  
**Then** the report displays only applicable differences involving Item A.

#### AC-18.4.4: Filter by date range

**Given** finalized delivery discrepancies exist inside and outside a selected date range  
**When** the Manager applies a valid date range  
**Then** the report includes applicable discrepancies recorded within that range  
**And** excludes discrepancies outside the selected range.

#### AC-18.4.5: Filter by discrepancy type

**Given** the report contains Shortages and Apparent Over-Delivery exceptions  
**When** the Manager selects Apparent Over-Delivery  
**Then** the report displays only applicable apparent over-delivery exceptions.

#### AC-18.4.6: Reject invalid date range

**Given** the Manager is entering report filters  
**When** the start date is later than the end date  
**Then** the system rejects the date range  
**And** requests valid dates.

#### AC-18.4.7: No matching discrepancies

**Given** no delivery discrepancies match the selected criteria  
**When** the Manager generates the report  
**Then** the system displays an empty result  
**And** indicates that no matching differences were found.

### US-18.5: Review Incomplete and Failed Deliveries

#### AC-18.5.1: Exclude incomplete delivery from finalized shortages

**Given** a Shipment is assigned to a Driver  
**And** the Delivery is still In Progress  
**When** the Manager generates the default finalized report  
**Then** the system does not classify the Shipment as a finalized delivery shortage.

#### AC-18.5.2: Include failed delivery attempt

**Given** a Delivery Attempt has been finalized as Failed Attempt  
**And** no units were delivered  
**When** the Manager generates the report  
**Then** the report identifies the failed delivery  
**And** displays the undelivered quantity  
**And** preserves the associated Delivery Route.

#### AC-18.5.3: Include partial delivery

**Given** a Shipment contains 30 units shipped  
**And** a finalized Delivery Attempt confirms 20 units delivered  
**When** the Manager generates the report  
**Then** the report identifies 10 outstanding units  
**And** associates the difference with the Shipment and Delivery Route.

### US-18.6: Review Historical Delivery Discrepancies

#### AC-18.6.1: Preserve discrepancy after later delivery

**Given** a first Delivery Attempt confirmed 15 units out of 20 shipped  
**And** a shortage of 5 units was recorded  
**And** a later authorized attempt delivered the remaining 5 units  
**When** the Manager requests historical discrepancy information  
**Then** the report includes the original shortage record  
**And** identifies its current resolution status  
**And** preserves the original Delivery Route and date.

#### AC-18.6.2: Exclude resolved shortage from current outstanding results

**Given** a Shipment originally had a shortage of 5 units  
**And** a later Delivery Attempt confirmed the remaining 5 units  
**When** the Manager generates the default current outstanding difference report  
**Then** the resolved shortage does not appear as an outstanding quantity difference  
**And** remains available in historical reporting.

#### AC-18.6.3: Prevent duplicate delivery counting

**Given** a Shipment Line has two finalized Delivery Lines for separate delivery attempts  
**When** the system calculates cumulative Quantity Delivered  
**Then** it includes each finalized Delivery Line exactly once  
**And** does not count a duplicate confirmation.

#### AC-18.6.4: Reject unauthorized report access

**Given** a User is authenticated as a Driver without reporting permission  
**When** the User attempts to generate the Delivery Difference Report  
**Then** the system denies access  
**And** does not display restricted report information.

---

## Data Ownership

### Customer Data

**Owning Feature:** Feature 6 - Maintain Customers

Feature 6 owns Customer master data, including:

- Customer ID
- Customer Number
- Customer Name
- Customer active or inactive status

Feature 18 reads Customer information to identify the Customer associated with each reported delivery difference.

Feature 18 MUST NOT create, update, deactivate, or delete Customer records.

Historical Customer identification MUST remain available after deactivation.

### Individual Item Data

**Owning Feature:** Feature 4 - Maintain Individual Items

Feature 4 owns Individual Item master data, including:

- Item ID
- Item Number
- Item Description

Feature 18 reads Item information to identify products involved in Shipment and Delivery differences.

Feature 18 MUST NOT modify Individual Item master data.

Historical Item identification MUST remain available after deactivation.

### Customer Order Data

**Owning Features:** Features 12 through 15 - Customer Order Processing

Customer Order functionality maintains:

- Customer Order ID
- Customer Order Number
- Customer ID
- Customer Order Lines
- Quantity Ordered
- Quantity Picked
- Cumulative Quantity Shipped
- Cumulative Quantity Delivered

Feature 18 reads Customer Order information to identify the orders associated with delivery differences.

Feature 18 MUST NOT modify Customer Orders or Customer Order Lines.

Quantity Ordered MUST NOT be substituted for Quantity Delivered.

Quantity Picked MUST NOT be substituted for Quantity Shipped.

### Shipment Data

**Owning Feature:** Feature 14 - Ship Customer Orders

Feature 14 owns Shipment and Shipment Line information, including:

- Shipment ID
- Shipment Number
- Customer Order ID
- Shipment Status
- Shipment Line ID
- Customer Order Line reference
- Individual Item reference
- Quantity Shipped

Feature 18 reads Shipment information to determine the original quantity shipped for each Shipment Line.

Feature 18 MUST preserve the original Quantity Shipped when later delivery attempts occur.

Feature 18 MUST NOT create, edit, cancel, or otherwise modify Shipments.

### Delivery Data

**Owning Feature:** Feature 15 - Deliver Customer Orders

Feature 15 owns Delivery and Delivery Line information, including:

- Delivery ID
- Shipment ID
- Delivery Route ID
- Driver ID
- Delivery Status
- Delivery completion date and time
- Delivery Line ID
- Shipment Line reference
- Actual Quantity Delivered

Feature 18 reads finalized Delivery Lines to calculate cumulative Quantity Delivered.

Only Delivery Lines belonging to finalized delivery attempts contribute to confirmed cumulative Quantity Delivered.

Feature 18 MUST NOT create, complete, or modify Deliveries.

### Delivery Route Data

**Owning Feature:** Delivery Route functionality used by Feature 15

Delivery Route information includes:

- Delivery Route ID
- Route Code
- Route Name

Feature 18 reads Delivery Route information to identify the route associated with each delivery attempt.

The original route associated with a historical discrepancy MUST remain identifiable.

Feature 18 MUST NOT create, edit, or delete Delivery Routes.

**[NEEDS CLARIFICATION]** Confirm which existing feature owns Delivery Route master data.

### Delivery Discrepancy Data

**Owning Feature:** Feature 15 - Deliver Customer Orders

Feature 15 maintains Delivery Discrepancy information, including:

- Delivery Discrepancy ID
- Delivery ID
- Delivery Line ID, when applicable
- Discrepancy Type
- Quantity Difference
- Reason
- Reported Date and Time
- Resolution Status

Feature 18 reads Delivery Discrepancy records to identify:

- Delivery shortages
- Apparent over-deliveries
- Failed delivery exceptions
- Open discrepancies
- Resolved historical discrepancies

Feature 18 MUST preserve historical discrepancy information even after later delivery attempts resolve an outstanding quantity.

Feature 18 MUST NOT change discrepancy status or modify recorded quantities.

### Delivery Difference Report

**Owning Feature:** Feature 18 - Report Deliveries That Do Not Match What Was Shipped

Feature 18 owns:

- Delivery Difference Report generation
- Report filtering
- Report sorting
- Quantity comparison calculations
- Cumulative delivered quantity calculations
- Current outstanding difference classification
- Pending Delivery presentation
- Historical discrepancy presentation
- Read-only report details

The Delivery Difference Report is a generated reporting view rather than a separate business transaction.

Feature 18 MUST NOT overwrite data owned by Features 4, 6, 12, 13, 14, or 15.

### User and Authorization Data

**Owning Component:** Shared User and Access Control functionality

The shared authorization component maintains:

- User accounts
- User roles
- Authentication information
- Reporting permissions

Feature 18 checks whether a User is authorized to generate or review the Delivery Difference Report.

Drivers without reporting permission MUST NOT access restricted report information.

Feature 18 MUST NOT modify User accounts or permissions.

### Data Ownership Rules

- Feature 4 owns Individual Item master data.
- Feature 6 owns Customer master data.
- Features 12 through 15 provide Customer Order processing data.
- Feature 14 owns Shipment and Shipment Line information.
- Feature 15 owns Delivery, Delivery Line, and Delivery Discrepancy information.
- Delivery Route ownership must be confirmed.
- Feature 18 owns reporting calculations, filtering, sorting, and presentation.
- Shared authorization functionality owns User access permissions.
- Feature 18 MUST preserve references to original source records.
- Feature 18 MUST remain read-only.

---

## API Requirements

The following API endpoints are proposed for Feature 18.

Final endpoint names, request formats, and response structures must follow the Warehouse Management System's established API conventions.

### API-18.1: Generate Delivery Difference Report

**Method:** GET

**Proposed Endpoint:**

`/api/reports/delivery-differences`

**Purpose:**

Generate a read-only report identifying differences between Quantity Shipped and cumulative confirmed Quantity Delivered.

**Query Parameters:**

| Parameter | Type | Required | Description |
|---|---|---|---|
| customerId | Integer | No | Filter by Customer |
| deliveryRouteId | Integer | No | Filter by Delivery Route |
| itemId | Integer | No | Filter by Individual Item |
| startDate | Date | No | Beginning of reporting period |
| endDate | Date | No | End of reporting period |
| discrepancyType | String | No | All, Shortage, Apparent Over-Delivery, or Failed Delivery |
| includePending | Boolean | No | Include pending delivery information; default false |
| includeHistorical | Boolean | No | Include resolved historical discrepancies; default false |
| sortBy | String | No | Customer, Route, Order Number, Item Number, Report Date, or Difference Magnitude |

**Expected Response Information:**

- Customer ID
- Customer Number
- Customer Name
- Customer Order ID
- Customer Order Number
- Shipment ID
- Shipment Number
- Shipment Line ID
- Delivery ID, when applicable
- Delivery Route ID
- Route Code
- Route Name
- Driver ID
- Item ID
- Item Number
- Item Description
- Quantity Shipped
- Cumulative Quantity Delivered
- Difference Units
- Outstanding Units
- Difference Type
- Delivery Status
- Report Date
- Pending or Finalized indicator
- Historical or Current indicator
- Delivery Discrepancy reference, when available
- Discrepancy Resolution Status, when applicable
- Historical data warning, when applicable

**Calculation Rules:**

Cumulative Quantity Delivered = Sum of Quantity Delivered from finalized Delivery Lines associated with the Shipment Line.

Difference Units = Cumulative Quantity Delivered - Quantity Shipped.

Outstanding Units = max(0, Quantity Shipped - Cumulative Quantity Delivered).

**Classification Rules:**

For finalized delivery information:

- Negative Difference Units indicates an outstanding Shortage.
- Zero Difference Units indicates no outstanding shipment-level quantity difference.
- A finalized Failed Attempt remains reportable when it contains a delivery exception.
- Apparent Over-Delivery exceptions are displayed separately from confirmed delivered quantities.

For pending delivery information:

- Assigned or In Progress Deliveries are identified as Pending Delivery.
- Outstanding quantities associated only with pending deliveries are not classified as confirmed shortages.

For historical information:

- Earlier Delivery Discrepancy records remain available after resolution.
- Resolved shortages are excluded from current outstanding shortage results.
- Historical results retain the original Delivery Route and discrepancy date.

**Validation Rules:**

- The requesting User must be authenticated.
- The requesting User must have reporting permission.
- Customer, Route, and Item filters must reference valid records.
- The start date must not be later than the end date.
- The discrepancy type must be supported.
- The sorting field must be supported.
- Only finalized Delivery Lines may contribute to confirmed Quantity Delivered.
- Each finalized Delivery Line must be counted once.
- Report generation must not modify source records.

**Possible Responses:**

- `200 OK` - Report generated successfully, including empty results.
- `400 Bad Request` - Invalid report parameters.
- `401 Unauthorized` - User is not authenticated.
- `403 Forbidden` - User lacks reporting permission.
- `500 Internal Server Error` - Unexpected server failure.

**[NEEDS CLARIFICATION]** Confirm the date filtering behavior for pending Deliveries that do not have a completedAt value.

**[NEEDS CLARIFICATION]** Confirm whether current outstanding quantities and historical delivery-attempt discrepancies should be returned in separate response collections or identified using a record type.

### API-18.2: Retrieve Delivery Difference Details

**Method:** GET

**Proposed Endpoint:**

`/api/reports/delivery-differences/{shipmentLineId}`

**Purpose:**

Retrieve detailed information about a Shipment Line and its associated delivery differences.

**Path Parameter:**

- `shipmentLineId` - Unique identifier of the Shipment Line.

**Expected Response Information:**

- Customer identification
- Customer Order Number
- Shipment Number
- Shipment Line ID
- Item Number
- Item Description
- Original Quantity Shipped
- Cumulative confirmed Quantity Delivered
- Difference Units
- Outstanding Units
- Delivery attempt history
- Delivery Route information
- Driver information
- Finalized Delivery statuses
- Delivery completion dates
- Associated Delivery Discrepancies
- Discrepancy resolution information

**Processing Rules:**

- Preserve original Quantity Shipped.
- Calculate cumulative Quantity Delivered from finalized Delivery Lines.
- Do not count duplicate Delivery Lines.
- Distinguish current outstanding differences from resolved historical discrepancies.
- Do not automatically increase confirmed Quantity Delivered for apparent over-deliveries.
- Do not modify Shipment or Delivery records.

**Possible Responses:**

- `200 OK` - Details returned successfully.
- `401 Unauthorized` - User is not authenticated.
- `403 Forbidden` - User lacks permission.
- `404 Not Found` - Requested Shipment Line does not exist.

### API-18.3: Retrieve Delivery History

**Method:** GET

**Proposed Endpoint:**

`/api/reports/delivery-differences/{shipmentLineId}/history`

**Purpose:**

Allow an authorized Manager to review all applicable delivery attempts and historical discrepancies associated with a Shipment Line.

**Expected Response Information:**

- Delivery ID
- Delivery Route
- Driver
- Delivery Status
- Delivery completion date and time
- Quantity Delivered during the attempt
- Delivery Discrepancy ID
- Discrepancy Type
- Discrepancy Quantity Difference
- Discrepancy Reason
- Discrepancy Reported Date and Time
- Discrepancy Resolution Status

**Processing Rules:**

- Include finalized delivery attempts.
- Preserve historical discrepancy records.
- Clearly identify resolved and unresolved discrepancies.
- Clearly distinguish pending attempts from finalized attempts when pending information is included.
- Preserve the Delivery Route used for each attempt.
- Do not modify delivery history.

### API-18.4: Retrieve Delivery Discrepancy Details

**Method:** GET

**Proposed Endpoint:**

`/api/reports/delivery-discrepancies/{deliveryDiscrepancyId}`

**Purpose:**

Retrieve the details of a recorded Delivery Discrepancy for management review.

**Expected Response Information:**

- Delivery Discrepancy ID
- Delivery ID
- Delivery Line ID, when applicable
- Shipment reference
- Customer Order reference
- Discrepancy Type
- Quantity Difference
- Reason
- Reported Date and Time
- Resolution Status
- Associated Delivery Route

**Processing Rules:**

- The endpoint must be read-only.
- Apparent Over-Delivery must be identified as a reported exception.
- Historical discrepancies must remain accessible after resolution.
- Access must be restricted to authorized reporting personnel.

### API Security Requirements

- All report endpoints MUST require authentication.
- Reporting permission MUST be checked on the server.
- Unauthorized Users MUST NOT receive restricted Customer, Shipment, or Delivery information.
- Drivers without reporting permission MUST be denied access.
- Report endpoints MUST be read-only.
- Report generation MUST NOT change Quantity Shipped or Quantity Delivered.
- Historical discrepancies MUST remain traceable to their original Delivery records.
- Source data relationships MUST be preserved.

---

## Screen Requirements

### SCREEN-18.1: Delivery Difference Report Screen

**Purpose:**

Allow authorized Managers to identify, filter, and review differences between Quantity Shipped and Quantity Delivered.

**Authorized Users:**

- Warehouse Managers
- Approved reporting personnel

**Screen Elements:**

- Page title: Delivery Difference Report
- Customer filter
- Delivery Route filter
- Individual Item filter
- Start Date filter
- End Date filter
- Discrepancy Type filter
- Include Pending Deliveries checkbox
- Include Historical Discrepancies checkbox
- Sort By selection
- Generate Report button
- Clear Filters button
- Results table
- Empty-results message
- Historical data warning, when applicable

**Results Table Columns:**

| Column | Description |
|---|---|
| Customer | Customer Name or Number |
| Customer Order | Customer Order Number |
| Shipment | Shipment Number |
| Delivery Route | Route associated with the discrepancy |
| Driver | Driver associated with the finalized Delivery |
| Item Number | Individual Item SKU |
| Item Description | Item description |
| Quantity Shipped | Original shipped quantity in units |
| Quantity Delivered | Cumulative confirmed delivered quantity |
| Difference Units | Delivered Units minus Shipped Units |
| Difference Type | Shortage, Apparent Over-Delivery, Failed Delivery, or Pending Delivery |
| Delivery Status | Delivery outcome |
| Report Date | Relevant delivery finalization or exception date |
| Details | Read-only access to delivery history |

**Screen Behavior:**

1. The Manager opens the Delivery Difference Report from the reporting menu.
2. The system displays the available report filters.
3. The Manager optionally selects a Customer.
4. The Manager optionally selects a Delivery Route.
5. The Manager optionally selects an Individual Item.
6. The Manager optionally selects a date range.
7. The Manager selects a discrepancy type or All.
8. The Manager may enable Include Pending Deliveries.
9. The Manager may enable Include Historical Discrepancies.
10. The Manager optionally selects a sorting method.
11. The Manager selects Generate Report.
12. The system validates the selected filters.
13. The system retrieves applicable Shipment and Delivery information.
14. The system calculates cumulative Quantity Delivered.
15. The system identifies reportable differences and exceptions.
16. The system displays matching results.
17. The Manager may select a result to review its details.

**Default Behavior:**

- Include Pending Deliveries is disabled.
- Include Historical Discrepancies is disabled.
- The report focuses on current outstanding differences and reportable finalized exceptions.
- Assigned and In Progress Deliveries are excluded from finalized discrepancy results.
- Resolved historical shortages do not appear as current outstanding shortages.
- The report remains read-only.

**Validation:**

- Start Date must not be later than End Date.
- Customer, Route, and Item filters must reference valid records.
- Invalid filters must display clear messages.
- No matching results must display an empty-results message.
- Incomplete historical information must display a warning.

### SCREEN-18.2: Delivery Difference Details Screen

**Purpose:**

Allow an authorized Manager to review the Shipment, Delivery, and discrepancy information associated with a reported difference.

**Displayed Information:**

- Customer Number
- Customer Name
- Customer Order Number
- Shipment Number
- Shipment Line ID
- Item Number
- Item Description
- Quantity Shipped
- Cumulative Quantity Delivered
- Difference Units
- Outstanding Units
- Difference Type
- Current or Historical classification
- Pending or Finalized classification

**Delivery Details:**

- Delivery ID
- Delivery Route
- Driver
- Delivery Status
- Delivery completion date and time
- Quantity Delivered during each finalized attempt
- Associated Delivery Discrepancies
- Discrepancy reasons
- Discrepancy resolution status

**Screen Behavior:**

1. The Manager selects a difference from the report.
2. The system retrieves the associated Shipment Line.
3. The system displays the original Quantity Shipped.
4. The system displays cumulative confirmed Quantity Delivered.
5. The system displays the calculated Difference Units.
6. The system identifies the difference type.
7. The system displays related Delivery attempts.
8. The Manager may open the Delivery History view.
9. The Manager may return to the report.
10. No edit, approve, or delete actions are available.

### SCREEN-18.3: Delivery History Screen

**Purpose:**

Allow an authorized Manager to review previous delivery attempts and historical discrepancies.

**Displayed Information:**

- Shipment Number
- Item Number
- Original Quantity Shipped
- Delivery Attempt reference
- Delivery Route
- Driver
- Delivery Status
- Quantity Delivered during the attempt
- Delivery completion date and time
- Discrepancy Type
- Discrepancy Quantity
- Discrepancy Reason
- Discrepancy Reported Date and Time
- Discrepancy Resolution Status

**Screen Behavior:**

1. The Manager opens Delivery History from a report result.
2. The system retrieves related Delivery attempts.
3. The system displays finalized attempts in chronological order.
4. The system displays historical discrepancies associated with each attempt.
5. The system identifies whether discrepancies are Open or Resolved.
6. The Manager may return to the Delivery Difference Details screen.
7. No historical records may be modified from this screen.

### SCREEN-18.4: Empty Results and Validation Messages

**Purpose:**

Provide clear feedback when report filters are invalid, no differences match the selected criteria, or historical information is incomplete.

**Required Messages:**

When no matching differences exist:

`No matching delivery differences were found.`

When the selected date range is invalid:

`Start Date must not be later than End Date.`

When historical delivery information is incomplete:

`Some historical Shipment or Delivery information is unavailable or incomplete. Report results may not include all delivery differences.`

When a pending Delivery is displayed:

`Pending Delivery - the delivery attempt has not been finalized.`

When an apparent over-delivery is displayed:

`Apparent Over-Delivery - reported quantity requires authorized review.`

When a historical shortage has been resolved:

`Resolved - the outstanding quantity was delivered during a later attempt.`

When a User lacks permission:

`You do not have permission to view this report.`

### Screen Design Requirements

- Follow the Warehouse Management System's established UI style.
- Use consistent Customer, Order, Shipment, Item, and Route labels.
- Clearly identify quantities as individual units.
- Clearly distinguish Shortage, Apparent Over-Delivery, Failed Delivery, and Pending Delivery.
- Display negative differences with a minus sign.
- Clearly identify current and historical records.
- Clearly identify Open and Resolved discrepancies.
- Display the Driver and Delivery Route associated with each relevant delivery attempt.
- Preserve historical identification after master record deactivation.
- Use consistent date and time formatting.
- Support readable tables containing multiple Shipments and Items.
- Do not provide report-side editing controls.
- Do not require paper records to review delivery discrepancies.

**[NEEDS CLARIFICATION]** Confirm final Figma screen layouts, navigation placement, and detailed table presentation.

---

## Definition of Done

Feature 18 is considered complete when the following conditions are satisfied.

### Requirements

- [ ] All Functional Requirements FR-001 through FR-058 are implemented or explicitly deferred.
- [ ] All User Stories US-18.1 through US-18.6 are supported.
- [ ] All 28 Gherkin Acceptance Criteria have corresponding tests.
- [ ] All clarification items have been reviewed.
- [ ] The implementation follows the approved requirements.

### Data Model

- [ ] Customer and Customer Order references are available.
- [ ] Shipment and Shipment Line references are available.
- [ ] Original Quantity Shipped is preserved.
- [ ] Delivery and Delivery Line references are available.
- [ ] Finalized Delivery statuses are available.
- [ ] Delivery completion dates are recorded.
- [ ] Delivery Route references are preserved.
- [ ] Driver references are preserved.
- [ ] Delivery Discrepancy records are available.
- [ ] Historical discrepancy resolution status is preserved.
- [ ] Source data relationships are maintained.

### Business Logic

- [ ] Quantity Shipped is obtained from Shipment Lines.
- [ ] Quantity Delivered is calculated from finalized Delivery Lines.
- [ ] Each finalized Delivery Line is counted once.
- [ ] Difference Units are calculated correctly.
- [ ] Outstanding Units are calculated correctly.
- [ ] Confirmed shortages are identified correctly.
- [ ] Apparent Over-Delivery exceptions are identified separately.
- [ ] Apparent over-deliveries do not automatically increase confirmed Quantity Delivered.
- [ ] Matching quantities are excluded from current outstanding shortage results.
- [ ] Assigned and In Progress Deliveries are excluded from finalized results.
- [ ] Pending Deliveries can be displayed separately.
- [ ] Finalized Failed Attempts remain reportable.
- [ ] Partial deliveries are reported correctly.
- [ ] Multiple delivery attempts are handled correctly.
- [ ] Resolved historical shortages are excluded from current outstanding shortage results.
- [ ] Historical discrepancies remain available after resolution.
- [ ] Quantity Picked is not substituted for Quantity Shipped.
- [ ] Quantity Ordered is not substituted for Quantity Delivered.

### API

- [ ] Delivery Difference Report API is implemented.
- [ ] Delivery Difference Details API is implemented.
- [ ] Delivery History API is implemented or integrated with existing delivery endpoints.
- [ ] Delivery Discrepancy Details API is implemented or integrated with existing discrepancy endpoints.
- [ ] Customer filtering works.
- [ ] Delivery Route filtering works.
- [ ] Individual Item filtering works.
- [ ] Date-range filtering works.
- [ ] Discrepancy-type filtering works.
- [ ] Pending delivery reporting works.
- [ ] Historical discrepancy reporting works.
- [ ] Report sorting works.
- [ ] Invalid filters are rejected.
- [ ] Authorization is enforced.
- [ ] API operations remain read-only.

### User Interface

- [ ] Delivery Difference Report screen is implemented.
- [ ] Customer filter is available.
- [ ] Delivery Route filter is available.
- [ ] Individual Item filter is available.
- [ ] Date-range filters are available.
- [ ] Discrepancy-type filter is available.
- [ ] Include Pending Deliveries option is available.
- [ ] Include Historical Discrepancies option is available.
- [ ] Sorting controls are available.
- [ ] Results display required Shipment and Delivery information.
- [ ] Confirmed shortages and apparent over-deliveries are clearly distinguished.
- [ ] Pending deliveries are clearly identified.
- [ ] Historical discrepancies are clearly identified.
- [ ] Delivery Difference Details screen is implemented.
- [ ] Delivery History screen is implemented.
- [ ] Empty results display a clear message.
- [ ] Incomplete historical information displays a warning.
- [ ] Screens follow the approved Figma design.
- [ ] No report-side editing controls are provided.

### Testing

- [ ] Unit tests verify Difference Units calculations.
- [ ] Unit tests verify cumulative Quantity Delivered calculations.
- [ ] Unit tests verify duplicate Delivery Line prevention.
- [ ] Unit tests verify confirmed shortage classification.
- [ ] Unit tests verify apparent over-delivery handling.
- [ ] Unit tests verify matching quantity exclusion.
- [ ] Unit tests verify partial delivery reporting.
- [ ] Unit tests verify failed delivery reporting.
- [ ] Unit tests verify pending delivery classification.
- [ ] Unit tests verify multiple delivery attempts.
- [ ] Unit tests verify historical discrepancy preservation.
- [ ] Unit tests verify resolved shortage exclusion from current results.
- [ ] Integration tests verify Customer Order and Shipment relationships.
- [ ] Integration tests verify Shipment and Delivery relationships.
- [ ] Integration tests verify Delivery Route and Driver identification.
- [ ] API tests verify report filters.
- [ ] API tests verify unauthorized access is denied.
- [ ] UI tests verify report generation and details.
- [ ] Tests verify historical identification after deactivation.
- [ ] Tests verify incomplete historical data warnings.
- [ ] All automated tests pass.

### Code Quality and Documentation

- [ ] Code follows project conventions.
- [ ] Report calculations are documented.
- [ ] API documentation is updated.
- [ ] Data model relationships are documented.
- [ ] Error and validation messages are reviewed.
- [ ] No unrelated feature behavior is modified.
- [ ] Code is reviewed and approved.
- [ ] Changes are committed to the correct Git branch.

---

## Out of Scope

The following capabilities are not included in Feature 18.

### Customer Maintenance

Feature 18 does not:

- Create Customers.
- Edit Customer information.
- Activate or deactivate Customers.
- Delete Customer records.

Customer maintenance belongs to Feature 6.

### Individual Item Maintenance

Feature 18 does not:

- Create Individual Items.
- Edit Item descriptions.
- Change Item Numbers.
- Modify Item master data.
- Activate or deactivate Items.

Individual Item maintenance belongs to Feature 4.

### Customer Order Maintenance

Feature 18 does not:

- Create Customer Orders.
- Add or remove Customer Order Lines.
- Change ordered quantities.
- Cancel Customer Orders.
- Modify Customer Order status.

These operations belong to the applicable Customer Order features.

### Picking Operations

Feature 18 does not:

- Generate picking tasks.
- Pick Items from storage bins.
- Confirm picked quantities.
- Adjust picked quantities.
- Replenish picking locations.

Picking operations belong to the applicable warehouse picking feature.

### Shipping Operations

Feature 18 does not:

- Create Shipments.
- Add or remove Shipment Lines.
- Change Quantity Shipped.
- Cancel Shipments.
- Prepare shipments for delivery.

Shipping operations belong to Feature 14.

### Delivery Operations

Feature 18 does not:

- Assign Deliveries to Drivers.
- Start delivery attempts.
- Confirm delivered quantities.
- Complete Deliveries.
- Record new Delivery Discrepancies.
- Resolve Delivery Discrepancies.
- Change Delivery Routes.
- Change delivery completion dates.

Delivery operations belong to Feature 15 and the applicable Delivery Route functionality.

### Inventory Maintenance

Feature 18 does not:

- Adjust Inventory quantities.
- Move Inventory between bins.
- Reconcile Inventory balances.
- Return undelivered Items to Inventory.
- Create replacement shipments.

These activities belong to separate warehouse operations.

### Financial Processing

Feature 18 does not:

- Generate Customer refunds.
- Issue credits for missing deliveries.
- Calculate delivery penalties.
- Create invoices.
- Process payments.
- Automatically generate insurance claims.

### Advanced Reporting

The following capabilities are deferred unless separately approved:

- Automatic Driver performance scores.
- Delivery Route performance rankings.
- Predictive delivery failure analysis.
- Automatic discrepancy alerts.
- Scheduled email reports.
- Custom report builders.
- Advanced reporting dashboards.
- Automatic PDF or spreadsheet exports.

### Historical Data Correction

Feature 18 does not provide report-screen functionality for modifying or deleting historical Shipments, Deliveries, Delivery Lines, or Delivery Discrepancies.

Historical corrections must be handled through separately authorized workflows.

---

**End of Feature 18: Report Deliveries That Do Not Match What Was Shipped**
