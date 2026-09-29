# Feature: Report Items That Have Been Out of Stock

**Feature ID:** 16  
**Branch pattern:** `feature/16-items-out-of-stock`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system provides a report identifying Individual Items that have been out of stock so that a manager can review inventory exceptions.

---

## User Stories

### US-16.1: View Items That Have Been Out of Stock

**As a** manager  
**I want to** see which items have been out of stock  
**So that** I can review inventory exceptions

**Priority:** P1  
**Independent test:** Generate the report and confirm that items recorded as having been out of stock are identified.

### US-16.2: Review Out-of-Stock Item Information

**As a** manager  
**I want to** review information about items that have been out of stock  
**So that** I can understand which inventory items experienced the exception

**Priority:** P1  
**Independent test:** View an item in the report and confirm that the system identifies the Individual Item and its out-of-stock information.

---

## Functional Requirements

- **FR-001:** The system MUST identify Individual Items that have been out of stock.
- **FR-002:** The system MUST provide the identified Individual Items in a report.
- **FR-003:** The report MUST identify the Individual Item associated with each out-of-stock occurrence.
- **FR-004:** The report MUST use Inventory information recorded by the warehouse system.
- **FR-005:** The system MUST preserve enough information to determine that an Individual Item has previously been out of stock.
- **FR-006:** If no Individual Items have been recorded as out of stock, the report MUST contain no out-of-stock items.
- **FR-007:** The exact condition that defines when an Individual Item is considered out of stock is **TBD**.
- **FR-008:** The exact historical information that must be stored for an out-of-stock occurrence is **TBD**.
- **FR-009:** Whether each out-of-stock occurrence or only each affected Individual Item is shown is **TBD**.
- **FR-010:** Whether the report shows when an Individual Item went out of stock is **TBD**.
- **FR-011:** Whether the report shows when Inventory became available again is **TBD**.
- **FR-012:** The time period covered by the report is **TBD**.
- **FR-013:** Whether the report supports a date range is **TBD**.
- **FR-014:** Whether the report can be filtered by Warehouse or Warehouse Location is **TBD**.
- **FR-015:** Behavior when historical Inventory information is unavailable is **TBD**.

---

## Key Entities

- **Out-of-Stock Report:** A reporting view used by a manager to identify Individual Items that have been out of stock.
- **Individual Item:** A product maintained by the warehouse that may appear in the report.
- **Inventory:** The quantity of an Individual Item in a Warehouse Location.
- **Out-of-Stock Record:** Historical information indicating that an Individual Item experienced an out-of-stock condition.

---

## Initial Data Model

### Out-of-Stock Report

Represents the reporting view used to identify Individual Items that have been out of stock.

**Relationships:**
- An Out-of-Stock Report contains information about Individual Items that have been out of stock.
- The report uses Inventory and historical out-of-stock information maintained by the warehouse system.

### Individual Item

Represents a product maintained by the warehouse.

**Relevant Attributes:**
- SKU / Item Number
- Description

**Relationships:**
- An Individual Item may exist as Inventory in one or more Warehouse Locations.
- An Individual Item may appear in the Out-of-Stock Report when it meets the out-of-stock condition.
- An Individual Item may have historical Out-of-Stock Records.

### Inventory

Represents an Individual Item quantity in a Warehouse Location.

**Relevant Attributes:**
- Individual Item
- Warehouse Location
- Quantity

**Relationships:**
- Inventory information is used to determine inventory availability.
- Historical Inventory information may be required to determine whether an Individual Item has been out of stock.

### Out-of-Stock Record

Represents historical information indicating that an Individual Item experienced an out-of-stock condition.

**Attributes:**
- Individual Item
- [TBD: Date/time information]
- [TBD: Quantity information]
- [TBD: Warehouse/Location information]

**Relationships:**
- An Out-of-Stock Record refers to an Individual Item.
- Out-of-Stock Records may be used to produce the Out-of-Stock Report.

---

## Gherkin AC

### US-16.1: View Items That Have Been Out of Stock

#### AC-16.1.1: Out-of-Stock Items exist

**Given** one or more Individual Items have been recorded as out of stock  
**When** the manager requests the Out-of-Stock Report  
**Then** the system identifies those Individual Items in the report

#### AC-16.1.2: No Out-of-Stock Items exist

**Given** no Individual Items have been recorded as out of stock  
**When** the manager requests the Out-of-Stock Report  
**Then** the report contains no out-of-stock items

#### AC-16.1.3: Previously Out-of-Stock Item

**Given** an Individual Item was previously out of stock  
**And** the Individual Item currently has Inventory available  
**When** the manager requests historical out-of-stock information  
**Then** [TBD: exact historical reporting behavior not specified in the interview or class notes]

### US-16.2: Review Out-of-Stock Item Information

#### AC-16.2.1: Individual Item is identified in Report

**Given** an Individual Item has been recorded as out of stock  
**When** the Individual Item appears in the report  
**Then** the report identifies the Individual Item

#### AC-16.2.2: Individual Item has multiple Out-of-Stock occurrences

**Given** the same Individual Item has been out of stock more than once  
**When** the manager views the report  
**Then** [TBD: whether separate occurrences or a summarized result should be displayed]

#### AC-16.2.3: Historical Inventory information is unavailable

**Given** historical Inventory information needed for the report is unavailable  
**When** the manager requests the Out-of-Stock Report  
**Then** [TBD: behavior not specified in the interview or class notes]