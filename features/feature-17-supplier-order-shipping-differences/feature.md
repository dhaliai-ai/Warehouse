
# Feature: Report Suppliers That Do Not Ship What Was Ordered

**Feature ID:** 17  
**Branch pattern:** `feature/17-supplier-order-differences`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System provides authorized Managers with a report identifying Supplier Order Lines where the total Quantity Received differs from the Quantity Ordered. The system compares ordered and received quantities in individual units, identifies shortages and overages, displays Supplier and Item information, and preserves receiving discrepancies for review. The report distinguishes finalized supplier delivery differences from orders that are still awaiting additional receipts. It uses the original Units Per Case recorded on the submitted Supplier Order and the actual quantities recorded through completed receiving sessions.

---

## User Stories

### US-17.1: View Supplier Order Differences

**As a** Warehouse Manager  
**I want to** generate a report of Supplier Orders where Quantity Received differs from Quantity Ordered  
**So that** I can identify Suppliers that delivered incorrect quantities.

**Priority:** P1  
**Independent test:** Generate a report containing finalized Supplier Orders with shortages and overages and verify that the differing order lines are displayed.

### US-17.2: Review Supplier Difference Details

**As a** Warehouse Manager  
**I want to** review the Supplier, Purchase Order, Individual Item, Quantity Ordered, Quantity Received, and confirmed receiving discrepancies  
**So that** I can understand each supplier delivery discrepancy and how it was resolved.

**Priority:** P1  
**Independent test:** Review a reported difference and verify that the Supplier, PO Number, Item, ordered quantity, received quantity, difference, and available discrepancy approval information are displayed.

### US-17.3: Distinguish Shortages from Overages

**As a** Warehouse Manager  
**I want to** see whether a Supplier delivered fewer or more units than ordered  
**So that** I can identify the type and size of each discrepancy.

**Priority:** P1  
**Independent test:** Create one finalized shortage and one finalized overage and verify that the report identifies them separately.

### US-17.4: Filter Supplier Difference Report

**As a** Warehouse Manager  
**I want to** filter the report by Supplier, Individual Item, and date range  
**So that** I can investigate particular Suppliers or periods.

**Priority:** P2  
**Independent test:** Apply Supplier and date filters and verify that only matching differences appear.

### US-17.5: Review Incomplete Receiving Separately

**As a** Warehouse Manager  
**I want to** distinguish Supplier Orders still awaiting deliveries from orders with confirmed shortages  
**So that** I do not incorrectly treat an outstanding shipment as a finalized supplier discrepancy.

**Priority:** P2  
**Independent test:** Generate the report while a Supplier Order is Partially Received and verify that it is excluded from finalized differences but can be viewed as a provisional difference.

---

## Functional Requirements

- **FR-001:** The system MUST compare Quantity Ordered with cumulative Quantity Received for Supplier Order Lines.
- **FR-002:** The system MUST identify Supplier Order Lines where Quantity Received differs from Quantity Ordered.
- **FR-003:** The system MUST provide identified differences in a Supplier Difference Report.
- **FR-004:** The report MUST identify the Supplier associated with each Supplier Order.
- **FR-005:** The report MUST identify the Supplier Order by PO Number.
- **FR-006:** The report MUST identify the Individual Item by Item Number and description.
- **FR-007:** The report MUST display Quantity Ordered and Quantity Received for each reported Item.
- **FR-008:** The system MUST preserve Quantity Ordered separately from Quantity Received.
- **FR-009:** The system MUST convert ordered case quantities into individual units before comparing them with received quantities.
- **FR-010:** Ordered Units MUST equal Quantity Ordered Cases multiplied by the Units Per Case recorded on the submitted Supplier Order Line.
- **FR-011:** The system MUST use the Units Per Case snapshot preserved when the Supplier Order was submitted. Subsequent changes to an Item's current packaging configuration MUST NOT change the original Ordered Units used for reporting.
- **FR-012:** The system MUST calculate cumulative Quantity Received from completed Receiving Record Lines associated with the Supplier Order Line.
- **FR-013:** The system MUST count received quantities across multiple completed receiving sessions for the same Supplier Order.
- **FR-014:** The system MUST NOT count the same Receiving Record Line more than once.
- **FR-015:** The system MUST identify a shortage when cumulative Quantity Received is less than Ordered Units on a finalized Supplier Order.
- **FR-016:** The system MUST identify an overage when cumulative Quantity Received is greater than Ordered Units.
- **FR-017:** The system MUST calculate Quantity Difference as Quantity Received minus Ordered Units.
- **FR-018:** The report MUST identify negative differences as Shortages for finalized Supplier Orders.
- **FR-019:** The report MUST identify positive differences as Overages.
- **FR-020:** Supplier Order Lines where Quantity Received equals Ordered Units MUST NOT appear as quantity differences.
- **FR-021:** The system MUST preserve both shortage and overage information.
- **FR-022:** The system MUST report each differing Supplier Order Line separately.
- **FR-023:** The system MUST allow multiple differing Items from one Supplier Order to appear in the report.
- **FR-024:** The system MUST allow differences from multiple Supplier Orders belonging to the same Supplier to appear in the report.
- **FR-025:** The system MUST distinguish finalized Supplier Order differences from provisional differences on incomplete orders.
- **FR-026:** The default Supplier Difference Report MUST include finalized Supplier Orders in Received status.
- **FR-027:** The default report MUST exclude Supplier Orders in Draft, Submitted, Partially Received, or Canceled status from finalized shortage results.
- **FR-028:** The system MUST allow a Manager to optionally include provisional differences from Supplier Orders in Submitted or Partially Received status.
- **FR-029:** Provisional negative differences MUST be clearly identified as Pending Receipt rather than confirmed supplier shortages.
- **FR-030:** The system MUST preserve overages identified during completed receiving sessions even if other lines on the Supplier Order remain incomplete.
- **FR-031:** The report MUST identify the date associated with each finalized Supplier Order difference.
- **FR-032:** For finalized Supplier Orders, the report date MUST be the date the Supplier Order was closed as Received.
- **FR-033:** For provisional differences, the report MUST identify the most recent completed receiving date when one exists. If no receiving session has been completed, the report MUST clearly indicate that no completed receiving date is available.
- **FR-034:** The system MUST allow the report to be filtered by Supplier.
- **FR-035:** The system MUST allow the report to be filtered by Individual Item.
- **FR-036:** The system MUST allow the report to be filtered by date range.
- **FR-037:** The system MUST allow the report to be filtered by difference type: Shortage, Overage, or All.
- **FR-038:** The system MUST allow a Manager to generate the report without selecting a specific Supplier or Item.
- **FR-039:** The system MUST validate that the report start date is not later than the end date.
- **FR-040:** The system MUST display an empty result when no Supplier Order Lines match the selected criteria.
- **FR-041:** The system MUST NOT report matching ordered and received quantities as quantity discrepancies.
- **FR-042:** The system MUST preserve original ordered quantities even when receiving differences are confirmed.
- **FR-043:** The system MUST use receiving information recorded in Feature 10.
- **FR-044:** The system MUST NOT use Quantity Put Away as a substitute for Quantity Received.
- **FR-045:** The system MUST preserve receiving discrepancies independently of subsequent Put Away operations.
- **FR-046:** The system MUST provide access to the associated Supplier Order and receiving information for each reported difference.
- **FR-047:** The system MUST allow authorized Managers to review report results without modifying Supplier Orders or Receiving Records.
- **FR-048:** The Supplier Difference Report MUST be read-only.
- **FR-049:** The system MUST restrict report access to authorized Managers and approved reporting personnel.
- **FR-050:** The system MUST preserve Supplier and Item identification even when those records are later deactivated.
- **FR-051:** The system MUST identify when required historical receiving information is unavailable or incomplete.
- **FR-052:** The system MUST NOT present incomplete historical receiving information as a confirmed zero discrepancy.
- **FR-053:** The system MUST preserve the relationships between Suppliers, Supplier Orders, Supplier Order Lines, Receiving Records, Receiving Record Lines, Receiving Discrepancies, and Individual Items.
- **FR-054:** The system MUST support sorting report results by Supplier, PO Number, Item Number, report date, or difference magnitude.
- **FR-055:** The report MUST display the units used for each quantity so that ordered cases are not confused with received individual units.
- **FR-056:** The system MUST associate finalized Supplier Order differences with the Receiving Discrepancy records maintained in Feature 10 when such records exist.
- **FR-057:** For confirmed receiving discrepancies, the report MUST provide access to the discrepancy type, quantity difference, approving Manager or Supervisor, approval date and time, and recorded notes.
- **FR-058:** The system MUST preserve the distinction between a discrepancy reported by a Receiving Clerk and one approved by an authorized Manager or Supervisor.
- **FR-059:** The system MUST identify the User and date and time associated with final Supplier Order closure when the order is closed with shortages or overages.
- **FR-060:** The system MUST NOT treat a Supplier Order as finalized merely because an individual Receiving Record has been completed.
- **FR-061:** A Supplier Order closed as Received with an approved shortage MUST appear in the finalized Supplier Difference Report even when its Quantity Received is less than Quantity Ordered.
- **FR-062:** The system MUST preserve the actual quantity received when a Case UPC represents a different number of units from the Units Per Case recorded on the submitted Supplier Order Line.
- **FR-063:** The system MUST calculate report differences using the original Ordered Units and actual Received Units without rewriting either value to make the quantities match.
- **FR-064:** The system MUST distinguish quantity discrepancies from packaging mismatches. A packaging mismatch MUST remain available in receiving details even when the actual received units equal Ordered Units.
- **FR-065:** The system MUST identify finalized Supplier Order differences using the Supplier Order status and closure information maintained by Features 9 and 10.

---

## Assumptions

- **A-001:** Feature 5 owns Supplier master data, including Supplier identification and active status.
- **A-002:** Feature 4 owns Individual Item master data, including Item Number and description.
- **A-003:** Feature 9 owns Supplier Orders and Supplier Order Lines, including submitted ordered case quantities and the original Units Per Case snapshot.
- **A-004:** Feature 10 owns Receiving Records, Receiving Record Lines, and Receiving Discrepancies.
- **A-005:** Features 9 and 10 maintain the Supplier Order status and final closure information used to distinguish finalized differences from provisional differences.
- **A-006:** Ordered Units are calculated using the submitted Supplier Order Line's original quantityOrderedCases and unitsPerCase values.
- **A-007:** Received Units are calculated using actual quantities from completed Receiving Record Lines only.
- **A-008:** Multiple completed receiving sessions may contribute to the cumulative Received Units for one Supplier Order Line.
- **A-009:** A completed Receiving Record does not automatically mean the Supplier Order is finalized.
- **A-010:** A Supplier Order in Received status is considered finalized for the default report.
- **A-011:** A Supplier Order in Submitted or Partially Received status may have provisional differences.
- **A-012:** Negative provisional differences are classified as Pending Receipt rather than confirmed shortages.
- **A-013:** A finalized shortage may exist when an authorized Manager or Supervisor approves the shortage and the Supplier Order is closed.
- **A-014:** Packaging mismatches are preserved independently of quantity differences.
- **A-015:** The report is read-only and does not change Supplier Orders, receiving information, or Inventory.
- **A-016:** Historical Supplier and Item references remain available after deactivation.
- **A-017:** Approved reporting personnel have access only to information permitted by their assigned roles.

**[NEEDS CLARIFICATION]** Confirm how provisional records without any completed receiving date should behave when a date-range filter is applied.

**[NEEDS CLARIFICATION]** Confirm whether historical Supplier Order closure records are guaranteed to contain both closedAt and closedBy.

**[NEEDS CLARIFICATION]** Confirm whether finalized report results should include a separate warning when receiving data is incomplete but the Supplier Order status is Received.

---

## Edge Cases

### EC-17.1: Supplier Delivers Fewer Units Than Ordered

A finalized Supplier Order Line contains fewer Received Units than Ordered Units.

The system calculates a negative Difference Units value and identifies the discrepancy as a Shortage.

### EC-17.2: Supplier Delivers More Units Than Ordered

A Supplier Order Line contains more Received Units than Ordered Units.

The system calculates a positive Difference Units value and identifies the discrepancy as an Overage.

### EC-17.3: Supplier Delivers Exactly the Ordered Quantity

Received Units equals Ordered Units.

The system does not include the Supplier Order Line as a quantity discrepancy.

### EC-17.4: Multiple Receiving Sessions

A Supplier Order is received through multiple completed receiving sessions.

The system sums the Received Units from all applicable completed Receiving Record Lines without counting any line twice.

### EC-17.5: Receiving Session Still In Progress

A Receiving Record is In Progress and contains scanned quantities.

The system excludes those quantities from cumulative Received Units until the session is completed.

### EC-17.6: Supplier Order Is Partially Received

A Supplier Order is Partially Received and still awaiting additional deliveries.

The default finalized report excludes its outstanding quantities from confirmed shortages.

If provisional differences are enabled, the system identifies the outstanding quantities as Pending Receipt.

### EC-17.7: Submitted Order With No Completed Receiving

A Supplier Order has been Submitted, but no Receiving Record has been completed.

The default finalized report excludes it.

The provisional report may identify its outstanding ordered quantity, with no completed receiving date available.

### EC-17.8: Approved Shortage and Final Closure

A Supplier Order contains a shortage approved by an authorized Manager or Supervisor.

When the order is closed as Received, the report includes the confirmed shortage and provides access to approval and closure information.

### EC-17.9: Packaging Configuration Changes

An Item's current Units Per Case changes after the Supplier Order is submitted.

The report continues to use the original Units Per Case snapshot rather than the updated packaging configuration.

### EC-17.10: Delivered Case Contains Different Units

A delivered Case UPC represents a different number of units than the original Supplier Order Line.

The report preserves actual Received Units and compares them with original Ordered Units.

It does not alter either quantity to force a match.

### EC-17.11: Packaging Mismatch Without Quantity Difference

The delivered packaging differs from the ordered packaging, but actual Received Units equal Ordered Units.

The system does not report a quantity shortage or overage.

The packaging mismatch remains available through the associated receiving information.

### EC-17.12: Overage on an Incomplete Supplier Order

One Supplier Order Line has an overage while another line remains partially received.

The provisional report identifies the overage and identifies the outstanding quantity on the other line as Pending Receipt.

### EC-17.13: Multiple Differing Items on One Order

A Supplier Order contains multiple Items with quantity differences.

The system displays each differing Supplier Order Line separately.

### EC-17.14: Multiple Orders From One Supplier

A Supplier has several Supplier Orders containing differences.

The system includes all matching order-line discrepancies without combining unrelated Supplier Orders.

### EC-17.15: Invalid Date Range

The selected start date is later than the end date.

The system rejects the filter and requests valid dates.

### EC-17.16: No Matching Differences

No Supplier Order Lines match the selected filters.

The report displays an empty result with a clear message.

### EC-17.17: Historical Receiving Information Is Incomplete

Required historical receiving information is unavailable.

The report identifies the incomplete information and does not present an unverified quantity comparison as a confirmed zero discrepancy.

### EC-17.18: Supplier or Item Is Deactivated

A Supplier or Individual Item is deactivated after receiving activity.

Historical Supplier Order differences remain identifiable in the report.

### EC-17.19: Unauthorized Report Access

A User without reporting permission attempts to generate the Supplier Difference Report.

The system denies access and does not display restricted information.

### EC-17.20: Receiving Discrepancy Is Not Approved

A Receiving Clerk records a discrepancy that has not yet been approved.

The report does not represent that discrepancy as approved and preserves the distinction between reporting and approval.

### EC-17.21: Put Away Quantity Differs From Received Quantity

An Item has been received but has not been fully put away.

The report uses completed receiving quantities rather than Put Away quantities.

### EC-17.22: Repeated Report Generation

A Manager generates the same report multiple times.

The report does not duplicate Receiving Record Lines or change stored quantities.

---

## Success Criteria

- **SC-001:** Authorized Managers can generate a Supplier Difference Report using finalized Supplier Orders.
- **SC-002:** Each reported difference identifies the Supplier, PO Number, Individual Item, Ordered Units, Received Units, and Difference Units.
- **SC-003:** Ordered Units are calculated using the original submitted quantityOrderedCases and unitsPerCase values.
- **SC-004:** Received Units are calculated from completed Receiving Record Lines only.
- **SC-005:** Multiple completed receiving sessions are combined without duplicate counting.
- **SC-006:** Finalized negative differences are correctly identified as Shortages.
- **SC-007:** Positive differences are correctly identified as Overages.
- **SC-008:** Supplier Order Lines with matching quantities are excluded from quantity difference results.
- **SC-009:** The default report includes finalized Supplier Orders in Received status.
- **SC-010:** Incomplete Supplier Orders are excluded from finalized shortage results.
- **SC-011:** Optional provisional reporting identifies outstanding quantities as Pending Receipt.
- **SC-012:** Provisional overages remain distinguishable from pending shortages.
- **SC-013:** Finalized differences use the Supplier Order closure date.
- **SC-014:** Provisional differences display the latest completed receiving date when available.
- **SC-015:** Supplier, Individual Item, date-range, and difference-type filters return matching results.
- **SC-016:** Invalid date ranges are rejected with a clear message.
- **SC-017:** Report results can be sorted by Supplier, PO Number, Item Number, report date, or difference magnitude.
- **SC-018:** Each reported difference provides access to its associated Supplier Order and receiving information.
- **SC-019:** Confirmed receiving discrepancies provide access to approval details and recorded notes.
- **SC-020:** Original ordered quantities and actual received quantities remain unchanged when discrepancies are confirmed.
- **SC-021:** Packaging mismatches remain identifiable without being incorrectly classified as quantity differences.
- **SC-022:** Historical differences remain available after Supplier or Item deactivation.
- **SC-023:** Incomplete historical information is identified rather than silently treated as complete.
- **SC-024:** Unauthorized Users cannot access restricted report information.
- **SC-025:** Generating the report does not modify Supplier Orders, Receiving Records, Receiving Discrepancies, or Inventory.
- **SC-026:** All 31 original Gherkin Acceptance Criteria have corresponding tests.

---

## Key Entities

### Supplier Difference Report

Represents a read-only reporting view of differences between quantities ordered from Suppliers and quantities received by the warehouse.

The report distinguishes finalized shortages and overages from provisional differences on orders awaiting further deliveries.

### Supplier

Represents the company supplying products to the warehouse.

Supplier information is maintained in Feature 5.

### Supplier Order

Represents a purchase order placed with a Supplier.

Supplier Order creation is defined in Feature 9.

Its status and closure information determine whether a quantity difference is finalized or provisional.

### Supplier Order Line

Represents an Individual Item ordered from a Supplier, including ordered case quantity, original Units Per Case, and cumulative received units.

### Receiving Record

Represents a receiving session for a Supplier Order.

Receiving is defined in Feature 10.

Completion of a Receiving Record does not necessarily finalize the associated Supplier Order.

### Receiving Record Line

Represents the quantity of an Individual Item recorded during a receiving session.

Only completed Receiving Record Lines contribute to cumulative Quantity Received.

### Receiving Discrepancy

Represents a recorded receiving difference or packaging issue, including the discrepancy type, quantity difference, approval information, and notes.

Receiving discrepancy approval is defined in Feature 10.

### Individual Item

Represents a product purchased from a Supplier.

### User

Represents an authorized Manager or reporting employee.

Managers and Supervisors may also be associated with receiving discrepancy approval and Supplier Order closure.

---

## Initial Data Model

### Supplier Difference Report

The Supplier Difference Report is a generated reporting view rather than a separate business transaction.

**Report Parameters:**

| Parameter | Type | Description |
|---|---|---|
| supplierId | Integer | Optional Supplier filter |
| itemId | Integer | Optional Individual Item filter |
| startDate | Date | Optional start date |
| endDate | Date | Optional end date |
| differenceType | String | All, Shortage, or Overage |
| includeProvisional | Boolean | Whether incomplete orders are included |

**Displayed Information:**

| Field | Description |
|---|---|
| Supplier | Supplier name and number |
| PO Number | Supplier Order reference |
| Item Number | Individual Item SKU |
| Item Description | Description of the Item |
| Quantity Ordered Cases | Original quantity ordered in cases |
| Units Per Case | Units per case preserved on the submitted Supplier Order |
| Quantity Ordered Units | Ordered cases multiplied by original Units Per Case |
| Quantity Received Units | Cumulative quantity received from completed Receiving Records |
| Difference Units | Received Units minus Ordered Units |
| Difference Type | Shortage, Overage, or Pending Receipt |
| Supplier Order Status | Current Supplier Order status |
| Report Date | Finalization date or latest completed receiving date |
| Receiving Discrepancy | Associated confirmed discrepancy information, when available |
| Approved By | Manager or Supervisor who approved the discrepancy, when applicable |
| Approved At | Date and time of discrepancy approval, when applicable |
| Closed By | User who authorized final Supplier Order closure, when applicable |
| Closed At | Date and time of final Supplier Order closure, when applicable |

**Relationships:**
- The report uses Supplier Order Lines and completed Receiving Record Lines.
- The report identifies Suppliers and Individual Items associated with differences.
- Each report row represents one Supplier Order Line with a qualifying quantity difference.
- Report rows may reference associated Receiving Discrepancy records.
- The report does not create or modify Supplier Orders, Receiving Records, or Receiving Discrepancies.

### Supplier

| Attribute | Type | Description |
|---|---|---|
| supplierId | Integer | Unique Supplier identifier |
| supplierNumber | String | Unique internal Supplier Number |
| name | String | Supplier name |
| isActive | Boolean | Indicates whether the Supplier is active |

**Relationships:**
- A Supplier may have multiple Supplier Orders.
- A Supplier may appear in multiple report rows.

### Supplier Order

| Attribute | Type | Description |
|---|---|---|
| supplierOrderId | Integer | Unique Supplier Order identifier |
| poNumber | String | Unique Purchase Order Number |
| supplierId | Integer | Foreign key referencing Supplier |
| warehouseId | Integer | Destination Warehouse recorded on the Supplier Order |
| status | String | Draft, Submitted, Partially Received, Received, or Canceled |
| createdAt | DateTime | Date and time the order was created |
| submittedAt | DateTime | Date and time the order was submitted |
| closedAt | DateTime | Date and time receiving was finalized |
| closedBy | Integer | User who authorized final closure, when applicable |

**Relationships:**
- Each Supplier Order belongs to one Supplier.
- Each Supplier Order is associated with one destination Warehouse.
- Each Supplier Order contains one or more Supplier Order Lines.
- Each Supplier Order may have multiple Receiving Records.
- A finalized Supplier Order may contain confirmed shortages or overages.

**Constraints:**
- The Supplier Order must be in Received status to appear in the default finalized report.
- Completing an individual Receiving Record does not automatically finalize the Supplier Order.
- Original ordered quantities remain preserved after submission.

### Supplier Order Line

| Attribute | Type | Description |
|---|---|---|
| supplierOrderLineId | Integer | Unique Supplier Order Line identifier |
| supplierOrderId | Integer | Foreign key referencing Supplier Order |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityOrderedCases | Integer | Original ordered quantity in cases |
| unitsPerCase | Integer | Units Per Case snapshot preserved at submission |
| quantityReceivedUnits | Integer | Cumulative received quantity in individual units |

**Relationships:**
- Each Supplier Order Line belongs to one Supplier Order.
- Each Supplier Order Line references one Individual Item.
- Receiving Record Lines reference Supplier Order Lines.

**Derived Values:**
- Ordered Units = quantityOrderedCases × unitsPerCase.
- Received Units = Sum of completed Receiving Record Line quantities for this Supplier Order Line.
- Difference Units = Received Units - Ordered Units.
- Shortage Units = max(0, Ordered Units - Received Units).
- Overage Units = max(0, Received Units - Ordered Units).

**Constraints:**
- quantityOrderedCases must be positive.
- unitsPerCase must be positive.
- quantityReceivedUnits cannot be negative.
- Original ordered quantities and Units Per Case remain preserved after submission.
- A completed Receiving Record Line must not be counted more than once.

### Receiving Record

| Attribute | Type | Description |
|---|---|---|
| receivingRecordId | Integer | Unique Receiving Record identifier |
| supplierOrderId | Integer | Foreign key referencing Supplier Order |
| warehouseId | Integer | Foreign key referencing Warehouse |
| receivingDoorId | Integer | Receiving Door where the shipment was unloaded |
| receivedBy | Integer | User who performed receiving |
| completedAt | DateTime | Date and time receiving session completed |
| status | String | In Progress or Completed |

**Relationships:**
- Each Receiving Record belongs to one Supplier Order.
- Each Receiving Record contains one or more Receiving Record Lines.
- A Supplier Order may have multiple Receiving Records.
- A Receiving Record may have Receiving Discrepancies.

**Constraints:**
- Only completed Receiving Record Lines contribute to report totals.
- A Receiving Record may be Completed while its Supplier Order remains Partially Received.

### Receiving Record Line

| Attribute | Type | Description |
|---|---|---|
| receivingRecordLineId | Integer | Unique Receiving Record Line identifier |
| receivingRecordId | Integer | Foreign key referencing Receiving Record |
| supplierOrderLineId | Integer | Foreign key referencing Supplier Order Line |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityReceivedUnits | Integer | Actual quantity received in individual units |

**Relationships:**
- Each Receiving Record Line belongs to one Receiving Record.
- Each Receiving Record Line references one Supplier Order Line.
- Completed Receiving Record Lines contribute to cumulative Quantity Received.

**Constraints:**
- quantityReceivedUnits cannot be negative.
- A Receiving Record Line must not be counted more than once in report totals.
- The actual received quantity must be preserved when packaging differs from the original order.

### Receiving Discrepancy

| Attribute | Type | Description |
|---|---|---|
| discrepancyId | Integer | Unique Receiving Discrepancy identifier |
| receivingRecordId | Integer | Foreign key referencing Receiving Record |
| supplierOrderLineId | Integer | Foreign key referencing Supplier Order Line, when applicable |
| quantityDifferenceUnits | Integer | Difference associated with the recorded discrepancy |
| discrepancyType | String | Shortage, Overage, Unexpected Item, or Packaging Mismatch |
| confirmedBy | Integer | Manager or Supervisor who approved the discrepancy |
| confirmedAt | DateTime | Date and time of approval |
| notes | String | Explanation or resolution of discrepancy |

**Relationships:**
- Each Receiving Discrepancy belongs to a Receiving Record.
- Each Receiving Discrepancy may reference a Supplier Order Line.
- Each confirmed discrepancy identifies the approving User.
- Receiving Discrepancies are created and approved through Feature 10.
- The Supplier Difference Report references these records without modifying them.

**Constraints:**
- Unapproved discrepancies must not be presented as approved.
- A packaging mismatch does not automatically imply a quantity shortage or overage.
- A Receiving Discrepancy must not replace the original ordered or actual received quantities.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |

**Relationships:**
- An Individual Item may appear on multiple Supplier Order Lines.
- An Individual Item may appear in multiple Supplier Difference Report rows.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Authorized Managers generate and review Supplier Difference Reports.
- Authorized Managers or Supervisors approve receiving discrepancies.
- Authorized Managers or Supervisors may authorize final Supplier Order closure.

---

## Gherkin AC

### US-17.1: View Supplier Order Differences

#### AC-17.1.1: Supplier delivered less than ordered

**Given** a finalized Supplier Order Line contains 10 cases ordered  
**And** each case contains 12 individual units  
**And** completed receiving sessions recorded 100 units received  
**When** the Manager generates the Supplier Difference Report  
**Then** the system displays 120 Ordered Units  
**And** 100 Received Units  
**And** identifies a Shortage of 20 units.

#### AC-17.1.2: Supplier delivered more than ordered

**Given** a finalized Supplier Order Line contains 5 cases ordered  
**And** each case contains 10 individual units  
**And** completed receiving sessions recorded 60 units received  
**When** the Manager generates the Supplier Difference Report  
**Then** the system displays 50 Ordered Units  
**And** 60 Received Units  
**And** identifies an Overage of 10 units.

#### AC-17.1.3: Supplier delivered the ordered quantity

**Given** a finalized Supplier Order Line contains 4 cases ordered  
**And** each case contains 12 units  
**And** completed receiving sessions recorded 48 units received  
**When** the Manager generates the Supplier Difference Report  
**Then** the system does not identify that Supplier Order Line as a quantity difference.

#### AC-17.1.4: No Supplier differences exist

**Given** all applicable finalized Supplier Order Lines have matching Ordered Units and Received Units  
**When** the Manager generates the Supplier Difference Report  
**Then** the report contains no supplier quantity differences  
**And** displays a message indicating that no matching discrepancies were found.

#### AC-17.1.5: Receiving is incomplete

**Given** a Supplier Order is in Partially Received status  
**And** the received quantity is less than the ordered quantity  
**When** the Manager generates the default finalized difference report  
**Then** the system excludes the incomplete order from finalized shortage results.

#### AC-17.1.6: Include provisional difference

**Given** a Supplier Order is in Partially Received status  
**And** its ordered quantity exceeds the cumulative received quantity  
**When** the Manager enables provisional differences  
**Then** the system displays the outstanding quantity  
**And** identifies it as Pending Receipt rather than a confirmed shortage.

### US-17.2: Review Supplier Difference Details

#### AC-17.2.1: Display Supplier difference details

**Given** a finalized Supplier Order Line has a quantity difference  
**When** the Manager reviews the reported difference  
**Then** the report identifies the Supplier and PO Number  
**And** identifies the Individual Item  
**And** displays Quantity Ordered Cases, Ordered Units, Received Units, and Difference Units  
**And** provides access to associated confirmed receiving discrepancy details when available.

#### AC-17.2.2: Report multiple differing Items

**Given** a finalized Supplier Order contains three Items  
**And** two Items have quantity differences  
**And** one Item has matching ordered and received quantities  
**When** the Manager generates the report  
**Then** the system displays the two differing Items  
**And** excludes the matching Item.

#### AC-17.2.3: Report multiple orders from one Supplier

**Given** Supplier A has two finalized Supplier Orders  
**And** both orders contain quantity differences  
**When** the Manager generates the report  
**Then** the report includes the applicable differences from both Supplier Orders.

#### AC-17.2.4: Count multiple receiving sessions

**Given** a Supplier Order Line contains 100 Ordered Units  
**And** the first completed Receiving Record contains 40 units  
**And** the second completed Receiving Record contains 60 units  
**When** the Manager generates the finalized Supplier Difference Report  
**Then** the system calculates 100 Received Units  
**And** does not identify a quantity difference.

#### AC-17.2.5: Exclude Put Away quantity from comparison

**Given** a Supplier Order Line contains 100 Ordered Units  
**And** receiving recorded 100 units  
**And** only 70 units have been put away into storage bins  
**When** the Manager generates the Supplier Difference Report  
**Then** the system compares 100 Ordered Units with 100 Received Units  
**And** does not report a supplier delivery shortage.

#### AC-17.2.6: Display discrepancy approval information

**Given** a finalized Supplier Order contains a confirmed shortage of 12 units  
**And** an authorized Supervisor approved the shortage during receiving  
**And** the Receiving Discrepancy contains the approving User and approval date and time  
**When** the Manager reviews the reported shortage  
**Then** the system displays the Shortage of 12 units  
**And** provides access to the approving Supervisor  
**And** provides access to the approval date and time  
**And** displays the recorded discrepancy notes when available.

#### AC-17.2.7: Preserve historical Units Per Case

**Given** a submitted Supplier Order Line contains 5 cases ordered  
**And** the original Units Per Case is 12  
**And** the Item's current Units Per Case is later changed to 10  
**And** completed receiving sessions recorded 50 units received  
**And** the Supplier Order has been finalized  
**When** the Manager generates the Supplier Difference Report  
**Then** the system calculates 60 Ordered Units using the original Units Per Case  
**And** displays 50 Received Units  
**And** identifies a Shortage of 10 units  
**And** does not recalculate the original order using the Item's current packaging configuration.

### US-17.3: Distinguish Shortages from Overages

#### AC-17.3.1: Identify shortage

**Given** a finalized Supplier Order Line has 100 Ordered Units  
**And** 80 Received Units  
**When** the Manager reviews the report  
**Then** the system identifies a Shortage  
**And** displays Difference Units as -20.

#### AC-17.3.2: Identify overage

**Given** a finalized Supplier Order Line has 100 Ordered Units  
**And** 115 Received Units  
**When** the Manager reviews the report  
**Then** the system identifies an Overage  
**And** displays Difference Units as +15.

#### AC-17.3.3: Preserve original ordered quantity

**Given** a Supplier Order Line originally contained 100 Ordered Units  
**And** 90 units were received  
**When** the Supplier Order is finalized with a confirmed shortage  
**Then** the system preserves 100 Ordered Units  
**And** records 90 Received Units  
**And** reports a shortage of 10 units.

#### AC-17.3.4: Finalize Supplier Order with an approved shortage

**Given** a Supplier Order contains 120 Ordered Units  
**And** completed receiving sessions recorded only 80 Received Units  
**And** a Receiving Clerk reported the shortage  
**And** an authorized Manager approved the shortage  
**And** the Manager confirmed that no further deliveries are expected  
**When** the Manager closes the Supplier Order as Received  
**Then** the system preserves 120 Ordered Units  
**And** preserves 80 actual Received Units  
**And** records the closing User and closing date and time  
**And** the finalized Supplier Difference Report identifies a Shortage of 40 units  
**And** provides access to the confirmed discrepancy approval information.

#### AC-17.3.5: Distinguish packaging mismatch from quantity difference

**Given** a submitted Supplier Order Line contains 5 cases ordered  
**And** the original Units Per Case is 12  
**And** the delivered Case UPC represents 10 units per case  
**And** the receiving worker scans 6 delivered cases  
**And** completed receiving records contain 60 actual received units  
**And** the packaging mismatch has been recorded and approved  
**And** the Supplier Order has been finalized  
**When** the Manager generates the Supplier Difference Report  
**Then** the system calculates 60 Ordered Units  
**And** calculates 60 Received Units  
**And** does not report a quantity shortage or overage for the line  
**And** preserves the packaging mismatch in the associated receiving information.

### US-17.4: Filter Supplier Difference Report

#### AC-17.4.1: Filter by Supplier

**Given** differences exist for Supplier A and Supplier B  
**When** the Manager filters the report to Supplier A  
**Then** the system displays only applicable differences from Supplier A.

#### AC-17.4.2: Filter by Individual Item

**Given** differences exist for Item A and Item B  
**When** the Manager filters the report to Item A  
**Then** the system displays only applicable differences involving Item A.

#### AC-17.4.3: Filter by date range

**Given** finalized supplier differences exist inside and outside a selected period  
**When** the Manager selects a valid date range  
**Then** the report includes differences with finalization dates inside the selected period  
**And** excludes differences finalized outside that period.

#### AC-17.4.4: Filter by difference type

**Given** the report contains both shortages and overages  
**When** the Manager selects the Shortage filter  
**Then** the report displays only shortage differences.

#### AC-17.4.5: Reject invalid date range

**Given** the Manager is selecting report dates  
**When** the start date is later than the end date  
**Then** the system rejects the date range  
**And** requests valid dates.

#### AC-17.4.6: No matching differences

**Given** no Supplier Order Lines match the selected filters  
**When** the Manager generates the report  
**Then** the system displays an empty result  
**And** indicates that no matching differences were found.

### US-17.5: Review Incomplete Receiving Separately

#### AC-17.5.1: Submitted order with no receiving

**Given** a Supplier Order has been Submitted  
**And** no Receiving Records have been completed  
**When** the Manager generates the default finalized report  
**Then** the system excludes the order from finalized shortage results.

#### AC-17.5.2: Provisional outstanding quantity

**Given** a Partially Received Supplier Order contains 120 Ordered Units  
**And** 80 units have been received  
**When** the Manager includes provisional differences  
**Then** the report displays 40 units as Pending Receipt  
**And** does not label the difference as a confirmed shortage.

#### AC-17.5.3: Finalized shortage after order closure

**Given** a Supplier Order contains 120 Ordered Units  
**And** only 80 units have been received  
**And** an authorized Manager or Supervisor has approved the shortage  
**And** the Supplier Order is finalized as Received with the closing User and date and time recorded  
**When** the Manager generates the default Supplier Difference Report  
**Then** the system reports a finalized Shortage of 40 units  
**And** provides access to the recorded approval and closure information.

#### AC-17.5.4: Reject unauthorized report access

**Given** a User is authenticated as a Driver without reporting permission  
**When** the User attempts to generate the Supplier Difference Report  
**Then** the system denies access  
**And** does not display restricted Supplier information.

#### AC-17.5.5: Do not finalize an order after one receiving session

**Given** a Supplier Order contains 100 Ordered Units  
**And** a completed Receiving Record contains 60 Received Units  
**And** additional deliveries are expected  
**And** the Supplier Order remains Partially Received  
**When** the Manager generates the default finalized Supplier Difference Report  
**Then** the system excludes the outstanding 40 units from finalized shortage results  
**And** does not treat completion of the Receiving Record as final Supplier Order closure.

#### AC-17.5.6: Exclude an uncompleted receiving session

**Given** a Supplier Order Line contains 100 Ordered Units  
**And** a completed Receiving Record contains 40 units  
**And** another Receiving Record is In Progress with 30 scanned units  
**When** the Manager includes provisional differences  
**Then** the system calculates 40 cumulative Received Units from completed sessions  
**And** does not count the 30 units in the In Progress session  
**And** identifies 60 units as Pending Receipt.

#### AC-17.5.7: Preserve overage on a partially received order

**Given** a Supplier Order contains Item A and Item B  
**And** Item A has 50 Ordered Units and 60 Received Units  
**And** Item B has 100 Ordered Units and 40 Received Units  
**And** the Supplier Order remains Partially Received  
**When** the Manager includes provisional differences  
**Then** the system identifies Item A as having a provisional Overage of 10 units  
**And** identifies Item B as having 60 units Pending Receipt  
**And** does not report Item B's outstanding quantity as a finalized shortage.

---

## Data Ownership

### Supplier Data

**Owning Feature:** Feature 5 - Maintain Suppliers

Feature 5 owns Supplier master data, including:

- Supplier ID
- Supplier Number
- Supplier Name
- Supplier active or inactive status

Feature 17 reads Supplier information to identify the Supplier associated with each reported difference.

Feature 17 MUST NOT create, update, deactivate, or delete Supplier records.

Historical Supplier identification MUST remain available after deactivation.

### Individual Item Data

**Owning Feature:** Feature 4 - Maintain Individual Items

Feature 4 owns Individual Item master data, including:

- Item ID
- Item Number
- Item Description
- Item packaging configuration

Feature 17 reads Item information to identify the products involved in Supplier Order differences.

Feature 17 MUST NOT modify Individual Item master data.

Changes to current Item packaging MUST NOT alter the original Units Per Case recorded on submitted Supplier Order Lines.

### Supplier Order Data

**Owning Feature:** Feature 9 - Create Supplier Order

Feature 9 owns Supplier Order and Supplier Order Line information, including:

- Supplier Order ID
- PO Number
- Supplier ID
- Warehouse ID
- Supplier Order status
- Quantity Ordered Cases
- Original Units Per Case snapshot
- Supplier Order submission information

Supplier Order status and closure information are maintained through the workflows defined by Features 9 and 10.

Feature 17 reads these records to calculate Ordered Units and determine whether a discrepancy is finalized or provisional.

Feature 17 MUST NOT modify original ordered quantities, Supplier Order status, or closure information.

### Receiving Data

**Owning Feature:** Feature 10 - Receive Supplier Order

Feature 10 owns receiving information, including:

- Receiving Record ID
- Receiving Record Line ID
- Supplier Order Line reference
- Actual Quantity Received Units
- Receiving session status
- Receiving completion timestamp
- Receiving Discrepancy information
- Discrepancy approval information

Feature 17 calculates cumulative Received Units using completed Receiving Record Lines.

Feature 17 MUST NOT modify Receiving Records, Receiving Record Lines, or Receiving Discrepancies.

### Receiving Discrepancy Approval Data

**Owning Feature:** Feature 10 - Receive Supplier Order

Feature 10 records the distinction between a discrepancy reported by a Receiving Clerk and one approved by an authorized Manager or Supervisor.

Feature 17 reads:

- Discrepancy Type
- Quantity Difference
- Approval Status
- Approving User
- Approval Date and Time
- Discrepancy Notes

Feature 17 MUST NOT approve, reject, or change receiving discrepancies.

### Supplier Difference Report

**Owning Feature:** Feature 17 - Report Suppliers That Do Not Ship What Was Ordered

Feature 17 owns:

- Report filtering logic
- Ordered Units calculations
- Cumulative Received Units calculations
- Difference calculations
- Finalized and provisional classification
- Report sorting
- Read-only presentation of discrepancies

The Supplier Difference Report is a generated reporting view rather than a separate business transaction.

Feature 17 MUST NOT overwrite data owned by Features 4, 5, 9, or 10.

### User and Authorization Data

**Owning Component:** Shared User and Access Control functionality

The shared authorization component owns:

- User accounts
- User roles
- Reporting permissions
- Authentication information

Feature 17 checks whether a User is authorized to generate or review the report.

Feature 17 MUST NOT modify User accounts or permissions.

### Data Ownership Rules

- Feature 4 owns Individual Item master data.
- Feature 5 owns Supplier master data.
- Feature 9 owns Supplier Orders and original ordered quantities.
- Feature 10 owns Receiving Records and Receiving Discrepancies.
- Features 9 and 10 provide Supplier Order closure information.
- Feature 17 owns Supplier Difference Report calculations and presentation.
- Shared authorization functionality owns User access permissions.
- Feature 17 MUST preserve relationships to the original source records.
- Feature 17 MUST remain read-only.

**[NEEDS CLARIFICATION]** Confirm which service owns the final transition of a Supplier Order to Received status and the associated closedAt and closedBy values.

---

## API Requirements

The following endpoints are proposed for Feature 17.

The final endpoint names, request formats, and response structures must follow the Warehouse Management System's established API conventions.

### API-17.1: Generate Supplier Difference Report

**Method:** GET

**Proposed Endpoint:**

`/api/reports/supplier-differences`

**Purpose:**

Generate a read-only report comparing original Ordered Units with cumulative Received Units for Supplier Order Lines.

**Query Parameters:**

| Parameter | Type | Required | Description |
|---|---|---|---|
| supplierId | Integer | No | Filter by Supplier |
| itemId | Integer | No | Filter by Individual Item |
| startDate | Date | No | Beginning of reporting period |
| endDate | Date | No | End of reporting period |
| differenceType | String | No | All, Shortage, or Overage |
| includeProvisional | Boolean | No | Include incomplete Supplier Orders; default false |
| sortBy | String | No | Supplier, PO Number, Item Number, Report Date, or Difference Magnitude |

**Expected Response Information:**

- Supplier ID
- Supplier Number
- Supplier Name
- Supplier Order ID
- PO Number
- Supplier Order Line ID
- Item ID
- Item Number
- Item Description
- Quantity Ordered Cases
- Original Units Per Case
- Ordered Units
- Cumulative Received Units
- Difference Units
- Difference Type
- Supplier Order Status
- Report Date
- Provisional or Finalized indicator
- Related Receiving Discrepancy references
- Approval information when available
- Supplier Order closure information when available
- Historical data completeness warning when applicable

**Calculation Rules:**

Ordered Units = Quantity Ordered Cases × Original Units Per Case

Received Units = Sum of quantityReceivedUnits from completed Receiving Record Lines associated with the Supplier Order Line

Difference Units = Received Units - Ordered Units

For finalized Supplier Orders:

- Negative difference = Shortage
- Positive difference = Overage
- Zero difference = No quantity discrepancy

For incomplete Supplier Orders:

- Negative difference = Pending Receipt
- Positive difference = Provisional Overage
- Zero difference = No quantity discrepancy

**Validation Rules:**

- The requesting User must have reporting permission.
- Supplier and Item filters must reference valid records.
- The start date must not be later than the end date.
- The difference type must be supported.
- The sort field must be supported.
- Only authorized information may be returned.
- In Progress Receiving Record Lines must not contribute to Received Units.
- A Receiving Record Line must not be counted more than once.
- Finalized differences must be determined using Supplier Order status and closure information.

**Possible Responses:**

- `200 OK` - Report generated successfully, including empty results.
- `400 Bad Request` - Invalid report filters.
- `401 Unauthorized` - User is not authenticated.
- `403 Forbidden` - User lacks reporting permission.
- `500 Internal Server Error` - Unexpected server failure.

**[NEEDS CLARIFICATION]** Confirm how the date filter should treat provisional Supplier Orders with no completed receiving date.

### API-17.2: Retrieve Supplier Difference Details

**Method:** GET

**Proposed Endpoint:**

`/api/reports/supplier-differences/{supplierOrderLineId}`

**Purpose:**

Retrieve detailed information for a Supplier Order Line appearing in the report.

**Path Parameter:**

- `supplierOrderLineId` - Unique identifier of the Supplier Order Line.

**Expected Response Information:**

- Supplier identification
- PO Number
- Supplier Order status
- Supplier Order Line identification
- Individual Item identification
- Original Quantity Ordered Cases
- Original Units Per Case
- Calculated Ordered Units
- Cumulative Received Units
- Difference Units
- Difference Type
- Related Receiving Record references
- Receiving Discrepancy details
- Approving Manager or Supervisor
- Approval date and time
- Discrepancy notes
- Supplier Order closure User
- Supplier Order closure date and time

**Validation Rules:**

- The requesting User must have reporting permission.
- The Supplier Order Line must exist.
- The User must be authorized to view the information.
- The endpoint must not modify Supplier Order or receiving information.

**Possible Responses:**

- `200 OK` - Details returned.
- `401 Unauthorized` - User is not authenticated.
- `403 Forbidden` - User lacks permission.
- `404 Not Found` - Requested record is unavailable.

### API-17.3: Retrieve Related Receiving Information

**Method:** GET

**Proposed Endpoint:**

`/api/reports/supplier-differences/{supplierOrderLineId}/receiving`

**Purpose:**

Allow an authorized Manager to review completed receiving activity and associated discrepancies contributing to a reported difference.

**Expected Response Information:**

- Receiving Record ID
- Receiving Record status
- Receiving completion date and time
- Receiving Record Line ID
- Actual Quantity Received Units
- Receiving User
- Receiving Discrepancy ID
- Discrepancy Type
- Discrepancy Quantity Difference
- Discrepancy approval status
- Approving User, when applicable
- Approval date and time, when applicable
- Recorded notes, when available

**Processing Rules:**

- Completed receiving quantities must be clearly distinguished from In Progress quantities.
- The same Receiving Record Line must not be counted more than once.
- Unapproved discrepancies must not be represented as approved.
- Packaging mismatches must remain visible even when no quantity difference exists.
- The endpoint must not modify receiving records.

### API Security Requirements

- All endpoints MUST require authentication.
- Reporting permission MUST be enforced on the server.
- Unauthorized Users MUST NOT receive restricted Supplier information.
- Drivers without reporting permission MUST be denied access.
- Report endpoints MUST be read-only.
- Report generation MUST NOT modify Supplier Orders, Receiving Records, Receiving Discrepancies, or Inventory.
- Source record references MUST remain traceable.

---

## Screen Requirements

### SCREEN-17.1: Supplier Difference Report Screen

**Purpose:**

Allow authorized Managers to review quantity differences between Supplier Orders and completed receiving activity.

**Authorized Users:**

- Warehouse Managers
- Approved reporting personnel

**Screen Elements:**

- Page title: Supplier Difference Report
- Supplier filter
- Individual Item filter
- Start Date filter
- End Date filter
- Difference Type filter
- Include Provisional Differences checkbox
- Sort By selection
- Generate Report button
- Clear Filters button
- Results table
- Empty-results message
- Historical data warning, when applicable

**Results Table Columns:**

| Column | Description |
|---|---|
| Supplier | Supplier Name or Number |
| PO Number | Supplier Order reference |
| Item Number | Individual Item SKU |
| Item Description | Individual Item description |
| Ordered Cases | Original ordered case quantity |
| Units Per Case | Original Units Per Case snapshot |
| Ordered Units | Calculated original ordered quantity |
| Received Units | Actual cumulative received quantity |
| Difference Units | Received Units minus Ordered Units |
| Difference Type | Shortage, Overage, or Pending Receipt |
| Order Status | Supplier Order status |
| Report Date | Closure date or latest completed receiving date |
| Details | Read-only access to discrepancy information |

**Screen Behavior:**

1. The Manager opens the Supplier Difference Report from the reporting menu.
2. The system displays the report filters.
3. The Manager optionally selects a Supplier.
4. The Manager optionally selects an Individual Item.
5. The Manager optionally selects a date range.
6. The Manager selects a Difference Type or All.
7. The Manager may enable Include Provisional Differences.
8. The Manager optionally selects a sorting method.
9. The Manager selects Generate Report.
10. The system validates the filters.
11. The system retrieves qualifying Supplier Order Lines.
12. The system calculates Ordered Units, Received Units, and Difference Units.
13. The system displays the matching report rows.
14. The Manager may select a row to review its details.

**Default Behavior:**

- Include Provisional Differences is disabled.
- The report includes finalized Supplier Orders in Received status.
- Incomplete Supplier Orders are excluded from finalized shortage results.
- Matching quantities do not appear as quantity discrepancies.
- The report remains read-only.

**Validation:**

- Start Date must not be later than End Date.
- Supplier and Item filters must reference valid records.
- Invalid filters must display clear messages.
- No matching differences must display an empty-results message.
- Incomplete historical information must display a warning.

### SCREEN-17.2: Supplier Difference Details Screen

**Purpose:**

Allow a Manager to review the quantities and receiving information associated with one reported Supplier Order Line.

**Displayed Information:**

- Supplier Number
- Supplier Name
- PO Number
- Supplier Order Status
- Supplier Order Line ID
- Item Number
- Item Description
- Quantity Ordered Cases
- Original Units Per Case
- Ordered Units
- Received Units
- Difference Units
- Difference Type
- Report Date
- Finalized or Provisional status
- Supplier Order closure information, when available

**Receiving Details:**

- Completed Receiving Record references
- Receiving completion dates
- Actual received quantities
- Receiving Discrepancy references
- Discrepancy Type
- Discrepancy approval status
- Approving Manager or Supervisor
- Approval date and time
- Discrepancy notes
- Packaging mismatch information, when applicable

**Screen Behavior:**

1. The Manager selects a Supplier Order Line from the report.
2. The system retrieves the associated Supplier Order information.
3. The system displays the original ordered quantities.
4. The system displays cumulative quantities from completed receiving sessions.
5. The system displays the calculated difference.
6. The system identifies the difference as finalized or provisional.
7. The system provides access to associated receiving information.
8. The Manager may return to the report.
9. No edit, approve, or delete actions are available.

### SCREEN-17.3: Empty Results and Data Quality Messages

**Purpose:**

Provide clear feedback when no differences match the report filters or historical information is incomplete.

**Required Messages:**

When no matching differences exist:

`No matching supplier quantity differences were found.`

When the selected date range is invalid:

`Start Date must not be later than End Date.`

When historical receiving information is incomplete:

`Some historical receiving information is unavailable or incomplete. Report results may not include all supplier differences.`

When a provisional shortage is displayed:

`Pending Receipt - additional Supplier deliveries may still be expected.`

When a User lacks permission:

`You do not have permission to view this report.`

### Screen Design Requirements

- Follow the Warehouse Management System's established UI style.
- Use consistent labels for Supplier, PO Number, and Item identification.
- Clearly distinguish cases from individual units.
- Clearly distinguish Shortage, Overage, and Pending Receipt.
- Display negative differences with a minus sign.
- Display positive differences with a plus sign where appropriate.
- Clearly identify provisional report rows.
- Preserve access to historical Supplier and Item identification.
- Display discrepancy approval information without allowing modifications.
- Use consistent date and time formatting.
- Support readable tables containing multiple Supplier Orders and Items.
- Do not require printed reports or paper-based processing.

**[NEEDS CLARIFICATION]** Confirm final Figma screen layouts, navigation placement, and detailed table presentation.

---

## Definition of Done

Feature 17 is considered complete when all the following conditions are satisfied.

### Requirements

- [ ] All Functional Requirements FR-001 through FR-065 are implemented or explicitly deferred.
- [ ] All User Stories US-17.1 through US-17.5 are supported.
- [ ] All 31 Gherkin Acceptance Criteria have corresponding tests.
- [ ] All clarification items have been reviewed.
- [ ] The implementation follows the approved requirements.

### Data Model

- [ ] Supplier Order Lines preserve original Quantity Ordered Cases.
- [ ] Supplier Order Lines preserve the original Units Per Case snapshot.
- [ ] Receiving Record Lines preserve actual Received Units.
- [ ] Completed Receiving Record Lines can be associated with Supplier Order Lines.
- [ ] Supplier Order closure information is available.
- [ ] Receiving Discrepancy approval information is available.
- [ ] Historical Supplier and Item identification is preserved.
- [ ] Source record relationships are maintained.

### Business Logic

- [ ] Ordered Units are calculated correctly.
- [ ] Received Units are calculated from completed receiving sessions only.
- [ ] Multiple receiving sessions are combined correctly.
- [ ] Receiving Record Lines are not counted more than once.
- [ ] Negative finalized differences are classified as Shortages.
- [ ] Positive differences are classified as Overages.
- [ ] Matching quantities are excluded from discrepancy results.
- [ ] Incomplete Supplier Orders are excluded from default finalized shortage results.
- [ ] Provisional negative differences are identified as Pending Receipt.
- [ ] Provisional overages are distinguished from finalized overages.
- [ ] Original ordered quantities are preserved after receiving discrepancies.
- [ ] Packaging mismatches do not automatically create quantity differences.
- [ ] Quantity Put Away is not substituted for Quantity Received.
- [ ] Supplier Order closure determines finalized report classification.

### API

- [ ] Supplier Difference Report API is implemented.
- [ ] Supplier Difference Details API is implemented.
- [ ] Related Receiving Information API is implemented or integrated with existing receiving endpoints.
- [ ] Supplier filtering works.
- [ ] Individual Item filtering works.
- [ ] Date-range filtering works.
- [ ] Difference-type filtering works.
- [ ] Provisional reporting works.
- [ ] Report sorting works.
- [ ] Invalid filters are rejected.
- [ ] Authorization is enforced.
- [ ] API responses identify incomplete historical information when applicable.
- [ ] API operations remain read-only.

### User Interface

- [ ] Supplier Difference Report screen is implemented.
- [ ] Supplier and Item filters are available.
- [ ] Date-range filters are available.
- [ ] Difference-type filtering is available.
- [ ] Include Provisional Differences option is available.
- [ ] Sorting controls are available.
- [ ] Results display required quantities and units.
- [ ] Finalized and provisional results are clearly distinguished.
- [ ] Supplier Difference Details screen is implemented.
- [ ] Receiving discrepancy approval details are accessible.
- [ ] Empty results display a clear message.
- [ ] Incomplete historical information displays a warning.
- [ ] Screens follow the approved Figma design.
- [ ] No report-side editing controls are provided.

### Testing

- [ ] Unit tests verify Ordered Units calculations.
- [ ] Unit tests verify cumulative Received Units calculations.
- [ ] Unit tests verify shortage and overage calculations.
- [ ] Unit tests verify matching quantity exclusion.
- [ ] Unit tests verify multiple receiving sessions.
- [ ] Unit tests verify duplicate Receiving Record Line prevention.
- [ ] Unit tests verify original Units Per Case preservation.
- [ ] Unit tests verify packaging mismatch handling.
- [ ] Integration tests verify Supplier Order and Receiving Record relationships.
- [ ] Integration tests verify Supplier Order closure handling.
- [ ] Integration tests verify approved shortage reporting.
- [ ] API tests verify all report filters.
- [ ] API tests verify unauthorized access is denied.
- [ ] UI tests verify report generation and details.
- [ ] Tests verify historical records remain available after deactivation.
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

The following capabilities are not included in Feature 17.

### Supplier Maintenance

Feature 17 does not:

- Create Suppliers.
- Edit Supplier information.
- Activate or deactivate Suppliers.
- Delete Supplier records.

Supplier maintenance belongs to Feature 5.

### Individual Item Maintenance

Feature 17 does not:

- Create Individual Items.
- Edit Item descriptions.
- Change Item Numbers.
- Modify Item packaging configuration.
- Activate or deactivate Items.

Individual Item maintenance belongs to Feature 4.

### Supplier Order Maintenance

Feature 17 does not:

- Create Supplier Orders.
- Add or remove Supplier Order Lines.
- Change ordered quantities.
- Change the original Units Per Case snapshot.
- Submit Supplier Orders.
- Cancel Supplier Orders.
- Close Supplier Orders as Received.

These operations belong to Features 9 and 10.

### Receiving Operations

Feature 17 does not:

- Scan received Items.
- Record receiving quantities.
- Start or complete Receiving Records.
- Approve receiving discrepancies.
- Change receiving approval information.
- Correct receiving quantities.
- Resolve packaging mismatches.

Receiving operations belong to Feature 10.

### Put Away and Inventory Maintenance

Feature 17 does not:

- Put received Items into storage bins.
- Move Inventory.
- Adjust Inventory quantities.
- Change Warehouse Locations.
- Use Put Away quantities as receiving quantities.

These operations belong to their respective warehouse operation features.

### Supplier Financial Processing

Feature 17 does not:

- Generate Supplier invoices.
- Calculate Supplier payments.
- Issue financial credits.
- Process refunds.
- Automatically create Supplier claims.
- Apply financial penalties for shortages or overages.

### Advanced Reporting

The following capabilities are deferred unless separately approved:

- Automatic Supplier performance scores.
- Supplier rankings based on discrepancy frequency.
- Predictive Supplier reliability analysis.
- Automatic discrepancy alerts.
- Scheduled email reports.
- Custom report builders.
- Advanced reporting dashboards.
- Automatic export to PDF or spreadsheet.

### Historical Data Correction

Feature 17 does not provide report-screen functionality for modifying or deleting historical Supplier Orders, Receiving Records, or Receiving Discrepancies.

Historical corrections must be handled through separately authorized workflows.

---

**End of Feature 17: Report Suppliers That Do Not Ship What Was Ordered**
