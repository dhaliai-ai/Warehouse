
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

## Gherkin AC

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
