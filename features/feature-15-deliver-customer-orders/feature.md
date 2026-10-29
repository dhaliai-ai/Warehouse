
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

## Assumptions

- **A-001:** Feature 14 prepares Shipments and marks them Ready for Delivery before they enter the delivery process.
- **A-002:** Only Shipments in Ready for Delivery status are eligible for initial delivery assignment and confirmation.
- **A-003:** Each Delivery references one Shipment.
- **A-004:** Each Delivery is associated with one Delivery Route and one assigned Driver.
- **A-005:** An authorized Shipping Supervisor or Manager assigns eligible Shipments to Delivery Routes.
- **A-006:** Only one active Delivery Assignment may exist for a Shipment at a time.
- **A-007:** A Shipment may have multiple historical Delivery Assignments when reassignment is required.
- **A-008:** Drivers can view and record only Deliveries assigned to them unless authorized reassignment occurs.
- **A-009:** The system provides authentication and role-based authorization for Drivers, Supervisors, and Managers.
- **A-010:** Customer Orders, Customer information, Shipment Lines, and shipped quantities are available from their owning features.
- **A-011:** Quantity Shipped is finalized by Feature 14 before ordinary delivery confirmation begins.
- **A-012:** Quantity Delivered is recorded separately from Quantity Shipped.
- **A-013:** Quantity Ordered and Quantity Picked remain unchanged during delivery confirmation.
- **A-014:** Delivered quantities are recorded in individual units.
- **A-015:** A Driver may record zero delivered units for a Shipment Line.
- **A-016:** Delivered quantities must be nonnegative whole numbers.
- **A-017:** A delivery attempt cannot confirm more units than remain undelivered on the associated Shipment Line.
- **A-018:** A Driver can report an apparent over-delivery without changing the approved shipped or delivered quantities.
- **A-019:** Delivery discrepancies preserve the original shipped quantity, delivered quantity, difference, and reason when applicable.
- **A-020:** Delivery Discrepancies remain available for Feature 18 reporting.
- **A-021:** Delivery statuses are Assigned, In Progress, Partially Delivered, Delivered, and Failed Attempt.
- **A-022:** A newly assigned Delivery begins in Assigned status.
- **A-023:** A Delivery becomes In Progress when its assigned Driver begins recording the outcome.
- **A-024:** A successful Delivery is finalized when all applicable shipped quantities have been confirmed received.
- **A-025:** A partially completed delivery attempt preserves the remaining undelivered quantities.
- **A-026:** An unsuccessful attempt records zero units delivered and requires a reason.
- **A-027:** Each finalized delivery outcome records the responsible Driver and completion timestamp.
- **A-028:** Finalized Delivery Line quantities contribute to cumulative Quantity Delivered on Customer Order Lines.
- **A-029:** Repeating the same finalized delivery confirmation cannot increase cumulative Quantity Delivered again.
- **A-030:** New delivery attempts for outstanding quantities require authorized reassignment.
- **A-031:** Previous delivery attempts remain preserved when follow-up attempts occur.
- **A-032:** A Customer Order becomes Delivered only when all ordered quantities have been confirmed delivered.
- **A-033:** A Customer Order becomes Partially Delivered when some, but not all, ordered quantities have been confirmed delivered.
- **A-034:** Shipment quantities remain unchanged when delivery is partial or unsuccessful.
- **A-035:** Authorized Managers can review Delivery history and discrepancies.
- **A-036:** Finalized Delivery records cannot be silently modified through ordinary Driver operations.
- **A-037:** Delivery confirmation is recorded electronically.
- **A-038:** Physical truck loading, route navigation, and driving are outside Feature 15.
- **A-039:** Delivery Route information is available before Shipments are assigned.
- **A-040:** Feature 18 consumes preserved delivery discrepancy information for reporting.

**[NEEDS CLARIFICATION]** Confirm which feature owns Delivery Route maintenance and how routes are assigned to Drivers.

**[NEEDS CLARIFICATION]** Confirm whether delivery confirmation requires a Customer signature, recipient name, photograph, or other proof of delivery. These are not specified in the original requirements.

**[NEEDS CLARIFICATION]** Confirm whether Drivers must have continuous connectivity or whether offline delivery recording is required.

---

## Edge Cases

### EC-15.1: Driver Has No Assigned Deliveries

**Condition:** An authenticated Driver opens the delivery process without eligible assigned Shipments.

**Expected Behavior:**
- The system displays that no Deliveries are assigned.
- No Delivery record is finalized.
- No quantities are modified.

### EC-15.2: Shipment Not Ready for Delivery

**Condition:** A Driver attempts to record delivery for a Shipment in Preparing, Canceled, or another unready status.

**Expected Behavior:**
- The system rejects delivery confirmation.
- The Shipment remains unchanged.
- No cumulative Quantity Delivered update occurs.

### EC-15.3: Shipment Assigned to Another Driver

**Condition:** Driver B attempts to confirm a Shipment assigned to Driver A.

**Expected Behavior:**
- The system denies the operation unless authorized reassignment has occurred.
- Delivery quantities remain unchanged.
- The existing assignment remains preserved.

### EC-15.4: Duplicate Active Delivery Assignment

**Condition:** A Supervisor attempts to assign a Shipment that already has an active Delivery Assignment.

**Expected Behavior:**
- The system rejects the duplicate active assignment.
- The original assignment remains valid.
- No additional active Delivery is created for the same Shipment.

### EC-15.5: Nonexistent Shipment

**Condition:** A Driver or Supervisor references a Shipment that does not exist.

**Expected Behavior:**
- The system rejects the request.
- No Delivery record is created.
- No delivery quantities are modified.

### EC-15.6: Nonexistent Delivery

**Condition:** A Driver attempts to update a Delivery record that does not exist.

**Expected Behavior:**
- The system reports that the Delivery was not found.
- No cumulative Quantity Delivered update occurs.

### EC-15.7: Negative Quantity Delivered

**Condition:** A Driver enters a negative delivered quantity.

**Expected Behavior:**
- The system rejects the quantity.
- No Delivery Line update is accepted.
- Cumulative Quantity Delivered remains unchanged.

### EC-15.8: Non-Integer Quantity Delivered

**Condition:** A Driver enters a fractional delivered quantity.

**Expected Behavior:**
- The system rejects the value.
- The Driver is informed that delivery quantities must be whole units.
- No cumulative quantity is updated.

### EC-15.9: Zero Quantity Delivered for an Item

**Condition:** A Customer receives none of an Item included in the Shipment.

**Expected Behavior:**
- The system permits zero Quantity Delivered for that Delivery Line.
- The undelivered quantity remains preserved.
- A discrepancy is recorded when required.
- The Shipment's Quantity Shipped remains unchanged.

### EC-15.10: Apparent Over-Delivery

**Condition:** A Driver reports that the Customer received more units than the remaining undelivered quantity on a Shipment Line.

**Expected Behavior:**
- The system prevents ordinary confirmation of the excess quantity.
- An apparent over-delivery exception is recorded.
- The issue is made available for Supervisor review.
- Quantity Shipped and cumulative Quantity Delivered are not silently increased.

### EC-15.11: Partial Delivery

**Condition:** A Customer receives some, but not all, shipped quantities during a delivery attempt.

**Expected Behavior:**
- The system records actual quantities delivered.
- The Delivery is marked Partially Delivered when finalized.
- Outstanding quantities are preserved.
- Relevant discrepancies are recorded.
- A follow-up attempt may be arranged through authorized reassignment.

### EC-15.12: Failed Delivery Attempt

**Condition:** A Customer cannot receive any products.

**Expected Behavior:**
- The Driver records an unsuccessful attempt and a reason.
- The Delivery is marked Failed Attempt.
- Zero units are recorded as delivered for that attempt.
- The Shipment remains available for authorized follow-up.

### EC-15.13: Missing Failure Reason

**Condition:** A Driver attempts to finalize a Failed Attempt without entering a reason.

**Expected Behavior:**
- The system rejects finalization.
- The Driver is prompted to provide a reason.
- No failed attempt is finalized without the required information.

### EC-15.14: Duplicate Delivery Finalization

**Condition:** A Driver submits a delivery outcome that has already been finalized.

**Expected Behavior:**
- The system rejects the duplicate finalization.
- Cumulative Quantity Delivered is not increased again.
- The original Delivery history remains unchanged.

### EC-15.15: Follow-Up Delivery Attempt

**Condition:** A Shipment has undelivered quantities remaining after a previous finalized attempt.

**Expected Behavior:**
- An authorized Supervisor or Manager can arrange another Delivery Assignment.
- The new attempt references the original Shipment.
- The new attempt is limited to the remaining undelivered quantities.
- Previous Delivery history remains preserved.

### EC-15.16: Attempt to Deliver Already Delivered Units

**Condition:** A Driver attempts to confirm quantities already recorded as delivered during a previous attempt.

**Expected Behavior:**
- The system calculates the remaining undelivered quantity.
- The system rejects confirmation exceeding that remaining quantity.
- Previously delivered quantities are not counted again.

### EC-15.17: Delivery Discrepancy Resolved Later

**Condition:** A later Delivery Attempt confirms quantities missing from an earlier attempt.

**Expected Behavior:**
- Cumulative Quantity Delivered is updated using the newly confirmed quantities.
- The original discrepancy remains preserved.
- The previous attempt's outcome and history are not overwritten.

### EC-15.18: Customer Order Not Fully Delivered

**Condition:** At least one ordered unit remains undelivered.

**Expected Behavior:**
- The system does not mark the Customer Order fully Delivered.
- If at least one unit has been delivered, the order is marked Partially Delivered.
- Outstanding quantities remain identifiable.

### EC-15.19: Customer Order Fully Delivered

**Condition:** All ordered quantities have been confirmed delivered across completed delivery attempts.

**Expected Behavior:**
- The system marks the Customer Order Delivered.
- Quantity Ordered, Quantity Picked, and Quantity Shipped remain preserved.
- Delivery history remains available.

### EC-15.20: Unauthorized Delivery Administration

**Condition:** A Driver attempts to assign or reassign Shipments without administrative permission.

**Expected Behavior:**
- The system denies the operation.
- Existing Delivery Assignments remain unchanged.
- No delivery quantities are modified.

### EC-15.21: Attempt to Modify Finalized Delivery

**Condition:** A Driver attempts to change delivered quantities after the Delivery has been finalized.

**Expected Behavior:**
- The system rejects ordinary modification.
- The finalized Delivery remains preserved.
- **[NEEDS CLARIFICATION]** Confirm the approved administrative correction or reversal process.

### EC-15.22: Concurrent Delivery Confirmation

**Condition:** Two requests attempt to finalize the same Delivery or confirm overlapping remaining quantities.

**Expected Behavior:**
- The system prevents duplicate finalization.
- Cumulative Quantity Delivered is updated at most once per finalized confirmation.
- Remaining undelivered quantities cannot become negative.

**[NEEDS CLARIFICATION]** Confirm the approved transaction and concurrency control strategy.

### EC-15.23: Connection Failure During Delivery Confirmation

**Condition:** A Driver loses connectivity while submitting a delivery outcome.

**Expected Behavior:**
- The system preserves any successfully committed delivery result.
- A repeated submission cannot duplicate cumulative Quantity Delivered.
- The Driver can retrieve the current Delivery status after reconnection.

**[NEEDS CLARIFICATION]** Confirm whether offline delivery recording and later synchronization are required.

### EC-15.24: Shipment With Multiple Delivery Attempts

**Condition:** A Shipment has a Failed Attempt or Partially Delivered attempt followed by another authorized attempt.

**Expected Behavior:**
- Each attempt has a separate Delivery record.
- Each Delivery references the original Shipment.
- Each attempt preserves its own Driver, route, quantities, status, and timestamps.
- Cumulative Quantity Delivered reflects finalized attempts without duplication.

### EC-15.25: Incorrect or Incomplete Delivery Address

**Condition:** A Driver identifies a problem with the Customer delivery address.

**Expected Behavior:**
- The Driver can report the issue through the appropriate exception or unsuccessful delivery process.
- Customer master data is not silently changed.
- The Shipment and Delivery history remain preserved.

**[NEEDS CLARIFICATION]** Confirm which authorized role and feature correct Customer delivery addresses.

### EC-15.26: Delivery Route Becomes Inactive

**Condition:** A Delivery Route is deactivated while a Shipment is assigned to it.

**Expected Behavior:**
- Existing Delivery history remains preserved.
- New assignments to the inactive route are prevented under the proposed design.
- **[NEEDS CLARIFICATION]** Confirm whether existing active assignments must be reassigned automatically or manually.

---

## Success Criteria

- **SC-001:** Authenticated Drivers can view eligible Shipments assigned to their Delivery Routes.
- **SC-002:** Assigned Deliveries display Customer Order Number, Shipment Number, Customer, delivery address, and shipped Items.
- **SC-003:** Drivers can view Quantity Shipped for each Shipment Line.
- **SC-004:** Only Shipments Ready for Delivery can enter ordinary delivery confirmation.
- **SC-005:** Drivers cannot confirm Deliveries assigned to other Drivers without authorized reassignment.
- **SC-006:** Authorized Shipping Supervisors or Managers can assign eligible Shipments to Delivery Routes.
- **SC-007:** A Shipment cannot have multiple active Delivery Assignments.
- **SC-008:** Every Delivery references its Shipment, Driver, and Delivery Route.
- **SC-009:** Drivers can record actual Quantity Delivered for each Shipment Line.
- **SC-010:** Quantity Delivered is recorded in individual units.
- **SC-011:** Zero Quantity Delivered is accepted when a Customer receives none of an Item.
- **SC-012:** Negative and non-integer Quantity Delivered values are rejected.
- **SC-013:** Quantity Delivered cannot exceed the remaining undelivered quantity of its Shipment Line.
- **SC-014:** Apparent over-deliveries are reported for Supervisor review without silently changing quantities.
- **SC-015:** Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered remain separately preserved.
- **SC-016:** The system identifies and records differences between Quantity Shipped and Quantity Delivered.
- **SC-017:** Delivery discrepancies preserve relevant Item, Shipment, Customer Order, quantities, and reasons.
- **SC-018:** Delivery discrepancies remain available for Feature 18 reporting.
- **SC-019:** Delivery statuses are maintained as Assigned, In Progress, Partially Delivered, Delivered, and Failed Attempt.
- **SC-020:** New Deliveries begin in Assigned status.
- **SC-021:** Starting delivery confirmation changes the Delivery status to In Progress.
- **SC-022:** Fully delivered Shipments produce a Delivered outcome.
- **SC-023:** Partially completed delivery attempts produce a Partially Delivered outcome.
- **SC-024:** Unsuccessful delivery attempts produce a Failed Attempt outcome and require a reason.
- **SC-025:** Finalized delivery outcomes record the Driver and completion timestamp.
- **SC-026:** Finalized Deliveries update cumulative Quantity Delivered on Customer Order Lines.
- **SC-027:** Duplicate delivery confirmation cannot increase cumulative Quantity Delivered more than once.
- **SC-028:** Undelivered quantities remain available for authorized follow-up.
- **SC-029:** Authorized reassignment supports additional delivery attempts for remaining quantities.
- **SC-030:** Previous delivery attempts remain preserved when follow-up attempts occur.
- **SC-031:** Customer Orders become Delivered only when all ordered quantities are confirmed delivered.
- **SC-032:** Customer Orders become Partially Delivered when some, but not all, ordered quantities are confirmed delivered.
- **SC-033:** Shipping quantities remain unchanged during delivery confirmation.
- **SC-034:** Authorized Managers can review Delivery records and discrepancy history.
- **SC-035:** Finalized Delivery records cannot be silently modified by ordinary Driver operations.
- **SC-036:** Unauthorized delivery administration operations are rejected.
- **SC-037:** Nonexistent Shipments and Deliveries are rejected.
- **SC-038:** Delivery confirmation remains separate from truck loading, route navigation, and driving.
- **SC-039:** Delivery discrepancy history remains preserved after later resolution.
- **SC-040:** All 25 original Gherkin Acceptance Criteria have corresponding verification tests.

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

## Gherkin Acceptance Criteria

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

---

## Data Ownership

### Feature 15 — Deliver Customer Orders

Feature 15 owns the delivery confirmation process, including Delivery records, Delivery Lines, Delivery Assignments, delivery outcomes, and Delivery Discrepancies.

**Owned Data:**
- Delivery
- Delivery Line
- Delivery Assignment
- Delivery status
- Delivery Assignment status
- Actual Quantity Delivered per Delivery Line
- Delivery start timestamp
- Delivery completion timestamp
- Delivery failure reason
- Delivery Discrepancy
- Discrepancy type
- Discrepancy quantity difference
- Discrepancy reason and status
- Delivery attempt history
- Delivery Assignment history

**Responsibilities:**
- Identify eligible Shipments assigned to Drivers.
- Support assignment of eligible Shipments to Delivery Routes.
- Associate Deliveries with Shipments, Drivers, and Delivery Routes.
- Prevent multiple active Delivery Assignments for one Shipment.
- Allow authorized Drivers to record delivery outcomes.
- Record actual Quantity Delivered for each Shipment Line.
- Compare Quantity Delivered with Quantity Shipped.
- Record shortages and apparent over-delivery exceptions.
- Preserve delivery discrepancy information.
- Maintain Delivery statuses.
- Record the responsible Driver and completion timestamp.
- Update cumulative Quantity Delivered through the approved Customer Order interface.
- Prevent duplicate delivery finalization.
- Preserve outstanding undelivered quantities.
- Support authorized reassignment and additional delivery attempts.
- Preserve previous delivery attempts.
- Coordinate Customer Order delivery status updates.
- Make discrepancy information available to Feature 18.
- Preserve completed and unsuccessful Delivery history.

### Delivery Route Ownership

**Referenced Data:**
- Delivery Route ID
- Route Code
- Route Name
- Active status

**Feature 15 Responsibilities:**
- Reference existing Delivery Routes.
- Associate Shipments and Drivers with Delivery Routes.
- Prevent invalid or unauthorized Delivery Assignments.
- Preserve route references in Delivery history.

**[NEEDS CLARIFICATION]** Confirm which feature owns Delivery Route creation, maintenance, activation, and deactivation.

Feature 15 owns the Delivery Assignment relationship described in its requirements, but the ownership of Delivery Route master data remains unresolved.

### Feature 14 — Ship Customer Orders

**Owned Data:**
- Shipment
- Shipment Number
- Shipment Line
- Shipment status
- Quantity Shipped
- Shipment verification and preparation records

**Feature 15 Responsibilities:**
- Retrieve Shipments marked Ready for Delivery.
- Retrieve Shipment Lines and Quantity Shipped.
- Reject Shipments not eligible for delivery.
- Preserve Shipment and Shipment Line references.
- Never silently modify Quantity Shipped.
- Calculate remaining undelivered quantities using confirmed Delivery history.
- Preserve the relationship between Deliveries and their original Shipments.

### Feature 12 — Receive Customer Orders

**Owned Data:**
- Customer Order
- Customer Order Line
- Customer Order Number
- Quantity Ordered
- Customer Order information

**Feature 15 Responsibilities:**
- Retrieve Customer Order information through Shipment references.
- Preserve Quantity Ordered.
- Coordinate cumulative Quantity Delivered updates.
- Coordinate Customer Order status changes to Delivered or Partially Delivered.
- Never modify original Quantity Ordered during delivery confirmation.

### Feature 13 — Pick Customer Orders

**Referenced Data:**
- Quantity Picked
- Picking history

**Feature 15 Responsibilities:**
- Preserve Quantity Picked.
- Keep delivery confirmation separate from picking.
- Never create or modify Picking Movements during ordinary delivery confirmation.

### Feature 6 — Customer Maintenance

**Owned Data:**
- Customer ID
- Customer Number
- Customer name
- Customer delivery address
- Other Customer master information

**Feature 15 Responsibilities:**
- Retrieve Customer information for assigned Deliveries.
- Display the Customer and delivery address.
- Preserve the Customer association in Delivery history.
- Never silently change Customer master data.

### Individual Item Maintenance

**Owned Data:**
- Individual Item ID
- Item Number
- Item description

**Feature 15 Responsibilities:**
- Retrieve Item information for Delivery Lines.
- Display shipped Items to Drivers.
- Preserve Item references in Delivery history.
- Never modify Item master data.

### Shared User and Authorization Services

**Owned Data:**
- User ID
- User role
- Authentication information
- Authorization permissions

**Feature 15 Responsibilities:**
- Authenticate Drivers before allowing delivery recording.
- Restrict delivery confirmation to the assigned Driver or authorized personnel.
- Restrict assignment administration to Shipping Supervisors and Managers.
- Record the Driver responsible for each finalized Delivery.
- Restrict history access to authorized Users.
- Reject unauthorized operations.

### Feature 18 — Delivery Discrepancy Reporting

**Referenced Data:**
- Delivery
- Delivery Line
- Delivery Discrepancy
- Shipment
- Customer Order
- Quantity Shipped
- Quantity Delivered
- Quantity Difference
- Discrepancy status

**Feature 15 Responsibilities:**
- Record delivery discrepancies.
- Preserve the original reported difference.
- Preserve discrepancies after later resolution.
- Make discrepancy information available to Feature 18.
- Keep reporting separate from delivery confirmation.

### Cross-Feature Data Rules

- Feature 15 owns Delivery records, Delivery Lines, Delivery Assignments, and Delivery Discrepancies.
- Feature 14 owns Shipment preparation and Quantity Shipped.
- Feature 12 owns Customer Orders and original Quantity Ordered.
- Feature 13 owns picking operations.
- Feature 6 owns Customer master data.
- Delivery Route master-data ownership requires clarification.
- Each Delivery references one Shipment.
- Each Delivery references one Delivery Assignment.
- Each Delivery is associated with one Driver and one Delivery Route.
- A Shipment may have multiple historical Delivery attempts.
- A Shipment may have only one active Delivery Assignment at a time.
- Quantity Delivered is recorded in individual units.
- Quantity Delivered cannot be negative.
- Confirmed Quantity Delivered cannot exceed remaining undelivered Shipment quantities.
- Finalized Delivery Lines contribute to cumulative Quantity Delivered.
- The same finalized Delivery cannot increase cumulative Quantity Delivered more than once.
- Quantity Shipped remains unchanged during ordinary delivery confirmation.
- Quantity Ordered and Quantity Picked remain unchanged.
- Previous Delivery attempts remain preserved.
- Delivery Discrepancies remain preserved after resolution.
- Customer Order delivery status is based on confirmed cumulative Quantity Delivered.

**[NEEDS CLARIFICATION]** Confirm the exact interface for updating Customer Order Line Quantity Delivered and Customer Order status.

**[NEEDS CLARIFICATION]** Confirm the ownership and administration of Delivery Route master data.

**[NEEDS CLARIFICATION]** Confirm how corrected or reversed delivery confirmations are authorized and recorded.

---

## API Requirements

The following API endpoints are proposed for the Feature 15 design draft. Final route names and service boundaries require architecture approval.

### API-15.1: Retrieve Assigned Deliveries

**Endpoint:** `GET /api/deliveries/assigned`

**Purpose:** Display eligible Deliveries assigned to the authenticated Driver.

**Authorized Roles:**
- Driver
- Shipping Supervisor
- Manager with approved access

**Response Data:**
- Delivery ID
- Shipment ID
- Shipment Number
- Customer Order Number
- Customer
- Delivery address
- Delivery Route
- Assigned Driver
- Delivery status
- Shipped Items
- Quantity Shipped
- Remaining undelivered quantities

**Validation and Behavior:**
- Require authentication.
- Restrict Driver results to their assigned Deliveries.
- Include eligible Shipments that have completed shipping.
- Exclude Shipments not Ready for Delivery.
- Display a clear empty result when no Deliveries are assigned.
- Do not modify delivery quantities.

**Error Conditions:**
- Unauthorized access
- Invalid request parameters

### API-15.2: Create Delivery Assignment

**Endpoint:** `POST /api/delivery-assignments`

**Purpose:** Assign an eligible Shipment to a Driver and Delivery Route.

**Authorized Roles:**
- Shipping Supervisor
- Manager

**Request Data:**
- shipmentId
- deliveryRouteId
- driverId

**System-Generated Data:**
- deliveryAssignmentId
- assignedAt
- status = Active

**Validation and Behavior:**
- Confirm the Shipment exists.
- Confirm the Shipment is Ready for Delivery.
- Confirm the Delivery Route exists.
- Confirm the Driver is authorized.
- Reject duplicate active assignments for the same Shipment.
- Preserve the Shipment association.
- Create an Assigned Delivery for the new attempt.
- Preserve previous attempts and assignments when applicable.
- Limit follow-up attempts to remaining undelivered quantities.

**Successful Response:**
- Delivery Assignment ID
- Delivery ID
- Shipment Number
- Delivery Route
- Assigned Driver
- Assignment status
- Delivery status

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Shipment not Ready for Delivery
- Delivery Route not found
- Invalid Driver
- Duplicate active assignment
- No remaining quantity eligible for follow-up

### API-15.3: Retrieve Delivery Details

**Endpoint:** `GET /api/deliveries/{deliveryId}`

**Purpose:** Retrieve a Delivery and its associated Shipment information.

**Authorized Roles:**
- Assigned Driver
- Shipping Supervisor
- Manager with approved access

**Response Data:**
- Delivery ID
- Shipment Number
- Customer Order Number
- Customer
- Delivery address
- Assigned Driver
- Delivery Route
- Delivery status
- Delivery Lines
- Item Number
- Item description
- Quantity Shipped
- Quantity previously delivered
- Remaining undelivered quantity
- Quantity Delivered for the current attempt
- Delivery discrepancies
- Delivery timestamps

**Validation and Behavior:**
- Confirm the Delivery exists.
- Confirm the User has permission to view it.
- Preserve Shipment and Customer Order associations.
- Return current Delivery information.
- Do not modify quantities.

**Error Conditions:**
- Delivery not found
- Unauthorized access

### API-15.4: Start Delivery

**Endpoint:** `POST /api/deliveries/{deliveryId}/start`

**Purpose:** Begin recording an assigned Delivery.

**Authorized Roles:**
- Assigned Driver
- Authorized Supervisor or Manager

**Validation and Behavior:**
- Confirm the Delivery exists.
- Confirm the Shipment is eligible for delivery.
- Confirm the assignment is active.
- Confirm the User is authorized.
- Require Delivery status Assigned.
- Change Delivery status to In Progress.
- Record the start timestamp.
- Preserve the Shipment association.

**Successful Response:**
- Delivery ID
- Updated status
- Start timestamp

**Error Conditions:**
- Unauthorized user
- Delivery not found
- Invalid Delivery status
- Inactive assignment
- Shipment not eligible

### API-15.5: Record Quantity Delivered

**Endpoint:** `PUT /api/deliveries/{deliveryId}/lines/{deliveryLineId}`

**Purpose:** Record actual Quantity Delivered for a Shipment Line during the current attempt.

**Authorized Roles:**
- Assigned Driver
- Authorized Supervisor or Manager

**Request Data:**
- quantityDelivered

**Validation and Behavior:**
- Confirm the Delivery exists.
- Confirm the Delivery Line exists.
- Confirm the Delivery is In Progress.
- Confirm the User is authorized.
- Require a nonnegative whole-number quantity.
- Allow zero Quantity Delivered.
- Prevent confirmation exceeding remaining undelivered quantity.
- Preserve original Quantity Shipped.
- Preserve Quantity Ordered and Quantity Picked.
- Identify potential delivery shortages.
- Do not increase cumulative Quantity Delivered until the attempt is finalized.

**Successful Response:**
- Delivery Line ID
- Quantity Shipped
- Quantity Delivered for current attempt
- Remaining undelivered quantity
- Validation result

**Error Conditions:**
- Unauthorized user
- Delivery not found
- Delivery Line not found
- Invalid Delivery status
- Negative quantity
- Non-integer quantity
- Quantity exceeds remaining undelivered amount

### API-15.6: Report Delivery Discrepancy

**Endpoint:** `POST /api/deliveries/{deliveryId}/discrepancies`

**Purpose:** Record a delivery shortage, apparent over-delivery, or failed delivery issue.

**Authorized Roles:**
- Assigned Driver
- Shipping Supervisor
- Manager

**Request Data:**
- deliveryLineId, when applicable
- discrepancyType
- quantityDifference
- reason

**Validation and Behavior:**
- Confirm the Delivery exists.
- Validate the discrepancy type.
- Validate the related Delivery Line when supplied.
- Preserve the original reported quantities.
- Record the discrepancy reason.
- Record the report timestamp.
- Initialize discrepancy status as Open.
- Prevent apparent over-deliveries from silently changing confirmed quantities.
- Make discrepancy information available for Supervisor review and Feature 18 reporting.

**Successful Response:**
- Delivery Discrepancy ID
- Discrepancy type
- Quantity difference
- Reason
- Discrepancy status
- Report timestamp

**Error Conditions:**
- Unauthorized user
- Delivery not found
- Invalid discrepancy type
- Invalid Delivery Line
- Invalid quantity difference

### API-15.7: Finalize Delivery

**Endpoint:** `POST /api/deliveries/{deliveryId}/finalize`

**Purpose:** Finalize a successful, partial, or unsuccessful delivery attempt.

**Authorized Roles:**
- Assigned Driver
- Authorized Supervisor or Manager

**Request Data:**
- Final delivery outcome
- Failure reason, when applicable

**Validation and Behavior:**
- Confirm the Delivery exists.
- Confirm the Delivery is In Progress.
- Confirm the User is authorized.
- Validate actual Quantity Delivered for each Delivery Line.
- Reject quantities exceeding remaining undelivered amounts.
- Require a failure reason when no products were delivered and the attempt is unsuccessful.
- Mark the Delivery as Delivered when all remaining Shipment quantities are confirmed received.
- Mark the Delivery as Partially Delivered when some, but not all, remaining Shipment quantities are confirmed received.
- Mark the Delivery as Failed Attempt when no products are delivered.
- Record the responsible Driver.
- Record the completion timestamp.
- Update cumulative Quantity Delivered on Customer Order Lines.
- Apply the cumulative quantity update exactly once.
- Preserve outstanding quantities.
- Preserve original Quantity Shipped.
- Record applicable discrepancies.
- Update Customer Order delivery status when appropriate.
- Preserve the finalized Delivery record.
- Prevent duplicate finalization.

**Successful Response:**
- Delivery ID
- Final Delivery status
- Confirmed Quantity Delivered
- Remaining undelivered quantities
- Updated Customer Order status
- Driver
- Completion timestamp

**Error Conditions:**
- Unauthorized user
- Delivery not found
- Invalid Delivery status
- Invalid quantities
- Missing failure reason
- Duplicate finalization
- Concurrent quantity conflict

**[NEEDS CLARIFICATION]** Confirm the precise handling of a follow-up attempt that completes all remaining quantities after an earlier partial delivery. The original requirements support cumulative delivery completion, but the distinction between the current attempt's outcome and the overall Shipment outcome should be approved.

### API-15.8: Retrieve Remaining Undelivered Quantities

**Endpoint:** `GET /api/shipments/{shipmentId}/remaining-delivery`

**Purpose:** Identify Shipment quantities still requiring delivery.

**Authorized Roles:**
- Assigned Driver with approved access
- Shipping Supervisor
- Manager

**Response Data:**
- Shipment Number
- Shipment Lines
- Quantity Shipped
- Cumulative Quantity Delivered
- Remaining Undelivered Quantity
- Previous Delivery attempts

**Validation and Behavior:**
- Confirm the Shipment exists.
- Calculate cumulative delivered quantities from finalized Delivery Lines.
- Prevent duplicate counting.
- Return the remaining quantities for each Shipment Line.
- Preserve original Shipment quantities.

**Error Conditions:**
- Unauthorized access
- Shipment not found

### API-15.9: Reassign Undelivered Shipment

**Endpoint:** `POST /api/shipments/{shipmentId}/delivery-reassignment`

**Purpose:** Authorize a new delivery attempt for remaining undelivered quantities.

**Authorized Roles:**
- Shipping Supervisor
- Manager

**Request Data:**
- deliveryRouteId
- driverId

**Validation and Behavior:**
- Confirm the Shipment exists.
- Confirm undelivered quantities remain.
- Confirm no conflicting active Delivery Assignment exists.
- Confirm the new Driver and Delivery Route are valid.
- Preserve earlier Delivery records.
- Preserve previous Delivery Assignment history.
- Create a new active Delivery Assignment.
- Create a new Delivery attempt in Assigned status.
- Limit the new attempt to outstanding quantities.

**Successful Response:**
- New Delivery Assignment ID
- New Delivery ID
- Shipment Number
- Assigned Driver
- Delivery Route
- Remaining quantities
- Assignment status

**Error Conditions:**
- Unauthorized user
- Shipment not found
- No remaining undelivered quantities
- Invalid Driver
- Invalid Delivery Route
- Conflicting active assignment

### API-15.10: Retrieve Delivery History

**Endpoint:** `GET /api/deliveries/history`

**Purpose:** Allow authorized personnel to review completed and unsuccessful Deliveries.

**Authorized Roles:**
- Shipping Supervisor
- Manager

**Optional Filters:**
- Shipment
- Customer Order
- Driver
- Delivery Route
- Delivery status
- Date range

**Response Data:**
- Delivery ID
- Shipment Number
- Customer Order Number
- Customer
- Driver
- Delivery Route
- Delivery status
- Delivery Lines
- Quantity Shipped
- Quantity Delivered
- Discrepancies
- Failure reason
- Start timestamp
- Completion timestamp

**Validation and Behavior:**
- Restrict access to authorized Users.
- Preserve historical delivery attempts.
- Include successful, partial, and failed outcomes.
- Do not silently modify finalized Delivery records.

**Error Conditions:**
- Unauthorized access
- Invalid filters

### API-15.11: Retrieve Delivery Discrepancies

**Endpoint:** `GET /api/delivery-discrepancies`

**Purpose:** Retrieve delivery discrepancies for Supervisor review and Feature 18 reporting.

**Authorized Roles:**
- Shipping Supervisor
- Manager
- Authorized reporting service

**Optional Filters:**
- Shipment
- Customer Order
- Driver
- Discrepancy type
- Discrepancy status

**Response Data:**
- Delivery Discrepancy ID
- Delivery ID
- Shipment Number
- Customer Order Number
- Item
- Quantity Shipped
- Quantity Delivered
- Quantity difference
- Reason
- Report timestamp
- Resolution status

**Validation and Behavior:**
- Return recorded discrepancies.
- Preserve original reported differences.
- Include resolved discrepancies in historical reporting.
- Do not automatically overwrite discrepancies when later delivery attempts resolve outstanding quantities.

**Error Conditions:**
- Unauthorized access
- Invalid filters

### API-15.12: Review or Resolve Delivery Discrepancy

**Endpoint:** `PATCH /api/delivery-discrepancies/{discrepancyId}`

**Purpose:** Allow authorized personnel to review and resolve a delivery discrepancy.

**Authorized Roles:**
- Shipping Supervisor
- Manager

**Request Data:**
- status
- resolution information

**Validation and Behavior:**
- Confirm the discrepancy exists.
- Verify authorization.
- Preserve the original discrepancy.
- Record the resolution decision.
- Prevent ordinary Driver operations from silently changing the discrepancy.
- Preserve the discrepancy for Feature 18 reporting.

**Successful Response:**
- Delivery Discrepancy ID
- Updated resolution status
- Resolution information

**Error Conditions:**
- Unauthorized user
- Discrepancy not found
- Invalid resolution

**[NEEDS CLARIFICATION]** Confirm the approved process for correcting quantities after a Supervisor reviews an apparent over-delivery.

### General API Requirements

- All write operations MUST enforce server-side authorization.
- Drivers MUST be restricted to their assigned Deliveries.
- Supervisors and Managers MUST have appropriate administrative permissions.
- Initial Delivery Assignments MUST reference Shipments Ready for Delivery.
- The same Shipment MUST NOT have multiple active Delivery Assignments.
- Every Delivery MUST reference a valid Shipment, Driver, and Delivery Route.
- Delivery Lines MUST reference valid Shipment Lines.
- Quantity Delivered MUST be a nonnegative integer.
- Zero Quantity Delivered MUST be supported.
- Confirmed Quantity Delivered MUST NOT exceed remaining undelivered quantities.
- Quantity Shipped MUST remain unchanged during ordinary delivery confirmation.
- Quantity Ordered and Quantity Picked MUST remain unchanged.
- Delivery statuses MUST follow the approved lifecycle.
- Finalized Delivery outcomes MUST record the responsible Driver and completion timestamp.
- Failed Attempts MUST require a reason.
- Finalization MUST update cumulative Quantity Delivered consistently.
- Duplicate finalization MUST NOT increase cumulative Quantity Delivered again.
- Outstanding quantities MUST remain available for authorized follow-up.
- Historical Delivery attempts MUST remain preserved.
- Discrepancies MUST remain preserved after resolution.
- Customer Order delivery status MUST reflect cumulative confirmed quantities.
- Delivery confirmation MUST remain separate from truck loading and route navigation.

**[NEEDS CLARIFICATION]** Confirm final API naming conventions, transaction boundaries, concurrency controls, and audit requirements.

---

## Screen Requirements

### SCREEN-15.1: Assigned Deliveries

**Purpose:** Allow Drivers to view Shipments assigned to their Delivery Routes.

**Authorized Users:**
- Driver
- Shipping Supervisor
- Manager with approved access

**Displayed Information:**
- Shipment Number
- Customer Order Number
- Customer name
- Delivery address
- Delivery Route
- Delivery status
- Shipped Items
- Quantity Shipped

**Controls:**
- View Assigned Deliveries
- Select Delivery
- Refresh List

**Behavior:**
- Display only eligible assigned Deliveries for ordinary Driver access.
- Exclude unready Shipments.
- Show a clear message when no Deliveries are assigned.
- Prevent Drivers from selecting another Driver's assignment without authorization.

### SCREEN-15.2: Delivery Details

**Purpose:** Display the selected Shipment and delivery information.

**Authorized Users:**
- Assigned Driver
- Shipping Supervisor
- Manager with approved access

**Displayed Information:**
- Delivery ID
- Shipment Number
- Customer Order Number
- Customer
- Delivery address
- Delivery Route
- Assigned Driver
- Delivery status
- Item Number
- Item description
- Quantity Shipped
- Remaining undelivered quantities

**Controls:**
- Start Delivery
- View Shipment Lines
- View Previous Attempts
- Return to Assigned Deliveries

**Behavior:**
- Display the correct Shipment and Customer information.
- Preserve Quantity Shipped.
- Prevent delivery recording for unready Shipments.
- Require authorization before starting the Delivery.

### SCREEN-15.3: Record Quantity Delivered

**Purpose:** Allow the assigned Driver to record actual quantities received by the Customer.

**Authorized Users:**
- Assigned Driver
- Authorized Supervisor or Manager

**Displayed Information:**
- Shipment Number
- Individual Item
- Quantity Shipped
- Previously delivered quantity
- Remaining undelivered quantity
- Quantity Delivered for the current attempt
- Quantity difference

**Controls:**
- Enter Quantity Delivered
- Save Quantity
- Report Discrepancy
- Continue Delivery

**Behavior:**
- Accept nonnegative whole-number quantities.
- Allow zero Quantity Delivered.
- Reject quantities exceeding remaining undelivered amounts.
- Preserve Quantity Shipped.
- Identify apparent shortages.
- Allow apparent over-delivery to be reported for Supervisor review.
- Do not silently increase cumulative Quantity Delivered before finalization.

### SCREEN-15.4: Delivery Discrepancy Entry

**Purpose:** Allow Drivers to record differences or problems identified during delivery.

**Authorized Users:**
- Assigned Driver
- Shipping Supervisor
- Manager

**Displayed Information:**
- Shipment Number
- Customer Order Number
- Item
- Quantity Shipped
- Quantity Delivered
- Quantity difference
- Discrepancy type
- Discrepancy status

**Controls:**
- Select Discrepancy Type
- Enter Reason
- Submit Discrepancy
- Return to Delivery

**Behavior:**
- Support Short Delivery, Apparent Over-Delivery, and Failed Delivery discrepancies.
- Preserve the reported issue.
- Prevent unauthorized quantity changes.
- Make discrepancies available for Supervisor review.
- Preserve discrepancy information for Feature 18.

### SCREEN-15.5: Delivery Outcome Confirmation

**Purpose:** Allow Drivers to finalize successful, partial, or unsuccessful delivery attempts.

**Authorized Users:**
- Assigned Driver
- Authorized Supervisor or Manager

**Displayed Information:**
- Delivery ID
- Shipment Number
- Customer Order Number
- Delivery Route
- Driver
- Shipped Items
- Quantity Shipped
- Quantity Delivered
- Outstanding quantities
- Delivery discrepancies
- Proposed Delivery status

**Controls:**
- Review Delivery
- Record Failure Reason
- Finalize Delivery
- Return to Quantity Entry

**Behavior:**
- Validate recorded quantities.
- Mark a fully delivered attempt Delivered.
- Mark a partial attempt Partially Delivered.
- Mark an unsuccessful attempt Failed Attempt.
- Require a reason for Failed Attempt.
- Record the responsible Driver and completion timestamp.
- Prevent duplicate finalization.
- Preserve outstanding quantities.
- Update cumulative Quantity Delivered.
- Update Customer Order status as appropriate.
- Preserve Shipment quantities.

### SCREEN-15.6: Delivery Assignment Administration

**Purpose:** Allow authorized Supervisors or Managers to assign Shipments to Drivers and Delivery Routes.

**Authorized Users:**
- Shipping Supervisor
- Manager

**Displayed Information:**
- Eligible Shipment Number
- Customer Order Number
- Customer
- Delivery address
- Delivery Route
- Assigned Driver
- Assignment status
- Remaining undelivered quantities

**Controls:**
- Select Shipment
- Select Delivery Route
- Select Driver
- Create Assignment
- Review Existing Assignment

**Behavior:**
- Allow assignment of eligible Shipments.
- Prevent duplicate active assignments.
- Require valid Driver and Delivery Route references.
- Preserve assignment history.
- Prevent ordinary Drivers from administering assignments.

### SCREEN-15.7: Delivery Reassignment

**Purpose:** Arrange another delivery attempt for outstanding quantities.

**Authorized Users:**
- Shipping Supervisor
- Manager

**Displayed Information:**
- Original Shipment Number
- Customer Order Number
- Previous Delivery attempts
- Previous Driver
- Previous Delivery Route
- Remaining undelivered quantities
- Current assignment status

**Controls:**
- Review Outstanding Quantities
- Select Driver
- Select Delivery Route
- Authorize Reassignment
- Return to Assignment List

**Behavior:**
- Require outstanding quantities.
- Preserve previous Delivery attempts.
- Prevent conflicting active assignments.
- Create a new Delivery Assignment and attempt.
- Limit the new attempt to remaining undelivered quantities.

### SCREEN-15.8: Delivery History

**Purpose:** Allow authorized Managers to review Delivery outcomes and historical records.

**Authorized Users:**
- Shipping Supervisor
- Manager

**Displayed Information:**
- Delivery ID
- Shipment Number
- Customer Order Number
- Customer
- Driver
- Delivery Route
- Delivery status
- Quantity Shipped
- Quantity Delivered
- Discrepancies
- Failure reason
- Delivery timestamps

**Controls:**
- Search Deliveries
- Filter by Driver
- Filter by Route
- Filter by Status
- View Delivery Details
- View Discrepancies

**Behavior:**
- Display completed, partially delivered, and unsuccessful attempts.
- Preserve previous Delivery records.
- Keep finalized records read-only through ordinary Driver operations.
- Restrict access according to role permissions.

### SCREEN-15.9: Delivery Discrepancy Review

**Purpose:** Allow authorized Supervisors or Managers to investigate delivery discrepancies.

**Authorized Users:**
- Shipping Supervisor
- Manager

**Displayed Information:**
- Delivery Discrepancy ID
- Shipment Number
- Customer Order Number
- Driver
- Item
- Quantity Shipped
- Quantity Delivered
- Quantity difference
- Discrepancy reason
- Report timestamp
- Resolution status

**Controls:**
- View Discrepancy
- View Delivery History
- Review Resolution
- Resolve Discrepancy, when authorized
- Refresh List

**Behavior:**
- Display open and resolved discrepancies.
- Preserve the original reported issue.
- Restrict resolution actions to authorized personnel.
- Prevent silent changes to finalized Delivery quantities.
- Keep discrepancy history available to Feature 18.

### General Screen Requirements

- Screens MUST follow the approved Warehouse System UI conventions.
- Delivery screens MUST identify the Shipment, Customer Order, and Customer.
- Drivers MUST see the delivery address and shipped Items.
- Quantity Shipped and Quantity Delivered MUST be clearly distinguishable.
- Previously delivered and remaining quantities MUST be visible when relevant.
- Quantity entry MUST reject invalid values.
- Zero delivered quantities MUST be supported.
- Apparent over-deliveries MUST be reported rather than silently accepted.
- Delivery status MUST remain visible.
- Failed Attempts MUST require a reason.
- Unresolved discrepancies MUST be identifiable.
- Unauthorized actions MUST be restricted.
- Finalized Delivery records MUST not be silently editable.
- Delivery history MUST remain available to authorized users.
- UI validation MUST be reinforced by server-side validation.
- Screen designs MUST be documented in Figma or the approved design tool before implementation.
- The interface SHOULD support practical electronic delivery recording on Driver devices.

**[NEEDS CLARIFICATION]** Confirm required Driver devices, connectivity expectations, and proof-of-delivery information.

---

## Definition of Done

Feature 15 is considered complete when all approved requirements and acceptance criteria have been implemented and verified.

### Requirements and Design

- [ ] All six User Stories are implemented.
- [ ] Functional Requirements FR-001 through FR-056 are satisfied.
- [ ] Assumptions and unresolved clarifications have been reviewed.
- [ ] Edge Cases have corresponding handling and verification.
- [ ] Success Criteria have been evaluated.
- [ ] Data ownership boundaries are documented and followed.
- [ ] Initial Data Model has been reviewed and approved.
- [ ] Delivery status rules are approved.
- [ ] Delivery Assignment and reassignment rules are approved.
- [ ] API contracts have been reviewed.
- [ ] Screen designs have been prepared and reviewed.

### Implementation

- [ ] Authenticated Drivers can view assigned Deliveries.
- [ ] Assigned Deliveries display Customer Orders, Shipments, Customers, addresses, and Items.
- [ ] Only Ready for Delivery Shipments can enter ordinary delivery confirmation.
- [ ] Drivers cannot confirm another Driver's Delivery without authorization.
- [ ] Supervisors or Managers can assign eligible Shipments.
- [ ] Duplicate active Delivery Assignments are prevented.
- [ ] Each Delivery references a valid Shipment, Driver, and Delivery Route.
- [ ] Drivers can start assigned Deliveries.
- [ ] New Deliveries begin in Assigned status.
- [ ] Started Deliveries change to In Progress.
- [ ] Drivers can record Quantity Delivered for each Shipment Line.
- [ ] Delivered quantities are recorded in individual units.
- [ ] Zero Quantity Delivered is supported.
- [ ] Negative and non-integer quantities are rejected.
- [ ] Delivered quantities cannot exceed remaining undelivered Shipment quantities.
- [ ] Apparent over-deliveries are reported for Supervisor review.
- [ ] Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered remain separate.
- [ ] Delivery shortages and discrepancies are recorded.
- [ ] Delivery discrepancies preserve the reported quantities and reasons.
- [ ] Successful delivery attempts can be finalized.
- [ ] Partial delivery attempts can be finalized.
- [ ] Failed Attempts can be finalized with a required reason.
- [ ] Delivery statuses are correctly maintained.
- [ ] Finalized outcomes record the responsible Driver and completion timestamp.
- [ ] Cumulative Quantity Delivered is updated after confirmed delivery.
- [ ] Duplicate finalization cannot update cumulative quantities twice.
- [ ] Outstanding quantities are preserved.
- [ ] Authorized reassignment supports follow-up delivery attempts.
- [ ] Follow-up attempts cannot exceed outstanding quantities.
- [ ] Previous delivery attempts remain preserved.
- [ ] Customer Orders become Delivered only when all ordered quantities are confirmed delivered.
- [ ] Customer Orders become Partially Delivered when some ordered quantities remain undelivered.
- [ ] Shipment quantities remain unchanged during delivery confirmation.
- [ ] Managers can retrieve Delivery history.
- [ ] Finalized Delivery records cannot be silently modified.
- [ ] Unauthorized operations are rejected.
- [ ] Nonexistent Shipments and Deliveries are rejected.
- [ ] Delivery Discrepancies remain available for Feature 18 reporting.
- [ ] Delivery Discrepancies remain preserved after resolution.
- [ ] Physical truck loading and route navigation remain outside delivery confirmation.

### Testing and Verification

- [ ] All 25 original Gherkin Acceptance Criteria have corresponding verification tests.
- [ ] Unit tests cover Delivery eligibility.
- [ ] Unit tests cover Driver assignment authorization.
- [ ] Unit tests cover duplicate active assignment prevention.
- [ ] Unit tests cover Delivery status transitions.
- [ ] Unit tests cover Quantity Delivered validation.
- [ ] Unit tests cover zero delivered quantities.
- [ ] Unit tests cover remaining undelivered quantity calculations.
- [ ] Unit tests cover delivery discrepancy calculations.
- [ ] Unit tests cover successful delivery outcomes.
- [ ] Unit tests cover partial delivery outcomes.
- [ ] Unit tests cover Failed Attempt outcomes.
- [ ] Unit tests cover Customer Order delivery status calculations.
- [ ] Unit tests cover duplicate finalization prevention.
- [ ] API tests verify successful Delivery operations.
- [ ] API tests verify unauthorized operations are rejected.
- [ ] API tests verify nonexistent records are rejected.
- [ ] API tests verify invalid quantities are rejected.
- [ ] API tests verify duplicate finalization is rejected.
- [ ] API tests verify reassignment rules.
- [ ] Integration tests verify Shipment eligibility from Feature 14.
- [ ] Integration tests verify Customer Order references from Feature 12.
- [ ] Integration tests verify Customer information from Feature 6.
- [ ] Integration tests verify cumulative Quantity Delivered updates.
- [ ] Integration tests verify Quantity Shipped remains unchanged.
- [ ] Integration tests verify Quantity Ordered and Quantity Picked remain unchanged.
- [ ] Integration tests verify delivery discrepancy reporting to Feature 18.
- [ ] Tests verify previous Delivery attempts remain preserved.
- [ ] Tests verify discrepancies remain preserved after resolution.
- [ ] Tests verify concurrent confirmation cannot count delivered units twice.
- [ ] Regression tests confirm existing Warehouse System features continue to operate correctly.

### Documentation and Review

- [ ] API documentation is updated.
- [ ] Data model documentation is updated.
- [ ] Screen documentation is updated.
- [ ] Driver delivery confirmation procedures are documented.
- [ ] Delivery Assignment procedures are documented.
- [ ] Reassignment procedures are documented.
- [ ] Delivery discrepancy procedures are documented.
- [ ] Delivery status transitions are documented.
- [ ] Role permissions are documented.
- [ ] Known limitations and approved deferrals are recorded.
- [ ] Code has been reviewed.
- [ ] Required tests pass.
- [ ] The feature is approved for integration.

---

## Out of Scope

The following activities are not implemented as part of Feature 15.

### Customer Order Entry

Creating Customer Orders, adding Customer Order Lines, and maintaining original Quantity Ordered belong to Feature 12.

Feature 15 references existing Customer Orders through completed Shipments.

### Customer Master Data Maintenance

Creating, editing, or deactivating Customers belongs to Feature 6.

Feature 15 displays Customer information and delivery addresses but does not maintain Customer master data.

### Individual Item Maintenance

Creating or modifying Individual Items is outside Feature 15.

Feature 15 uses existing Item information to identify delivered products.

### Picking Customer Orders

Generating picking instructions, assigning Pickers, verifying warehouse bins, and recording Picking Movements belong to Feature 13.

Feature 15 does not change Quantity Picked.

### Shipping Preparation

Creating Shipments, verifying products for shipping, recording Quantity Shipped, shrink-wrapping, and labeling belong to Feature 14.

Feature 15 processes Shipments that have already been marked Ready for Delivery.

### Physical Truck Loading

Physically loading products onto trucks and verifying truck loading are outside the delivery confirmation workflow.

Feature 15 does not perform physical loading operations.

### Route Navigation and Driving

GPS navigation, turn-by-turn directions, vehicle operation, and driving activities are outside Feature 15.

Feature 15 records Delivery Route references and outcomes without implementing navigation.

### Delivery Route Master Data Maintenance

Creating, editing, activating, or deactivating Delivery Routes is not defined as part of this feature's original requirements.

Feature 15 uses existing Delivery Routes for assignments.

**[NEEDS CLARIFICATION]** Confirm which feature owns Delivery Route maintenance.

### Advanced Transportation Planning

Automatic route optimization, traffic prediction, delivery time optimization, and vehicle scheduling are not included unless separately approved.

### Customer Billing and Payment Processing

Invoice generation, payment collection, and Customer billing adjustments are outside Feature 15.

### Delivery Discrepancy Reporting

Feature 15 records and preserves Delivery Discrepancies.

Formal discrepancy reports and broader analysis belong to Feature 18.

### Finalized Delivery Corrections

Feature 15 prevents ordinary Drivers from silently modifying finalized Delivery records.

A separate authorized correction or reversal process requires approval.

**[NEEDS CLARIFICATION]** Define the correction procedure and permitted roles.

### Proof of Delivery

Customer signatures, recipient identification, delivery photographs, and electronic proof-of-delivery documents are not specified in the original Feature 15 requirements.

**[NEEDS CLARIFICATION]** Confirm whether any of these are required.

### Offline Delivery Recording

Offline delivery confirmation and synchronization after reconnecting are not defined in the original requirements.

**[NEEDS CLARIFICATION]** Confirm whether Drivers must be able to record Deliveries without connectivity.

### Final Deferrals and Clarifications

The following decisions remain open for review:

- **[NEEDS CLARIFICATION]** Which feature owns Delivery Route master data.
- **[NEEDS CLARIFICATION]** How Delivery Routes are assigned to Drivers.
- **[NEEDS CLARIFICATION]** Whether a Delivery Route may have multiple assigned Drivers.
- **[NEEDS CLARIFICATION]** How active Delivery Assignments are closed after finalized attempts.
- **[NEEDS CLARIFICATION]** Whether existing assignments on inactive routes must be reassigned.
- **[NEEDS CLARIFICATION]** The exact interface for updating cumulative Quantity Delivered.
- **[NEEDS CLARIFICATION]** The interface for updating Customer Order delivery status.
- **[NEEDS CLARIFICATION]** The precise status semantics for follow-up attempts after partial delivery.
- **[NEEDS CLARIFICATION]** The approved administrative correction or reversal process.
- **[NEEDS CLARIFICATION]** The procedure for resolving apparent over-deliveries.
- **[NEEDS CLARIFICATION]** Whether Customer signatures or other proof of delivery are required.
- **[NEEDS CLARIFICATION]** Whether offline delivery recording is required.
- **[NEEDS CLARIFICATION]** Required Driver devices and connectivity expectations.
- **[NEEDS CLARIFICATION]** Final API conventions and concurrency controls.
- **[NEEDS CLARIFICATION]** Final audit and retention requirements.

These decisions require review before implementation. They do not prevent Feature 15 from remaining a design draft.
