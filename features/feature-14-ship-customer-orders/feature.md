
# Feature: Ship Customer Orders

**Feature ID:** 14  
**Branch pattern:** `feature/14-ship-customer-orders`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  

**Input:** The Warehouse Management System assists Shipping Clerks in preparing picked Customer Orders for delivery. The system identifies orders with picked products, verifies the Items and quantities prepared for shipment, records actual Quantity Shipped separately from Quantity Ordered, Quantity Picked, and Quantity Delivered, supports verification, shrink-wrapping and labeling, and records completed Shipments for the delivery process. Shipping remains separate from picking and delivery.

---

## User Stories

### US-14.1: Select Picked Customer Order for Shipping

**As a** Shipping Clerk  
**I want to** select a Customer Order containing products that have been picked  
**So that** I can identify which products are ready to be prepared for shipment.

**Priority:** P1  
**Independent test:** Select a Customer Order in Picked status and verify that its picked Items and quantities are displayed.

### US-14.2: Verify Items for Shipment

**As a** Shipping Clerk  
**I want to** verify the products prepared for shipment  
**So that** I can detect incorrect or missing Items before they leave the warehouse.

**Priority:** P1  
**Independent test:** Verify the correct products for a Shipment and confirm that an incorrect product is identified and prevented from being shipped.

### US-14.3: Record Quantity Shipped

**As a** Shipping Clerk  
**I want to** record the actual quantity shipped for each Item  
**So that** the system can distinguish shipped products from the quantities ordered and picked.

**Priority:** P1  
**Independent test:** Record a Quantity Shipped smaller than Quantity Picked and verify that the actual quantity and difference are preserved.

### US-14.4: Prepare Customer Order for Delivery

**As a** Shipping Clerk  
**I want to** verify, shrink-wrap, and label the prepared Shipment  
**So that** the products can be safely identified and handled during delivery.

**Priority:** P1  
**Independent test:** Complete shipment preparation and verify that the system records the verification, packaging, and labeling steps.

### US-14.5: Complete Shipment and Release for Delivery

**As a** Shipping Clerk  
**I want to** complete shipping after all required preparation steps are finished  
**So that** the Shipment becomes available for loading and delivery.

**Priority:** P1  
**Independent test:** Complete a valid Shipment and verify that it becomes available to Feature 15 without automatically recording the products as delivered.

### US-14.6: Handle Shipping Exceptions

**As a** Shipping Clerk  
**I want to** record problems that prevent a Shipment from being completed  
**So that** incorrect products, missing quantities, and incomplete preparation can be resolved without losing shipment information.

**Priority:** P2  
**Independent test:** Report an incorrect Item or incomplete packaging and verify that shipment completion is blocked until the issue is resolved.

---

## Functional Requirements

- **FR-001:** The system MUST identify Customer Orders with picked quantities available for shipping.
- **FR-002:** The system MUST allow authorized Shipping Clerks to select eligible Customer Orders for shipping.
- **FR-003:** The system MUST display the Customer, Customer Order Number, Individual Items, and Quantity Picked for the selected order.
- **FR-004:** The system MUST prevent Customer Orders in Draft, Ready for Picking, Picking, or Canceled status from being selected for ordinary shipping.
- **FR-005:** The system MUST allow Customer Orders in Picked status to proceed to shipping.
- **FR-006:** The system MUST support authorized release of available picked quantities from Partially Picked Customer Orders for partial shipping.
- **FR-007:** The system MUST create a unique Shipment identifier for each Shipment.
- **FR-008:** The system MUST associate each Shipment with one Customer Order.
- **FR-009:** The system MUST allow a Customer Order to have more than one Shipment when partial shipments are permitted.
- **FR-010:** The system MUST prevent the same picked quantities from being allocated to multiple active Shipments.
- **FR-011:** The system MUST allow the Shipping Clerk to verify each Item prepared for shipment.
- **FR-012:** The system MUST support product barcode scanning to identify Items during shipping verification.
- **FR-013:** The system MUST compare a scanned Item with the expected Item on the Shipment.
- **FR-014:** The system MUST identify incorrect or unexpected Items during shipment verification.
- **FR-015:** The system MUST prevent an incorrect Item from being silently added to a Shipment.
- **FR-016:** The system MUST identify unreadable or unknown product barcodes without recording successful verification.
- **FR-017:** The system MUST record the actual Quantity Shipped for each Shipment Line.
- **FR-018:** Quantity Shipped MUST be recorded in individual units.
- **FR-019:** The system MUST prevent negative Quantity Shipped values.
- **FR-020:** The system MUST prevent Quantity Shipped from exceeding the picked quantity not already allocated to other Shipments.
- **FR-021:** The system MUST preserve Quantity Ordered separately from Quantity Picked, Quantity Shipped, and Quantity Delivered.
- **FR-022:** The system MUST compare Quantity Shipped with Quantity Picked.
- **FR-023:** The system MUST preserve differences between Quantity Picked and Quantity Shipped.
- **FR-024:** The system MUST allow a Shipping Clerk to record a smaller Quantity Shipped when fewer products are actually prepared for shipment.
- **FR-025:** The system MUST identify and record shipping discrepancies when the quantity prepared differs from the quantity allocated for shipment.
- **FR-026:** The system MUST preserve unshipped picked quantities for later shipment or authorized review.
- **FR-027:** The system MUST support recording shipment verification as completed.
- **FR-028:** The system MUST support recording shrink-wrapping or other required packaging as completed.
- **FR-029:** The system MUST support recording shipment labeling as completed.
- **FR-030:** The system MUST associate each Shipment with the Customer Order Number and Customer delivery information needed for labeling.
- **FR-031:** The system MUST prevent Shipment completion when required verification has not been completed.
- **FR-032:** The system MUST prevent Shipment completion when required packaging or labeling has not been completed.
- **FR-033:** The system MUST maintain Shipment statuses of Preparing, Ready for Delivery, Canceled, and Exception.
- **FR-034:** A newly created Shipment MUST initially have Preparing status.
- **FR-035:** The system MUST allow an authorized Shipping Clerk to mark a fully prepared Shipment as Ready for Delivery.
- **FR-036:** The system MUST record the User and date and time when a Shipment becomes Ready for Delivery.
- **FR-037:** The system MUST make Ready for Delivery Shipments available to Feature 15.
- **FR-038:** The system MUST NOT automatically mark a Shipment as Delivered when shipping is completed.
- **FR-039:** The system MUST NOT automatically update Quantity Delivered during the shipping process.
- **FR-040:** The system MUST update the Customer Order Line's cumulative Quantity Shipped when a Shipment is finalized.
- **FR-041:** The system MUST prevent the same Shipment from increasing cumulative Quantity Shipped more than once.
- **FR-042:** The system MUST mark a Customer Order as Shipped when all ordered quantities have been shipped.
- **FR-043:** The system MUST mark a Customer Order as Partially Shipped when at least one unit has been shipped but some ordered quantities remain unshipped.
- **FR-044:** The system MUST preserve the status and history of partially shipped Customer Orders.
- **FR-045:** The system MUST allow Shipping Clerks to report incorrect Items, missing quantities, damaged packaging, or incomplete preparation.
- **FR-046:** The system MUST prevent Shipments with unresolved blocking exceptions from being marked Ready for Delivery.
- **FR-047:** The system MUST make unresolved shipping exceptions available for Supervisor review.
- **FR-048:** The system MUST preserve shipment history, including Items, quantities, verification, packaging, labeling, and shipping personnel.
- **FR-049:** The system MUST restrict shipping operations to authorized Shipping Clerks and Supervisors.
- **FR-050:** The system MUST reject attempts to modify nonexistent Shipments.
- **FR-051:** The system MUST prevent completed Shipments from being silently modified through ordinary shipping operations.
- **FR-052:** The system MUST maintain the relationships between Shipments, Shipment Lines, Customer Orders, Customer Order Lines, Individual Items, and Users.
- **FR-053:** The system MUST keep shipping separate from the delivery confirmation process.
- **FR-054:** The system MUST preserve Quantity Shipped for comparison with Quantity Delivered in Feature 18.

---

## Assumptions

- **A-001:** Feature 12 creates Customer Orders and maintains the original Quantity Ordered.
- **A-002:** Feature 13 records Quantity Picked and identifies Customer Orders that have completed picking.
- **A-003:** Customer Orders in Picked status are eligible for ordinary shipping.
- **A-004:** Customer Orders in Partially Picked status may be eligible for partial shipping when authorized.
- **A-005:** Customer Orders in Draft, Ready for Picking, Picking, or Canceled status are not eligible for ordinary shipping.
- **A-006:** Only authenticated and authorized Shipping Clerks or Supervisors may perform shipping operations.
- **A-007:** Each Shipment belongs to one Customer Order.
- **A-008:** A Customer Order may have multiple Shipments when partial shipping is permitted.
- **A-009:** Each Shipment receives a unique Shipment identifier.
- **A-010:** Shipment Lines identify the Individual Items and picked quantities allocated to the Shipment.
- **A-011:** The same picked quantities cannot be allocated to more than one active Shipment.
- **A-012:** Individual Items have UPCs available for product verification.
- **A-013:** Shipping Clerks use electronic devices to verify shipment products.
- **A-014:** Quantity Shipped is recorded in individual units.
- **A-015:** Quantity Shipped cannot exceed the picked quantity available for shipment.
- **A-016:** Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered remain separate.
- **A-017:** Shipping discrepancies are recorded when prepared quantities differ from allocated quantities.
- **A-018:** Unshipped picked quantities remain available for later shipment or authorized review.
- **A-019:** Each Shipment must complete required verification, packaging, and labeling before release.
- **A-020:** Shipment labels use the Customer Order Number and relevant Customer delivery information.
- **A-021:** A newly created Shipment begins in Preparing status.
- **A-022:** Shipments use Preparing, Ready for Delivery, Canceled, and Exception statuses.
- **A-023:** Shipments with unresolved blocking exceptions cannot become Ready for Delivery.
- **A-024:** The system records the User and timestamp when a Shipment becomes Ready for Delivery.
- **A-025:** Cumulative Quantity Shipped is updated when a Shipment is finalized.
- **A-026:** Finalizing the same Shipment more than once cannot duplicate Quantity Shipped updates.
- **A-027:** A Customer Order becomes Shipped when all ordered quantities have been shipped.
- **A-028:** A Customer Order becomes Partially Shipped when some, but not all, ordered quantities have been shipped.
- **A-029:** Ready for Delivery Shipments become available to Feature 15.
- **A-030:** Shipping does not automatically record delivery confirmation.
- **A-031:** Quantity Delivered remains unchanged during shipping.
- **A-032:** Shipment history remains available for authorized review.
- **A-033:** Supervisors can review unresolved shipping exceptions.
- **A-034:** Shared authentication and authorization are provided by the Warehouse Management System.
- **A-035:** Feature 18 uses preserved Quantity Shipped information for comparison with Quantity Delivered, as stated in FR-054.
- **A-036:** Physical loading and delivery confirmation occur outside the ordinary Shipment preparation workflow.

**[NEEDS CLARIFICATION]** Confirm whether the Feature 18 reference in FR-054 is correct or whether the comparison is intended to be part of Feature 15.

---

## Edge Cases

### EC-14.1: No Customer Orders Eligible for Shipping

**Condition:** A Shipping Clerk requests available shipping work when no Customer Orders have picked quantities eligible for shipment.

**Expected Behavior:**
- The system reports that no shipping work is available.
- No empty Shipment is created.
- Existing Customer Orders remain unchanged.

### EC-14.2: Customer Order Not Eligible

**Condition:** A Shipping Clerk selects a Customer Order in Draft, Ready for Picking, Picking, or Canceled status.

**Expected Behavior:**
- The system rejects ordinary shipping.
- No Shipment is created.
- No Quantity Shipped is updated.

### EC-14.3: Partially Picked Order Without Authorization

**Condition:** A Shipping Clerk attempts to ship available quantities from a Partially Picked Customer Order without the required authorization.

**Expected Behavior:**
- The system prevents the partial Shipment from proceeding.
- Picked quantities remain unchanged.
- The order remains available for authorized review.

**[NEEDS CLARIFICATION]** Confirm who may authorize partial shipping and how authorization is recorded.

### EC-14.4: Duplicate Picked Quantity Allocation

**Condition:** Two active Shipments attempt to allocate the same picked units.

**Expected Behavior:**
- The system rejects duplicate allocation.
- Previously allocated quantities remain reserved.
- Cumulative allocations cannot exceed the available picked quantity.

### EC-14.5: No Picked Quantity Available

**Condition:** A Customer Order has no picked quantity remaining for allocation to a Shipment.

**Expected Behavior:**
- The system rejects Shipment creation.
- No empty Shipment is created.
- The Clerk receives an explanation.

### EC-14.6: Incorrect Product Scanned

**Condition:** A Shipping Clerk scans a UPC associated with an Item not expected on the Shipment Line.

**Expected Behavior:**
- The system identifies the mismatch.
- The incorrect Item is not verified.
- A shipping exception is recorded.
- Shipment completion remains blocked while the exception is unresolved.

### EC-14.7: Unknown or Unreadable Barcode

**Condition:** A product barcode cannot be read or is not recognized.

**Expected Behavior:**
- The system reports failed verification.
- The Item is not marked as verified.
- The Clerk may retry or request Supervisor assistance.
- No successful verification is recorded.

### EC-14.8: Quantity Shipped Exceeds Allocation

**Condition:** A Shipping Clerk attempts to record a quantity greater than the Shipment Line allocation.

**Expected Behavior:**
- The system rejects the quantity.
- Quantity Shipped is not increased beyond the allocation.
- Existing shipment information remains unchanged.

### EC-14.9: Negative Quantity Shipped

**Condition:** A Shipping Clerk enters a negative Quantity Shipped.

**Expected Behavior:**
- The system rejects the invalid quantity.
- No cumulative shipping update occurs.

### EC-14.10: Fewer Products Available Than Allocated

**Condition:** A Shipment Line has 20 units allocated, but only 15 units are available during preparation.

**Expected Behavior:**
- The Clerk records the actual 15 units.
- The system identifies the 5-unit difference.
- A shipping discrepancy is preserved.
- The missing 5 units are not recorded as shipped.
- Unshipped picked quantities remain available for later resolution.

### EC-14.11: Unverified Shipment Line

**Condition:** A Shipment contains an Item that has not passed verification.

**Expected Behavior:**
- The system prevents the Shipment from becoming Ready for Delivery.
- The unverified Item is identified.
- The Clerk may complete verification before attempting release again.

### EC-14.12: Packaging Not Completed

**Condition:** A Shipping Clerk attempts to release a Shipment before required shrink-wrapping or other packaging is completed.

**Expected Behavior:**
- The system rejects release.
- The incomplete packaging step is identified.
- Shipment status remains non-final.

### EC-14.13: Labeling Not Completed

**Condition:** A Shipment has been verified and packaged but lacks required labeling confirmation.

**Expected Behavior:**
- The system rejects release.
- The missing labeling step is identified.
- The Shipment remains unavailable to Feature 15.

### EC-14.14: Incorrect Customer Delivery Information

**Condition:** A Shipment label contains incomplete or inconsistent Customer delivery information.

**Expected Behavior:**
- The system prevents confirmation of an invalid label when the inconsistency is detected.
- The issue is made available for correction.
- **[NEEDS CLARIFICATION]** Confirm whether address corrections occur through Customer maintenance, Customer Order maintenance, or an authorized shipment-specific process.

### EC-14.15: Unresolved Blocking Shipping Exception

**Condition:** A Shipment has an unresolved incorrect Item, missing quantity, packaging, or labeling exception that prevents completion.

**Expected Behavior:**
- The system rejects Ready for Delivery status.
- The exception remains recorded.
- The issue is available for Supervisor review.

**[NEEDS CLARIFICATION]** Define which exception types are blocking and the required resolution or approval process.

### EC-14.16: Shipment Contains No Valid Lines

**Condition:** A Shipping Clerk attempts to finalize a Shipment with no valid Shipment Lines.

**Expected Behavior:**
- The system rejects completion.
- No Quantity Shipped update occurs.
- The Shipment does not become Ready for Delivery.

### EC-14.17: Duplicate Shipment Finalization

**Condition:** A Shipment already marked Ready for Delivery is finalized again.

**Expected Behavior:**
- The system rejects the duplicate operation.
- Cumulative Quantity Shipped is not increased again.
- Original completion information is preserved.

### EC-14.18: Attempt to Modify Completed Shipment

**Condition:** A Shipping Clerk attempts to change Shipment Lines or quantities after the Shipment becomes Ready for Delivery.

**Expected Behavior:**
- The system prevents silent modification.
- Historical shipment information remains preserved.
- **[NEEDS CLARIFICATION]** Confirm the authorized correction or reversal process for completed Shipments.

### EC-14.19: Multiple Partial Shipments

**Condition:** A Customer Order has several completed or active partial Shipments.

**Expected Behavior:**
- Each Shipment has a unique identifier.
- Previously shipped quantities remain preserved.
- The system prevents allocation of the same picked units more than once.
- Cumulative Quantity Shipped cannot exceed cumulative Quantity Picked.

### EC-14.20: Customer Order Partially Shipped

**Condition:** Some ordered units have been shipped while other ordered units remain unshipped.

**Expected Behavior:**
- The system marks the Customer Order Partially Shipped.
- Quantity Shipped reflects only finalized Shipments.
- Remaining quantities are preserved.

### EC-14.21: Customer Order Fully Shipped

**Condition:** All ordered quantities have been included in finalized Shipments.

**Expected Behavior:**
- The system marks the Customer Order Shipped.
- Quantity Shipped is preserved separately from Quantity Delivered.
- Delivery confirmation remains outside Feature 14.

### EC-14.22: Unauthorized Shipping Operation

**Condition:** A Driver or another user without shipping permission attempts to finalize a Shipment.

**Expected Behavior:**
- The system denies the operation.
- Shipment status remains unchanged.
- Quantity Shipped remains unchanged.

### EC-14.23: Nonexistent Shipment

**Condition:** A Shipping Clerk attempts to verify, update, or complete a Shipment that does not exist.

**Expected Behavior:**
- The system rejects the operation.
- No Customer Order quantities are modified.

### EC-14.24: Concurrent Shipment Allocation

**Condition:** Two Shipping Clerks attempt to allocate the same remaining picked quantity at nearly the same time.

**Expected Behavior:**
- The system validates available picked quantities during allocation.
- Duplicate allocation is prevented.
- **[NEEDS CLARIFICATION]** Confirm the transaction or locking strategy used for concurrent allocations.

### EC-14.25: Connection Failure During Shipment Finalization

**Condition:** A device loses connectivity while the Clerk is finalizing a Shipment.

**Expected Behavior:**
- The system preserves successfully committed shipment records.
- Repeated requests must not increase Quantity Shipped more than once.
- The Clerk can retrieve the current Shipment status after reconnection.
- **[NEEDS CLARIFICATION]** Confirm whether offline shipping operations are supported.

### EC-14.26: Shipment Canceled During Preparation

**Condition:** A Shipment in Preparing status is canceled before finalization.

**Expected Behavior:**
- The system preserves the canceled Shipment history.
- The Shipment cannot become Ready for Delivery.
- **[NEEDS CLARIFICATION]** Confirm who can cancel Shipments and when allocated picked quantities are released for reuse.

---

## Success Criteria

- **SC-001:** Authorized Shipping Clerks can identify Customer Orders with picked quantities available for shipping.
- **SC-002:** Customer Orders in Picked status can proceed to shipping.
- **SC-003:** Partially Picked Customer Orders can proceed to partial shipping only when authorized.
- **SC-004:** Ineligible Customer Orders cannot be selected for ordinary shipping.
- **SC-005:** Each Shipment has a unique identifier and references one Customer Order.
- **SC-006:** Multiple Shipments can reference the same Customer Order when partial shipping is permitted.
- **SC-007:** The same picked quantities cannot be allocated to multiple active Shipments.
- **SC-008:** Shipping Clerks can verify Items using product UPCs.
- **SC-009:** Incorrect Items cannot be silently verified or added to a Shipment.
- **SC-010:** Unknown or unreadable barcodes cannot produce successful verification.
- **SC-011:** Actual Quantity Shipped is recorded for each Shipment Line in individual units.
- **SC-012:** Quantity Shipped cannot be negative.
- **SC-013:** Quantity Shipped cannot exceed available picked allocations.
- **SC-014:** Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered remain separately recorded.
- **SC-015:** Differences between allocated and actually shipped quantities are preserved.
- **SC-016:** Unshipped picked quantities remain available for later shipment or authorized review.
- **SC-017:** Shipment verification is recorded with the responsible User and timestamp.
- **SC-018:** Required shrink-wrapping or packaging completion is recorded.
- **SC-019:** Shipment labeling completion is recorded.
- **SC-020:** Shipments cannot become Ready for Delivery without required verification, packaging, and labeling.
- **SC-021:** Shipments with unresolved blocking exceptions cannot become Ready for Delivery.
- **SC-022:** Newly created Shipments begin in Preparing status.
- **SC-023:** Fully prepared Shipments can be marked Ready for Delivery by authorized personnel.
- **SC-024:** Shipment finalization records the responsible User and timestamp.
- **SC-025:** Ready for Delivery Shipments are available to Feature 15.
- **SC-026:** Shipment finalization updates cumulative Quantity Shipped exactly once.
- **SC-027:** Customer Orders become Shipped when all ordered quantities have been shipped.
- **SC-028:** Customer Orders become Partially Shipped when some ordered quantities remain unshipped.
- **SC-029:** Shipment completion does not automatically update Quantity Delivered.
- **SC-030:** Shipping exceptions are recorded and available for Supervisor review.
- **SC-031:** Shipment history preserves Items, quantities, verification, packaging, labeling, and shipping personnel.
- **SC-032:** Unauthorized users cannot perform shipping operations.
- **SC-033:** Completed Shipments cannot be silently modified.
- **SC-034:** Concurrent shipping operations cannot allocate the same picked quantities more than once.
- **SC-035:** All 26 original Gherkin Acceptance Criteria have corresponding verification tests.
- **SC-036:** Shipping remains separate from delivery confirmation.

---

## Key Entities

### Shipment

Represents a set of picked products prepared for delivery to a Customer.

Each Shipment identifies its Customer Order, shipping status, preparation information, and Shipping Clerk.

### Shipment Line

Represents an Individual Item included in a Shipment.

Each line records the quantity allocated from picked products and the actual Quantity Shipped.

### Customer Order

Represents an order received from a Customer.

A Customer Order may have one or more Shipments.

### Customer Order Line

Represents an Individual Item requested by the Customer.

Each line maintains Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered separately.

### Individual Item

Represents a product included in the Customer Order and Shipment.

### UPC

Represents a barcode used to verify an Individual Item during shipping.

### Shipment Exception

Represents a problem discovered during shipping verification or preparation.

### User

Represents an employee authorized to prepare, verify, or review Shipments.

---

## Initial Data Model

### Shipment

| Attribute | Type | Description |
|---|---|---|
| shipmentId | Integer | Unique Shipment identifier |
| shipmentNumber | String | Unique shipment reference number |
| customerOrderId | Integer | Foreign key referencing Customer Order |
| preparedBy | Integer | User who created the Shipment |
| verifiedBy | Integer | User who verified the Shipment |
| status | String | Preparing, Ready for Delivery, Canceled, or Exception |
| createdAt | DateTime | Date and time Shipment preparation began |
| verifiedAt | DateTime | Date and time verification was completed |
| packagedAt | DateTime | Date and time packaging was completed |
| labeledAt | DateTime | Date and time labeling was completed |
| readyAt | DateTime | Date and time the Shipment became Ready for Delivery |

**Relationships:**
- Each Shipment belongs to one Customer Order.
- Each Shipment contains one or more Shipment Lines before completion.
- A Customer Order may have multiple Shipments.
- A Shipment is prepared and verified by authorized Users.
- Ready for Delivery Shipments are available to Feature 15.

**Constraints:**
- shipmentId must be unique.
- shipmentNumber must be unique.
- A Shipment must contain at least one valid Shipment Line before completion.
- A Shipment cannot become Ready for Delivery while blocking exceptions remain unresolved.
- Required verification, packaging, and labeling must be completed before release.

### Shipment Line

| Attribute | Type | Description |
|---|---|---|
| shipmentLineId | Integer | Unique Shipment Line identifier |
| shipmentId | Integer | Foreign key referencing Shipment |
| customerOrderLineId | Integer | Foreign key referencing Customer Order Line |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityAllocated | Integer | Picked quantity reserved for this Shipment |
| quantityShipped | Integer | Actual quantity included in the completed Shipment |
| isVerified | Boolean | Indicates whether the Item was verified |

**Relationships:**
- Each Shipment Line belongs to one Shipment.
- Each Shipment Line references one Customer Order Line.
- Each Shipment Line identifies one Individual Item.

**Constraints:**
- quantityAllocated must be positive.
- quantityShipped cannot be negative.
- quantityShipped cannot exceed quantityAllocated.
- A Customer Order Line cannot allocate the same picked units to multiple active Shipments.
- The combination of shipmentId and customerOrderLineId must be unique.

**Derived Value:**
- Unshipped Allocated Quantity = quantityAllocated - quantityShipped.

### Customer Order

| Attribute | Type | Description |
|---|---|---|
| customerOrderId | Integer | Unique Customer Order identifier |
| orderNumber | String | Unique Customer Order Number |
| customerId | Integer | Foreign key referencing Customer |
| status | String | Current Customer Order status |

**Relationships:**
- A Customer Order contains one or more Customer Order Lines.
- A Customer Order may have multiple Shipments.
- Customer Order entry is defined in Feature 12.

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
- Finalized Shipment Lines contribute to cumulative Quantity Shipped.

**Constraints:**
- quantityOrdered must remain preserved.
- quantityPicked cannot be negative.
- quantityShipped cannot be negative.
- quantityDelivered cannot be negative.
- Cumulative Quantity Shipped cannot exceed cumulative Quantity Picked.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |

**Relationships:**
- One Individual Item can appear on multiple Customer Order Lines.
- One Individual Item can appear on multiple Shipment Lines.

### UPC

| Attribute | Type | Description |
|---|---|---|
| upcId | Integer | Unique UPC identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| upcCode | String | Unique product barcode |
| barcodeType | String | Individual Unit or Case |

**Relationships:**
- Each UPC identifies one Individual Item.
- UPCs support product verification during shipping.

### Shipment Exception

| Attribute | Type | Description |
|---|---|---|
| shipmentExceptionId | Integer | Unique Shipment Exception identifier |
| shipmentId | Integer | Foreign key referencing Shipment |
| shipmentLineId | Integer | Optional foreign key referencing Shipment Line |
| exceptionType | String | Incorrect Item, Missing Quantity, Packaging Issue, or Labeling Issue |
| description | String | Description of the exception |
| reportedBy | Integer | User who reported the exception |
| reportedAt | DateTime | Date and time reported |
| status | String | Open or Resolved |

**Relationships:**
- Each Shipment Exception belongs to one Shipment.
- An Exception may reference a specific Shipment Line.
- Unresolved blocking exceptions prevent Shipment completion.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Shipping Clerks prepare and verify Shipments.
- Supervisors review shipping exceptions.

---

## Gherkin Acceptance Criteria

### US-14.1: Select Picked Customer Order for Shipping

#### AC-14.1.1: Select fully picked Customer Order

**Given** a Customer Order exists in Picked status  
**And** its picked quantities have not already been allocated to another Shipment  
**And** the user is authenticated as a Shipping Clerk  
**When** the Clerk selects the order for shipping  
**Then** the system displays the Customer Order and its picked Items  
**And** allows the Clerk to create a Shipment.

#### AC-14.1.2: Select partially picked Customer Order

**Given** a Customer Order exists in Partially Picked status  
**And** some picked quantities are available for shipping  
**And** partial shipping has been authorized  
**When** the Shipping Clerk selects the order  
**Then** the system allows a Shipment to be prepared using the available picked quantities  
**And** preserves the quantities not yet picked.

#### AC-14.1.3: Reject Customer Order without picked quantities

**Given** a Customer Order has no picked quantities available for shipping  
**When** the Shipping Clerk attempts to create a Shipment  
**Then** the system rejects the request  
**And** does not create an empty Shipment.

#### AC-14.1.4: Prevent duplicate allocation

**Given** 20 picked units of Item A are already allocated to an active Shipment  
**When** another Shipment attempts to allocate the same 20 units  
**Then** the system rejects the duplicate allocation.

### US-14.2: Verify Items for Shipment

#### AC-14.2.1: Verify correct Item

**Given** a Shipment Line requires Item A  
**And** the Shipping Clerk is preparing the Shipment  
**When** the Clerk scans a UPC associated with Item A  
**Then** the system verifies the expected Item  
**And** allows its verification status to be recorded.

#### AC-14.2.2: Detect incorrect Item

**Given** a Shipment Line requires Item A  
**When** the Shipping Clerk scans a UPC associated with Item B  
**Then** the system identifies the incorrect Item  
**And** prevents Item B from being confirmed as Item A  
**And** records an exception requiring correction.

#### AC-14.2.3: Handle unreadable barcode

**Given** a Shipping Clerk is verifying a Shipment Item  
**When** the product barcode cannot be read  
**Then** the system reports that verification has not succeeded  
**And** does not mark the Item as verified  
**And** allows the Clerk to retry or request Supervisor assistance.

#### AC-14.2.4: Prevent unverified shipment completion

**Given** a Shipment contains an Item that has not been verified  
**When** the Shipping Clerk attempts to mark the Shipment Ready for Delivery  
**Then** the system rejects completion  
**And** identifies the unverified Item.

### US-14.3: Record Quantity Shipped

#### AC-14.3.1: Record full picked quantity

**Given** a Shipment Line has 20 picked units allocated  
**And** all 20 units have been verified  
**When** the Shipping Clerk confirms 20 units for shipping  
**Then** the system records Quantity Shipped as 20  
**And** preserves Quantity Picked separately.

#### AC-14.3.2: Record smaller shipped quantity

**Given** a Shipment Line has 20 picked units allocated  
**And** only 15 units are prepared for shipment  
**When** the Shipping Clerk records Quantity Shipped as 15  
**Then** the system records the actual 15 units  
**And** identifies 5 allocated units that were not shipped  
**And** preserves those 5 units for later resolution.

#### AC-14.3.3: Reject quantity greater than picked allocation

**Given** a Shipment Line has 20 picked units allocated  
**When** the Shipping Clerk attempts to record Quantity Shipped as 25  
**Then** the system rejects the quantity  
**And** does not increase Quantity Shipped beyond the picked allocation.

#### AC-14.3.4: Preserve separate quantities

**Given** a Customer Order Line has 30 units ordered  
**And** 25 units picked  
**And** 20 units shipped  
**When** the system displays the Customer Order Line  
**Then** Quantity Ordered remains 30  
**And** Quantity Picked remains 25  
**And** Quantity Shipped is 20  
**And** Quantity Delivered remains unchanged.

### US-14.4: Prepare Customer Order for Delivery

#### AC-14.4.1: Record shipment verification

**Given** all Items and quantities in a Shipment have been checked  
**When** the Shipping Clerk confirms verification  
**Then** the system records that verification was completed  
**And** records the verifying User and date and time.

#### AC-14.4.2: Record shrink-wrapping

**Given** a Shipment has been verified  
**When** the Shipping Clerk completes the required shrink-wrapping  
**Then** the system records packaging as completed  
**And** preserves the packaging completion time.

#### AC-14.4.3: Record shipment labeling

**Given** a Shipment has been verified and packaged  
**When** the Shipping Clerk attaches and confirms the required shipment label  
**Then** the system records labeling as completed  
**And** associates the Shipment with the Customer Order and delivery information.

#### AC-14.4.4: Prevent incomplete preparation

**Given** a Shipment has been verified  
**And** required packaging or labeling has not been completed  
**When** the Shipping Clerk attempts to release the Shipment  
**Then** the system rejects the release  
**And** identifies the incomplete preparation step.

### US-14.5: Complete Shipment and Release for Delivery

#### AC-14.5.1: Complete valid Shipment

**Given** a Shipment contains valid Shipment Lines  
**And** all Items have been verified  
**And** required packaging and labeling are completed  
**And** no blocking exceptions remain  
**When** the Shipping Clerk completes shipping  
**Then** the system marks the Shipment Ready for Delivery  
**And** records the completion date and time  
**And** makes the Shipment available to Feature 15.

#### AC-14.5.2: Mark Customer Order Shipped

**Given** all ordered quantities for a Customer Order have been picked  
**And** all ordered quantities have been included in completed Shipments  
**When** the system evaluates shipping completion  
**Then** the system sets the Customer Order status to Shipped  
**And** preserves Quantity Delivered separately.

#### AC-14.5.3: Mark Customer Order Partially Shipped

**Given** a Customer Order contains 30 units ordered  
**And** completed Shipments contain 20 units shipped  
**When** the system evaluates the Customer Order  
**Then** the system sets the Customer Order status to Partially Shipped  
**And** preserves the remaining 10 units as not shipped.

#### AC-14.5.4: Prevent duplicate shipment completion

**Given** a Shipment is already Ready for Delivery  
**When** the Shipping Clerk attempts to finalize the same Shipment again  
**Then** the system rejects the duplicate operation  
**And** does not increase cumulative Quantity Shipped a second time.

#### AC-14.5.5: Keep delivery separate

**Given** a Shipment has been marked Ready for Delivery  
**When** the system makes it available for delivery  
**Then** Quantity Shipped is preserved  
**And** Quantity Delivered is not automatically increased  
**And** delivery confirmation remains part of Feature 15.

### US-14.6: Handle Shipping Exceptions

#### AC-14.6.1: Record missing quantity

**Given** a Shipment Line has 20 units allocated  
**And** only 15 units can be located during shipping verification  
**When** the Shipping Clerk reports the missing quantity  
**Then** the system records a shipping exception for 5 units  
**And** preserves the actual available quantity  
**And** prevents the missing units from being recorded as shipped.

#### AC-14.6.2: Record incorrect Item

**Given** the Shipping Clerk discovers an Item that does not match the Customer Order  
**When** the Clerk reports the incorrect Item  
**Then** the system records the exception  
**And** prevents the incorrect Item from being verified for shipment.

#### AC-14.6.3: Block incomplete Shipment

**Given** a Shipment has an unresolved blocking exception  
**When** the Shipping Clerk attempts to mark it Ready for Delivery  
**Then** the system rejects the request  
**And** leaves the Shipment unavailable for delivery  
**And** makes the exception available for Supervisor review.

#### AC-14.6.4: Preserve shipping history

**Given** a Shipment has been completed  
**When** an authorized Manager reviews the Shipment history  
**Then** the system displays the Customer Order, shipped Items, Quantity Shipped, verification information, packaging and labeling records, and Shipping Clerk.

#### AC-14.6.5: Reject unauthorized shipping

**Given** the user is authenticated as a Driver without shipping permission  
**When** the user attempts to finalize a Shipment  
**Then** the system denies the operation  
**And** Quantity Shipped remains unchanged.

---

## Data Ownership

### Feature 14 — Ship Customer Orders

Feature 14 owns the shipment preparation and shipping workflow, including Shipments, Shipment Lines, Shipment Exceptions, verification records, packaging records, labeling records, and shipping history.

**Owned Data:**
- Shipment
- Shipment Number
- Shipment status
- Shipment Line
- Quantity Allocated
- Quantity Shipped per Shipment Line
- Shipment verification information
- Verified By
- Verification timestamp
- Packaging completion timestamp
- Labeling completion timestamp
- Shipment preparation and completion timestamps
- Shipment Exception
- Exception type, description, and status
- Shipping personnel references
- Shipment preparation and completion history

**Responsibilities:**
- Identify Customer Orders with picked quantities available for shipping.
- Allow authorized Shipping Clerks to select eligible Customer Orders.
- Create Shipments with unique identifiers.
- Associate each Shipment with one Customer Order.
- Support multiple Shipments when partial shipping is permitted.
- Prevent duplicate allocation of picked quantities.
- Verify Shipment Items through UPC scanning.
- Record actual quantities prepared for shipment.
- Preserve differences between allocated and shipped quantities.
- Record shipment verification, packaging, and labeling.
- Record shipping exceptions.
- Prevent release when required preparation is incomplete.
- Prevent release when blocking exceptions remain unresolved.
- Finalize eligible Shipments as Ready for Delivery.
- Coordinate updates to cumulative Quantity Shipped.
- Coordinate Customer Order shipping status updates.
- Make Ready for Delivery Shipments available to Feature 15.
- Preserve Shipment history.

### Feature 12 — Receive Customer Orders

**Owned Data:**
- Customer Order
- Customer Order Line
- Customer Order Number
- Customer association
- Quantity Ordered
- Original Customer Order information

**Feature 14 Responsibilities:**
- Retrieve existing Customer Orders and Customer Order Lines.
- Preserve Quantity Ordered.
- Reference Customer information needed for shipping labels.
- Coordinate cumulative Quantity Shipped updates through the approved Customer Order interface.
- Coordinate Customer Order status changes to Shipped or Partially Shipped.
- Never modify original ordered quantities through ordinary shipping operations.

### Feature 13 — Pick Customer Orders

**Owned Data:**
- Picking Assignment
- Picking Instruction
- Picking Movement
- Picking Shortage
- Picking history

**Feature 14 Responsibilities:**
- Retrieve available picked quantities.
- Use Quantity Picked to determine shipping eligibility.
- Prevent allocation of more picked units than are available.
- Preserve Quantity Picked during shipping.
- Keep shipping separate from picking.
- Never create Picking Movements through ordinary shipping operations.

### Individual Item Maintenance

**Owned Data:**
- Individual Item ID
- Item Number
- Item description
- Item master information

**Feature 14 Responsibilities:**
- Retrieve Item information for Shipment Lines.
- Display Item details during verification.
- Verify scanned products against expected Items.
- Never modify Item master data.

### UPC Maintenance

**Owned Data:**
- UPC ID
- UPC Code
- Associated Individual Item
- Barcode Type

**Feature 14 Responsibilities:**
- Retrieve UPC information.
- Resolve scanned UPCs to Individual Items.
- Reject incorrect or unknown product barcodes.
- Never modify UPC master data.

### Customer Maintenance

**Owned Data:**
- Customer ID
- Customer name
- Customer contact information
- Customer delivery information

**Feature 14 Responsibilities:**
- Retrieve Customer information needed for labeling.
- Associate Shipment labels with the correct Customer Order.
- Never silently modify Customer master data.

### Feature 15 — Delivery Processing

**Responsibilities:**
- Retrieve Shipments in Ready for Delivery status.
- Manage loading and delivery activities.
- Perform delivery confirmation according to the delivery feature requirements.

**Feature 14 Responsibilities:**
- Make completed Shipments available to Feature 15.
- Preserve Shipment identifiers and shipped quantities.
- Never automatically mark a Shipment as Delivered.
- Never automatically update Quantity Delivered.

### Feature 18 — Shipped and Delivered Quantity Comparison

Feature 14 preserves Quantity Shipped for comparison with Quantity Delivered in Feature 18, as stated in FR-054.

**[NEEDS CLARIFICATION]** Confirm the scope of Feature 18 and whether the comparison belongs there or in Feature 15. The original requirement is preserved pending approval.

### Shared Authentication and Authorization

**Owned Data:**
- User ID
- User role
- Authentication information
- Authorization permissions

**Feature 14 Responsibilities:**
- Require authentication for shipping operations.
- Restrict shipping operations to authorized Shipping Clerks and Supervisors.
- Record the User responsible for Shipment preparation and verification.
- Record the User who finalizes a Shipment.
- Restrict Supervisor review to authorized personnel.
- Deny unauthorized shipping operations.

### Cross-Feature Data Rules

- Feature 14 owns Shipments, Shipment Lines, and Shipment Exceptions.
- Feature 12 maintains Customer Orders and original Quantity Ordered.
- Feature 13 provides completed picking information.
- Quantity Picked remains unchanged through ordinary shipping.
- Feature 14 coordinates cumulative Quantity Shipped updates when Shipments are finalized.
- Quantity Delivered remains unchanged during shipping.
- Each Shipment belongs to one Customer Order.
- A Customer Order may have multiple Shipments.
- The same picked quantities cannot be allocated to multiple active Shipments.
- Cumulative Quantity Shipped cannot exceed cumulative Quantity Picked.
- A Shipment cannot increase cumulative Quantity Shipped more than once.
- Completed Shipment history must remain preserved.
- Shipping does not perform delivery confirmation.

**[NEEDS CLARIFICATION]** Confirm the exact interface for updating Customer Order Line Quantity Shipped and Customer Order shipping status.

**[NEEDS CLARIFICATION]** Confirm the ownership of picked-quantity allocation and reservation records.

**[NEEDS CLARIFICATION]** Confirm the approved correction or reversal process for completed Shipments.

---

## API Requirements

The following endpoints are proposed for the Feature 14 design draft. Final route naming and service boundaries require architecture approval.

### API-14.1: Retrieve Customer Orders Available for Shipping

**Endpoint:** `GET /api/shipping/available-orders`

**Purpose:** Identify Customer Orders containing picked quantities eligible for shipping.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Response Data:**
- Customer Order ID
- Customer Order Number
- Customer
- Customer Order status
- Individual Items
- Quantity Picked
- Quantity already allocated
- Quantity available for shipping

**Validation and Behavior:**
- Require authentication and shipping permission.
- Include eligible Picked Customer Orders.
- Include Partially Picked Customer Orders only when partial shipping is authorized.
- Exclude Draft, Ready for Picking, Picking, and Canceled Customer Orders from ordinary shipping.
- Identify when no eligible orders are available.
- Do not modify Customer Order quantities.

**Error Conditions:**
- Unauthorized access
- Invalid request parameters

### API-14.2: Create Shipment

**Endpoint:** `POST /api/shipments`

**Purpose:** Create a Shipment for an eligible Customer Order.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Request Data:**
- customerOrderId
- Requested Shipment Line allocations
- Partial shipping authorization reference, when required

**System-Generated Data:**
- shipmentId
- shipmentNumber
- preparedBy
- createdAt
- status = Preparing

**Validation and Behavior:**
- Confirm the Customer Order exists.
- Confirm the order is eligible for shipping.
- Confirm picked quantities are available.
- Reject an empty Shipment.
- Generate a unique Shipment identifier.
- Associate the Shipment with one Customer Order.
- Prevent duplicate allocation of picked quantities.
- Record the authenticated User.
- Initialize Shipment status as Preparing.

**Successful Response:**
- Shipment ID
- Shipment Number
- Customer Order reference
- Shipment status
- Shipment Lines

**Error Conditions:**
- Unauthorized user
- Customer Order not found
- Ineligible Customer Order
- No available picked quantities
- Invalid allocation
- Duplicate allocation

### API-14.3: Retrieve Shipment

**Endpoint:** `GET /api/shipments/{shipmentId}`

**Purpose:** Retrieve Shipment details and preparation progress.

**Authorized Roles:**
- Shipping Clerk
- Supervisor
- Manager with approved read permission

**Response Data:**
- Shipment ID
- Shipment Number
- Customer Order Number
- Customer delivery information
- Shipment status
- Shipment Lines
- Quantity Allocated
- Quantity Shipped
- Verification status
- Packaging completion
- Labeling completion
- Shipping Exceptions
- Preparation and completion timestamps

**Validation and Behavior:**
- Confirm the Shipment exists.
- Verify the User has permission to view it.
- Return current Shipment information.
- Do not modify shipment quantities.

**Error Conditions:**
- Shipment not found
- Unauthorized access

### API-14.4: Allocate Picked Quantities

**Endpoint:** `POST /api/shipments/{shipmentId}/lines`

**Purpose:** Add or update Shipment Lines using available picked quantities.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Request Data:**
- customerOrderLineId
- quantityAllocated

**Validation and Behavior:**
- Confirm the Shipment exists and is Preparing.
- Confirm the Customer Order Line belongs to the Shipment's Customer Order.
- Require a positive allocation quantity.
- Verify sufficient unallocated picked quantity exists.
- Prevent duplicate allocation across active Shipments.
- Preserve Quantity Picked.
- Create or update the corresponding Shipment Line.

**Successful Response:**
- Shipment Line ID
- Individual Item
- Quantity Allocated
- Remaining available picked quantity

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Invalid Shipment status
- Invalid Customer Order Line
- Invalid quantity
- Insufficient available picked quantity
- Concurrent allocation conflict

### API-14.5: Verify Shipment Item

**Endpoint:** `POST /api/shipments/{shipmentId}/lines/{shipmentLineId}/verify`

**Purpose:** Verify a Shipment Item using its product barcode.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Request Data:**
- scannedUpcCode

**Validation and Behavior:**
- Confirm the Shipment and Shipment Line exist.
- Confirm the Shipment is Preparing.
- Resolve the scanned UPC to an Individual Item.
- Compare the scanned Item with the expected Shipment Line Item.
- Record successful Item verification.
- Reject incorrect or unknown products.
- Record an exception when an incorrect Item is identified.
- Do not update cumulative Quantity Shipped during verification.

**Successful Response:**
- Shipment Line ID
- Verified Item
- Verification result

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Shipment Line not found
- Unknown UPC
- Incorrect Item
- Shipment not editable

### API-14.6: Record Shipment Line Quantity

**Endpoint:** `PUT /api/shipments/{shipmentId}/lines/{shipmentLineId}/quantity`

**Purpose:** Record the actual quantity prepared for shipping.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Request Data:**
- quantityShipped

**Validation and Behavior:**
- Confirm the Shipment is Preparing.
- Confirm the Shipment Line exists.
- Require a nonnegative whole-number quantity.
- Prevent Quantity Shipped from exceeding Quantity Allocated.
- Prevent cumulative shipped quantities from exceeding available picked quantities.
- Preserve differences between allocated and prepared quantities.
- Record discrepancies when required.
- Do not update Customer Order cumulative Quantity Shipped until finalization.

**Successful Response:**
- Shipment Line ID
- Quantity Allocated
- Recorded Quantity Shipped
- Unshipped Allocated Quantity

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Shipment Line not found
- Invalid quantity
- Quantity exceeds allocation
- Shipment already finalized

### API-14.7: Complete Shipment Verification

**Endpoint:** `POST /api/shipments/{shipmentId}/verify`

**Purpose:** Record completion of required Shipment verification.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Validation and Behavior:**
- Confirm the Shipment exists and is Preparing.
- Confirm required Items and quantities have been checked.
- Reject incomplete verification.
- Record the verifying User.
- Record the verification timestamp.
- Preserve any reported discrepancies.

**Successful Response:**
- Shipment ID
- Verification completion status
- Verified By
- Verification timestamp

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Incomplete verification
- Shipment not editable

### API-14.8: Record Packaging Completion

**Endpoint:** `POST /api/shipments/{shipmentId}/packaging`

**Purpose:** Record required shrink-wrapping or other packaging as completed.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Validation and Behavior:**
- Confirm the Shipment exists.
- Confirm required verification has been completed.
- Confirm the Shipment is Preparing.
- Record packaging completion.
- Record the completion timestamp.
- Preserve packaging-related exceptions.

**Successful Response:**
- Shipment ID
- Packaging completion status
- Packaging timestamp

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Verification incomplete
- Shipment not editable

### API-14.9: Record Labeling Completion

**Endpoint:** `POST /api/shipments/{shipmentId}/labeling`

**Purpose:** Record required Shipment labeling as completed.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Validation and Behavior:**
- Confirm the Shipment exists.
- Confirm required verification and packaging are completed.
- Confirm the Shipment is Preparing.
- Associate labeling with the Customer Order Number and delivery information.
- Record labeling completion.
- Record the labeling timestamp.

**Successful Response:**
- Shipment ID
- Labeling completion status
- Customer Order Number
- Labeling timestamp

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Incomplete preparation
- Shipment not editable

### API-14.10: Report Shipping Exception

**Endpoint:** `POST /api/shipments/{shipmentId}/exceptions`

**Purpose:** Record a problem discovered during Shipment verification or preparation.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Request Data:**
- shipmentLineId, when applicable
- exceptionType
- description

**Validation and Behavior:**
- Confirm the Shipment exists.
- Validate the exception type.
- Record the reporting User and timestamp.
- Associate the exception with the Shipment.
- Associate it with a Shipment Line when applicable.
- Preserve the exception for review.
- Prevent release while blocking exceptions remain unresolved.

**Successful Response:**
- Shipment Exception ID
- Exception type
- Exception status
- Reported timestamp

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Invalid exception type
- Invalid Shipment Line reference

### API-14.11: Review or Resolve Shipping Exception

**Endpoint:** `PATCH /api/shipments/{shipmentId}/exceptions/{exceptionId}`

**Purpose:** Allow an authorized Supervisor to review and resolve a recorded shipping exception.

**Authorized Role:**
- Supervisor

**Request Data:**
- resolution information
- status

**Validation and Behavior:**
- Confirm the Shipment and exception exist.
- Verify Supervisor authorization.
- Preserve the original exception record.
- Record the resolution decision.
- Prevent unsupported or unauthorized resolution.
- Reevaluate whether the Shipment remains blocked.

**Successful Response:**
- Shipment Exception ID
- Updated exception status
- Resolution information

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Exception not found
- Invalid resolution

**[NEEDS CLARIFICATION]** Confirm which exception types require Supervisor approval and what evidence is needed for resolution.

### API-14.12: Finalize Shipment

**Endpoint:** `POST /api/shipments/{shipmentId}/finalize`

**Purpose:** Mark a fully prepared Shipment Ready for Delivery.

**Authorized Roles:**
- Shipping Clerk
- Supervisor

**Validation and Behavior:**
- Confirm the Shipment exists.
- Confirm the Shipment is Preparing.
- Confirm the Shipment contains valid Shipment Lines.
- Confirm all required Items have been verified.
- Confirm actual quantities have been recorded.
- Confirm required packaging is complete.
- Confirm required labeling is complete.
- Confirm no unresolved blocking exceptions remain.
- Prevent duplicate finalization.
- Update cumulative Quantity Shipped on the corresponding Customer Order Lines.
- Apply cumulative shipping updates exactly once.
- Set Shipment status to Ready for Delivery.
- Record the finalizing User and completion timestamp.
- Update the Customer Order to Shipped or Partially Shipped as appropriate.
- Make the Shipment available to Feature 15.
- Preserve Quantity Delivered without modification.

**Successful Response:**
- Shipment ID
- Shipment Number
- Ready for Delivery status
- Final Quantity Shipped
- Updated Customer Order shipping status
- Finalizing User
- Completion timestamp

**Error Conditions:**
- Unauthorized user
- Shipment not found
- Invalid Shipment status
- Empty Shipment
- Unverified Item
- Incomplete packaging
- Incomplete labeling
- Unresolved blocking exception
- Invalid shipping quantity
- Duplicate finalization

### API-14.13: Retrieve Shipping Exceptions

**Endpoint:** `GET /api/shipping/exceptions`

**Purpose:** Allow authorized Supervisors to review unresolved shipping exceptions.

**Authorized Roles:**
- Supervisor
- Manager with approved read permission

**Optional Filters:**
- Shipment
- Customer Order
- Exception type
- Exception status

**Response Data:**
- Shipment Exception ID
- Shipment Number
- Customer Order Number
- Exception type
- Description
- Reporting User
- Report timestamp
- Exception status

**Validation and Behavior:**
- Return matching exceptions.
- Preserve unresolved issues for review.
- Do not modify Shipment quantities.

**Error Conditions:**
- Unauthorized access
- Invalid filters

### API-14.14: Retrieve Shipment History

**Endpoint:** `GET /api/shipments/{shipmentId}/history`

**Purpose:** Review preserved Shipment preparation and completion information.

**Authorized Roles:**
- Supervisor
- Manager
- Other users with approved read permissions

**Response Data:**
- Shipment Number
- Customer Order Number
- Shipment Lines
- Individual Items
- Quantity Allocated
- Quantity Shipped
- Verification information
- Packaging information
- Labeling information
- Shipping Exceptions
- Shipping personnel
- Shipment status
- Relevant timestamps

**Validation and Behavior:**
- Confirm the Shipment exists.
- Restrict access according to permissions.
- Return preserved historical information.
- Do not silently modify completed Shipment records.

**Error Conditions:**
- Unauthorized access
- Shipment not found

### General API Requirements

- All shipping write operations MUST enforce server-side authorization.
- Shipments MUST reference valid Customer Orders.
- Shipment Lines MUST reference valid Customer Order Lines and Individual Items.
- Shipment identifiers MUST be unique.
- New Shipments MUST begin in Preparing status.
- Duplicate allocation of picked quantities MUST be prevented.
- Product verification MUST reject incorrect or unknown UPCs.
- Quantity Shipped MUST be recorded in individual units.
- Quantity Shipped MUST NOT be negative.
- Quantity Shipped MUST NOT exceed available picked allocations.
- Cumulative Quantity Shipped MUST NOT exceed cumulative Quantity Picked.
- Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered MUST remain separate.
- Shipping discrepancies MUST be preserved.
- Required verification, packaging, and labeling MUST be completed before finalization.
- Unresolved blocking exceptions MUST prevent Shipment finalization.
- Finalization MUST update cumulative Quantity Shipped consistently.
- The same Shipment MUST NOT increase cumulative Quantity Shipped more than once.
- Completed Shipments MUST NOT be silently modified.
- Shipping MUST NOT automatically update Quantity Delivered.
- Ready for Delivery Shipments MUST be available to Feature 15.
- Shipment history MUST remain available to authorized users.

**[NEEDS CLARIFICATION]** Confirm final API naming conventions, allocation concurrency controls, and the authorized correction process for completed Shipments.

---

## Screen Requirements

### SCREEN-14.1: Available Customer Orders for Shipping

**Purpose:** Allow Shipping Clerks to identify Customer Orders with picked quantities available for shipping.

**Authorized Users:**
- Shipping Clerk
- Supervisor

**Displayed Information:**
- Customer Order Number
- Customer
- Customer Order status
- Individual Items
- Quantity Picked
- Quantity available for shipping
- Partial shipping eligibility

**Controls:**
- Select Customer Order
- Create Shipment
- Refresh Available Orders

**Behavior:**
- Show eligible Customer Orders.
- Allow ordinary shipping of Picked Customer Orders.
- Allow authorized partial shipping of Partially Picked Customer Orders.
- Exclude ineligible Customer Orders.
- Prevent Shipment creation when no picked quantities are available.

### SCREEN-14.2: Shipment Preparation

**Purpose:** Allow Shipping Clerks to prepare a Shipment using picked products.

**Authorized Users:**
- Shipping Clerk
- Supervisor

**Displayed Information:**
- Shipment Number
- Customer Order Number
- Customer information
- Shipment status
- Shipment Lines
- Individual Items
- Quantity Allocated
- Quantity Shipped
- Preparation progress

**Controls:**
- Add Shipment Line
- Update Allocation
- Verify Items
- Record Quantity Shipped
- Report Exception
- Continue Preparation

**Behavior:**
- Associate the Shipment with one Customer Order.
- Prevent duplicate allocation of picked quantities.
- Display available picked quantities.
- Preserve actual quantities prepared for shipment.
- Prevent ordinary editing after finalization.

### SCREEN-14.3: Shipment Item Verification

**Purpose:** Verify the products included in a Shipment.

**Authorized Users:**
- Shipping Clerk
- Supervisor

**Displayed Information:**
- Shipment Number
- Expected Item Number
- Item Description
- Expected UPC
- Scanned UPC
- Quantity Allocated
- Quantity Prepared
- Verification status

**Controls:**
- Scan Product UPC
- Retry Scan
- Confirm Verification
- Report Incorrect Item
- Request Supervisor Assistance

**Behavior:**
- Compare scanned products with expected Shipment Items.
- Mark correct Items as verified.
- Reject incorrect or unknown products.
- Record exceptions for incorrect Items.
- Prevent unverified Items from passing finalization.

### SCREEN-14.4: Shipment Quantity Confirmation

**Purpose:** Record actual quantities prepared for shipping.

**Authorized Users:**
- Shipping Clerk
- Supervisor

**Displayed Information:**
- Shipment Line
- Individual Item
- Quantity Picked
- Quantity Allocated
- Actual Quantity Shipped
- Unshipped Allocated Quantity
- Shipping discrepancies

**Controls:**
- Enter Quantity Shipped
- Save Quantity
- Report Missing Quantity
- Return to Shipment

**Behavior:**
- Accept nonnegative whole-number quantities.
- Prevent quantities exceeding allocated picked units.
- Preserve differences between allocated and shipped quantities.
- Identify missing quantities.
- Do not update cumulative Quantity Shipped until finalization.

### SCREEN-14.5: Shipment Packaging and Labeling

**Purpose:** Record required Shipment preparation steps.

**Authorized Users:**
- Shipping Clerk
- Supervisor

**Displayed Information:**
- Shipment Number
- Customer Order Number
- Customer delivery information
- Verification completion status
- Packaging completion status
- Labeling completion status
- Relevant timestamps

**Controls:**
- Confirm Verification
- Confirm Packaging
- Confirm Labeling
- View Shipment Details
- Report Preparation Exception

**Behavior:**
- Require verification before completing preparation.
- Record shrink-wrapping or other required packaging.
- Record labeling completion.
- Preserve preparation timestamps.
- Identify missing preparation steps.
- Prevent release until all required steps are complete.

### SCREEN-14.6: Shipment Completion

**Purpose:** Review and finalize a prepared Shipment.

**Authorized Users:**
- Shipping Clerk
- Supervisor

**Displayed Information:**
- Shipment Number
- Customer Order Number
- Shipment Lines
- Actual Quantity Shipped
- Verification status
- Packaging status
- Labeling status
- Unresolved exceptions
- Expected Customer Order shipping status

**Controls:**
- Review Shipment
- Review Exceptions
- Complete Preparation
- Mark Ready for Delivery
- Return to Shipment

**Behavior:**
- Validate all required preparation steps.
- Reject incomplete or invalid Shipments.
- Reject unresolved blocking exceptions.
- Prevent duplicate finalization.
- Update cumulative Quantity Shipped once.
- Set Shipment status to Ready for Delivery.
- Update Customer Order shipping status.
- Make the Shipment available to Feature 15.
- Preserve Quantity Delivered.

### SCREEN-14.7: Shipping Exception Review

**Purpose:** Allow authorized Supervisors to review shipping problems.

**Authorized Users:**
- Supervisor
- Manager with approved read permission

**Displayed Information:**
- Shipment Number
- Customer Order Number
- Exception type
- Description
- Related Shipment Line
- Reporting User
- Report timestamp
- Exception status

**Controls:**
- View Exception
- View Shipment
- Review Resolution
- Resolve Exception, when authorized
- Refresh Exception List

**Behavior:**
- Display unresolved shipping exceptions.
- Preserve exception history.
- Restrict resolution actions to authorized personnel.
- Prevent release while blocking exceptions remain unresolved.

### SCREEN-14.8: Shipment History

**Purpose:** Allow authorized personnel to review completed Shipments.

**Authorized Users:**
- Supervisor
- Manager
- Other users with approved read permissions

**Displayed Information:**
- Shipment Number
- Customer Order Number
- Customer
- Individual Items
- Quantity Allocated
- Quantity Shipped
- Verification records
- Packaging records
- Labeling records
- Shipping Exceptions
- Shipping personnel
- Shipment status
- Completion timestamp

**Controls:**
- Search Shipments
- View Shipment Details
- View Shipment Lines
- View Exceptions
- Return to Shipment List

**Behavior:**
- Display preserved Shipment history.
- Keep completed Shipment records read-only through ordinary shipping screens.
- Preserve actual Quantity Shipped.
- Restrict access according to role permissions.

### General Screen Requirements

- Screens MUST follow the approved Warehouse System UI style conventions.
- Shipping screens MUST clearly identify the Customer Order and Shipment.
- Shipment Lines MUST display Item details and relevant quantities.
- Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered MUST remain distinguishable.
- Product scanning controls MUST support barcode-based verification.
- Incorrect and unknown barcodes MUST produce clear error messages.
- Quantity entry MUST reject invalid values.
- Required verification, packaging, and labeling steps MUST be visible.
- Shipping discrepancies MUST be clearly identified.
- Unresolved blocking exceptions MUST prevent release.
- Shipment status MUST remain visible.
- Unauthorized actions MUST be restricted.
- UI validation MUST be reinforced by server-side validation.
- Screen designs MUST be documented in Figma or the approved design tool before implementation.

**[NEEDS CLARIFICATION]** Confirm required shipping workstation devices, barcode scanner integration, and label-printing requirements.

---

## Definition of Done

Feature 14 is considered complete when all approved requirements and acceptance criteria have been implemented and verified.

### Requirements and Design

- [ ] All six User Stories are implemented.
- [ ] Functional Requirements FR-001 through FR-054 are satisfied.
- [ ] Assumptions and unresolved clarifications have been reviewed.
- [ ] Edge Cases have corresponding handling and verification.
- [ ] Success Criteria have been evaluated.
- [ ] Data ownership boundaries are documented and followed.
- [ ] Initial Data Model has been reviewed and approved.
- [ ] Shipment status rules are approved.
- [ ] Partial shipping authorization rules are approved.
- [ ] API contracts have been reviewed.
- [ ] Screen designs have been prepared and reviewed.

### Implementation

- [ ] Authorized Shipping Clerks can identify eligible Customer Orders.
- [ ] Customer Orders in Picked status can proceed to shipping.
- [ ] Partially Picked orders require authorization for partial shipping.
- [ ] Ineligible Customer Orders are rejected.
- [ ] Each Shipment receives a unique identifier.
- [ ] Each Shipment references one Customer Order.
- [ ] Multiple Shipments are supported when partial shipping is permitted.
- [ ] Duplicate picked-quantity allocation is prevented.
- [ ] Shipment Items can be verified using UPC scanning.
- [ ] Incorrect and unknown products are rejected.
- [ ] Actual Quantity Shipped is recorded for each Shipment Line.
- [ ] Quantity Shipped is recorded in individual units.
- [ ] Negative shipping quantities are rejected.
- [ ] Quantity Shipped cannot exceed available picked allocations.
- [ ] Quantity Ordered, Quantity Picked, Quantity Shipped, and Quantity Delivered remain separate.
- [ ] Shipping discrepancies are recorded.
- [ ] Unshipped picked quantities remain preserved.
- [ ] Shipment verification completion is recorded.
- [ ] Required packaging completion is recorded.
- [ ] Required labeling completion is recorded.
- [ ] Incomplete preparation prevents Shipment finalization.
- [ ] Shipments use Preparing, Ready for Delivery, Canceled, and Exception statuses.
- [ ] New Shipments begin in Preparing status.
- [ ] Valid Shipments can be marked Ready for Delivery.
- [ ] Finalization records the responsible User and timestamp.
- [ ] Ready for Delivery Shipments are available to Feature 15.
- [ ] Shipment finalization updates cumulative Quantity Shipped.
- [ ] Duplicate finalization cannot increase Quantity Shipped again.
- [ ] Fully shipped Customer Orders receive Shipped status.
- [ ] Partially shipped Customer Orders receive Partially Shipped status.
- [ ] Shipping exceptions can be reported.
- [ ] Unresolved blocking exceptions prevent release.
- [ ] Supervisors can review unresolved exceptions.
- [ ] Shipment history is preserved.
- [ ] Unauthorized shipping operations are rejected.
- [ ] Nonexistent Shipments cannot be modified.
- [ ] Completed Shipments cannot be silently modified.
- [ ] Shipping does not automatically update Quantity Delivered.

### Testing and Verification

- [ ] All 26 Gherkin Acceptance Criteria have corresponding verification tests.
- [ ] Unit tests cover Customer Order shipping eligibility.
- [ ] Unit tests cover partial shipping authorization.
- [ ] Unit tests cover Shipment creation.
- [ ] Unit tests cover duplicate allocation prevention.
- [ ] Unit tests cover product UPC verification.
- [ ] Unit tests cover shipping quantity validation.
- [ ] Unit tests cover shipping discrepancy calculations.
- [ ] Unit tests cover preparation completion rules.
- [ ] Unit tests cover Shipment status transitions.
- [ ] Unit tests cover Customer Order shipping status updates.
- [ ] Unit tests cover duplicate finalization prevention.
- [ ] API tests verify successful Shipment operations.
- [ ] API tests verify unauthorized operations are denied.
- [ ] API tests verify incorrect UPCs are rejected.
- [ ] API tests verify invalid quantities are rejected.
- [ ] API tests verify incomplete preparation prevents finalization.
- [ ] API tests verify unresolved blocking exceptions prevent release.
- [ ] Integration tests verify Customer Order retrieval from Feature 12.
- [ ] Integration tests verify picked quantities from Feature 13.
- [ ] Integration tests verify Item and UPC references.
- [ ] Integration tests verify cumulative Quantity Shipped updates.
- [ ] Integration tests verify Ready for Delivery Shipments are available to Feature 15.
- [ ] Tests verify Quantity Ordered remains unchanged.
- [ ] Tests verify Quantity Picked remains unchanged during shipping.
- [ ] Tests verify Quantity Delivered remains unchanged during shipping.
- [ ] Tests verify duplicate finalization does not update quantities twice.
- [ ] Tests verify concurrent allocation cannot reserve the same picked quantities twice.
- [ ] Regression tests confirm existing warehouse features continue to operate correctly.

### Documentation and Review

- [ ] API documentation is updated.
- [ ] Data model documentation is updated.
- [ ] Screen documentation is updated.
- [ ] Shipment verification procedures are documented.
- [ ] Packaging and labeling procedures are documented.
- [ ] Partial shipping authorization rules are documented.
- [ ] Shipping exception procedures are documented.
- [ ] Shipment status transitions are documented.
- [ ] Role permissions are documented.
- [ ] Known limitations and approved deferrals are recorded.
- [ ] Code has been reviewed.
- [ ] Required tests pass.
- [ ] The feature is approved for integration.

---

## Out of Scope

The following activities are not implemented as part of Feature 14.

### Customer Order Entry

Creating Customer Orders, adding original order lines, selecting Customers, and maintaining Quantity Ordered belong to Feature 12.

Feature 14 processes existing Customer Orders with picked quantities available for shipping.

### Customer Master Data Maintenance

Creating, editing, or deactivating Customers is outside Feature 14.

Feature 14 uses existing Customer information for shipment preparation and labeling.

### Individual Item and UPC Maintenance

Creating or editing Individual Items and UPC definitions is outside Feature 14.

Feature 14 uses existing Item and UPC records for verification.

### Picking Customer Orders

Assigning Pickers, generating picking instructions, verifying source bins, recording Picking Movements, and increasing Quantity Picked belong to Feature 13.

Feature 14 uses the results of completed picking operations.

### Inventory Putaway and Replenishment

Receiving products, placing Inventory into storage bins, and replenishing picking locations are outside Feature 14.

Feature 14 does not perform general Inventory movement operations.

### Physical Loading and Delivery

Loading delivery vehicles, assigning delivery routes, transporting Shipments, and confirming Customer delivery are outside the ordinary shipping preparation workflow.

These activities belong to the appropriate delivery feature.

### Delivery Confirmation

Recording Quantity Delivered, delivery timestamps, and proof of delivery is outside Feature 14.

Feature 14 preserves Quantity Shipped and makes completed Shipments available to Feature 15.

### Customer Billing and Payment Processing

Generating invoices, collecting payments, and maintaining billing information are outside Feature 14.

### Advanced Shipping Optimization

Complex load optimization, automated carrier selection, predictive delivery scheduling, and advanced transportation planning are not included unless separately approved.

### Completed Shipment Corrections

Feature 14 prevents completed Shipments from being silently modified.

A separate authorized correction, reversal, or cancellation workflow requires approval.

**[NEEDS CLARIFICATION]** Define the approved correction process for finalized Shipments.

### Offline Shipping

Offline barcode verification, offline Shipment finalization, and synchronization after reconnection are not included in the current draft.

**[NEEDS CLARIFICATION]** Confirm whether offline shipping support is required.

### Automated Label Printing

Feature 14 records labeling completion and associates Shipments with the required delivery information.

Automatic label generation and printer integration require separate confirmation.

**[NEEDS CLARIFICATION]** Confirm whether label printing is required for this feature.

### Final Deferrals and Clarifications

The following decisions remain open for review:

- **[NEEDS CLARIFICATION]** Whether Feature 18 or Feature 15 owns the comparison between Quantity Shipped and Quantity Delivered.
- **[NEEDS CLARIFICATION]** Who authorizes partial shipping and how approval is recorded.
- **[NEEDS CLARIFICATION]** Exact ownership of picked-quantity allocation and reservation.
- **[NEEDS CLARIFICATION]** Concurrency control for simultaneous Shipment allocations.
- **[NEEDS CLARIFICATION]** Customer Order Quantity Shipped update interface.
- **[NEEDS CLARIFICATION]** Customer Order shipping status update mechanism.
- **[NEEDS CLARIFICATION]** Which shipping exceptions are blocking.
- **[NEEDS CLARIFICATION]** Supervisor exception resolution permissions and procedures.
- **[NEEDS CLARIFICATION]** Authorized correction or reversal of completed Shipments.
- **[NEEDS CLARIFICATION]** Shipment cancellation permissions and release of allocated quantities.
- **[NEEDS CLARIFICATION]** Customer delivery information correction procedure.
- **[NEEDS CLARIFICATION]** Offline shipping support.
- **[NEEDS CLARIFICATION]** Barcode scanner and shipping workstation requirements.
- **[NEEDS CLARIFICATION]** Automatic label generation and printer integration.
- **[NEEDS CLARIFICATION]** Final API conventions and audit requirements.

These decisions require review before implementation. They do not prevent Feature 14 from remaining a design draft.
