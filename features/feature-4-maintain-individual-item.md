# Feature: Maintain Individual Item

**Feature ID:** 4  
**Branch pattern:** `feature/4-maintain-individual-item`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system maintains the individual items that the warehouse buys, stores, and sells.

---

## User Stories

### US-4.1: Add an Individual Item

**As a** [TBD: authorized role not specified]  
**I want to** add an individual item  
**So that** the system can keep track of items the warehouse deals with

**Priority:** P1  
**Independent test:** Add an item with valid information and confirm it is saved.

### US-4.2: Edit an Individual Item

**As a** [TBD: authorized role not specified]  
**I want to** edit an individual item  
**So that** the item's information stays accurate

**Priority:** P1  
**Independent test:** Change an existing item's information and confirm the changes are saved.

### US-4.3: Delete an Individual Item

**As a** [TBD: authorized role not specified]  
**I want to** delete an individual item  
**So that** an item record that should no longer be kept can be removed

**Priority:** P1  
**Independent test:** Delete an existing item and confirm it is no longer kept.

---

## Functional Requirements

- **FR-001:** The system MUST allow an Individual Item to be added.
- **FR-002:** The system MUST allow an existing Individual Item to be edited.
- **FR-003:** The system MUST allow an existing Individual Item to be deleted.
- **FR-004:** The system MUST maintain a Price for each Individual Item.
- **FR-005:** The system MUST maintain an SKU / Item Number for each Individual Item.
- **FR-006:** The system MUST maintain a UPC for each Individual Item.
- **FR-007:** The system MUST maintain a Supplier for each Individual Item.
- **FR-008:** The system MUST maintain a Description for each Individual Item.
- **FR-009:** The system MUST NOT allow a duplicate SKU / Item Number.
- **FR-010:** The system MUST save an Individual Item when the information is valid.
- **FR-011:** The system MUST NOT save an Individual Item when the information is invalid.
- **FR-012:** The authorized role for adding, editing, or deleting Individual Items is **TBD**.
- **FR-013:** The required formats and validation rules for Price, SKU / Item Number, UPC, and Description are **TBD**.
- **FR-014:** Behavior when Edit or Delete is attempted for an Individual Item that does not exist is **TBD**.
- **FR-015:** Behavior when an Individual Item is deleted while referenced by Inventory or an Order is **TBD**.

---

## Key Entities

- **Individual Item:** A product that the warehouse buys, stores, and sells.
- **Supplier:** The Supplier associated with the Individual Item.
- **Inventory:** The quantity of an Individual Item stored in a Warehouse Location.

---

## Initial Data Model

### Individual Item

Represents a product that the warehouse buys, stores, and sells.

**Attributes:**
- Price
- SKU / Item Number
- UPC
- Description

**Relationships:**
- An Individual Item is associated with a Supplier.
- An Individual Item may have Inventory in one or more Warehouse Locations.

**Business Rule:**
- SKU / Item Number must not be duplicated.

### Supplier

Represents the Supplier associated with an Individual Item.

**Relationships:**
- A Supplier may supply Individual Items.
- Supplier records are maintained separately in Feature 5.

### Inventory

Represents the quantity of an Individual Item stored in a Warehouse Location.

**Relationships:**
- Inventory refers to an Individual Item.
- Inventory maintenance is handled separately in Feature 3.

---

## Gherkin AC

### US-4.1: Add an Individual Item

#### AC-4.1.1: Item is saved

**Given** an Individual Item is being added  
**When** valid item information is entered and saved  
**Then** the system saves the Individual Item  
**And** the saved item includes its Price, SKU / Item Number, UPC, Supplier, and Description

#### AC-4.1.2: Invalid Item is not saved

**Given** an Individual Item is being added  
**When** invalid item information is entered  
**Then** the system does not save the Individual Item

#### AC-4.1.3: Duplicate Item Number is not allowed

**Given** an Individual Item already exists with an SKU / Item Number  
**When** another Individual Item is added with the same SKU / Item Number  
**Then** the system does not save the duplicate Individual Item

### US-4.2: Edit an Individual Item

#### AC-4.2.1: Item changes are saved

**Given** an existing Individual Item  
**When** the item information is changed with valid information  
**Then** the system saves the updated Individual Item information

#### AC-4.2.2: Invalid changes are not saved

**Given** an existing Individual Item  
**When** invalid item information is entered  
**Then** the system does not save the invalid changes  
**And** the existing Individual Item information remains unchanged

#### AC-4.2.3: Edit does not create a duplicate Item Number

**Given** two Individual Items already exist with different SKU / Item Numbers  
**When** one item is edited to use the other item's SKU / Item Number  
**Then** the system does not save the duplicate SKU / Item Number

### US-4.3: Delete an Individual Item

#### AC-4.3.1: Item is deleted

**Given** an existing Individual Item  
**When** the Individual Item is deleted  
**Then** the Individual Item record is removed

#### AC-4.3.2: Item does not exist

**Given** no matching Individual Item exists  
**When** an attempt is made to delete the Individual Item  
**Then** [TBD: behavior not specified in the interview or class notes]