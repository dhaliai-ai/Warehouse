
# Feature: Maintain Warehouse(s)

**Feature ID:** 2  
**Branch pattern:** `feature/2-maintain-warehouses`  
**Status:** Draft - Proposed Rules and Design Pending Approval  
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

## Assumptions

- **A-001:** The system manages one Company, which may operate multiple Warehouses.
- **A-002:** A Company must exist before any Warehouse can be created.
- **A-003:** Each Warehouse belongs to the existing Company.
- **A-004:** Warehouse codes are unique within the Company.
- **A-005:** Managers and Administrators maintain Warehouse master information.
- **A-006:** Warehouse Workers, Receivers, Pickers, and Drivers cannot modify Warehouse master information.
- **A-007:** The system provides shared authentication and authorization services.
- **A-008:** An inactive Warehouse remains in the database for historical reporting.
- **A-009:** New operational transactions cannot be assigned to an inactive Warehouse.
- **A-010:** Warehouse deletion is allowed only when no Inventory records or historical transactions reference the Warehouse.
- **A-011:** Warehouse information is maintained through a management interface connected to the Warehouse backend.
- **A-012:** Warehouse storage locations and Inventory quantities are maintained by their respective features rather than directly through Warehouse maintenance.
- **A-013:** The exact format of warehouse codes, addresses, and telephone numbers requires stakeholder confirmation.
- **A-014:** Whether a Warehouse with unfinished operational work may be deactivated requires clarification. The existing requirements prohibit new transactions at inactive Warehouses but do not specify how unfinished work is completed.

---

## Edge Cases

- **EC-001:** A user attempts to create a Warehouse before the Company exists. The system rejects the request.
- **EC-002:** A user attempts to create a Warehouse without a name. The system rejects the request.
- **EC-003:** A user attempts to create a Warehouse without a warehouse code. The system rejects the request.
- **EC-004:** A user attempts to create a Warehouse using an existing warehouse code. The system rejects the duplicate.
- **EC-005:** A user attempts to change a Warehouse code to one already assigned to another Warehouse. The system rejects the update.
- **EC-006:** A user attempts to update a nonexistent Warehouse. The system rejects the request.
- **EC-007:** A user attempts to delete a nonexistent Warehouse. The system rejects the request.
- **EC-008:** A user attempts to delete a Warehouse containing Inventory records. The system rejects the deletion.
- **EC-009:** A user attempts to delete a Warehouse with historical receiving, picking, or shipping transactions. The system rejects the deletion.
- **EC-010:** An unauthorized user attempts to create, update, or delete Warehouse information. The system denies access.
- **EC-011:** An authorized user marks a Warehouse inactive. The Warehouse remains available for historical reporting.
- **EC-012:** A user attempts to create a new operational transaction for an inactive Warehouse. The system rejects the selection.
- **EC-013:** Two authorized users attempt to create Warehouses with the same code simultaneously. The system permits only one successful creation.
- **EC-014:** An update fails validation. The previously stored Warehouse information remains unchanged.
- **EC-015:** The backend becomes unavailable during a save request. The interface displays an error and does not claim that the operation succeeded.
- **EC-016:** A related Inventory or transaction record is created while Warehouse deletion is being processed. The system must preserve valid relationships and prevent an unsafe deletion.
- **EC-017:** A Warehouse with unfinished receiving, Put Away, picking, or shipping work is selected for deactivation. The handling of existing work must follow a stakeholder-approved policy.

---

## Success Criteria

- **SC-001:** The system successfully maintains multiple Warehouses belonging to the single Company.
- **SC-002:** Every Warehouse has a unique, system-generated Warehouse ID.
- **SC-003:** Every Warehouse is associated with the existing Company.
- **SC-004:** The system prevents duplicate warehouse codes within the Company.
- **SC-005:** Authorized Managers and Administrators can create and update valid Warehouse records.
- **SC-006:** Unauthorized users cannot modify Warehouse master information.
- **SC-007:** Invalid creation and update requests do not modify existing Warehouse information.
- **SC-008:** Warehouses with Inventory records or historical transactions cannot be deleted.
- **SC-009:** Inactive Warehouses remain available for historical reporting.
- **SC-010:** Inactive Warehouses cannot be selected for new operational transactions.
- **SC-011:** All seventeen original Gherkin acceptance scenarios pass their corresponding verification tests.
- **SC-012:** Concurrent requests cannot create duplicate warehouse codes or invalidate Company relationships.
- **SC-013:** The Warehouse Maintenance interface displays appropriate validation, authorization, and operation-result messages.

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

**Design constraints:**
- The database must enforce the uniqueness of the warehouse code within the Company.
- The Company relationship must be protected by a foreign key or equivalent integrity mechanism.
- Deleting a Warehouse must not automatically delete Inventory or historical business transactions.
- Inactive Warehouses must remain queryable for reporting.
- Warehouse ID must not be editable through the maintenance interface.

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique inventory record identifier |
| warehouseId | Integer | Reference to the warehouse containing the inventory |

**Relationships:**
- Each inventory record is associated with a warehouse.
- Detailed inventory quantities and storage locations are defined in Feature 3.

**Cross-feature design note:**
- Feature 3 models stored Inventory through an Inventory record associated with a Warehouse Location, which belongs to a Warehouse.
- The Warehouse association in this Feature 2 summary may therefore be resolved through Warehouse Location rather than stored as a duplicate direct Inventory foreign key.
- The final database schema must use a consistent relationship across Features 2 and 3.

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

---

## Data Ownership

### Warehouse Data

**Owner:** Maintain Warehouse(s) functionality (Feature 2).

Feature 2 is responsible for:
- Creating Warehouse records.
- Assigning system-generated Warehouse IDs.
- Maintaining warehouse codes, names, addresses, phone numbers, and active status.
- Enforcing unique warehouse codes.
- Validating Warehouse information.
- Managing Warehouse activation and deactivation.
- Checking whether a Warehouse is eligible for deletion.
- Deleting unused Warehouse records.

Other features may reference Warehouse information but must not directly modify Warehouse master data.

### Company Data

**Owner:** Maintain Company (Feature 1).

Feature 2 reads the existing Company record to associate a Warehouse with the Company.

Feature 2 must not create, modify, or delete Company information.

### Inventory Data

**Owner:** Maintain Inventory (Feature 3).

Feature 2 may check for Inventory records associated with a Warehouse before deletion.

Feature 2 must not directly change Inventory quantities, storage locations, or transaction history.

### Operational Transaction Data

**Owners:** The corresponding receiving, Put Away, picking, shipping, and other operational features.

Feature 2 may check for related operational records before deleting a Warehouse.

It must not delete or modify those transactions.

### User and Authorization Data

**Owner:** Shared authentication and authorization functionality.

Feature 2 uses the authenticated user's role to determine access to Warehouse maintenance operations.

Feature 2 does not create user accounts or assign roles.

### Data Consistency Rules

- Every Warehouse must reference the existing Company.
- Warehouse IDs remain stable after creation.
- Warehouse codes must remain unique within the Company.
- Warehouse deletion must not orphan Inventory, storage locations, or historical transactions.
- Deactivation must preserve historical Warehouse references.
- Backend authorization and database constraints must protect Warehouse master data.
- Related records must not be deleted automatically when a Warehouse deletion request is processed.

---

## API Requirements

**Design status:** Proposed API contracts for the Warehouse backend. Exact endpoint conventions and response formats must be checked against the project's API rules.

**Base resource:** `/api/warehouses`

### API-2.1: List Warehouses

**Method:** GET  
**Endpoint:** `/api/warehouses`

**Purpose:** Retrieve Warehouses belonging to the Company.

**Authorization:** Authenticated users with Warehouse viewing permission.

**Successful response:** `200 OK`

Example:

```json
[
  {
    "warehouseId": 1,
    "companyId": 1,
    "warehouseCode": "WH001",
    "name": "Main Warehouse",
    "address": "123 Distribution Drive",
    "phone": "405-555-0100",
    "isActive": true
  },
  {
    "warehouseId": 2,
    "companyId": 1,
    "warehouseCode": "WH002",
    "name": "Secondary Warehouse",
    "address": "456 Storage Avenue",
    "phone": "405-555-0200",
    "isActive": false
  }
]
```

**Behavior:**
- Return Warehouse records associated with the Company.
- Include inactive Warehouses when needed for maintenance and historical reporting.
- Support displaying active and inactive status.

**Error responses:**
- `401 Unauthorized` when authentication is missing.
- `403 Forbidden` when the user lacks viewing permission.

**Traceability:** FR-001, FR-004, FR-015 through FR-017.

### API-2.2: Retrieve Warehouse

**Method:** GET  
**Endpoint:** `/api/warehouses/{warehouseId}`

**Purpose:** Retrieve the details of one Warehouse.

**Authorization:** Authenticated users with Warehouse viewing permission.

**Successful response:** `200 OK`

The response contains the Warehouse ID, Company ID, warehouse code, name, address, phone, and active status.

**Error responses:**
- `401 Unauthorized`
- `403 Forbidden`
- `404 Not Found` when the Warehouse does not exist.

**Traceability:** US-2.2; FR-004, FR-009, FR-020.

### API-2.3: Create Warehouse

**Method:** POST  
**Endpoint:** `/api/warehouses`

**Purpose:** Create a Warehouse belonging to the existing Company.

**Authorization:** Manager or Administrator.

**Request body:**

```json
{
  "warehouseCode": "WH003",
  "name": "North Warehouse",
  "address": "789 Warehouse Road",
  "phone": "405-555-0300",
  "isActive": true
}
```

**Successful response:** `201 Created`

The response contains the new Warehouse ID and saved Warehouse information.

**Validation:**
- A Company must exist.
- Warehouse name is required.
- Warehouse code is required.
- Warehouse code must be unique within the Company.
- Warehouse ID is system-generated.
- The backend associates the new Warehouse with the existing Company.
- Invalid requests must not create a Warehouse.

**Error responses:**
- `400 Bad Request` for missing or invalid information.
- `401 Unauthorized` for missing authentication.
- `403 Forbidden` for insufficient permissions.
- `409 Conflict` for a duplicate warehouse code.
- `409 Conflict` when no Company exists and the Warehouse cannot be created.

**Traceability:** US-2.1; FR-001 through FR-008, FR-018, FR-019; AC-2.1.1 through AC-2.1.6.

### API-2.4: Update Warehouse

**Method:** PUT  
**Endpoint:** `/api/warehouses/{warehouseId}`

**Purpose:** Update Warehouse information, including its active status.

**Authorization:** Manager or Administrator.

**Request body:**

```json
{
  "warehouseCode": "WH001",
  "name": "Main Distribution Warehouse",
  "address": "123 Updated Distribution Drive",
  "phone": "405-555-0100",
  "isActive": true
}
```

**Successful response:** `200 OK`

The response contains the updated Warehouse record.

**Validation:**
- The Warehouse must exist.
- Warehouse ID cannot be changed.
- Company association must be preserved.
- Warehouse name and code must be nonempty.
- Warehouse code must not duplicate another Warehouse's code.
- Invalid updates must leave the existing Warehouse unchanged.
- Deactivation must prevent the Warehouse from being selected for new operational transactions.
- Any stakeholder-approved rules for unfinished work must be applied when deactivating a Warehouse.

**Error responses:**
- `400 Bad Request` for invalid information.
- `401 Unauthorized` for missing authentication.
- `403 Forbidden` for insufficient permissions.
- `404 Not Found` for a nonexistent Warehouse.
- `409 Conflict` for a duplicate code or another applicable business-rule conflict.

**Traceability:** US-2.2; FR-009 through FR-011, FR-015 through FR-021; AC-2.2.1 through AC-2.2.6.

### API-2.5: Delete Warehouse

**Method:** DELETE  
**Endpoint:** `/api/warehouses/{warehouseId}`

**Purpose:** Delete a Warehouse only when no Inventory records or historical transactions reference it.

**Authorization:** Manager or Administrator.

**Successful response:** `204 No Content`

**Deletion rules:**
- The Warehouse must exist.
- The user must be authorized.
- No Inventory records may reference the Warehouse.
- No historical operational transactions may depend on the Warehouse.
- The Company record must remain unchanged.
- The deletion must not cascade into Inventory or historical transactions.
- Dependency checking and deletion must be consistent even when other operations are occurring.

**Error responses:**
- `401 Unauthorized`
- `403 Forbidden`
- `404 Not Found`
- `409 Conflict` when related Inventory or historical transactions prevent deletion.

**Traceability:** US-2.3; FR-012 through FR-014, FR-018 through FR-021; AC-2.3.1 through AC-2.3.5.

### Shared API Design Rules

- Backend endpoints must enforce authentication and authorization.
- Managers and Administrators are the only roles permitted to modify Warehouse master information.
- Input validation must occur on the backend.
- The frontend must not assume a save or deletion succeeded until the backend confirms it.
- Warehouse code uniqueness must be enforced consistently, including during concurrent requests.
- Warehouse and Company relationships must remain valid.
- Inactive Warehouses must not be accepted for new operational transactions.
- Error messages must be understandable without exposing sensitive implementation details.
- Final API contracts must follow the existing Warehouse backend conventions.

---

## Screen Requirements
### UI Design

![Maintain Warehouse Screen](../../docs/ui/Maintain%20Warehouse.png)
**Screen ID:** UI-2A  
**Screen Name:** Warehouse List  
**Proposed design file:** `docs/UI/warehouse-list.png`

**Screen ID:** UI-2B  
**Screen Name:** Warehouse Add/Edit  
**Proposed design file:** `docs/UI/warehouse-edit.png`

### Screen UI-2A: Warehouse List

**Purpose:** Allow authorized users to view existing Warehouses and allow Managers and Administrators to maintain Warehouse records.

**Displayed Information:**

| Column | Description |
|---|---|
| Warehouse Code | Unique Warehouse identifier used by the business |
| Warehouse Name | Name of the Warehouse |
| Address | Physical Warehouse address |
| Phone | Warehouse contact number |
| Status | Active or Inactive |

**Actions:**

**Add**
- Available to Managers and Administrators.
- Opens the Warehouse Add/Edit screen in Add mode.
- Requires the Company to exist.

**Edit**
- Available to Managers and Administrators.
- Requires selecting an existing Warehouse.
- Opens the Warehouse Add/Edit screen in Edit mode.

**Delete**
- Available to Managers and Administrators.
- Requires selecting an existing Warehouse.
- Displays a confirmation before requesting deletion.
- Displays an error if Inventory or historical transactions prevent deletion.

**Close / Back**
- Returns the user to the appropriate Warehouse Management menu.

**List behavior:**
- Display Warehouses belonging to the Company.
- Display active and inactive status.
- Allow selection of a Warehouse.
- Refresh the list after successful creation, update, or deletion.
- Show an appropriate message when no Warehouses exist.

### Screen UI-2B: Warehouse Add/Edit

**Purpose:** Create or update Warehouse master information.

**Fields:**

| Field | Control | Required | Behavior |
|---|---|---|---|
| Warehouse ID | Read-only text | System generated | Displayed for existing Warehouses |
| Company | Read-only text | Yes | Displays the existing Company |
| Warehouse Code | Text input | Yes | Must be unique within the Company |
| Warehouse Name | Text input | Yes | Cannot be empty |
| Address | Text input | No | Stores the physical address |
| Phone | Text input | No | Stores the contact number |
| Active Status | Checkbox or toggle | Yes | Indicates whether the Warehouse is active |

**Add Mode:**
- Display an empty form.
- Show the existing Company.
- Allow entry of Warehouse details.
- Do not allow the user to choose a different Company.
- Warehouse ID is assigned after successful creation.

**Edit Mode:**
- Load the selected Warehouse.
- Display its Warehouse ID as read-only.
- Allow authorized changes to editable fields.
- Preserve the Company association.
- Permit changes to active status according to the business rules.

**Save**
- Validate required fields.
- Submit a create or update request.
- Prevent accidental duplicate submissions.
- Display a success message after backend confirmation.
- Display validation or authorization errors when necessary.

**Cancel**
- Discard unsaved changes.
- Return to the Warehouse List screen.

### Permissions

| Role | View | Add | Edit | Delete |
|---|---|---|---|---|
| Manager | Yes | Yes | Yes | Yes |
| Administrator | Yes | Yes | Yes | Yes |
| Warehouse Worker | If authorized | No | No | No |
| Receiver | If authorized | No | No | No |
| Picker | If authorized | No | No | No |
| Driver | If authorized | No | No | No |

### Validation and Messages

| Condition | Proposed Message |
|---|---|
| Missing Warehouse name | Warehouse name is required. |
| Missing Warehouse code | Warehouse code is required. |
| Duplicate Warehouse code | This warehouse code is already in use. |
| No Company exists | Create the company before adding a warehouse. |
| Warehouse not found | The selected warehouse was not found. |
| Unauthorized modification | You do not have permission to maintain warehouse information. |
| Inventory prevents deletion | This warehouse cannot be deleted because inventory records are associated with it. |
| Historical transactions prevent deletion | This warehouse cannot be deleted because historical transactions depend on it. |
| Warehouse created | Warehouse created successfully. |
| Warehouse updated | Warehouse updated successfully. |
| Warehouse deleted | Warehouse deleted successfully. |
| Warehouse deactivated | Warehouse marked inactive. |
| Backend unavailable | The operation could not be completed. Please try again. |

### Deactivation Behavior

- Managers and Administrators may change Warehouse active status.
- Inactive Warehouses remain visible for maintenance and historical reporting.
- New operational transactions must not select inactive Warehouses.
- The screen must clearly display inactive status.
- Rules for unfinished operational work at deactivation require stakeholder clarification.

### Navigation

- The Warehouse List screen is available through the appropriate management or administration menu.
- The Add and Edit actions open the Warehouse Add/Edit screen.
- Save or Cancel returns the user to the Warehouse List screen.
- The Close or Back action returns to the main menu.

### UI Deliverables

The following screen images must be created:

- `docs/UI/warehouse-list.png`
- `docs/UI/warehouse-edit.png`

These images must be linked to Feature 2 and should reflect the fields, actions, and permissions described above.

**Traceability:** US-2.1, US-2.2, US-2.3; FR-001 through FR-021; AC-2.1.1 through AC-2.3.5.

---

## Definition of Done

Feature 2 is considered complete when its requirements, design artifacts, implementation, and verification criteria have been satisfied.

### Requirements and Design

- [ ] All three User Stories are documented.
- [ ] All twenty-one Functional Requirements are addressed.
- [ ] Assumptions are documented.
- [ ] Edge Cases are documented.
- [ ] Success Criteria are documented.
- [ ] Key Entities are identified.
- [ ] Initial Data Model is documented.
- [ ] All seventeen Gherkin acceptance scenarios are retained.
- [ ] Data Ownership responsibilities are defined.
- [ ] API Requirements are documented.
- [ ] Screen Requirements are documented.
- [ ] Out-of-Scope functionality is identified.
- [ ] Unresolved design decisions are reviewed with the stakeholder or professor.

### API and Backend

- [ ] Warehouse listing is supported.
- [ ] Individual Warehouse retrieval is supported.
- [ ] Authorized Warehouse creation is supported.
- [ ] Authorized Warehouse updates are supported.
- [ ] Authorized Warehouse deletion is supported.
- [ ] Warehouse IDs are system-generated.
- [ ] Warehouse codes are unique within the Company.
- [ ] Every Warehouse references the existing Company.
- [ ] Warehouse creation is rejected when no Company exists.
- [ ] Required fields are validated.
- [ ] Invalid updates leave existing data unchanged.
- [ ] Inactive Warehouses remain available for historical reporting.
- [ ] Inactive Warehouses cannot be selected for new operational transactions.
- [ ] Warehouse deletion is blocked when Inventory records exist.
- [ ] Warehouse deletion is blocked when historical transactions exist.
- [ ] Backend authorization restricts maintenance operations.
- [ ] Concurrent requests preserve Warehouse code uniqueness and related data integrity.

### User Interface

- [ ] Warehouse List screen is designed.
- [ ] Warehouse Add/Edit screen is designed.
- [ ] Add, Edit, Delete, Save, Cancel, and Back actions are defined.
- [ ] Required fields are validated.
- [ ] Warehouse ID and Company association are protected from unauthorized editing.
- [ ] Active and inactive statuses are displayed.
- [ ] Unauthorized users cannot perform maintenance actions.
- [ ] Successful operations display confirmation messages.
- [ ] Failed operations display understandable error messages.
- [ ] Warehouse List screen image is stored in `docs/UI/`.
- [ ] Warehouse Add/Edit screen image is stored in `docs/UI/`.
- [ ] Both screen images are linked to Feature 2.

### Testing

- [ ] AC-2.1.1 through AC-2.1.6 are verified.
- [ ] AC-2.2.1 through AC-2.2.6 are verified.
- [ ] AC-2.3.1 through AC-2.3.5 are verified.
- [ ] Tests cover duplicate warehouse codes.
- [ ] Tests cover missing required fields.
- [ ] Tests cover Warehouse creation without a Company.
- [ ] Tests cover unauthorized maintenance attempts.
- [ ] Tests cover nonexistent Warehouse records.
- [ ] Tests cover Warehouse activation and deactivation.
- [ ] Tests verify inactive Warehouses cannot be selected for new transactions.
- [ ] Tests cover deletion with Inventory records.
- [ ] Tests cover deletion with historical transactions.
- [ ] Tests cover concurrent Warehouse creation using duplicate codes.
- [ ] Tests confirm that failed operations preserve existing data.
- [ ] Regression tests verify Company, Warehouse, and Inventory relationships remain valid.

### Documentation and Review

- [ ] Feature 2 follows the required OC Speckit section structure.
- [ ] Relevant architecture decisions are documented in `docs/ADRs/`.
- [ ] Relevant non-functional requirements are addressed in `docs/NFR/`.
- [ ] Warehouse components are represented in the appropriate C4 architecture diagrams.
- [ ] Design documentation is committed to the `design-draft` branch.
- [ ] Changes are pushed to GitHub for review.

**Draft note:** These checkboxes are completion criteria, not claims that the system has already been implemented or tested.

---

## Out of Scope

The following functionality is not included in Feature 2:

- Creating or maintaining the Company; this belongs to Feature 1.
- Managing multiple independent Companies.
- Creating, editing, or deleting Individual Items.
- Managing Inventory quantities; this belongs to Feature 3.
- Creating or maintaining individual Warehouse storage locations or bins.
- Performing receiving, Put Away, picking, shipping, or delivery operations.
- Creating Supplier Orders or Customer Orders.
- Transferring Inventory between Warehouses.
- Managing employees, passwords, or user roles.
- Editing or deleting historical operational transactions.
- Automatically deleting Inventory or transaction history when deleting a Warehouse.
- Optimizing warehouse picking or Put Away routes.
- Managing warehouse equipment or maintenance schedules.
- Building warehouse financial accounting or payroll functionality.

**Future consideration:** Rules for deactivating a Warehouse with unfinished operational work require stakeholder clarification. Those rules should be resolved before implementation and must remain consistent with the receiving, Put Away, picking, and shipping features.
