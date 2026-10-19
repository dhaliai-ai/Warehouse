
# Feature: Report Suppliers That Do Not Ship What Was Ordered

**Feature ID:** 17  
**Branch pattern:** `feature/17-supplier-order-differences`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System provides authorized Managers with a report identifying Supplier Order Lines where the total Quantity Received differs from the Quantity Ordered. The system compares ordered and received quantities in individual units, identifies shortages and overages, displays Supplier and Item information, and preserves receiving discrepancies for review. The report distinguishes finalized supplier delivery differences from orders that are still awaiting additional receipts.

---

## User Stories

### US-17.1: View Supplier Order Differences

**As a** Warehouse Manager  
**I want to** generate a report of Supplier Orders where Quantity Received differs from Quantity Ordered  
**So that** I can identify Suppliers that delivered incorrect quantities.

**Priority:** P1  
**Independent test:** Generate a report containing completed Supplier Orders with shortages and overages and verify that the differing order lines are displayed.

### US-17.2: Review Supplier Difference Details

**As a** Warehouse Manager  
**I want to** review the Supplier, Purchase Order, Individual Item, Quantity Ordered, and Quantity Received  
**So that** I can understand each supplier delivery discrepancy.

**Priority:** P1  
**Independent test:** Review a reported difference and verify that the Supplier, PO Number, Item, ordered quantity, received quantity, and difference are displayed.

### US-17.3: Distinguish Shortages from Overages

**As a** Warehouse Manager  
**I want to** see whether a Supplier delivered fewer or more units than ordered  
**So that** I can identify the type and size of each discrepancy.

**Priority:** P1  
**Independent test:** Create one shortage and one overage and verify that the report identifies them separately.

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
- **FR-010:** Ordered Units MUST equal Quantity Ordered Cases multiplied by the Units Per Case recorded on the Supplier Order Line.
- **FR-011:** The system MUST use the Units Per Case snapshot stored when the Supplier Order was created.
- **FR-012:** The system MUST calculate cumulative Quantity Received from completed Receiving Record Lines associated with the Supplier Order Line.
- **FR-013:** The system MUST count received quantities across multiple completed receiving sessions for the same Supplier Order.
- **FR-014:** The system MUST NOT count the same Receiving Record Line more than once.
- **FR-015:** The system MUST identify a shortage when cumulative Quantity Received is less than Ordered Units on a finalized Supplier Order.
- **FR-016:** The system MUST identify an overage when cumulative Quantity Received is greater than Ordered Units.
- **FR-017:** The system MUST calculate Quantity Difference as Quantity Received minus Ordered Units.
- **FR-018:** The report MUST identify negative differences as Shortages.
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
- **FR-029:** Provisional differences MUST be clearly identified as Pending Receipt rather than confirmed supplier shortages.
- **FR-030:** The system MUST preserve overages identified during completed receiving sessions even if other lines on the Supplier Order remain incomplete.
- **FR-031:** The report MUST identify the date associated with each finalized Supplier Order difference.
- **FR-032:** For finalized Supplier Orders, the report date MUST be the date the Supplier Order was closed as Received.
- **FR-033:** For provisional differences, the report MUST identify the most recent completed receiving date when one exists.
- **FR-034:** The system MUST allow the report to be filtered by Supplier.
- **FR-035:** The system MUST allow the report to be filtered by Individual Item.
- **FR-036:** The system MUST allow the report to be filtered by date range.
- **FR-037:** The system MUST allow the report to be filtered by difference type: Shortage, Overage, or All.
- **FR-038:** The system MUST allow a Manager to generate the report without selecting a specific Supplier or Item.
- **FR-039:** The system MUST validate that the report start date is not later than the end date.
- **FR-040:** The system MUST display an empty result when no Supplier Order Lines match the selected criteria.
- **FR-041:** The system MUST NOT report matching ordered and received quantities as discrepancies.
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
- **FR-053:** The system MUST preserve the relationships between Suppliers, Supplier Orders, Supplier Order Lines, Receiving Records, Receiving Record Lines, and Individual Items.
- **FR-054:** The system MUST support sorting report results by Supplier, PO Number, Item Number, report date, or difference magnitude.
- **FR-055:** The report MUST display the units used for each quantity so that ordered cases are not confused with received individual units.

---

## Key Entities

### Supplier Difference Report

Represents a read-only reporting view of differences between quantities ordered from Suppliers and quantities received by the warehouse.

### Supplier

Represents the company supplying products to the warehouse.

Supplier information is maintained in Feature 5.

### Supplier Order

Represents a purchase order placed with a Supplier.

Supplier Order creation is defined in Feature 9.

### Supplier Order Line

Represents an Individual Item ordered from a Supplier, including ordered case quantity, Units Per Case, and cumulative received units.

### Receiving Record

Represents a receiving session for a Supplier Order.

Receiving is defined in Feature 10.

### Receiving Record Line

Represents the quantity of an Individual Item recorded during a receiving session.

### Individual Item

Represents a product purchased from a Supplier.

### User

Represents an authorized Manager or reporting employee.

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
| Units Per Case | Units in each ordered case |
| Quantity Ordered Units | Ordered cases multiplied by Units Per Case |
| Quantity Received Units | Cumulative quantity received |
| Difference Units | Received Units minus Ordered Units |
| Difference Type | Shortage, Overage, or Pending Receipt |
| Supplier Order Status | Current order status |
| Report Date | Finalization date or latest receiving date |

**Relationships:**
- The report uses Supplier Order Lines and Receiving Record Lines.
- The report identifies Suppliers and Individual Items associated with differences.
- Each report row represents one Supplier Order Line with a qualifying quantity difference.

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
| status | String | Draft, Submitted, Partially Received, Received, or Canceled |
| createdAt | DateTime | Date and time the order was created |
| submittedAt | DateTime | Date and time the order was submitted |
| closedAt | DateTime | Date and time receiving was finalized |

**Relationships:**
- Each Supplier Order belongs to one Supplier.
- Each Supplier Order contains one or more Supplier Order Lines.
- Each Supplier Order may have multiple Receiving Records.

### Supplier Order Line

| Attribute | Type | Description |
|---|---|---|
| supplierOrderLineId | Integer | Unique Supplier Order Line identifier |
| supplierOrderId | Integer | Foreign key referencing Supplier Order |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityOrderedCases | Integer | Original ordered quantity in cases |
| unitsPerCase | Integer | Units Per Case snapshot |
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
- Original ordered quantities must remain preserved after submission.

### Receiving Record

| Attribute | Type | Description |
|---|---|---|
| receivingRecordId | Integer | Unique Receiving Record identifier |
| supplierOrderId | Integer | Foreign key referencing Supplier Order |
| warehouseId | Integer | Foreign key referencing Warehouse |
| completedAt | DateTime | Date and time receiving session completed |
| status | String | In Progress or Completed |

**Relationships:**
- Each Receiving Record belongs to one Supplier Order.
- Each Receiving Record contains one or more Receiving Record Lines.
- A Supplier Order may have multiple Receiving Records.

### Receiving Record Line

| Attribute | Type | Description |
|---|---|---|
| receivingRecordLineId | Integer | Unique Receiving Record Line identifier |
| receivingRecordId | Integer | Foreign key referencing Receiving Record |
| supplierOrderLineId | Integer | Foreign key referencing Supplier Order Line |
| itemId | Integer | Foreign key referencing Individual Item |
| quantityReceivedUnits | Integer | Quantity received in individual units |

**Relationships:**
- Each Receiving Record Line belongs to one Receiving Record.
- Each Receiving Record Line references one Supplier Order Line.
- Completed Receiving Record Lines contribute to cumulative Quantity Received.

**Constraints:**
- quantityReceivedUnits cannot be negative.
- A Receiving Record Line must not be counted more than once in report totals.

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
**And** displays Quantity Ordered Cases, Ordered Units, Received Units, and Difference Units.

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
**And** the Supplier Order is finalized as Received with a confirmed shortage  
**When** the Manager generates the default Supplier Difference Report  
**Then** the system reports a finalized Shortage of 40 units.

#### AC-17.5.4: Reject unauthorized report access

**Given** a User is authenticated as a Driver without reporting permission  
**When** the User attempts to generate the Supplier Difference Report  
**Then** the system denies access  
**And** does not display restricted Supplier information.
