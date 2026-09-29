# Feature: Maintain Suppliers

**Feature ID:** 5  
**Branch pattern:** `feature/5-maintain-suppliers`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system maintains information about the suppliers from whom the warehouse orders items.

---

## User Stories

### US-5.1: Add a Supplier

**As a** [TBD: authorized role not specified]  
**I want to** add a supplier  
**So that** the warehouse can keep information about suppliers it orders from

**Priority:** P1  
**Independent test:** Add a supplier with valid information and confirm it is saved.

### US-5.2: Edit a Supplier

**As a** [TBD: authorized role not specified]  
**I want to** edit a supplier  
**So that** the supplier information stays accurate

**Priority:** P1  
**Independent test:** Change an existing supplier's information and confirm the changes are saved.

### US-5.3: Delete a Supplier

**As a** [TBD: authorized role not specified]  
**I want to** delete a supplier  
**So that** a supplier record that should no longer be kept can be removed

**Priority:** P1  
**Independent test:** Delete an existing supplier and confirm it is no longer kept.

---

## Functional Requirements

- **FR-001:** The system MUST allow a Supplier to be added.
- **FR-002:** The system MUST allow an existing Supplier to be edited.
- **FR-003:** The system MUST allow an existing Supplier to be deleted.
- **FR-004:** The system MUST maintain a Name for each Supplier.
- **FR-005:** The system MUST maintain an Address for each Supplier.
- **FR-006:** The system MUST maintain a Phone Number for each Supplier.
- **FR-007:** The system MUST maintain an Email for each Supplier.
- **FR-008:** The system MUST maintain a Supplier Number for each Supplier.
- **FR-009:** The system MUST maintain the identifying number the Supplier uses for the Warehouse/Company.
- **FR-010:** The system MUST save a Supplier when the information is valid.
- **FR-011:** The system MUST NOT save a Supplier when the information is invalid.
- **FR-012:** The authorized role for adding, editing, or deleting Suppliers is **TBD**.
- **FR-013:** Whether Supplier Number must be unique is **TBD**.
- **FR-014:** The exact name of the identifying number the Supplier uses for the Warehouse/Company is **TBD**.
- **FR-015:** Behavior when Edit or Delete is attempted for a Supplier that does not exist is **TBD**.
- **FR-016:** Behavior when a Supplier is deleted while associated with an Individual Item or Supplier Order is **TBD**.

---

## Key Entities

- **Supplier:** A supplier from whom the warehouse orders items.
- **Individual Item:** A product that may be associated with a Supplier.
- **Supplier Order:** An order placed with a Supplier.

---

## Initial Data Model

### Supplier

Represents a Supplier from whom the warehouse orders items.

**Attributes:**
- Name
- Address
- Phone Number
- Email
- Supplier Number
- Warehouse/Company Number used by the Supplier

**Relationships:**
- A Supplier may be associated with Individual Items.
- A Supplier may be associated with Supplier Orders.

### Individual Item

Represents a product that may be supplied by a Supplier.

**Relationships:**
- An Individual Item may be associated with a Supplier.
- Individual Item maintenance is handled separately in Feature 4.

### Supplier Order

Represents an order placed with a Supplier.

**Relationships:**
- A Supplier may have Supplier Orders.
- Supplier Order creation is handled separately in Feature 9.

---

## Gherkin AC

### US-5.1: Add a Supplier

#### AC-5.1.1: Supplier is saved

**Given** a Supplier is being added  
**When** valid Supplier information is entered and saved  
**Then** the system saves the Supplier record

#### AC-5.1.2: Invalid Supplier is not saved

**Given** a Supplier is being added  
**When** invalid Supplier information is entered  
**Then** the system does not save the Supplier record

### US-5.2: Edit a Supplier

#### AC-5.2.1: Supplier changes are saved

**Given** an existing Supplier record  
**When** the Supplier information is changed with valid information  
**Then** the system saves the updated Supplier information

#### AC-5.2.2: Invalid changes are not saved

**Given** an existing Supplier record  
**When** invalid Supplier information is entered  
**Then** the system does not save the invalid changes  
**And** the existing Supplier information remains unchanged

### US-5.3: Delete a Supplier

#### AC-5.3.1: Supplier is deleted

**Given** an existing Supplier record  
**When** the Supplier is deleted  
**Then** the Supplier record is removed

#### AC-5.3.2: Supplier does not exist

**Given** no matching Supplier record exists  
**When** an attempt is made to delete the Supplier  
**Then** [TBD: behavior not specified in the interview or class notes]