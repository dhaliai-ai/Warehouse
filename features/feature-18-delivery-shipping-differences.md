
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
