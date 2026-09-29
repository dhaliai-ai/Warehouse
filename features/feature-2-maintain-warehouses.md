# Feature: Maintain Warehouse(s)

**Feature ID:** 2  
**Branch pattern:** `feature/2-maintain-warehouses`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system allows warehouse records for the company to be added, edited, and deleted.

---

## User Stories

### US-2.1: Add a Warehouse

**As a** [TBD: authorized role not specified]  
**I want to** add a warehouse  
**So that** the company can keep a record of its warehouses

**Priority:** P1  
**Independent test:** Add a warehouse with valid information and confirm it is saved.

### US-2.2: Edit a Warehouse

**As a** [TBD: authorized role not specified]  
**I want to** edit a warehouse  
**So that** the warehouse information stays accurate

**Priority:** P1  
**Independent test:** Change an existing warehouse and confirm the saved record shows the updated information.

### US-2.3: Delete a Warehouse

**As a** [TBD: authorized role not specified]  
**I want to** delete a warehouse  
**So that** a warehouse record can be removed when it should no longer be kept

**Priority:** P1  
**Independent test:** Delete an existing warehouse and confirm it is no longer kept.

---

## Functional Requirements

- **FR-001:** The system MUST allow more than one Warehouse to be maintained for the Company.
- **FR-002:** The system MUST allow a Warehouse to be added.
- **FR-003:** The system MUST allow an existing Warehouse to be edited.
- **FR-004:** The system MUST allow an existing Warehouse to be deleted.
- **FR-005:** The system MUST save a Warehouse when the information is valid.
- **FR-006:** The system MUST NOT save a Warehouse when the information is invalid.
- **FR-007:** Warehouse attributes are **TBD** because they were not specified in the interview or class notes.
- **FR-008:** The authorized role for adding, editing, or deleting Warehouses is **TBD**.
- **FR-009:** Each Warehouse MUST belong to the Company.
- **FR-010:** Behavior when Edit or Delete is attempted for a Warehouse that does not exist is **TBD**.

---

## Key Entities

- **Company:** The company that has one or more Warehouses.
- **Warehouse:** A warehouse belonging to the Company. Its exact attributes are **TBD**.

---

## Initial Data Model

### Company

Represents the company associated with the Warehouses.

**Relationships:**
- A Company can have one or more Warehouses.

### Warehouse

Represents a warehouse belonging to the Company.

**Attributes:**
- [TBD: Warehouse attributes were not specified in the interview or class notes]

**Relationships:**
- A Warehouse belongs to the Company.

---

## Gherkin AC

### US-2.1: Add a Warehouse

#### AC-2.1.1: Warehouse is saved

**Given** a Warehouse is being added  
**When** valid Warehouse information is entered and saved  
**Then** the system saves the Warehouse record  
**And** the Warehouse is associated with the Company

#### AC-2.1.2: Invalid Warehouse is not saved

**Given** a Warehouse is being added  
**When** invalid Warehouse information is entered  
**Then** the system does not save the Warehouse record

### US-2.2: Edit a Warehouse

#### AC-2.2.1: Warehouse changes are saved

**Given** an existing Warehouse record  
**When** the Warehouse is edited with valid information  
**Then** the system saves the updated Warehouse information

#### AC-2.2.2: Invalid Warehouse changes are not saved

**Given** an existing Warehouse record  
**When** invalid Warehouse information is entered  
**Then** the system does not save the invalid changes  
**And** the existing Warehouse information remains unchanged

### US-2.3: Delete a Warehouse

#### AC-2.3.1: Warehouse is deleted

**Given** an existing Warehouse record  
**When** the Warehouse is deleted  
**Then** the Warehouse record is removed

#### AC-2.3.2: Warehouse does not exist

**Given** no matching Warehouse record exists  
**When** an attempt is made to delete the Warehouse  
**Then** [TBD: behavior not specified in the interview or class notes]