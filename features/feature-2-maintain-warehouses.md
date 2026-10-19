
# Feature: Maintain Warehouse(s)

**Feature ID:** 2  
**Branch pattern:** `feature/2-maintain-warehouses`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System supports multiple warehouses operated by one company. Authorized management personnel can add, update, and remove warehouse records. The system maintains accurate warehouse information and protects existing inventory and historical transactions.

---

## User Stories

### US-2.1: Add a Warehouse

**As a** Manager or Administrator  
**I want to** add a warehouse to the system  
**So that** the company can manage inventory and warehouse operations at multiple locations.

**Priority:** P1  
**Independent test:** Create a warehouse with valid information and verify that it is saved and associated with the company.

### US-2.2: Edit a Warehouse

**As a** Manager or Administrator  
**I want to** update warehouse information  
**So that** the company maintains accurate information about its warehouse locations.

**Priority:** P1  
**Independent test:** Update an existing warehouse's address or contact information and verify that the changes are saved.

### US-2.3: Delete a Warehouse

**As a** Manager or Administrator  
**I want to** delete a warehouse that has no inventory or historical transactions  
**So that** an unused warehouse record can be removed without losing important business information.

**Priority:** P1  
**Independent test:** Verify that an unused warehouse can be deleted and that deletion is prevented when inventory or historical transactions exist.

---

## Functional Requirements

- **FR-001:** The system MUST support multiple warehouses belonging to one company.
- **FR-002:** The system MUST allow an authorized Manager or Administrator to create a warehouse.
- **FR-003:** The system MUST assign a unique, system-generated Warehouse ID to each warehouse.
- **FR-004:** The system MUST store the warehouse name, warehouse code, address, phone number, and active status.
- **FR-005:** The system MUST require a nonempty warehouse name and warehouse code.
- **FR-006:** The system MUST prevent duplicate warehouse codes within the company.
- **FR-007:** The system MUST associate each warehouse with the existing company.
- **FR-008:** The system MUST reject warehouse creation when no company record exists.
- **FR-009:** The system MUST allow authorized Managers and Administrators to update warehouse information.
- **FR-010:** The system MUST validate warehouse information before saving.
- **FR-011:** The system MUST reject invalid warehouse information without changing the existing record.
- **FR-012:** The system MUST allow authorized Managers and Administrators to delete a warehouse only when it has no inventory or historical transactions.
- **FR-013:** The system MUST prevent warehouse deletion when inventory or historical transactions reference it.
- **FR-014:** The system MUST preserve warehouse information when a deletion request is rejected.
- **FR-015:** The system MUST support marking an existing warehouse as inactive when it is no longer used.
- **FR-016:** An inactive warehouse MUST remain available for historical reporting.
- **FR-017:** The system MUST prevent inactive warehouses from being selected for new operational transactions.
- **FR-018:** The system MUST restrict warehouse creation, modification, and deletion to Managers and Administrators.
- **FR-019:** Warehouse workers, receivers, pickers, and drivers MUST NOT modify warehouse master information.
- **FR-020:** The system MUST reject attempts to edit or delete a warehouse that does not exist.
- **FR-021:** The system MUST preserve the association between each warehouse and its company.

---

## Key Entities

### Company

Represents the business operating the Warehouse Management System.

One company may operate multiple warehouses.

### Warehouse

Represents a physical location where inventory is received, stored, picked, and shipped.

Each warehouse has identifying information, contact details, and an operational status.

### Inventory

Represents quantities of items stored in warehouse locations.

Inventory records are associated with the warehouse where the items are physically stored.

### User

Represents an authenticated system user whose assigned role determines whether warehouse information may be maintained.

---

## Initial Data Model

### Company

| Attribute | Type | Description |
|---|---|---|
| companyId | Integer | Unique company identifier; primary key |

**Relationships:**
- One Company can have zero or many Warehouses.
- Each Warehouse belongs to one Company.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique, system-generated identifier; primary key |
| companyId | Integer | Foreign key referencing Company |
| warehouseCode | String | Unique code identifying the warehouse |
| name | String | Warehouse name; required |
| address | String | Physical warehouse address |
| phone | String | Warehouse contact telephone number |
| isActive | Boolean | Indicates whether the warehouse is active |

**Relationships:**
- Each Warehouse belongs to one Company.
- One Warehouse can contain multiple inventory records.
- Warehouse inventory is maintained through Feature 3.

**Constraints:**
- `warehouseId` is unique and cannot be changed.
- `warehouseCode` must be unique within the company.
- `name` and `warehouseCode` cannot be empty.
- `companyId` must reference the existing Company.
- Warehouse deletion is restricted when inventory or historical transactions reference it.

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique inventory record identifier |
| warehouseId | Integer | Reference to the warehouse containing the inventory |

**Relationships:**
- Each inventory record is associated with a warehouse.
- Detailed inventory quantities and storage locations are defined in Feature 3.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique user identifier |
| role | String | Assigned authorization role |

**Relationships:**
- Managers and Administrators can maintain warehouse master information.
- Other operational roles cannot modify warehouse master information.

---

## Gherkin AC

### US-2.1: Add a Warehouse

#### AC-2.1.1: Successfully create Warehouse

**Given** a Company record exists  
**And** the user is authenticated as a Manager or Administrator  
**When** the user enters valid warehouse information  
**And** saves the record  
**Then** the system creates the Warehouse  
**And** assigns a unique Warehouse ID  
**And** associates the Warehouse with the Company.

#### AC-2.1.2: Create multiple Warehouses

**Given** a Company record exists  
**And** one Warehouse already belongs to the Company  
**And** the user is authenticated as a Manager  
**When** the user creates another Warehouse with valid information and a different warehouse code  
**Then** the system saves the new Warehouse  
**And** both Warehouses remain associated with the same Company.

#### AC-2.1.3: Reject missing Warehouse name

**Given** a Company record exists  
**And** the user is authenticated as an Administrator  
**When** the user submits a Warehouse with an empty name  
**Then** the system rejects the request  
**And** no Warehouse record is created.

#### AC-2.1.4: Reject duplicate Warehouse code

**Given** a Warehouse with code "WH001" already exists  
**And** the user is authenticated as a Manager  
**When** the user attempts to create another Warehouse with code "WH001"  
**Then** the system rejects the request  
**And** the existing Warehouse remains unchanged.

#### AC-2.1.5: Reject Warehouse creation without Company

**Given** no Company record exists  
**And** the user is authenticated as an Administrator  
**When** the user attempts to create a Warehouse  
**Then** the system rejects the request  
**And** no Warehouse record is created.

#### AC-2.1.6: Reject unauthorized Warehouse creation

**Given** a Company record exists  
**And** the user is authenticated as a Warehouse Worker  
**When** the user attempts to create a Warehouse  
**Then** the system denies the request  
**And** no Warehouse record is created.

### US-2.2: Edit a Warehouse

#### AC-2.2.1: Successfully update Warehouse

**Given** a Warehouse record exists  
**And** the user is authenticated as a Manager  
**When** the user changes the warehouse address  
**And** saves the changes  
**Then** the system stores the updated address  
**And** the Warehouse ID remains unchanged.

#### AC-2.2.2: Reject invalid Warehouse update

**Given** a Warehouse record exists  
**And** the user is authenticated as an Administrator  
**When** the user removes the required warehouse name  
**And** attempts to save the changes  
**Then** the system rejects the update  
**And** the previously stored warehouse information remains unchanged.

#### AC-2.2.3: Reject duplicate code during update

**Given** two Warehouses exist with different warehouse codes  
**And** the user is authenticated as a Manager  
**When** the user changes one warehouse code to match the other  
**Then** the system rejects the update  
**And** both original warehouse codes remain unchanged.

#### AC-2.2.4: Deactivate an unused Warehouse

**Given** an active Warehouse exists  
**And** the user is authenticated as a Manager  
**When** the user changes the Warehouse status to inactive  
**Then** the system saves the inactive status  
**And** the Warehouse remains available for historical reporting  
**And** the Warehouse cannot be selected for new operational transactions.

#### AC-2.2.5: Reject unauthorized Warehouse update

**Given** a Warehouse record exists  
**And** the user is authenticated as a Picker  
**When** the user attempts to modify Warehouse information  
**Then** the system denies the request  
**And** the Warehouse record remains unchanged.

#### AC-2.2.6: Reject editing nonexistent Warehouse

**Given** no Warehouse exists with the requested Warehouse ID  
**And** the user is authenticated as a Manager  
**When** the user attempts to update that Warehouse  
**Then** the system rejects the request  
**And** no Warehouse record is changed.

### US-2.3: Delete a Warehouse

#### AC-2.3.1: Successfully delete unused Warehouse

**Given** a Warehouse exists  
**And** no inventory records or historical transactions reference it  
**And** the user is authenticated as an Administrator  
**When** the user requests Warehouse deletion  
**Then** the system deletes the Warehouse record  
**And** the Company record remains unchanged.

#### AC-2.3.2: Prevent deletion when inventory exists

**Given** a Warehouse contains inventory records  
**And** the user is authenticated as a Manager  
**When** the user requests Warehouse deletion  
**Then** the system rejects the deletion  
**And** the Warehouse and its inventory records remain unchanged.

#### AC-2.3.3: Prevent deletion when historical transactions exist

**Given** a Warehouse has historical receiving, picking, or shipping transactions  
**And** the user is authenticated as an Administrator  
**When** the user requests Warehouse deletion  
**Then** the system rejects the deletion  
**And** the Warehouse and its historical records remain unchanged.

#### AC-2.3.4: Reject unauthorized Warehouse deletion

**Given** a Warehouse record exists  
**And** the user is authenticated as a Driver  
**When** the user attempts to delete the Warehouse  
**Then** the system denies the request  
**And** the Warehouse remains unchanged.

#### AC-2.3.5: Reject deletion of nonexistent Warehouse

**Given** no Warehouse exists with the requested Warehouse ID  
**And** the user is authenticated as an Administrator  
**When** the user requests deletion of that Warehouse  
**Then** the system rejects the request  
**And** no Warehouse record is changed.
