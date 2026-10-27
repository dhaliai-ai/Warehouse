
# Feature: Maintain Company

**Feature ID:** 1  
**Branch pattern:** `feature/1-maintain-company`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-25  
**Input:** The Warehouse Management System supports one company that may operate multiple warehouses. Authorized management personnel maintain company information. The system protects relationships and historical records when company information is updated or deleted.

---

## User Stories

### US-1.1: Add Company

**As a** Manager or Administrator  
**I want to** add the company's information  
**So that** the system can identify the business operating the warehouses.

**Priority:** P1  
**Independent test:** Create a company with valid information and verify that exactly one company record exists.

### US-1.2: Edit Company

**As a** Manager or Administrator  
**I want to** update the company's information  
**So that** the business information remains accurate and current.

**Priority:** P1  
**Independent test:** Update the company's contact information and verify that the changes are saved.

### US-1.3: Delete Company

**As a** Manager or Administrator  
**I want to** delete a company record when it has no associated warehouses or historical transactions  
**So that** an unused company record can be removed safely.

**Priority:** P1  
**Independent test:** Verify that deletion succeeds for an unused company and is rejected when related business records exist.

---

## Functional Requirements

- **FR-001:** The system MUST support at most one company record at a time.
- **FR-002:** The system MUST allow an authorized Manager or Administrator to create a company when no company record exists.
- **FR-003:** The system MUST prevent creation of a second company record.
- **FR-004:** The system MUST assign a unique, system-generated Company ID.
- **FR-005:** The system MUST store the company's name, address, phone number, and email address.
- **FR-006:** The system MUST require a nonempty company name.
- **FR-007:** The system MUST allow authorized Managers and Administrators to update company information.
- **FR-008:** The system MUST validate required company information before saving.
- **FR-009:** The system MUST reject invalid information without changing the existing company record.
- **FR-010:** The system MUST support multiple warehouses associated with the company.
- **FR-011:** Each warehouse MUST reference the company to which it belongs.
- **FR-012:** The system MUST allow authorized Managers and Administrators to delete the company only when no associated warehouses or historical transactions exist.
- **FR-013:** The system MUST prevent company deletion when associated warehouses or historical transactions exist.
- **FR-014:** The system MUST preserve existing company information when a deletion request is rejected.
- **FR-015:** The system MUST restrict company creation, modification, and deletion to Managers and Administrators.
- **FR-016:** Warehouse workers, pickers, receivers, and drivers MUST NOT modify company information.
- **FR-017:** The system MUST reject attempts to edit or delete a company record that does not exist.

---

## Key Entities

### Company

Represents the single business operating the Warehouse Management System.

The Company stores identifying and contact information and is associated with multiple warehouses.

### Warehouse

Represents a physical warehouse operated by the company.

Each warehouse belongs to the company. Warehouse maintenance is specified in Feature 2.

### User

Represents an authenticated system user whose assigned role determines whether company information may be maintained.

---

## Initial Data Model

### Company

| Attribute | Type | Description |
|---|---|---|
| companyId | Integer | Unique, system-generated identifier; primary key |
| name | String | Company name; required |
| address | String | Company business address |
| phone | String | Company contact telephone number |
| email | String | Company contact email address |

**Relationships:**
- One Company can have zero or many Warehouses.
- Each Warehouse belongs to one Company.
- The system permits at most one Company record.

### Warehouse

| Attribute | Type | Description |
|---|---|---|
| warehouseId | Integer | Unique warehouse identifier |
| companyId | Integer | Foreign key referencing Company |

**Relationships:**
- Each Warehouse belongs to the Company.
- Additional Warehouse attributes are defined in Feature 2.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique user identifier |
| role | String | Assigned authorization role |

**Relationships:**
- A user's role determines whether the user may maintain Company information.
- User authentication and role management are handled by the system's shared security functionality.

---

## Gherkin AC

### US-1.1: Add Company

#### AC-1.1.1: Successfully create Company

**Given** no Company record exists  
**And** the user is authenticated as a Manager or Administrator  
**When** the user enters valid company information  
**And** saves the record  
**Then** the system creates the Company  
**And** assigns a unique Company ID  
**And** exactly one Company record exists.

#### AC-1.1.2: Reject duplicate Company

**Given** a Company record already exists  
**And** the user is authenticated as a Manager  
**When** the user attempts to create another Company  
**Then** the system rejects the request  
**And** the existing Company remains unchanged.

#### AC-1.1.3: Reject missing company name

**Given** no Company record exists  
**And** the user is authenticated as an Administrator  
**When** the user submits Company information with an empty name  
**Then** the system rejects the request  
**And** no Company record is created.

#### AC-1.1.4: Reject unauthorized Company creation

**Given** no Company record exists  
**And** the user is authenticated as a Warehouse Worker  
**When** the user attempts to create a Company  
**Then** the system denies the operation  
**And** no Company record is created.

### US-1.2: Edit Company

#### AC-1.2.1: Successfully update Company

**Given** a Company record exists  
**And** the user is authenticated as a Manager  
**When** the user updates the company's address  
**And** saves the changes  
**Then** the system stores the updated address  
**And** the Company ID remains unchanged.

#### AC-1.2.2: Reject invalid Company updates

**Given** a Company record exists  
**And** the user is authenticated as an Administrator  
**When** the user removes the required company name  
**And** attempts to save the changes  
**Then** the system rejects the update  
**And** the previously stored information remains unchanged.

#### AC-1.2.3: Reject unauthorized Company updates

**Given** a Company record exists  
**And** the user is authenticated as a Driver  
**When** the user attempts to modify Company information  
**Then** the system denies the request  
**And** the Company record remains unchanged.

#### AC-1.2.4: Reject editing a nonexistent Company

**Given** no Company record exists  
**And** the user is authenticated as a Manager  
**When** the user attempts to update Company information  
**Then** the system rejects the request  
**And** no Company record is created.

### US-1.3: Delete Company

#### AC-1.3.1: Successfully delete an unused Company

**Given** a Company record exists  
**And** no Warehouses are associated with it  
**And** no historical transactions reference it  
**And** the user is authenticated as an Administrator  
**When** the user requests Company deletion  
**Then** the system deletes the Company record  
**And** no Company record remains.

#### AC-1.3.2: Prevent deletion when Warehouses exist

**Given** a Company record exists  
**And** one or more Warehouses belong to it  
**And** the user is authenticated as a Manager  
**When** the user requests Company deletion  
**Then** the system rejects the deletion  
**And** the Company remains stored  
**And** its associated Warehouses remain unchanged.

#### AC-1.3.3: Prevent deletion when historical transactions exist

**Given** a Company record exists  
**And** historical business transactions reference it  
**And** the user is authenticated as an Administrator  
**When** the user requests Company deletion  
**Then** the system rejects the deletion  
**And** the Company and its historical records remain unchanged.

#### AC-1.3.4: Reject unauthorized Company deletion

**Given** a Company record exists  
**And** the user is authenticated as a Warehouse Worker  
**When** the user attempts to delete the Company  
**Then** the system denies the request  
**And** the Company remains unchanged.

#### AC-1.3.5: Reject deletion when Company does not exist

**Given** no Company record exists  
**And** the user is authenticated as an Administrator  
**When** the user requests Company deletion  
**Then** the system rejects the request  
**And** no Company record is changed.
