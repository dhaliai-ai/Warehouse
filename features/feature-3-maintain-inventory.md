# Feature: Maintain Inventory

**Feature ID:** 3  
**Branch pattern:** `feature/3-maintain-inventory`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system maintains the quantity of each item in its warehouse location.

---

## User Stories

### US-3.1: Add Inventory

**As a** [TBD: authorized role not specified]  
**I want to** add inventory for an item in a warehouse location  
**So that** the system can keep track of the item's quantity in that location

**Priority:** P1  
**Independent test:** Add inventory for an item in a warehouse location and confirm it is saved.

### US-3.2: Edit Inventory

**As a** [TBD: authorized role not specified]  
**I want to** edit an item's inventory quantity  
**So that** the system keeps an accurate quantity for the item

**Priority:** P1  
**Independent test:** Change an existing inventory quantity and confirm the updated quantity is saved.

### US-3.3: Delete Inventory

**As a** [TBD: authorized role not specified]  
**I want to** delete an inventory record  
**So that** an inventory record that should no longer be kept can be removed

**Priority:** P1  
**Independent test:** Delete an existing inventory record and confirm it is no longer kept.

---

## Functional Requirements

- **FR-001:** The system MUST maintain Inventory for Individual Items in Warehouse Locations.
- **FR-002:** Each Inventory record MUST identify an Individual Item.
- **FR-003:** Each Inventory record MUST identify a Warehouse Location.
- **FR-004:** Each Inventory record MUST maintain the Quantity of the Individual Item in that Warehouse Location.
- **FR-005:** The system MUST allow an Inventory record to be added.
- **FR-006:** The system MUST allow an existing Inventory record to be edited.
- **FR-007:** The system MUST allow an existing Inventory record to be deleted.
- **FR-008:** The system MUST save Inventory information when the information is valid.
- **FR-009:** The system MUST NOT save Inventory information when the information is invalid.
- **FR-010:** Inventory Quantity MUST remain separate from Quantity Ordered, Quantity Received, Quantity Picked, Quantity Shipped, and Quantity Delivered.
- **FR-011:** The authorized role for adding, editing, or deleting Inventory is **TBD**.
- **FR-012:** Behavior when Edit or Delete is attempted for an Inventory record that does not exist is **TBD**.
- **FR-013:** Whether the same Individual Item can have more than one Inventory record in the same Warehouse Location is **TBD**.

---

## Key Entities

- **Inventory:** Represents the quantity of an Individual Item in a Warehouse Location.
- **Individual Item:** The product whose quantity is being maintained.
- **Warehouse Location:** The location in the Warehouse where the Individual Item is stored.

---

## Initial Data Model

### Inventory

Represents the quantity of an Individual Item stored in a Warehouse Location.

**Attributes:**
- Individual Item
- Warehouse Location
- Quantity

**Relationships:**
- Inventory is associated with an Individual Item.
- Inventory is associated with a Warehouse Location.
- An Individual Item may have Inventory in one or more Warehouse Locations.

### Individual Item

Represents the product whose Inventory Quantity is maintained.

**Relationships:**
- An Individual Item may have Inventory in one or more Warehouse Locations.
- Individual Item details are maintained separately in Feature 4.

### Warehouse Location

Represents a location in the Warehouse where Inventory is stored.

**Attributes:**
- [TBD: exact Warehouse Location information was not specified]

**Relationships:**
- A Warehouse Location may contain Inventory.
- Inventory associates an Individual Item and Quantity with a Warehouse Location.

---

## Gherkin AC

### US-3.1: Add Inventory

#### AC-3.1.1: Inventory is saved

**Given** Inventory is being added for an Individual Item in a Warehouse Location  
**When** valid Inventory information is entered and saved  
**Then** the system saves the Inventory record  
**And** the record identifies the Individual Item, Warehouse Location, and Quantity

#### AC-3.1.2: Invalid Inventory is not saved

**Given** Inventory is being added  
**When** invalid Inventory information is entered  
**Then** the system does not save the Inventory record

### US-3.2: Edit Inventory

#### AC-3.2.1: Inventory changes are saved

**Given** an existing Inventory record  
**When** the Inventory Quantity is changed with valid information  
**Then** the system saves the updated Inventory Quantity

#### AC-3.2.2: Invalid Inventory changes are not saved

**Given** an existing Inventory record  
**When** invalid Inventory information is entered  
**Then** the system does not save the invalid changes  
**And** the existing Inventory information remains unchanged

### US-3.3: Delete Inventory

#### AC-3.3.1: Inventory is deleted

**Given** an existing Inventory record  
**When** the Inventory record is deleted  
**Then** the Inventory record is removed

#### AC-3.3.2: Inventory record does not exist

**Given** no matching Inventory record exists  
**When** an attempt is made to delete the Inventory record  
**Then** [TBD: behavior not specified in the interview or class notes]