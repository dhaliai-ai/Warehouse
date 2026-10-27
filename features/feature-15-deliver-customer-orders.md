
# Feature: Deliver Customer Orders

**Feature ID:** 15  
**Branch pattern:** `feature/15-deliver-customer-orders`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System assists Drivers in delivering shipped Customer Orders. The system identifies Shipments assigned to a Driver's Delivery Route, displays the Customer and shipped Items, allows the Driver to record actual Quantity Delivered, identifies differences between Quantity Shipped and Quantity Delivered, and preserves delivery records for reporting. Delivery confirmation is separate from shipping. Physical truck loading, route navigation, and driving are outside the scope of this feature.

---

## User Stories

### US-15.1: Identify Customer Orders for Delivery

**As a** Driver  
**I want to** see the shipped Customer Orders assigned to my Delivery Route  
**So that** I know which Customers and Shipments require delivery.

**Priority:** P1  
**Independent test:** Sign in as a Driver with an assigned Delivery Route and verify that eligible Shipments and Customer Orders appear.

### US-15.2: Deliver Customer Order

**As a** Driver  
**I want to** select an assigned Shipment and record its delivery outcome  
**So that** the warehouse knows whether the Customer received the products.

**Priority:** P1  
**Independent test:** Select a Shipment assigned to the Driver's route and verify that delivery information can be recorded.

### US-15.3: Record Quantity Delivered

**As a** Driver  
**I want to** record the actual quantity delivered for each Item  
**So that** the system distinguishes what the Customer received from what the warehouse shipped.

**Priority:** P1  
**Independent test:** Record actual delivered quantities and verify that Quantity Delivered is updated without changing Quantity Shipped.

### US-15.4: Identify Delivery Differences

**As a** Driver  
**I want to** record differences between Quantity Shipped and Quantity Delivered  
**So that** the warehouse can investigate shortages and prepare accurate delivery discrepancy reports.

**Priority:** P1  
**Independent test:** Record fewer units delivered than shipped and verify that the system preserves the difference for Feature 18.

### US-15.5: Record Unsuccessful Delivery Attempt

**As a** Driver  
**I want to** report when a Customer cannot receive a Shipment  
**So that** the warehouse knows that delivery remains incomplete and can arrange follow-up.

**Priority:** P2  
**Independent test:** Record an unsuccessful delivery attempt and verify that the Shipment is not marked as fully delivered.

### US-15.6: Review Delivery History

**As a** Warehouse Manager  
**I want to** review completed and unsuccessful Deliveries  
**So that** I can investigate delivery problems and compare shipped quantities with delivered quantities.

**Priority:** P2  
**Independent test:** Retrieve a Delivery and verify that its Shipment, Driver, route, quantities, status, and discrepancies are displayed.

---

## Functional Requirements

- **FR-001:** The system MUST identify Shipments assigned to a Driver's Delivery Route.
- **FR-002:** The system MUST allow an authenticated Driver to view eligible Deliveries assigned to that Driver.
- **FR-003:** The system MUST display the Customer Order Number, Shipment Number, Customer, delivery address, and shipped Items for each assigned Delivery.
- **FR-004:** The system MUST display Quantity Shipped for each Item included in the Shipment.
- **FR-005:** The system MUST allow the Driver to select an assigned Shipment for delivery confirmation.
- **FR-006:** The system MUST allow delivery confirmation only for Shipments that have completed shipping and are Ready for Delivery.
- **FR-007:** The system MUST prevent Draft, Preparing, Canceled, or otherwise unready Shipments from entering ordinary delivery confirmation.
- **FR-008:** The system MUST associate each Delivery with a specific Shipment.
- **FR-009:** The system MUST associate each Delivery with a Delivery Route and assigned Driver.
- **FR-010:** The system MUST preserve the relationship between the Delivery, Shipment, Customer Order, Customer, and Delivery Route.
- **FR-011:** The system MUST prevent a Driver from confirming a Delivery assigned to another Driver without authorized reassignment.
- **FR-012:** The system MUST support assignment of eligible Shipments to a Delivery Route by an authorized Shipping Supervisor or Manager.
- **FR-013:** The system MUST prevent the same Shipment from having multiple active Delivery assignments.
- **FR-014:** The system MUST allow the Driver to record the actual Quantity Delivered for each Shipment Line.
- **FR-015:** Quantity Delivered MUST be recorded in individual units.
- **FR-016:** The system MUST allow Quantity Delivered to be zero when the Customer receives none of an Item.
- **FR-017:** The system MUST reject negative or non-integer Quantity Delivered values.
- **FR-018:** The system MUST preserve Quantity Shipped separately from Quantity Delivered.
- **FR-019:** The system MUST preserve Quantity Ordered and Quantity Picked separately from delivery information.
- **FR-020:** The system MUST compare Quantity Delivered with Quantity Shipped for each Shipment Line.
- **FR-021:** The system MUST calculate the difference between Quantity Shipped and Quantity Delivered.
- **FR-022:** The system MUST record delivery discrepancies when actual Quantity Delivered differs from Quantity Shipped.
- **FR-023:** The system MUST preserve the Item, Shipment, Customer Order, shipped quantity, delivered quantity, and difference for each discrepancy.
- **FR-024:** The system MUST prevent ordinary delivery confirmation from recording more units delivered than the remaining undelivered quantity of the Shipment Line.
- **FR-025:** The system MUST allow the Driver to report an apparent over-delivery as an exception for Supervisor review without silently increasing Quantity Delivered.
- **FR-026:** The system MUST allow a Driver to record a reason when the Customer receives fewer units than shipped.
- **FR-027:** The system MUST preserve discrepancies for reporting in Feature 18.
- **FR-028:** The system MUST allow a Driver to record a successful delivery when all shipped quantities have been received by the Customer.
- **FR-029:** The system MUST allow a Driver to record a partial delivery when only some shipped quantities are received.
- **FR-030:** The system MUST allow a Driver to record an unsuccessful delivery attempt when no products can be delivered.
- **FR-031:** The system MUST record a reason for an unsuccessful delivery attempt.
- **FR-032:** The system MUST maintain Delivery statuses of Assigned, In Progress, Partially Delivered, Delivered, and Failed Attempt.
- **FR-033:** A newly assigned Delivery MUST initially have Assigned status.
- **FR-034:** The system MUST change the Delivery status to In Progress when the Driver begins recording the delivery.
- **FR-035:** The system MUST mark a Delivery as Delivered when all shipped quantities for that Shipment have been confirmed delivered.
- **FR-036:** The system MUST mark a Delivery as Partially Delivered when some, but not all, shipped quantities have been confirmed delivered and the delivery attempt has been finalized.
- **FR-037:** The system MUST mark a Delivery as Failed Attempt when no products were delivered and the Driver records an unsuccessful attempt.
- **FR-038:** The system MUST record the date and time of each finalized delivery outcome.
- **FR-039:** The system MUST record the Driver who finalized the delivery outcome.
- **FR-040:** The system MUST update cumulative Quantity Delivered on the associated Customer Order Lines after confirmed delivery.
- **FR-041:** The system MUST prevent the same delivery confirmation from increasing cumulative Quantity Delivered more than once.
- **FR-042:** The system MUST preserve undelivered quantities for authorized follow-up and reconciliation.
- **FR-043:** The system MUST allow a new delivery attempt for undelivered quantities through an authorized reassignment process.
- **FR-044:** The system MUST preserve previous delivery attempts when a new attempt is created.
- **FR-045:** The system MUST mark a Customer Order as Delivered only when all ordered quantities have been confirmed delivered.
- **FR-046:** The system MUST mark a Customer Order as Partially Delivered when at least one unit has been delivered but some ordered quantities remain undelivered.
- **FR-047:** The system MUST NOT mark a Customer Order as fully Delivered solely because a Shipment was marked Ready for Delivery.
- **FR-048:** The system MUST preserve Shipment quantities even when delivery is incomplete or unsuccessful.
- **FR-049:** The system MUST allow authorized Managers to retrieve Delivery records for review.
- **FR-050:** The system MUST preserve Delivery history, including Driver, Delivery Route, Shipment, Item quantities, delivery outcome, and discrepancies.
- **FR-051:** The system MUST prevent finalized delivery records from being silently changed through ordinary Driver operations.
- **FR-052:** The system MUST restrict delivery recording to authorized Drivers and delivery administration to authorized Supervisors or Managers.
- **FR-053:** The system MUST reject attempts to record delivery against nonexistent Shipments or Deliveries.
- **FR-054:** The system MUST keep delivery confirmation separate from physical truck loading and route navigation.
- **FR-055:** The system MUST NOT automatically modify Quantity Shipped when Quantity Delivered differs.
- **FR-056:** The system MUST preserve delivery discrepancies even after a later delivery attempt resolves the outstanding quantity.

---

## Key Entities

### Delivery

Represents the delivery confirmation process for a specific Shipment.

A Delivery identifies its Shipment, Driver, Delivery Route, current status, and delivery outcome.

### Delivery Line

Represents an Individual Item included in a Delivery.

Each line records the quantity shipped in the associated Shipment and the quantity actually delivered during that delivery attempt.

### Delivery Route

Represents a route used to organize deliveries to Customers.

A Delivery Route is associated with a Driver through a route assignment.

### Delivery Assignment

Represents the assignment of a Shipment to a Driver and Delivery Route.

### Shipment

Represents products prepared and released for delivery in Feature 14.

### Shipment Line

Represents an Individual Item and Quantity Shipped in a Shipment.

### Customer Order

Represents an order placed by a Customer.

### Customer Order Line

Represents an Individual Item ordered by a Customer with quantities maintained across warehouse processes.

### Customer

Represents the retail store or business receiving the Shipment.

### Individual Item

Represents a product included in a Shipment and Delivery.

### Delivery Discrepancy

Represents a recorded difference or exception identified during delivery.

### User

Represents an authenticated Driver, Shipping Supervisor, or Manager.

---

## Initial Data Model

### Delivery

| Attribute | Type | Description |
|---|---|---|
| deliveryId | Integer | Unique Delivery identifier |
| shipmentId | Integer | Foreign key referencing Shipment |
| deliveryAssignmentId | Integer | Foreign key referencing Delivery Assignment |
| driverId | Integer | Foreign key referencing User |
| deliveryRouteId | Integer | Foreign key referencing Delivery Route |
| status | String | Assigned, In Progress, Partially Delivered, Delivered, or Failed Attempt |
| startedAt | DateTime | Date and time the Driver started delivery confirmation |
| completedAt | DateTime | Date and time the delivery outcome was finalized |
| failureReason | String | Optional reason for an unsuccessful delivery attempt |

**Relationships:**
- Each Delivery references one Shipment.
- Each Delivery references one Delivery Assignment.
- Each Delivery is associated with one Driver and one Delivery Route.
- Each Delivery contains one or more Delivery Lines.
- A Shipment may have multiple Deliveries over time when additional delivery attempts are required.

**Constraints:**
- deliveryId must be unique.
- The referenced Shipment must exist and be Ready for Delivery before initial assignment.
- Only the assigned Driver or authorized personnel may finalize the Delivery.
- A finalized Delivery cannot be finalized again.

### Delivery Line

| Attribute | Type | Description |
|---|---|---|
| deliveryLineId | Integer | Unique Delivery Line identifier |
| deliveryId | Integer | Foreign key referencing Delivery |
| shipmentLineId | Integer | Foreign key referencing Shipment Line |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityShipped | Integer | Original quantity shipped on the Shipment Line |
| quantityDelivered | Integer | Quantity confirmed delivered during this attempt |

**Relationships:**
- Each Delivery Line belongs to one Delivery.
- Each Delivery Line references one Shipment Line.
- Each Delivery Line identifies one Individual Item.
- Confirmed Delivery Lines contribute to cumulative Quantity Delivered on Customer Order Lines.

**Constraints:**
- quantityShipped cannot be negative.
- quantityDelivered cannot be negative.
- quantityDelivered cannot exceed the remaining undelivered quantity of the associated Shipment Line.
- The combination of deliveryId and shipmentLineId must be unique.

**Derived Values:**
- Cumulative Delivered for Shipment Line = Sum of finalized Delivery Line quantities for that Shipment Line.
- Remaining Undelivered for Shipment Line = Quantity Shipped - Cumulative Delivered.
- Original Delivery Difference = Quantity Shipped - Quantity Delivered confirmed during the first finalized delivery attempt.

### Delivery Route

| Attribute | Type | Description |
|---|---|---|
| deliveryRouteId | Integer | Unique Delivery Route identifier |
| routeCode | String | Unique route code |
| routeName | String | Descriptive route name |
| isActive | Boolean | Indicates whether the route is active |

**Relationships:**
- A Delivery Route may serve multiple Customers.
- A Delivery Route may contain multiple Delivery Assignments.
- A Delivery Route may be assigned to a Driver for delivery work.

### Delivery Assignment

| Attribute | Type | Description |
|---|---|---|
| deliveryAssignmentId | Integer | Unique Delivery Assignment identifier |
| shipmentId | Integer | Foreign key referencing Shipment |
| deliveryRouteId | Integer | Foreign key referencing Delivery Route |
| driverId | Integer | Foreign key referencing User |
| assignedAt | DateTime | Date and time of assignment |
| status | String | Active, Completed, or Reassigned |

**Relationships:**
- Each Delivery Assignment references one Shipment.
- Each Delivery Assignment identifies one Delivery Route and Driver.
- A Shipment may have multiple historical Delivery Assignments.
- Only one active Delivery Assignment may exist for a Shipment at a time.

### Shipment

| Attribute | Type | Description |
|---|---|---|
| shipmentId | Integer | Unique Shipment identifier |
| shipmentNumber | String | Unique Shipment reference |
| customerOrderId | Integer | Foreign key referencing Customer Order |
| status | String | Shipping preparation status |

**Relationships:**
- A Shipment belongs to one Customer Order.
- A Shipment contains one or more Shipment Lines.
- A Shipment becomes eligible for delivery after Feature 14 marks it Ready for Delivery.

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
- One Shipment Line may be referenced by multiple Delivery Lines across separate attempts.

### Customer Order

| Attribute | Type | Description |
|---|---|---|
| customerOrderId | Integer | Unique Customer Order identifier |
| orderNumber | String | Unique Customer Order Number |
| customerId | Integer | Foreign key referencing Customer |
| status | String | Current Customer Order status |

**Relationships:**
- A Customer Order belongs to one Customer.
- A Customer Order may have multiple Shipments.
- A Customer Order contains one or more Customer Order Lines.

### Customer Order Line

| Attribute | Type | Description |
|---|---|---|
| customerOrderLineId | Integer | Unique Customer Order Line identifier |
| customerOrderId | Integer | Foreign key referencing Customer Order |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityOrdered | Integer | Quantity originally ordered |
| quantityPicked | Integer | Cumulative quantity picked |
| quantityShipped | Integer | Cumulative quantity shipped |
| quantityDelivered | Integer | Cumulative quantity delivered |

**Relationships:**
- Each Customer Order Line belongs to one Customer Order.
- Shipment Lines reference Customer Order Lines.
- Finalized Delivery Lines contribute to cumulative Quantity Delivered.

**Constraints:**
- quantityDelivered cannot be negative.
- Cumulative Quantity Delivered cannot exceed cumulative Quantity Shipped under ordinary delivery confirmation.

### Customer

| Attribute | Type | Description |
|---|---|---|
| customerId | Integer | Unique Customer identifier |
| customerNumber | String | Unique Customer Number |
| name | String | Customer business name |
| deliveryAddress | String | Customer delivery address |

**Relationships:**
- A Customer may have multiple Customer Orders.
- Customers may be associated with a default Delivery Route.
- Customer maintenance is defined in Feature 6.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |

**Relationships:**
- An Individual Item may appear on multiple Customer Order Lines.
- An Individual Item may appear on multiple Delivery Lines.

### Delivery Discrepancy

| Attribute | Type | Description |
|---|---|---|
| deliveryDiscrepancyId | Integer | Unique discrepancy identifier |
| deliveryId | Integer | Foreign key referencing Delivery |
| deliveryLineId | Integer | Optional foreign key referencing Delivery Line |
| discrepancyType | String | Short Delivery, Apparent Over-Delivery, or Failed Delivery |
| quantityDifference | Integer | Difference associated with the reported issue |
| reason | String | Explanation provided by the Driver |
| reportedAt | DateTime | Date and time reported |
| status | String | Open or Resolved |

**Relationships:**
- Each Delivery Discrepancy belongs to one Delivery.
- A discrepancy may reference a specific Delivery Line.
- Delivery Discrepancies are available to Feature 18 for reporting.

**Constraints:**
- A discrepancy record must preserve the reported issue even after resolution.
- Apparent over-deliveries must be reviewed before quantities are corrected.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Driver, Shipping Supervisor, Manager, or another authorized role |

**Relationships:**
- Drivers record Deliveries assigned to them.
- Shipping Supervisors and Managers administer assignments and review exceptions.

---

## Gherkin AC

### US-15.1: Identify Customer Orders for Delivery

#### AC-15.1.1: Display assigned Deliveries

**Given** a Driver has an active Delivery Route assignment  
**And** eligible Shipments are assigned to that Driver  
**When** the Driver opens the delivery process  
**Then** the system displays the assigned Shipments and Customer Orders  
**And** identifies the Customers and delivery addresses.

#### AC-15.1.2: Select assigned Shipment

**Given** a Shipment is assigned to the Driver's Delivery Route  
**And** the Shipment is Ready for Delivery  
**When** the Driver selects the Shipment  
**Then** the system displays its Customer Order Number, shipped Items, and Quantity Shipped.

#### AC-15.1.3: No assigned Deliveries

**Given** a Driver has no eligible assigned Shipments  
**When** the Driver opens the delivery process  
**Then** the system reports that no Deliveries are currently assigned.

#### AC-15.1.4: Reject another Driver's assignment

**Given** Shipment S100 is assigned to Driver A  
**When** Driver B attempts to confirm delivery for Shipment S100 without authorization  
**Then** the system denies the operation  
**And** does not modify delivery quantities.

### US-15.2: Deliver Customer Order

#### AC-15.2.1: Start assigned Delivery

**Given** a Shipment is Ready for Delivery  
**And** it is assigned to the authenticated Driver  
**When** the Driver begins recording the Delivery  
**Then** the system changes the Delivery status to In Progress  
**And** allows the Driver to enter actual delivered quantities.

#### AC-15.2.2: Reject unready Shipment

**Given** a Shipment is still in Preparing status  
**When** a Driver attempts to confirm its delivery  
**Then** the system rejects the request  
**And** does not create a completed Delivery record.

#### AC-15.2.3: Record successful Delivery

**Given** a Shipment contains 20 units of Item A and 10 units of Item B  
**And** the Customer receives all shipped quantities  
**When** the Driver records 20 units of Item A and 10 units of Item B as delivered  
**And** finalizes the Delivery  
**Then** the system marks the Delivery as Delivered  
**And** records the Driver and completion time.

#### AC-15.2.4: Preserve Shipment association

**Given** a Driver finalizes a Delivery  
**When** the system saves the delivery outcome  
**Then** the Delivery remains associated with its Shipment, Customer Order, Driver, and Delivery Route.

### US-15.3: Record Quantity Delivered

#### AC-15.3.1: Quantity Delivered equals Quantity Shipped

**Given** a Shipment Line contains 25 units shipped  
**And** none of those units have been delivered previously  
**When** the Driver records 25 units delivered  
**And** finalizes the Delivery  
**Then** the system records 25 units as delivered  
**And** preserves Quantity Shipped as 25  
**And** records no quantity shortage.

#### AC-15.3.2: Quantity Delivered is less than Quantity Shipped

**Given** a Shipment Line contains 25 units shipped  
**And** none of those units have been delivered previously  
**When** the Driver records 20 units delivered  
**And** finalizes the Delivery  
**Then** the system records 20 units delivered  
**And** preserves Quantity Shipped as 25  
**And** identifies 5 units as undelivered.

#### AC-15.3.3: Reject negative Quantity Delivered

**Given** a Driver is recording delivery for an assigned Shipment  
**When** the Driver enters Quantity Delivered of -3  
**Then** the system rejects the quantity  
**And** does not modify cumulative Quantity Delivered.

#### AC-15.3.4: Handle apparent over-delivery

**Given** a Shipment Line contains 20 units shipped  
**And** none of those units have been delivered previously  
**When** the Driver reports that the Customer received 23 units  
**Then** the system flags an apparent over-delivery of 3 units  
**And** requires Supervisor review  
**And** does not silently change the recorded Quantity Shipped or Quantity Delivered.

#### AC-15.3.5: Prevent duplicate delivery confirmation

**Given** a Delivery confirmation for 15 units has already been finalized  
**When** the same confirmation is submitted again  
**Then** the system rejects the duplicate operation  
**And** does not increase cumulative Quantity Delivered a second time.

### US-15.4: Identify Delivery Differences

#### AC-15.4.1: Record delivery shortage

**Given** a Shipment Line contains 30 units shipped  
**And** the Customer receives 26 units  
**When** the Driver finalizes the Delivery  
**Then** the system records Quantity Delivered as 26  
**And** records a delivery shortage of 4 units  
**And** preserves the discrepancy for Feature 18.

#### AC-15.4.2: Preserve separate warehouse quantities

**Given** a Customer Order Line contains 50 units ordered  
**And** 45 units picked  
**And** 40 units shipped  
**And** 38 units delivered  
**When** an authorized User reviews the order  
**Then** the system displays Quantity Ordered as 50  
**And** Quantity Picked as 45  
**And** Quantity Shipped as 40  
**And** Quantity Delivered as 38.

#### AC-15.4.3: Preserve discrepancy after later delivery

**Given** a first Delivery Attempt recorded 15 units delivered out of 20 shipped  
**And** a discrepancy of 5 units was recorded  
**When** a later authorized Delivery Attempt confirms the remaining 5 units  
**Then** the system updates cumulative Quantity Delivered to 20  
**And** preserves the first Delivery Attempt and its original discrepancy history.

#### AC-15.4.4: Make discrepancies available for reporting

**Given** a finalized Delivery contains a quantity discrepancy  
**When** an authorized Manager requests delivery discrepancy information  
**Then** the system provides the Shipment, Customer Order, Item, Quantity Shipped, Quantity Delivered, and difference  
**And** makes the information available to Feature 18.

### US-15.5: Record Unsuccessful Delivery Attempt

#### AC-15.5.1: Customer cannot receive Shipment

**Given** a Driver is assigned a Shipment  
**And** the Customer cannot receive any products  
**When** the Driver records an unsuccessful delivery attempt and provides a reason  
**Then** the system marks the Delivery as Failed Attempt  
**And** records zero units delivered during that attempt  
**And** preserves the Shipment for follow-up.

#### AC-15.5.2: Partial delivery

**Given** a Shipment contains 20 units of Item A  
**And** the Customer receives only 12 units  
**When** the Driver records 12 units delivered and finalizes the attempt  
**Then** the system marks the Delivery as Partially Delivered  
**And** records 8 units as undelivered  
**And** preserves the outstanding quantity for follow-up.

#### AC-15.5.3: Authorize another delivery attempt

**Given** a Shipment has 8 undelivered units remaining  
**And** an authorized Supervisor approves another attempt  
**When** a new Delivery Assignment is created  
**Then** the system associates the new attempt with the original Shipment  
**And** limits the new attempt to the 8 outstanding units  
**And** preserves the earlier Delivery history.

### US-15.6: Review Delivery History

#### AC-15.6.1: Review completed Delivery

**Given** a Delivery has been finalized  
**When** an authorized Manager retrieves its record  
**Then** the system displays the Shipment, Customer Order, Driver, Delivery Route, Items, quantities, outcome, and completion time.

#### AC-15.6.2: Review unsuccessful Delivery

**Given** a Delivery Attempt was marked Failed Attempt  
**When** an authorized Manager reviews the Delivery  
**Then** the system displays the failure reason  
**And** identifies the undelivered quantities  
**And** preserves the Shipment association.

#### AC-15.6.3: Prevent unauthorized modification

**Given** a Driver has finalized a Delivery  
**When** the Driver attempts to change the finalized quantities through ordinary delivery entry  
**Then** the system rejects the modification  
**And** preserves the original Delivery record.

#### AC-15.6.4: Reject nonexistent Shipment

**Given** Shipment S999 does not exist  
**When** a Driver attempts to record a Delivery for Shipment S999  
**Then** the system rejects the request  
**And** does not create a Delivery record.

#### AC-15.6.5: Preserve reporting history

**Given** a Delivery Discrepancy has been recorded  
**When** the discrepancy is later resolved  
**Then** the system preserves the original discrepancy and its resolution status  
**And** keeps the history available for reporting.
