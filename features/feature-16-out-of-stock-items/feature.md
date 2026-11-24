
# Feature: Report Items That Have Been Out of Stock

**Feature ID:** 16  
**Branch pattern:** `feature/16-items-out-of-stock`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System provides authorized Managers with a report identifying Individual Items that have experienced an out-of-stock condition. The system uses physical Inventory quantities and preserved stockout history to identify affected Items, display when stockouts began and ended, and support review by Warehouse and date range. Previously out-of-stock Items remain reportable after Inventory is replenished.

---

## User Stories

### US-16.1: View Items That Have Been Out of Stock

**As a** Warehouse Manager  
**I want to** generate a report of Items that have been out of stock  
**So that** I can identify inventory availability problems.

**Priority:** P1  
**Independent test:** Generate the report when stockout records exist and verify that the affected Individual Items appear.

### US-16.2: Review Out-of-Stock Item Information

**As a** Warehouse Manager  
**I want to** review the details of each out-of-stock occurrence  
**So that** I can determine which Items were affected and when the shortages occurred.

**Priority:** P1  
**Independent test:** Open an out-of-stock report containing historical records and verify that Item identification, Warehouse, stockout dates, and current status are displayed.

### US-16.3: Review Historical Stockouts

**As a** Warehouse Manager  
**I want to** see Items that were previously out of stock even after they have been replenished  
**So that** I can identify recurring stock availability problems.

**Priority:** P1  
**Independent test:** Record a stockout, restore Inventory, and verify that the completed stockout occurrence remains visible in the report.

### US-16.4: Filter Out-of-Stock Report

**As a** Warehouse Manager  
**I want to** filter stockout information by Warehouse and date range  
**So that** I can focus on inventory exceptions relevant to a particular location or period.

**Priority:** P2  
**Independent test:** Generate a report for a selected Warehouse and date range and verify that only matching stockout occurrences appear.

---

## Functional Requirements

- **FR-001:** The system MUST identify Individual Items that have experienced an out-of-stock condition.
- **FR-002:** The system MUST provide an Out-of-Stock Report to authorized Warehouse Managers.
- **FR-003:** The report MUST identify each affected Individual Item by Item Number and description.
- **FR-004:** The system MUST use Inventory information maintained by the Warehouse Management System.
- **FR-005:** The system MUST evaluate out-of-stock conditions separately for each Warehouse.
- **FR-006:** An Item MUST be considered out of stock in a Warehouse when its total physical Inventory quantity across all storage locations in that Warehouse reaches zero.
- **FR-007:** The system MUST NOT count outstanding Supplier Order quantities as physical Inventory when determining stockout conditions.
- **FR-008:** The system MUST calculate an Item's total physical Inventory by summing its Inventory quantities across all storage bins in the selected Warehouse.
- **FR-009:** The system MUST create an Out-of-Stock Record when an Item's total physical Inventory changes from a positive quantity to zero.
- **FR-010:** The system MUST record the date and time when an out-of-stock condition begins.
- **FR-011:** The system MUST associate each Out-of-Stock Record with the affected Individual Item and Warehouse.
- **FR-012:** The system MUST preserve an active Out-of-Stock Record while the Item remains out of stock.
- **FR-013:** The system MUST NOT create duplicate active Out-of-Stock Records for the same Item and Warehouse.
- **FR-014:** The system MUST record when Inventory becomes available again after an out-of-stock condition.
- **FR-015:** The system MUST mark an Out-of-Stock Record as Resolved when physical Inventory increases above zero.
- **FR-016:** The system MUST preserve resolved Out-of-Stock Records for historical reporting.
- **FR-017:** The system MUST create a new Out-of-Stock Record if an Item becomes out of stock again after a previous occurrence was resolved.
- **FR-018:** The system MUST preserve each separate out-of-stock occurrence.
- **FR-019:** The report MUST display the Item Number, description, Warehouse, stockout start date and time, and stockout status.
- **FR-020:** The report MUST display the date and time Inventory became available again for resolved occurrences.
- **FR-021:** The report MUST identify unresolved occurrences as Currently Out of Stock.
- **FR-022:** The report MUST identify resolved occurrences as Restocked.
- **FR-023:** The report MUST allow a Manager to review multiple stockout occurrences for the same Item.
- **FR-024:** The report MUST display separate occurrences rather than combining all stockouts of the same Item into one record.
- **FR-025:** The system MUST allow a Manager to filter the report by Warehouse.
- **FR-026:** The system MUST allow a Manager to filter the report by a selected date range.
- **FR-027:** The system MUST include an occurrence in a selected date range when any part of its stockout period overlaps that range.
- **FR-028:** The system MUST allow a Manager to generate the report without selecting a specific Warehouse.
- **FR-029:** When no Warehouse is selected, the report MUST include matching occurrences from all Warehouses the Manager is authorized to review.
- **FR-030:** The system MUST validate that a selected report start date is not later than the end date.
- **FR-031:** The system MUST identify when no out-of-stock occurrences match the selected filters.
- **FR-032:** When no matching occurrences exist, the report MUST display an empty result with a clear message.
- **FR-033:** The system MUST preserve historical stockout records even when an Item is currently in stock.
- **FR-034:** The system MUST preserve stockout history when an Individual Item is deactivated.
- **FR-035:** The system MUST preserve stockout history when a Warehouse is deactivated.
- **FR-036:** The system MUST NOT delete historical stockout records merely because Inventory quantities later change.
- **FR-037:** The system MUST distinguish between no recorded stockouts and unavailable historical information.
- **FR-038:** The system MUST identify when requested historical information is unavailable or incomplete.
- **FR-039:** The system MUST NOT represent missing historical records as proof that no stockout occurred.
- **FR-040:** The system MUST preserve the source and date of historical stockout information.
- **FR-041:** The system MUST restrict access to the Out-of-Stock Report to authorized Managers and other approved reporting personnel.
- **FR-042:** The system MUST prevent unauthorized Users from modifying Out-of-Stock Records through the reporting feature.
- **FR-043:** The Out-of-Stock Report MUST be read-only.
- **FR-044:** The system MUST preserve the relationship between Out-of-Stock Records, Individual Items, Warehouses, and Inventory.
- **FR-045:** The system MUST update stockout history when confirmed Inventory transactions cause the total physical quantity to cross the zero threshold.
- **FR-046:** The system MUST NOT create additional stockout occurrences merely because an Item remains at zero after another transaction.
- **FR-047:** The system MUST support initialization of an active Out-of-Stock Record when an Item is first placed under Inventory tracking with zero physical stock.
- **FR-048:** The system MUST preserve the earliest reliable start time for each recorded stockout occurrence.
- **FR-049:** The system MUST distinguish stockout events recorded by the system from historical information imported or entered later.
- **FR-050:** The system MUST make the report available without changing physical Inventory quantities.

---

## Assumptions

- **A-001:** Feature 3 maintains physical Inventory quantities by Individual Item and Warehouse Location.
- **A-002:** Feature 4 owns Individual Item master data; Feature 2 owns Warehouse master data.
- **A-003:** Stockout detection is evaluated for each Item and Warehouse, not globally across all Warehouses.
- **A-004:** Only confirmed Inventory transactions trigger stockout state changes; outstanding Supplier Orders do not count as physical stock.
- **A-005:** An Out-of-Stock Record represents one uninterrupted period of zero physical Inventory.
- **A-006:** An Item with no positive Inventory when tracking begins can receive an initialized active stockout record.
- **A-007:** Stockout records are retained after restocking or deactivation of the Item or Warehouse.
- **A-008:** The report is read-only; only authorized Managers and approved reporting personnel can access it.
- **A-009:** The date range includes any occurrence whose stockout interval overlaps the requested period.
- **A-010:** Missing historical coverage is distinguishable from a confirmed period with no stockouts.

**[NEEDS CLARIFICATION]** Define how the system records and exposes the coverage dates and reliability of imported historical information.

**[NEEDS CLARIFICATION]** Confirm how the initial tracking time is established for Items that begin with zero Inventory.

**[NEEDS CLARIFICATION]** Confirm whether report dates are interpreted in Warehouse-local time or a shared system time zone.

---

## Edge Cases

### EC-16.1: Stock Reaches Zero

A confirmed Inventory transaction changes the Item's total physical Inventory in one Warehouse from positive to zero. Create one Active Out-of-Stock Record with the earliest reliable start timestamp.

### EC-16.2: Stock Remains Zero

Another confirmed transaction leaves the Item at zero. Preserve the existing Active record without creating a duplicate occurrence.

### EC-16.3: Stock Becomes Positive

Physical Inventory increases from zero to a positive quantity. Resolve the Active record, record `resolvedAt`, and preserve the occurrence for history.

### EC-16.4: Repeated Stockout

After restocking, Inventory later returns to zero. Create a new occurrence and retain the earlier resolved record.

### EC-16.5: Stock in Another Warehouse

An Item has zero stock in Warehouse W1 but positive stock in W2. Record the stockout for W1 independently; W2 does not prevent the W1 stockout.

### EC-16.6: Supplier Order Outstanding

An outstanding Supplier Order exists while physical Inventory is zero. Do not count the ordered quantity as available physical Inventory.

### EC-16.7: Initial Zero Inventory

An Item enters Inventory tracking with zero stock. Initialize an Active record according to FR-047, preserving the reliable tracking start time.

### EC-16.8: Deactivated Item or Warehouse

An Item or Warehouse is deactivated. Retain associated historical occurrences and identifiers in authorized reports.

### EC-16.9: No Matching Records with Complete History

No stockout overlaps the selected filters and history is complete. Show an empty result and a clear no-matching-records message.

### EC-16.10: Incomplete Historical Coverage

The selected period includes unavailable or incomplete stockout history. Display a coverage warning; do not treat missing history as evidence of no stockout.

### EC-16.11: Invalid Date Range

The start date is later than the end date. Reject the filter and request valid dates.

### EC-16.12: Ongoing Stockout Overlaps Range

A stockout started before the filter start date and remains Active during the selected period. Include the occurrence.

### EC-16.13: Resolved Stockout Overlaps Range

A stockout started before the selected period and ended within it, or started within the period and ended afterward. Include the occurrence.

### EC-16.14: Unauthorized Report Request

A User without approved reporting permission requests the report. Deny access and disclose no restricted report data.

### EC-16.15: Attempted Report-Side Modification

A User attempts to modify an Out-of-Stock Record through the reporting interface. Reject the operation; the report remains read-only.

### EC-16.16: Simultaneous Inventory Updates

Multiple confirmed Inventory changes affect the same Item and Warehouse near the zero threshold. Prevent duplicate Active records and preserve the correct state transition.

**[NEEDS CLARIFICATION]** Confirm the inventory-event transaction and concurrency strategy used to guarantee one Active record per Item and Warehouse.

---

## Success Criteria

- **SC-001:** Authorized Managers can generate the Out-of-Stock Report; unauthorized Users cannot.
- **SC-002:** Each result identifies Item Number, description, Warehouse, start time, and current stockout status.
- **SC-003:** Resolved occurrences display the time Inventory became available again.
- **SC-004:** Warehouse-level stockout detection uses the sum of physical Inventory quantities across its locations.
- **SC-005:** Outstanding Supplier Orders never increase the physical quantity used for stockout detection.
- **SC-006:** A positive-to-zero transition creates one Active record; remaining at zero creates no duplicate.
- **SC-007:** A zero-to-positive transition resolves the Active record without deleting it.
- **SC-008:** A later stockout creates a separate historical occurrence.
- **SC-009:** Historical occurrences remain available after replenishment and Item or Warehouse deactivation.
- **SC-010:** Warehouse and date-range filters return only occurrences overlapping the requested range and within the User's authorization scope.
- **SC-011:** An invalid date range is rejected with a clear validation message.
- **SC-012:** An empty report is distinguished from incomplete or unavailable historical coverage.
- **SC-013:** Every record retains its source and recording timestamp.
- **SC-014:** Generating the report does not change Inventory or stockout records.
- **SC-015:** All 20 original Gherkin Acceptance Criteria have corresponding tests.

---

## Key Entities

### Out-of-Stock Report

Represents a read-only reporting view of Individual Items that have experienced an out-of-stock condition.

The report includes active and resolved stockout occurrences and supports filtering by Warehouse and date range.

### Out-of-Stock Record

Represents one continuous period during which an Individual Item has zero total physical Inventory in a particular Warehouse.

Each record identifies the Item, Warehouse, stockout start time, resolution time when applicable, status, and historical information source.

A new record is created when an Item becomes out of stock again after being restocked.

### Individual Item

Represents a product tracked by the Warehouse Management System.

Individual Item information is maintained in Feature 4.

An Individual Item may experience multiple stockout occurrences in one or more Warehouses.

### Warehouse

Represents a physical facility where Inventory is stored.

Warehouse information is maintained in Feature 2.

Stockout conditions are evaluated separately for each Warehouse.

### Warehouse Location

Represents a storage bin or location within a Warehouse.

An Item may have Inventory in multiple Warehouse Locations.

The system uses the combined physical Inventory quantities from all applicable locations when determining whether the Item is out of stock.

### Inventory

Represents the physical quantity of an Individual Item stored at a Warehouse Location.

Inventory information is maintained in Feature 3.

Confirmed Inventory changes are used to determine when stockout conditions begin and end.

### User

Represents a person authenticated in the Warehouse Management System.

Authorized Managers and approved reporting personnel may generate and review the Out-of-Stock Report.

The reporting feature does not allow Users to modify Inventory or Out-of-Stock Records.

---

## Initial Data Model

### Out-of-Stock Report

The Out-of-Stock Report is a generated reporting view rather than a separate Inventory transaction.

**Report Parameters:**

| Parameter | Type | Description |
|---|---|---|
| warehouseId | Integer | Optional Warehouse filter |
| startDate | Date | Optional report start date |
| endDate | Date | Optional report end date |

**Displayed Information:**

| Field | Description |
|---|---|
| Item Number | Unique identifier of the Individual Item |
| Item Description | Description of the Individual Item |
| Warehouse | Warehouse where the stockout occurred |
| Stockout Start | Date and time the stockout began |
| Stockout End | Date and time Inventory became available again, if resolved |
| Stockout Status | Currently Out of Stock or Restocked |
| Information Source | Origin of the stockout information |
| Recorded At | Date and time the historical information was recorded |

**Relationships:**

- The report uses Out-of-Stock Records.
- Each Out-of-Stock Record references one Individual Item and one Warehouse.
- The report may include multiple occurrences for the same Item.
- The report does not create or modify physical Inventory quantities.
- The report includes only records the requesting User is authorized to review.

**Derived Values:**

- Total Physical Inventory = Sum of physical Inventory quantities for the Item across all Warehouse Locations in the selected Warehouse.
- Active Stockout = Total Physical Inventory is zero and the stockout has not been resolved.
- Resolved Stockout = A previously active stockout for which physical Inventory has increased above zero.
- Stockout Duration = Stockout End minus Stockout Start for resolved occurrences.

**Constraints:**

- A report start date must not be later than its end date.
- Date-range filtering must include occurrences that overlap the selected period.
- An unresolved occurrence has no Stockout End timestamp.
- The report must not modify the underlying stockout history.

### Out-of-Stock Record

| Attribute | Type | Description |
|---|---|---|
| stockoutRecordId | Integer | Unique stockout occurrence identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| warehouseId | Integer | Foreign key referencing Warehouse |
| startedAt | DateTime | Date and time the stockout began |
| resolvedAt | DateTime | Date and time Inventory became positive again; nullable |
| status | String | Active or Resolved |
| source | String | System Recorded, Imported, or Historical Entry |
| recordedAt | DateTime | Date and time the record was stored |
| sourceReference | String | Optional reference to the originating Inventory event or historical source |

**Relationships:**

- Each Out-of-Stock Record belongs to one Individual Item.
- Each Out-of-Stock Record belongs to one Warehouse.
- An Individual Item may have multiple Out-of-Stock Records.
- A Warehouse may have multiple Out-of-Stock Records.
- A record may reference the Inventory event that caused the stockout or its resolution.

**Constraints:**

- stockoutRecordId must be unique.
- itemId and warehouseId must reference valid records.
- startedAt must contain a reliable stockout start time.
- resolvedAt must be null while the record is Active.
- resolvedAt must not precede startedAt.
- Only one Active Out-of-Stock Record may exist for the same Item and Warehouse.
- Resolved records must remain available for historical reporting.
- Repeated stockouts must be stored as separate occurrences.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique Item Number or SKU |
| description | String | Item description |
| isActive | Boolean | Indicates whether the Item is active |

**Relationships:**

- An Individual Item may have Inventory in multiple Warehouse Locations.
- An Individual Item may have multiple Out-of-Stock Records.
- Deactivated Items remain identifiable in historical stockout reports.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique Warehouse identifier |
| warehouseCode | String | Unique Warehouse Code |
| name | String | Warehouse name |
| isActive | Boolean | Indicates whether the Warehouse is active |

**Relationships:**

- A Warehouse contains multiple Warehouse Locations.
- A Warehouse may have multiple Inventory records.
- A Warehouse may have multiple Out-of-Stock Records.
- Deactivated Warehouses remain identifiable in historical reporting.

### Warehouse Location

| Attribute | Type | Description |
|---|---|---|
| warehouseLocationId | Integer | Unique Warehouse Location identifier |
| warehouseId | Integer | Foreign key referencing Warehouse |
| locationCode | String | Unique location identifier within the Warehouse |

**Relationships:**

- Each Warehouse Location belongs to one Warehouse.
- A Warehouse Location may contain Inventory for multiple Individual Items.
- Inventory quantities across applicable locations contribute to the Warehouse-level stockout calculation.

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique Inventory record identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| warehouseLocationId | Integer | Foreign key referencing Warehouse Location |
| quantity | Integer | Physical quantity of the Item in the location |
| updatedAt | DateTime | Date and time the Inventory record was last updated |

**Relationships:**

- Each Inventory record references one Individual Item.
- Each Inventory record references one Warehouse Location.
- A Warehouse Location belongs to one Warehouse.
- Multiple Inventory records for the same Item in one Warehouse contribute to its total physical Inventory.

**Derived Value:**

Total Physical Inventory for an Item in a Warehouse:

Total Physical Inventory = Sum of quantity across all applicable Inventory records for that Item and Warehouse.

**Constraints:**

- Physical Inventory quantities must be maintained by the Inventory feature.
- Stockout detection must use confirmed physical Inventory quantities.
- Outstanding Supplier Orders must not increase physical Inventory totals.
- Inventory changes crossing the zero threshold must update stockout history.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**

- Authorized Managers generate Out-of-Stock Reports.
- Approved reporting personnel may review report information.
- Unauthorized Users must not access restricted stockout information.
- Report generation must not change Inventory or Out-of-Stock Records.

---

## Gherkin AC

### US-16.1: View Items That Have Been Out of Stock

#### AC-16.1.1: Item becomes out of stock

**Given** an Individual Item has a positive total physical Inventory quantity in a Warehouse  
**And** a confirmed Inventory transaction reduces that quantity to zero  
**When** the system processes the Inventory change  
**Then** the system creates an Active Out-of-Stock Record  
**And** associates the record with the Individual Item and Warehouse  
**And** records when the stockout began.

#### AC-16.1.2: View currently out-of-stock Item

**Given** an Individual Item has an Active Out-of-Stock Record  
**When** an authorized Manager generates the Out-of-Stock Report  
**Then** the report identifies the Item and Warehouse  
**And** displays the stockout start date and time  
**And** identifies the Item as Currently Out of Stock.

#### AC-16.1.3: Item remains at zero

**Given** an Item already has an Active Out-of-Stock Record in a Warehouse  
**And** its total physical Inventory remains zero  
**When** another confirmed Inventory transaction is processed  
**Then** the system preserves the existing Active Out-of-Stock Record  
**And** does not create a duplicate occurrence.

#### AC-16.1.4: Item has stock in another Warehouse

**Given** Item A has zero physical Inventory in Warehouse W1  
**And** Item A has positive physical Inventory in Warehouse W2  
**When** the Manager generates the Out-of-Stock Report  
**Then** the system identifies the stockout in Warehouse W1  
**And** does not treat the stock available in Warehouse W2 as stock in Warehouse W1.

#### AC-16.1.5: Outstanding Supplier Order does not prevent stockout

**Given** an Item has zero physical Inventory in a Warehouse  
**And** a Supplier Order contains additional units that have not been received  
**When** the system evaluates the Item's stockout status  
**Then** the system considers the Item out of stock  
**And** does not count the outstanding Supplier Order quantity as physical Inventory.

### US-16.2: Review Out-of-Stock Item Information

#### AC-16.2.1: Display stockout details

**Given** an Out-of-Stock Record exists for an Individual Item  
**When** the Manager reviews the report  
**Then** the report displays the Item Number and description  
**And** identifies the Warehouse  
**And** displays the stockout start date and time  
**And** displays the stockout status.

#### AC-16.2.2: Display resolved stockout information

**Given** an Item was previously out of stock  
**And** physical Inventory was subsequently replenished  
**When** the Manager reviews the historical Out-of-Stock Record  
**Then** the report displays when the stockout began  
**And** displays when Inventory became available again  
**And** identifies the occurrence as Restocked.

#### AC-16.2.3: Item has multiple Inventory locations

**Given** an Individual Item has Inventory in multiple locations within one Warehouse  
**And** the combined physical Inventory quantity is greater than zero  
**When** the system evaluates whether the Item is out of stock  
**Then** the system does not identify an active Warehouse-level stockout solely because one location is empty.

#### AC-16.2.4: Item begins tracking with zero Inventory

**Given** an Individual Item is first placed under Inventory tracking in a Warehouse  
**And** its initial total physical Inventory quantity is zero  
**When** the system initializes stockout tracking  
**Then** the system creates an Active Out-of-Stock Record  
**And** preserves the reliable tracking start time  
**And** does not invent an earlier stockout date.

### US-16.3: Review Historical Stockouts

#### AC-16.3.1: Preserve stockout after restocking

**Given** an Individual Item has an Active Out-of-Stock Record  
**And** confirmed Inventory increases above zero  
**When** the system processes the Inventory change  
**Then** the system marks the Out-of-Stock Record as Resolved  
**And** records the resolution date and time  
**And** preserves the occurrence for historical reporting.

#### AC-16.3.2: Record repeated stockouts

**Given** an Individual Item previously experienced a stockout  
**And** its earlier Out-of-Stock Record was resolved  
**And** the Item later becomes out of stock again  
**When** the system processes the new stockout  
**Then** the system creates a new Out-of-Stock Record  
**And** preserves the previous resolved occurrence  
**And** keeps the occurrences separate.

#### AC-16.3.3: Preserve history after Item deactivation

**Given** an Individual Item has historical Out-of-Stock Records  
**And** the Item is later deactivated  
**When** the Manager generates a historical Out-of-Stock Report  
**Then** the Item remains identifiable  
**And** its historical stockout occurrences remain available.

#### AC-16.3.4: Preserve history after Warehouse deactivation

**Given** a Warehouse has historical Out-of-Stock Records  
**And** the Warehouse is later deactivated  
**When** the Manager generates a historical Out-of-Stock Report  
**Then** the Warehouse remains identifiable  
**And** its historical stockout occurrences remain available.

#### AC-16.3.5: Historical information is incomplete

**Given** some historical stockout information is unavailable  
**When** the Manager generates a report for the affected period  
**Then** the system identifies that historical information is incomplete  
**And** does not claim that no stockouts occurred during the missing period.

#### AC-16.3.6: Preserve historical information source

**Given** a stockout occurrence was recorded by the system or imported from historical information  
**When** the Manager reviews the occurrence  
**Then** the system preserves its information source  
**And** preserves the date and time the record was stored  
**And** distinguishes imported historical information from system-recorded stockout events.

### US-16.4: Filter Out-of-Stock Report

#### AC-16.4.1: Filter by Warehouse

**Given** stockout occurrences exist in Warehouse W1 and Warehouse W2  
**When** the Manager filters the report to Warehouse W1  
**Then** the report includes only applicable occurrences from Warehouse W1.

#### AC-16.4.2: Filter by date range

**Given** stockout occurrences exist inside and outside a selected reporting period  
**When** the Manager applies a valid date range  
**Then** the report includes occurrences that overlap the selected period  
**And** excludes occurrences that do not overlap that period.

#### AC-16.4.3: Reject invalid date range

**Given** the Manager is selecting report dates  
**When** the start date is later than the end date  
**Then** the system rejects the date range  
**And** requests valid dates.

#### AC-16.4.4: No matching stockouts

**Given** no stockout occurrences match the selected filters  
**And** historical information for the selected period is complete  
**When** the Manager generates the Out-of-Stock Report  
**Then** the system displays an empty result  
**And** indicates that no matching stockout occurrences were found.

#### AC-16.4.5: Reject unauthorized report access

**Given** a User is authenticated as a Driver without reporting permission  
**When** the User attempts to generate the Out-of-Stock Report  
**Then** the system denies access  
**And** does not display restricted stockout information.

---

## Data Ownership

### Individual Item Data

**Owning Feature:** Feature 4 - Maintain Individual Items

Feature 4 owns Individual Item master data, including:

- Item ID
- Item Number
- Item Description
- Item active or inactive status

Feature 16 reads Individual Item information to identify Items appearing in the Out-of-Stock Report.

Feature 16 MUST NOT create, update, deactivate, or delete Individual Item records.

### Warehouse Data

**Owning Feature:** Feature 2 - Maintain Warehouses

Feature 2 owns Warehouse master data, including:

- Warehouse ID
- Warehouse Code
- Warehouse Name
- Warehouse active or inactive status

Feature 16 reads Warehouse information to identify where each stockout occurred.

Feature 16 MUST NOT modify Warehouse master data.

### Inventory Data

**Owning Feature:** Feature 3 - Maintain Inventory

Feature 3 owns physical Inventory quantities and their associated Warehouse Locations.

Feature 16 uses confirmed Inventory changes to determine when an Item becomes out of stock or becomes available again.

Feature 16 MUST NOT directly modify physical Inventory quantities.

Inventory quantities from all applicable locations within the same Warehouse are combined when determining Warehouse-level stockout status.

### Out-of-Stock Record Data

**Owning Feature:** Feature 16 - Report Items That Have Been Out of Stock

Feature 16 owns the historical Out-of-Stock Records used for reporting.

These records include:

- Stockout Record ID
- Individual Item ID
- Warehouse ID
- Stockout start date and time
- Stockout resolution date and time
- Stockout status
- Historical information source
- Record creation date and time

Out-of-Stock Records are created or updated by authorized system processes responding to confirmed Inventory changes.

The reporting interface MUST remain read-only.

A Manager viewing the report MUST NOT be able to manually change stockout start times, resolution times, or status through the report.

### User and Authorization Data

**Owning Component:** Shared User and Access Control functionality

The shared authorization component determines which Users may access the Out-of-Stock Report.

Feature 16 reads User roles and reporting permissions.

Feature 16 MUST NOT modify User accounts, passwords, or role assignments.

### Data Ownership Rules

- Feature 2 owns Warehouse master data.
- Feature 3 owns physical Inventory quantities.
- Feature 4 owns Individual Item master data.
- Feature 16 owns Out-of-Stock Records and reporting logic.
- Shared authorization functionality owns User permissions.
- Feature 16 MUST NOT duplicate or overwrite data owned by another feature.
- Feature 16 MUST preserve historical references to deactivated Items and Warehouses.

**[NEEDS CLARIFICATION]** Confirm whether stockout event processing belongs within Feature 16 or is implemented as a shared Inventory event handler coordinated with Feature 3.

---

## API Requirements

The following endpoints are proposed for the Warehouse Management System.

The final endpoint names and response formats must follow the project's established API conventions.

### API-16.1: Generate Out-of-Stock Report

**Method:** GET

**Proposed Endpoint:**

`/api/reports/out-of-stock`

**Purpose:**

Retrieve active and historical stockout occurrences matching the selected report filters.

**Query Parameters:**

| Parameter | Type | Required | Description |
|---|---|---|---|
| warehouseId | Integer | No | Filter by Warehouse |
| startDate | Date | No | Beginning of reporting period |
| endDate | Date | No | End of reporting period |

**Expected Response Information:**

- Stockout Record ID
- Item ID
- Item Number
- Item Description
- Warehouse ID
- Warehouse Code
- Warehouse Name
- Stockout start date and time
- Stockout resolution date and time, if applicable
- Stockout status
- Information source
- Record creation date and time
- Historical data completeness indicator, when applicable

**Validation Rules:**

- The requesting User must have reporting permission.
- The start date must not be later than the end date.
- A selected Warehouse must exist and be accessible to the User.
- Results must include only authorized Warehouses.
- Date filtering must include occurrences overlapping the requested period.
- An empty result must be distinguishable from incomplete historical information.

**Possible Responses:**

- `200 OK` - Report generated successfully, including when no records match.
- `400 Bad Request` - Invalid filter parameters.
- `401 Unauthorized` - User is not authenticated.
- `403 Forbidden` - User lacks permission.
- `500 Internal Server Error` - Unexpected server failure.

### API-16.2: Retrieve Out-of-Stock Record Details

**Method:** GET

**Proposed Endpoint:**

`/api/reports/out-of-stock/{stockoutRecordId}`

**Purpose:**

Retrieve the details of one historical or active stockout occurrence.

**Path Parameter:**

- `stockoutRecordId` - Unique identifier of the Out-of-Stock Record.

**Expected Response Information:**

- Item identification
- Warehouse identification
- Stockout start date and time
- Resolution date and time, when applicable
- Current occurrence status
- Historical information source
- Record creation date and time
- Source reference, when available

**Validation Rules:**

- The User must have reporting permission.
- The requested record must exist.
- The User must be authorized to view the associated Warehouse.
- The endpoint must not modify the record.

**Possible Responses:**

- `200 OK` - Record details returned.
- `401 Unauthorized` - User is not authenticated.
- `403 Forbidden` - User lacks permission.
- `404 Not Found` - Record does not exist or is not available to the requesting User.

### API-16.3: Process Inventory Stockout State Changes

**Type:** Internal system operation

**Purpose:**

Maintain Out-of-Stock Records when confirmed Inventory changes cause an Item's Warehouse-level physical quantity to cross the zero threshold.

This operation is not exposed as a report-editing endpoint.

**Required Information:**

- Individual Item ID
- Warehouse ID
- Previous total physical Inventory quantity
- New total physical Inventory quantity
- Confirmed Inventory transaction date and time
- Inventory transaction reference, when available

**Processing Rules:**

1. If the previous total is positive and the new total is zero, create one Active Out-of-Stock Record.
2. If the previous total is zero and the new total remains zero, preserve the existing Active record.
3. If the previous total is zero and the new total becomes positive, resolve the Active record.
4. If the Item becomes out of stock again after resolution, create a new occurrence.
5. Prevent duplicate Active records for the same Item and Warehouse.
6. Preserve all resolved historical occurrences.
7. Do not modify physical Inventory quantities.

**[NEEDS CLARIFICATION]** Confirm whether this operation will be implemented using Inventory events, a service method, or another internal integration mechanism.

### API Security Requirements

- All report endpoints MUST require authentication.
- Reporting permissions MUST be checked on the server.
- Warehouse-level access restrictions MUST be enforced.
- Drivers and other unauthorized roles MUST NOT receive restricted report data.
- Report endpoints MUST NOT permit changes to Inventory or historical stockout records.
- Internal stockout processing MUST NOT be accessible as an unrestricted public operation.

---

## Screen Requirements

### SCREEN-16.1: Out-of-Stock Report Screen

**Purpose:**

Allow authorized Managers to view active and historical stockout occurrences.

**Authorized Users:**

- Warehouse Managers
- Approved reporting personnel

**Screen Elements:**

- Page title: Out-of-Stock Report
- Warehouse filter
- Start Date filter
- End Date filter
- Generate Report button
- Clear Filters button
- Results table
- Empty-results message
- Historical information warning, when applicable

**Results Table Columns:**

| Column | Description |
|---|---|
| Item Number | Unique Item Number |
| Item Description | Item description |
| Warehouse | Warehouse where stockout occurred |
| Stockout Start | Date and time stockout began |
| Stockout End | Date and time stockout ended |
| Status | Currently Out of Stock or Restocked |
| Source | Source of stockout information |
| Details | Read-only access to occurrence details |

**Screen Behavior:**

1. The User opens the Out-of-Stock Report from an authorized reporting menu.
2. The system displays the available filters.
3. The User optionally selects a Warehouse.
4. The User optionally enters a date range.
5. The User selects Generate Report.
6. The system validates the filters.
7. The system retrieves matching stockout occurrences.
8. The results table displays the matching records.
9. The User may open an occurrence to review additional details.
10. The User cannot modify stockout records from this screen.

**Validation:**

- Start Date must not be later than End Date.
- A selected Warehouse must be accessible to the User.
- Invalid filters must display a clear error message.
- No matching records must display an appropriate empty-results message.
- Incomplete historical information must display a warning.

### SCREEN-16.2: Out-of-Stock Record Details

**Purpose:**

Allow an authorized Manager to review one stockout occurrence.

**Displayed Information:**

- Item Number
- Item Description
- Warehouse Code
- Warehouse Name
- Stockout Record ID
- Stockout Start
- Stockout End, if resolved
- Stockout Status
- Information Source
- Record Creation Date and Time
- Source Reference, when available

**Screen Behavior:**

1. The User selects a stockout occurrence from the report.
2. The system retrieves the selected record.
3. The system displays the record details.
4. The User may return to the report.
5. No edit or delete actions are provided.

### SCREEN-16.3: Empty Results and Historical Data Warning

**Purpose:**

Clearly distinguish between no matching stockout occurrences and unavailable historical information.

**Required Messages:**

When no matching records exist and historical information is complete:

`No matching out-of-stock occurrences were found.`

When historical information is incomplete:

`Some historical stockout information is unavailable or incomplete. Report results may not represent all stockout occurrences.`

When a date range is invalid:

`Start Date must not be later than End Date.`

When access is denied:

`You do not have permission to view this report.`

### Screen Design Requirements

- Follow the Warehouse Management System's established UI style.
- Display clear labels for all report filters.
- Keep report information read-only.
- Use consistent date and time formatting.
- Clearly distinguish Currently Out of Stock from Restocked.
- Provide readable tables for multiple historical occurrences.
- Preserve access to historical records for deactivated Items and Warehouses.
- Do not require printed reports or paper-based processing.

**[NEEDS CLARIFICATION]** Confirm the final Figma screen layouts, navigation placement, and table presentation.

---

## Definition of Done

Feature 16 is considered complete when all of the following conditions are satisfied.

### Requirements

- [ ] All Functional Requirements FR-001 through FR-050 are implemented or explicitly deferred.
- [ ] All User Stories US-16.1 through US-16.4 are supported.
- [ ] All Gherkin Acceptance Criteria are tested.
- [ ] All unresolved clarification items have been reviewed.
- [ ] The implemented behavior matches approved requirements.

### Data Model

- [ ] Out-of-Stock Record data is implemented.
- [ ] Each record references the correct Individual Item and Warehouse.
- [ ] Active and Resolved statuses are supported.
- [ ] Stockout start and resolution timestamps are preserved.
- [ ] Historical information sources are recorded.
- [ ] Duplicate Active records are prevented.
- [ ] Historical records remain available after restocking.
- [ ] Historical records remain available after Item or Warehouse deactivation.

### Business Logic

- [ ] Stockout detection uses total physical Inventory across Warehouse Locations.
- [ ] Stockout detection is performed separately for each Warehouse.
- [ ] Outstanding Supplier Orders are excluded from physical Inventory totals.
- [ ] Positive-to-zero changes create an Active record.
- [ ] Zero-to-zero changes do not create duplicate records.
- [ ] Zero-to-positive changes resolve the Active record.
- [ ] Repeated stockouts create separate occurrences.
- [ ] Initial zero-stock tracking is handled.
- [ ] Concurrent Inventory changes cannot create duplicate Active records.

### API

- [ ] The report API is implemented.
- [ ] Record-detail retrieval is implemented.
- [ ] Invalid filter values are rejected.
- [ ] Warehouse authorization is enforced.
- [ ] Unauthorized Users cannot retrieve restricted information.
- [ ] Report operations do not modify Inventory.
- [ ] API tests cover successful and unsuccessful requests.

### User Interface

- [ ] The Out-of-Stock Report screen is implemented.
- [ ] Warehouse filtering works.
- [ ] Date-range filtering works.
- [ ] Report results display required information.
- [ ] Record details are accessible.
- [ ] Active and Resolved stockouts are clearly identified.
- [ ] Empty results display an appropriate message.
- [ ] Incomplete historical information displays a warning.
- [ ] The interface contains no report-side editing controls.
- [ ] Screens follow the approved Figma design.

### Testing

- [ ] Unit tests verify stockout threshold calculations.
- [ ] Unit tests verify record creation and resolution.
- [ ] Unit tests verify repeated stockout handling.
- [ ] Unit tests verify duplicate prevention.
- [ ] Integration tests verify Inventory and stockout history interaction.
- [ ] Integration tests verify Warehouse and Item references.
- [ ] API tests verify report filters.
- [ ] API tests verify authorization.
- [ ] UI tests verify report generation and details.
- [ ] Tests verify historical records remain available after deactivation.
- [ ] Tests verify missing historical information is not reported as complete.
- [ ] All automated tests pass.

### Code Quality and Documentation

- [ ] Code follows project conventions.
- [ ] No unrelated feature behavior is modified.
- [ ] Required API documentation is updated.
- [ ] Data model changes are documented.
- [ ] User-facing validation messages are reviewed.
- [ ] Code is reviewed and approved.
- [ ] Feature changes are committed to the correct Git branch.

---

## Out of Scope

The following capabilities are not included in Feature 16.

### Inventory Maintenance

Feature 16 does not:

- Create Inventory records manually.
- Change physical Inventory quantities.
- Move Inventory between Warehouse Locations.
- Perform Put Away operations.
- Perform Picking operations.
- Perform Inventory adjustments.

These operations belong to their respective Inventory and warehouse operation features.

### Individual Item Maintenance

Feature 16 does not:

- Create Individual Items.
- Edit Item descriptions.
- Change Item Numbers.
- Activate or deactivate Items.
- Delete Item master records.

Individual Item maintenance belongs to Feature 4.

### Warehouse Maintenance

Feature 16 does not:

- Create Warehouses.
- Edit Warehouse information.
- Activate or deactivate Warehouses.
- Delete Warehouse records.

Warehouse maintenance belongs to Feature 2.

### Supplier Ordering

Feature 16 does not:

- Create Supplier Orders.
- Change Supplier Order quantities.
- Receive Supplier shipments.
- Treat unreceived Supplier Orders as available Inventory.

### Inventory Forecasting

Feature 16 does not:

- Predict future stockouts.
- Recommend reorder quantities.
- Automatically create replenishment orders.
- Calculate future Inventory demand.
- Perform supplier performance forecasting.

### Advanced Reporting

The following capabilities are deferred unless separately approved:

- Automatic stockout alert notifications.
- Scheduled report delivery by email.
- Advanced charts and dashboards.
- Stockout trend prediction.
- Automatic report exports.
- Custom report builders.
- Financial calculations of lost sales caused by stockouts.

### Historical Data Correction

Feature 16 does not provide a report-screen function for manually editing or deleting historical Out-of-Stock Records.

Any historical data correction process must be defined separately and authorized.

---

**End of Feature 16: Report Items That Have Been Out of Stock**
