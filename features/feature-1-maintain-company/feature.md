
# Feature: Maintain Company

**Feature ID:** 1  
**Branch pattern:** `feature/1-maintain-company`  
**Status:** Draft - Proposed Rules and Design Pending Approval  
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

## Assumptions

- **A-001:** The Warehouse Management System is intended to manage one company, which may operate multiple warehouses.
- **A-002:** Managers and Administrators are authorized to maintain company information.
- **A-003:** Company information is shared across warehouses rather than owned by individual users.
- **A-004:** Company deletion is permitted only when no associated warehouses or historical transactions exist.
- **A-005:** User authentication and role management are provided by shared system security functionality.
- **A-006:** The exact company address format and contact-field validation rules remain subject to stakeholder confirmation.
- **A-007:** Company information is maintained through a screen that communicates with the Warehouse backend.
- **A-008:** The database enforces the single-company rule in addition to application-level validation.

---

## Edge Cases

- **EC-001:** A user attempts to create a second company when one already exists. The system rejects the request.
- **EC-002:** A user submits an empty or whitespace-only company name. The system rejects the request.
- **EC-003:** A user attempts to edit or delete a company when no company record exists. The system rejects the request.
- **EC-004:** A Warehouse Worker, Receiver, Picker, or Driver attempts to modify company information. The system denies access.
- **EC-005:** A user attempts to delete a company with associated warehouses. The system rejects the deletion.
- **EC-006:** A user attempts to delete a company with historical transactions. The system rejects the deletion.
- **EC-007:** Two authorized users attempt to create the company simultaneously. Only one creation can succeed.
- **EC-008:** An invalid update is submitted for an existing company. The original record remains unchanged.
- **EC-009:** A user attempts to save company information when the backend is unavailable. The screen reports the failure and does not claim that the changes were saved.
- **EC-010:** A user attempts to delete a company while another transaction is creating a related warehouse. The system must not leave an invalid relationship.

---

## Success Criteria

- **SC-001:** The system never stores more than one Company record.
- **SC-002:** An authorized Manager or Administrator can create a valid Company record when none exists.
- **SC-003:** Authorized users can update Company information without changing its Company ID.
- **SC-004:** All invalid creation and update requests are rejected without unintended changes.
- **SC-005:** Company deletion succeeds only when no associated warehouses or historical transactions exist.
- **SC-006:** Unauthorized users cannot create, modify, or delete Company records.
- **SC-007:** All thirteen original Gherkin acceptance scenarios for Feature 1 pass their corresponding verification tests.
- **SC-008:** Concurrent company creation requests cannot produce duplicate Company records.
- **SC-009:** Failed deletion requests preserve existing Company and Warehouse relationships.
- **SC-010:** Company maintenance screens display appropriate validation, authorization, and operation-result messages.

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

**Design constraints:**
- companyId is generated by the system and cannot be edited.
- name must not be empty or contain only whitespace.
- The database must enforce the single-company constraint.
- Company deletion must be blocked when dependent records exist.
- Company deletion must not cascade into Warehouse or historical business records.

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

---

## Data Ownership

### Company Data

**Owner:** Company Management functionality (Feature 1).

The Company component is responsible for:
- Creating the single Company record.
- Validating Company information.
- Updating Company contact information.
- Enforcing the single-company rule.
- Checking deletion eligibility.
- Deleting an unused Company record.

Other features may read Company information but must not modify it directly.

### Warehouse Data

**Owner:** Maintain Warehouses (Feature 2).

Feature 1 may check whether Warehouses reference the Company before deletion.

Feature 1 must not create, modify, or delete Warehouse records as a side effect of Company maintenance.

### User and Authorization Data

**Owner:** Shared authentication and authorization functionality.

Feature 1 uses the authenticated user's role to determine whether Company maintenance operations are permitted.

Feature 1 does not manage user accounts, passwords, or role assignments.

### Data Consistency Rules

- The Company ID is the reference used by associated Warehouses.
- Company updates must preserve the Company ID.
- Company deletion must not orphan Warehouses or invalidate historical transactions.
- Database relationship constraints must protect referenced Company records.
- Validation and authorization must be enforced by the backend, not only by the user interface.

---

## API Requirements

**Design status:** Proposed API contract for the Warehouse backend. Endpoint names and implementation details must be checked against the project's API conventions.

**Base resource:** `/api/company`

### API-1.1: Retrieve Company

**Method:** GET  
**Endpoint:** `/api/company`

**Purpose:** Retrieve the current Company record for display.

**Authorization:**
- Authenticated users with Company viewing permission may retrieve the record.
- Managers and Administrators may use the returned information for maintenance.

**Successful response: 200 OK**

Example:

```json
{
  "companyId": 1,
  "name": "Warehouse Distribution Company",
  "address": "123 Distribution Drive",
  "phone": "405-555-0100",
  "email": "contact@example.com"
}
```

**Error responses:**
- `401 Unauthorized` when authentication is required but missing.
- `403 Forbidden` when the user lacks Company viewing permission.
- `404 Not Found` when no Company exists.

**Traceability:** FR-001, FR-005, FR-015; US-1.1, US-1.2.

### API-1.2: Create Company

**Method:** POST  
**Endpoint:** `/api/company`

**Purpose:** Create the single Company record.

**Authorization:** Manager or Administrator.

**Request body:**

```json
{
  "name": "Warehouse Distribution Company",
  "address": "123 Distribution Drive",
  "phone": "405-555-0100",
  "email": "contact@example.com"
}
```

**Successful response: 201 Created**

The response includes the newly generated Company ID and stored Company information.

**Validation:**
- Company name is required.
- Company name must not be blank after trimming whitespace.
- A second Company cannot be created.
- Company ID is generated by the system.
- Invalid requests must not change stored Company data.

**Error responses:**
- `400 Bad Request` for invalid Company information.
- `401 Unauthorized` for missing authentication.
- `403 Forbidden` for insufficient permissions.
- `409 Conflict` when a Company already exists.

**Traceability:** US-1.1; FR-001 through FR-006, FR-008, FR-009, FR-015, FR-016; AC-1.1.1 through AC-1.1.4.

### API-1.3: Update Company

**Method:** PUT  
**Endpoint:** `/api/company/{companyId}`

**Purpose:** Update the existing Company's identifying and contact information.

**Authorization:** Manager or Administrator.

**Request body:**

```json
{
  "name": "Warehouse Distribution Company",
  "address": "456 Updated Drive",
  "phone": "405-555-0100",
  "email": "contact@example.com"
}
```

**Successful response: 200 OK**

The response contains the updated Company record.

**Validation:**
- The Company must exist.
- The Company ID cannot be changed.
- The Company name must remain nonempty.
- Invalid updates must leave the existing record unchanged.
- Only authorized users may update the Company.

**Error responses:**
- `400 Bad Request` for invalid information.
- `401 Unauthorized` for missing authentication.
- `403 Forbidden` for insufficient permissions.
- `404 Not Found` when the Company does not exist.

**Traceability:** US-1.2; FR-005 through FR-009, FR-015 through FR-017; AC-1.2.1 through AC-1.2.4.

### API-1.4: Delete Company

**Method:** DELETE  
**Endpoint:** `/api/company/{companyId}`

**Purpose:** Delete the Company only when it has no associated Warehouses or historical transactions.

**Authorization:** Manager or Administrator.

**Successful response: 204 No Content**

**Deletion rules:**
- The Company must exist.
- The user must be authorized.
- No Warehouse may reference the Company.
- No historical transaction may depend on the Company.
- The Company and related records must remain unchanged when deletion is rejected.
- Eligibility checking and deletion must be performed consistently to prevent concurrent operations from invalidating relationships.

**Error responses:**
- `401 Unauthorized` for missing authentication.
- `403 Forbidden` for insufficient permissions.
- `404 Not Found` when the Company does not exist.
- `409 Conflict` when associated Warehouses or historical transactions prevent deletion.

**Traceability:** US-1.3; FR-010 through FR-017; AC-1.3.1 through AC-1.3.5.

### Shared API Design Rules

- All Company maintenance endpoints require appropriate authentication and authorization.
- API input must be validated by the backend.
- Error responses must provide a safe, understandable explanation.
- Internal database details and sensitive server information must not appear in error messages.
- Database operations must preserve Company and Warehouse relationships.
- The frontend must not assume that an operation succeeded until the backend confirms it.
- API routes, error formatting, and service structure must follow the Warehouse starter project's existing conventions.

---

## Screen Requirements
### UI Design

### UI Design

### UI Design

![Maintain Company Screen](../../docs/ui/Maintain%20Company.png)
**Screen ID:** UI-1  
**Screen Name:** Company Maintenance  
**Proposed design file:** `docs/UI/company-maintenance.png`

### Purpose

Allow authorized Managers and Administrators to create, view, update, or delete the single Company record.

### Users and Permissions

| Role | View | Add | Edit | Delete |
|---|---|---|---|---|
| Manager | Yes | Yes | Yes | Yes |
| Administrator | Yes | Yes | Yes | Yes |
| Warehouse Worker | If authorized | No | No | No |
| Receiver | If authorized | No | No | No |
| Picker | If authorized | No | No | No |
| Driver | If authorized | No | No | No |

### Screen Fields

| Field | Control | Required | Behavior |
|---|---|---|---|
| Company ID | Read-only text | System generated | Displayed after Company creation |
| Company Name | Text input | Yes | Cannot be empty or whitespace-only |
| Address | Text input | No | Stores the Company business address |
| Phone | Text input | No | Stores the Company contact number |
| Email | Text input | No | Stores the Company contact email |

### Screen Actions

**Add Company**
- Available only when no Company exists.
- Opens an empty Company form.
- Available only to Managers and Administrators.
- Saves through the Company creation API.

**Edit Company**
- Available when a Company exists.
- Loads the current Company information.
- Allows authorized users to update editable fields.
- Does not allow Company ID modification.

**Save**
- Validates the form.
- Sends the appropriate create or update request.
- Displays confirmation after successful completion.
- Displays validation errors when saving fails.

**Cancel**
- Discards unsaved changes.
- Returns to the previous Company display state.

**Delete**
- Available to authorized Managers and Administrators when a Company exists.
- Requires a confirmation step.
- Sends a deletion request to the backend.
- Displays a meaningful message if associated Warehouses or historical transactions prevent deletion.

### Screen States

**No Company Exists**
- Display an informational message.
- Show Add Company for authorized users.
- Do not show usable Edit or Delete actions.

**Company Exists**
- Display the current Company information.
- Show permitted maintenance actions according to the user's role.
- Prevent creation of a second Company.

**Editing**
- Display editable Company fields.
- Show Save and Cancel actions.
- Keep Company ID read-only.

**Saving**
- Prevent accidental duplicate submission.
- Wait for the backend response.
- Show success or error feedback.

**Deletion Confirmation**
- Display a confirmation dialog before requesting deletion.
- Allow the user to confirm or cancel.

### Validation and Messages

| Condition | Proposed Message |
|---|---|
| Company name missing | Company name is required. |
| Duplicate Company | A company already exists. |
| Company not found | Company record was not found. |
| Unauthorized action | You do not have permission to maintain company information. |
| Company has Warehouses | This company cannot be deleted because warehouses are associated with it. |
| Historical records exist | This company cannot be deleted because historical records depend on it. |
| Successful creation | Company created successfully. |
| Successful update | Company updated successfully. |
| Successful deletion | Company deleted successfully. |
| Backend unavailable | The operation could not be completed. Please try again. |

### Navigation

- The Company Maintenance screen is accessible through the appropriate management or administration menu.
- Unauthorized roles must not be offered Company maintenance actions.
- The screen must support returning to the main Warehouse menu.

### UI Deliverable

A design image for the Company Maintenance screen must be created in:

`docs/UI/company-maintenance.png`

The image must be linked to Feature 1.

The proposed image should show the Company fields, available actions, and the single-company workflow.

**Traceability:** US-1.1, US-1.2, US-1.3; FR-001 through FR-017; AC-1.1.1 through AC-1.3.5.

---

## Definition of Done

Feature 1 is considered complete when all applicable requirements, design artifacts, and verification activities are satisfied.

### Requirements and Design

- [ ] All three User Stories are documented.
- [ ] All seventeen Functional Requirements are addressed.
- [ ] Assumptions, Edge Cases, and Success Criteria are documented.
- [ ] Key Entities and the Initial Data Model are documented.
- [ ] Data Ownership responsibilities are defined.
- [ ] API Requirements are documented.
- [ ] Screen Requirements are documented.
- [ ] Out-of-Scope functionality is identified.
- [ ] Unresolved design choices are reviewed with the stakeholder or professor.

### API and Backend

- [ ] Company retrieval is supported.
- [ ] Authorized Company creation is supported.
- [ ] Authorized Company updates are supported.
- [ ] Authorized Company deletion is supported.
- [ ] The system enforces the single-company constraint.
- [ ] The Company ID is system-generated and remains unchanged during updates.
- [ ] Invalid input is rejected without modifying existing data.
- [ ] Deletion is blocked when associated Warehouses or historical transactions exist.
- [ ] Backend authorization protects all Company maintenance operations.
- [ ] Database constraints protect Company and Warehouse relationships.
- [ ] Concurrent requests cannot create multiple Companies or orphan dependent records.

### User Interface

- [ ] The Company Maintenance screen is designed.
- [ ] The screen supports Add, Edit, Save, Cancel, and Delete actions as appropriate.
- [ ] Company ID is displayed as read-only.
- [ ] Required field validation is displayed.
- [ ] Unauthorized users cannot perform maintenance actions.
- [ ] Successful operations display confirmation messages.
- [ ] Failed operations display understandable error messages.
- [ ] A Company Maintenance screen image is stored in `docs/UI/`.
- [ ] The screen image is linked to this feature specification.

### Testing

- [ ] AC-1.1.1 through AC-1.1.4 are verified.
- [ ] AC-1.2.1 through AC-1.2.4 are verified.
- [ ] AC-1.3.1 through AC-1.3.5 are verified.
- [ ] Tests cover missing and invalid Company information.
- [ ] Tests cover unauthorized access.
- [ ] Tests cover duplicate Company creation.
- [ ] Tests cover deletion with dependent Warehouses.
- [ ] Tests cover deletion with historical transactions.
- [ ] Tests cover attempts to update or delete a nonexistent Company.
- [ ] Tests cover concurrent Company creation and deletion-related consistency.
- [ ] Regression tests confirm that Company maintenance does not damage Warehouse relationships.

### Documentation and Review

- [ ] Feature 1 follows the required OC Speckit section structure.
- [ ] Relevant architecture decisions are documented in `docs/ADRs/`.
- [ ] Relevant non-functional requirements are addressed in `docs/NFR/`.
- [ ] The Company component is represented in the appropriate C4 architecture diagrams.
- [ ] Design documentation is committed to the `design-draft` branch.
- [ ] Changes are pushed to GitHub for review.

**Draft note:** These checkboxes represent completion criteria. They are not claims that implementation, testing, or UI design has already been completed.

---

## Out of Scope

The following functionality is not included in Feature 1:

- Managing multiple independent Companies within the same Warehouse Management System.
- Creating, editing, or deleting Warehouses; these operations belong to Feature 2.
- Maintaining Individual Items, Suppliers, Customers, or Inventory.
- Creating Supplier Orders or Customer Orders.
- Receiving, Put Away, Picking, Shipping, or Delivery operations.
- Creating user accounts or assigning user roles.
- Managing authentication credentials or passwords.
- Editing historical transactions through Company maintenance.
- Automatically deleting Warehouses or historical transactions when deleting a Company.
- Building financial accounting, payroll, or human resources functionality.
- Maintaining company branches as separate legal businesses.

**Future consideration:** Multi-company support would require changes to the current single-company rule, data relationships, authorization model, and associated Warehouse features. It is not part of the present requirements.
