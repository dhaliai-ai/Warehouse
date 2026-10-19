
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

## Key Entities

### Out-of-Stock Report

Represents a read-only reporting view that displays historical and current stockout occurrences.

The report may be filtered by Warehouse and date range.

### Out-of-Stock Record

Represents one period during which an Individual Item had zero physical Inventory in a particular Warehouse.

Each occurrence has a start time, optional resolution time, and status.

### Individual Item

Represents a product maintained by the Warehouse Management System.

Individual Item information is defined in Feature 4.

### Warehouse

Represents the warehouse where an Item experienced an out-of-stock condition.

Warehouse maintenance is defined in Feature 2.

### Warehouse Location

Represents a physical storage bin or slot containing Inventory.

### Inventory

Represents the quantity of an Individual Item stored at a Warehouse Location.

Inventory maintenance is defined in Feature 3.

### User

Represents an authorized Manager or reporting employee who requests the report.

---

## Initial Data Model

### Out-of-Stock Report

The Out-of-Stock Report is a generated reporting view rather than a permanent business transaction.

**Report Parameters:**

| Parameter | Type | Description |
|---|---|---|
| warehouseId | Integer | Optional Warehouse filter |
| startDate | Date | Optional report start date |
| endDate | Date | Optional report end date |

**Displayed Information:**

| Field | Description |
|---|---|
| Item Number | SKU identifying the Individual Item |
| Item Description | Description of the affected Item |
| Warehouse | Warehouse where the stockout occurred |
| Out-of-Stock Start | Date and time the stockout began |
| Restocked At | Date and time physical Inventory became available again |
| Status | Currently Out of Stock or Restocked |
| Duration | Time between stockout start and resolution, or elapsed time for an active occurrence |

**Relationships:**
- The report contains zero or more Out-of-Stock Records.
- The report uses Individual Item and Warehouse information.
- The report is generated from preserved stockout history.

### Out-of-Stock Record

| Attribute | Type | Description |
|---|---|---|
| outOfStockRecordId | Integer | Unique stockout occurrence identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| warehouseId | Integer | Foreign key referencing Warehouse |
| startedAt | DateTime | Date and time the stockout began |
| resolvedAt | DateTime | Date and time Inventory became available again; nullable |
| status | String | Active or Resolved |
| source | String | System Recorded or Historical Import |
| recordedAt | DateTime | Date and time the record was created |

**Relationships:**
- Each Out-of-Stock Record references one Individual Item.
- Each Out-of-Stock Record references one Warehouse.
- An Item may have multiple Out-of-Stock Records over time.
- One Warehouse may have many Out-of-Stock Records.

**Constraints:**
- outOfStockRecordId must be unique.
- startedAt must be present.
- resolvedAt must be later than or equal to startedAt when provided.
- Only one Active Out-of-Stock Record may exist for a particular Item and Warehouse at a time.
- Resolved records must remain available for historical reporting.

**Derived Values:**
- Total Physical Inventory = Sum of Inventory quantities for the Item across all locations in the Warehouse.
- Stockout Duration = resolvedAt - startedAt for resolved occurrences.
- Active Stockout Duration = Report Time - startedAt for active occurrences.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| itemNumber | String | Unique SKU or Item Number |
| description | String | Item description |
| isActive | Boolean | Indicates whether the Item is active |

**Relationships:**
- One Individual Item may exist in multiple Warehouse Locations.
- One Individual Item may have multiple historical Out-of-Stock Records.
- Individual Item maintenance is defined in Feature 4.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique Warehouse identifier |
| warehouseCode | String | Unique Warehouse Code |
| name | String | Warehouse name |
| isActive | Boolean | Indicates whether the Warehouse is active |

**Relationships:**
- One Warehouse contains multiple Warehouse Locations.
- One Warehouse may have multiple Out-of-Stock Records.
- Warehouse maintenance is defined in Feature 2.

### Warehouse Location

| Attribute | Type | Description |
|---|---|---|
| locationId | Integer | Unique Warehouse Location identifier |
| warehouseId | Integer | Foreign key referencing Warehouse |

**Relationships:**
- Each Warehouse Location belongs to one Warehouse.
- Each Warehouse Location may contain Inventory records.

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique Inventory identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| locationId | Integer | Foreign key referencing Warehouse Location |
| quantity | Integer | Current physical quantity in individual units |

**Relationships:**
- Each Inventory record references one Individual Item.
- Each Inventory record references one Warehouse Location.
- Warehouse-level Inventory totals are calculated from the locations belonging to that Warehouse.

**Constraints:**
- quantity cannot be negative.
- The combination of itemId and locationId must be unique.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Authorization role |

**Relationships:**
- Authorized Managers generate and review Out-of-Stock Reports.
- Report access is read-only.

---

## Gherkin AC

### US-16.1: View Items That Have Been Out of Stock

#### AC-16.1.1: Out-of-Stock Items exist

**Given** Item A has an Out-of-Stock Record in Warehouse W1  
**And** the User is authenticated as a Manager  
**When** the Manager generates the Out-of-Stock Report  
**Then** the report identifies Item A  
**And** displays the Warehouse and stockout information.

#### AC-16.1.2: No Out-of-Stock Items exist

**Given** the system has complete stockout history for the requested reporting period  
**And** no Out-of-Stock Records match the report filters  
**When** the Manager generates the report  
**Then** the system displays no out-of-stock occurrences  
**And** indicates that no matching records were found.

#### AC-16.1.3: Item previously out of stock

**Given** Item A was out of stock in Warehouse W1  
**And** the Item has since been replenished  
**When** the Manager requests historical out-of-stock information  
**Then** the report includes the previous stockout occurrence  
**And** identifies the occurrence as Restocked.

#### AC-16.1.4: Out-of-stock condition begins

**Given** Item A has 5 physical units remaining across Warehouse W1  
**And** no active stockout record exists for that Item and Warehouse  
**When** a confirmed Inventory transaction reduces the total physical quantity to zero  
**Then** the system creates an Out-of-Stock Record  
**And** records the start date and time  
**And** identifies the occurrence as Active.

#### AC-16.1.5: Item is restocked

**Given** Item A has an active Out-of-Stock Record in Warehouse W1  
**And** its total physical Inventory is zero  
**When** a confirmed Put Away movement increases its total physical Inventory to 10 units  
**Then** the system records the stockout resolution time  
**And** changes the record status to Resolved  
**And** preserves the historical occurrence.

### US-16.2: Review Out-of-Stock Item Information

#### AC-16.2.1: Display Item information

**Given** an Out-of-Stock Record exists for Item A  
**When** the Manager views the report  
**Then** the report displays the Item Number and description  
**And** identifies the Warehouse and stockout start time.

#### AC-16.2.2: Display multiple occurrences

**Given** Item A was out of stock twice during the selected period  
**When** the Manager generates the report  
**Then** the report displays both occurrences separately  
**And** preserves their individual start and resolution times.

#### AC-16.2.3: Display active occurrence

**Given** Item A has an active Out-of-Stock Record  
**When** the Manager views the report  
**Then** the occurrence is identified as Currently Out of Stock  
**And** the Restocked At field is empty.

#### AC-16.2.4: Display resolved occurrence

**Given** Item A has a resolved Out-of-Stock Record  
**When** the Manager views the report  
**Then** the occurrence is identified as Restocked  
**And** the date and time Inventory became available again are displayed.

#### AC-16.2.5: Prevent duplicate active stockout records

**Given** Item A already has an active Out-of-Stock Record in Warehouse W1  
**And** its total physical Inventory remains zero  
**When** another Inventory transaction is recorded without restoring positive Inventory  
**Then** the system does not create a second active Out-of-Stock Record.

### US-16.3: Review Historical Stockouts

#### AC-16.3.1: Preserve historical occurrence after replenishment

**Given** Item A was out of stock on October 1  
**And** Inventory was replenished on October 3  
**When** the Manager generates a report covering October 1 through October 3  
**Then** the report includes the occurrence  
**And** displays October 1 as the start date  
**And** October 3 as the restocking date.

#### AC-16.3.2: Preserve stockout history after deactivation

**Given** Item A has a historical Out-of-Stock Record  
**When** Item A is deactivated  
**Then** the system preserves the historical record  
**And** keeps the Item identifiable in the report.

#### AC-16.3.3: Historical information is unavailable

**Given** the requested reporting period includes dates before reliable Inventory history was available  
**When** the Manager generates the report  
**Then** the system identifies that the historical information is incomplete  
**And** does not claim that no stockouts occurred during the missing period.

#### AC-16.3.4: Record another stockout after restocking

**Given** Item A had a stockout that was resolved  
**And** the Item currently has positive physical Inventory  
**When** a later confirmed Inventory transaction reduces the total to zero again  
**Then** the system creates a new Out-of-Stock Record  
**And** preserves the earlier resolved occurrence.

### US-16.4: Filter Out-of-Stock Report

#### AC-16.4.1: Filter by Warehouse

**Given** stockout occurrences exist in Warehouses W1 and W2  
**When** the Manager filters the report to Warehouse W1  
**Then** the report includes matching occurrences from W1  
**And** excludes occurrences from W2.

#### AC-16.4.2: Filter by date range

**Given** stockout occurrences exist both inside and outside the selected period  
**When** the Manager selects a valid date range  
**Then** the system displays occurrences that overlap the selected period  
**And** excludes occurrences entirely outside the period.

#### AC-16.4.3: Include ongoing stockout in date range

**Given** Item A became out of stock before the selected start date  
**And** it remained out of stock during the selected period  
**When** the Manager generates the report  
**Then** the report includes the ongoing stockout occurrence.

#### AC-16.4.4: Reject invalid date range

**Given** the Manager is entering report filters  
**When** the selected start date is later than the end date  
**Then** the system rejects the date range  
**And** requests valid dates.

#### AC-16.4.5: No matching records

**Given** reliable stockout history exists for the selected period  
**And** no occurrences match the selected Warehouse and dates  
**When** the Manager generates the report  
**Then** the report displays an empty result  
**And** indicates that no matching out-of-stock occurrences were found.

#### AC-16.4.6: Reject unauthorized report access

**Given** a User is authenticated as a Driver without reporting permission  
**When** the User attempts to generate the Out-of-Stock Report  
**Then** the system denies access  
**And** does not display restricted report information.
