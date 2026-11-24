
# Feature: Maintain Customer Order Forms

**Feature ID:** 8  
**Branch pattern:** `feature/8-maintain-customer-order-forms`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System maintains reusable Customer Order Form templates used when preparing orders from retail store customers. Authorized office personnel can create, update, deactivate, and delete unused forms. Each form contains customer information and default items and quantities. Actual Customer Orders are received and processed separately in Feature 12.

---

## User Stories

### US-8.1: Add a Customer Order Form

**As a** Customer Service Clerk or Manager  
**I want to** create a Customer Order Form template  
**So that** customer orders can be prepared using consistent customer and item information.

**Priority:** P1  
**Independent test:** Create a form with a unique Form Code, a name, and an existing Customer, then verify that the form is saved.

### US-8.2: Edit a Customer Order Form

**As a** Customer Service Clerk or Manager  
**I want to** update an existing Customer Order Form template  
**So that** future customer orders use accurate information without changing orders already received.

**Priority:** P1  
**Independent test:** Update a form's name or instructions and verify that the changes are saved while previously received orders remain unchanged.

### US-8.3: Delete or Deactivate a Customer Order Form

**As a** Manager or Administrator  
**I want to** delete an unused Customer Order Form or deactivate an obsolete form  
**So that** outdated forms are not used for new customer orders while historical order records remain protected.

**Priority:** P1  
**Independent test:** Delete an unused form and verify that a form referenced by an existing Customer Order cannot be deleted but can be deactivated.

### US-8.4: Maintain Customer Order Form Items

**As a** Customer Service Clerk or Manager  
**I want to** maintain default items and quantities on a Customer Order Form  
**So that** frequently ordered products can be included when preparing customer orders.

**Priority:** P1  
**Independent test:** Add an existing item and default quantity to a form and verify that the information is available when preparing a Customer Order.

---

## Functional Requirements

- **FR-001:** The system MUST allow authorized Customer Service Clerks and Managers to create Customer Order Form templates.
- **FR-002:** The system MUST assign a unique, system-generated Form ID to each Customer Order Form.
- **FR-003:** The system MUST maintain a unique Form Code for each Customer Order Form.
- **FR-004:** The system MUST maintain a nonempty Form Name.
- **FR-005:** The system MUST associate each Customer Order Form with an existing Customer.
- **FR-006:** The system MUST prevent creation of a form for a nonexistent Customer.
- **FR-007:** The system MUST prevent creation of a new active form for an inactive Customer.
- **FR-008:** The system MUST support multiple Customer Order Forms for one Customer.
- **FR-009:** The system MUST support adding Individual Items to a Customer Order Form.
- **FR-010:** Each Form Item MUST reference an existing Individual Item.
- **FR-011:** The system MUST prevent inactive Individual Items from being added to active Customer Order Forms.
- **FR-012:** The system MUST maintain a default order quantity for each Form Item in individual units.
- **FR-013:** Default order quantities MUST be positive integers.
- **FR-014:** The system MUST prevent duplicate entries for the same Individual Item within one form.
- **FR-015:** The system MUST support storing default ordering instructions on a form.
- **FR-016:** The system MUST allow authorized Customer Service Clerks and Managers to edit existing forms.
- **FR-017:** The system MUST validate Customer Order Form information before saving.
- **FR-018:** The system MUST reject invalid form information without changing existing records.
- **FR-019:** The system MUST preserve the Form ID when a form is updated.
- **FR-020:** The system MUST support adding, updating, and removing default Form Items.
- **FR-021:** The system MUST support marking a Customer Order Form as active or inactive.
- **FR-022:** The system MUST prevent inactive forms from being selected for new Customer Orders.
- **FR-023:** The system MUST preserve forms referenced by existing Customer Orders.
- **FR-024:** The system MUST allow authorized Managers and Administrators to delete a form only when no Customer Orders reference it.
- **FR-025:** The system MUST reject deletion of a form referenced by an existing Customer Order.
- **FR-026:** The system MUST preserve form information when deletion is rejected.
- **FR-027:** The system MUST reject attempts to edit or delete a form that does not exist.
- **FR-028:** The system MUST restrict Customer Order Form creation and modification to authorized office personnel.
- **FR-029:** Warehouse workers, receivers, pickers, and drivers MUST NOT modify Customer Order Forms.
- **FR-030:** The system MUST keep Customer Order Form maintenance separate from actual Customer Order receipt and processing.
- **FR-031:** The system MUST allow an active Customer Order Form to be selected when preparing a new Customer Order.
- **FR-032:** The system MUST copy applicable Customer and Item information from the form into a new draft Customer Order.
- **FR-033:** The system MUST allow authorized personnel to review and modify copied order details before the Customer Order is accepted.
- **FR-034:** Changes to a Customer Order Form MUST NOT automatically modify Customer Orders already received or created from that form.
- **FR-035:** The system MUST maintain relationships between Customer Order Forms, Customers, Individual Items, and Customer Orders.

---

## Assumptions

- **A-001:** Customer Order Forms are reusable templates, not actual Customer Orders.
- **A-002:** Every form has a unique, system-generated Form ID and a unique Form Code.
- **A-003:** Form Code and Form Name are required.
- **A-004:** Each form references one existing Customer.
- **A-005:** A Customer may have multiple Customer Order Forms.
- **A-006:** A new active form cannot be created for an inactive Customer.
- **A-007:** Customer Service Clerks and Managers may create and edit forms.
- **A-008:** Managers and Administrators may delete forms that are not referenced by Customer Orders.
- **A-009:** Warehouse Workers, Receivers, Pickers, and Drivers cannot modify forms.
- **A-010:** A form may contain multiple default Individual Items.
- **A-011:** Each Form Item references an existing Individual Item.
- **A-012:** Inactive Individual Items cannot be added to active forms.
- **A-013:** Default quantities are positive integers measured in individual units, not cases.
- **A-014:** Each Individual Item may appear only once on a particular form.
- **A-015:** Customer master information is owned by Feature 6.
- **A-016:** Individual Item master information is owned by Feature 4.
- **A-017:** Customer Order receipt, acceptance, and processing are owned by Feature 12.
- **A-018:** Form information is copied into a draft Customer Order rather than dynamically linked to its editable order lines.
- **A-019:** Updating a template does not change previously created Customer Orders.
- **A-020:** Inactive forms remain available for historical reference.
- **A-021:** A form referenced by a Customer Order cannot be deleted.
- **A-022:** A draft Customer Order is not automatically accepted or submitted when created from a form.
- **A-023:** Shared authentication and authorization services determine user permissions.

---

## Edge Cases

- **EC-001:** A user attempts to create a form with a duplicate Form Code.
- **EC-002:** A user submits an empty or whitespace-only Form Code.
- **EC-003:** A user submits an empty or whitespace-only Form Name.
- **EC-004:** A user selects a Customer that does not exist.
- **EC-005:** A user attempts to create an active form for an inactive Customer.
- **EC-006:** One Customer has multiple forms with different Form Codes.
- **EC-007:** A Warehouse Worker attempts to create a form.
- **EC-008:** A Picker attempts to modify a form.
- **EC-009:** A Driver attempts to delete a form.
- **EC-010:** A user attempts to edit a nonexistent form.
- **EC-011:** A user attempts to delete a nonexistent form.
- **EC-012:** A user changes a Form Code to one already used by another form.
- **EC-013:** A user attempts to add a nonexistent Individual Item.
- **EC-014:** A user attempts to add an inactive Item to an active form.
- **EC-015:** A user enters zero, a negative number, or a fractional default quantity.
- **EC-016:** A user attempts to add the same Item twice to one form.
- **EC-017:** A user updates or removes a default Form Item.
- **EC-018:** A form is edited after Customer Orders have been created from it.
- **EC-019:** A user attempts to delete a form referenced by a Customer Order.
- **EC-020:** A Manager deactivates a form referenced by historical Orders.
- **EC-021:** A user selects an inactive form for a new Customer Order.
- **EC-022:** An active form's Customer becomes inactive after form creation.
- **EC-023:** An Item on a form becomes inactive after being added.
- **EC-024:** A user changes copied draft quantities before Order acceptance.
- **EC-025:** A user cancels draft preparation without accepting an Order.
- **EC-026:** Two users simultaneously create forms with the same Form Code.
- **EC-027:** A form deletion conflicts with creation of an Order referencing that form.
- **EC-028:** An invalid form update must preserve all existing stored values.
- **EC-029:** A Customer is changed on an existing form, potentially affecting default Items or previous Orders.
- **EC-030:** A user attempts to prepare an Order from a form containing no default Items.

---

## Success Criteria

- **SC-001:** Authorized Customer Service Clerks and Managers can create valid Customer Order Forms.
- **SC-002:** Every form receives a unique, immutable Form ID.
- **SC-003:** Form Codes are unique and required; Form Names are required.
- **SC-004:** Every form references an existing Customer.
- **SC-005:** Active forms cannot be created for inactive Customers.
- **SC-006:** A Customer can have multiple forms.
- **SC-007:** Authorized users can edit form information without changing Form IDs.
- **SC-008:** Form Items reference existing Individual Items.
- **SC-009:** Inactive Items cannot be added to active forms.
- **SC-010:** Default quantities are positive integers in individual units.
- **SC-011:** Duplicate Items on the same form are rejected.
- **SC-012:** Authorized users can add, update, and remove default Items.
- **SC-013:** Inactive forms cannot be selected for new Customer Orders.
- **SC-014:** Forms referenced by Customer Orders cannot be deleted.
- **SC-015:** Authorized Managers and Administrators can delete unused forms.
- **SC-016:** Existing Customer Orders remain unchanged when forms are edited.
- **SC-017:** Valid active forms can supply defaults to new draft Customer Orders.
- **SC-018:** Authorized users can review and modify draft details before acceptance.
- **SC-019:** Preparing an Order from a form does not automatically accept or submit it.
- **SC-020:** Invalid and unauthorized operations leave stored information unchanged.
- **SC-021:** All 22 original Gherkin acceptance scenarios are covered by verification tests.
- **SC-022:** API and screen validation consistently enforce the same business rules.

---

## Key Entities

### Customer Order Form

Represents a reusable template containing customer information, ordering instructions, and default items.

A Customer Order Form can be active or inactive and may be used to prepare multiple Customer Orders.

### Customer Order Form Item

Represents an Individual Item included as a default entry on a Customer Order Form.

Each Form Item identifies the product and its default order quantity.

### Customer

Represents a retail store or business that orders products from the warehouse.

Customer information is maintained in Feature 6.

### Individual Item

Represents a product sold by the warehouse to its customers.

Individual Item information is maintained in Feature 4.

### Customer Order

Represents an actual order received from a Customer.

Customer Order receipt and processing are handled in Feature 12.

### User

Represents an authenticated employee whose role determines whether Customer Order Forms may be maintained.

---

## Initial Data Model

### Customer Order Form

| Attribute | Type | Description |
|---|---|---|
| formId | Integer | Unique, system-generated identifier; primary key |
| formCode | String | Unique Customer Order Form code |
| formName | String | Name identifying the form |
| customerId | Integer | Foreign key referencing Customer |
| instructions | String | Default ordering instructions |
| isActive | Boolean | Indicates whether the form is active |

**Relationships:**
- Each Customer Order Form belongs to one Customer.
- One Customer can have multiple Customer Order Forms.
- One Customer Order Form can contain multiple Customer Order Form Items.
- One Customer Order Form can be used to prepare multiple Customer Orders.

**Constraints:**
- formId must be unique and cannot be changed.
- formCode must be unique and nonempty.
- formName must be nonempty.
- customerId must reference an existing Customer.
- Forms referenced by Customer Orders cannot be deleted.

### Customer Order Form Item

| Attribute | Type | Description |
|---|---|---|
| formItemId | Integer | Unique Form Item identifier |
| formId | Integer | Foreign key referencing Customer Order Form |
| itemId | Integer | Foreign key referencing Individual Item |
| defaultQuantity | Integer | Default quantity ordered in individual units |

**Relationships:**
- Each Form Item belongs to one Customer Order Form.
- Each Form Item references one Individual Item.
- One Customer Order Form can contain multiple Form Items.

**Constraints:**
- The combination of formId and itemId must be unique.
- defaultQuantity must be greater than zero.
- The referenced Individual Item must exist.
- Inactive Individual Items cannot be added to active forms.

### Customer

| Attribute | Type | Description |
|---|---|---|
| customerId | Integer | Unique Customer identifier |
| isActive | Boolean | Indicates whether the Customer is active |

**Relationships:**
- One Customer can have multiple Customer Order Forms.
- Customer maintenance is defined in Feature 6.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| isActive | Boolean | Indicates whether the Item is active |

**Relationships:**
- An Individual Item can appear on multiple Customer Order Forms.
- Item maintenance is defined in Feature 4.

### Customer Order

| Attribute | Type | Description |
|---|---|---|
| customerOrderId | Integer | Unique Customer Order identifier |
| customerId | Integer | Foreign key referencing Customer |
| sourceFormId | Integer | Optional reference to the form used to prepare the order |

**Relationships:**
- A Customer Order belongs to one Customer.
- A Customer Order may be prepared using a Customer Order Form.
- Actual ordered quantities and prices are stored on the Customer Order and its order lines.
- Customer Order receipt and processing are defined in Feature 12.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- User roles determine who may create, update, deactivate, or delete Customer Order Forms.

---

## Gherkin AC

### US-8.1: Add a Customer Order Form

#### AC-8.1.1: Successfully create Customer Order Form

**Given** an active Customer exists  
**And** the user is authenticated as a Customer Service Clerk or Manager  
**When** the user enters a unique Form Code, nonempty Form Name, and selects the Customer  
**And** saves the form  
**Then** the system creates the Customer Order Form  
**And** assigns a unique Form ID  
**And** associates the form with the selected Customer.

#### AC-8.1.2: Reject duplicate Form Code

**Given** a Customer Order Form exists with Form Code "COF001"  
**And** the user is authorized to maintain forms  
**When** the user attempts to create another form with Form Code "COF001"  
**Then** the system rejects the request  
**And** the existing form remains unchanged.

#### AC-8.1.3: Reject missing Form Name

**Given** the user is authorized to maintain forms  
**When** the user attempts to create a form with an empty Form Name  
**Then** the system rejects the request  
**And** no new form is created.

#### AC-8.1.4: Reject nonexistent Customer

**Given** the requested Customer does not exist  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user attempts to create a form for that Customer  
**Then** the system rejects the request  
**And** no form is created.

#### AC-8.1.5: Reject inactive Customer

**Given** a Customer exists and is inactive  
**And** the user is authorized to maintain forms  
**When** the user attempts to create an active form for that Customer  
**Then** the system rejects the request  
**And** no active form is created.

#### AC-8.1.6: Reject unauthorized Form creation

**Given** the user is authenticated as a Warehouse Worker  
**When** the user attempts to create a Customer Order Form  
**Then** the system denies the operation  
**And** no form is created.

### US-8.2: Edit a Customer Order Form

#### AC-8.2.1: Successfully update Customer Order Form

**Given** a Customer Order Form exists  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user updates the Form Name and ordering instructions  
**And** saves the changes  
**Then** the system stores the updated information  
**And** the Form ID remains unchanged.

#### AC-8.2.2: Reject invalid Form update

**Given** a Customer Order Form exists  
**And** the user is authenticated as a Manager  
**When** the user removes the required Form Name  
**And** attempts to save the changes  
**Then** the system rejects the update  
**And** the previously stored form information remains unchanged.

#### AC-8.2.3: Reject duplicate Form Code during update

**Given** Form A has Form Code "COF001"  
**And** Form B has Form Code "COF002"  
**And** the user is authorized to maintain forms  
**When** the user changes Form B's code to "COF001"  
**Then** the system rejects the update  
**And** both original Form Codes remain unchanged.

#### AC-8.2.4: Preserve existing Customer Orders

**Given** a Customer Order Form has already been used to create a Customer Order  
**And** the user is authenticated as a Manager  
**When** the user updates the Form's default instructions  
**And** saves the changes  
**Then** the system updates the Form  
**And** the existing Customer Order remains unchanged.

#### AC-8.2.5: Reject unauthorized Form modification

**Given** a Customer Order Form exists  
**And** the user is authenticated as a Picker  
**When** the user attempts to modify the Form  
**Then** the system denies the request  
**And** the Form remains unchanged.

#### AC-8.2.6: Reject editing nonexistent Form

**Given** no Customer Order Form exists with the requested Form ID  
**And** the user is authenticated as a Manager  
**When** the user attempts to update that Form  
**Then** the system rejects the request  
**And** no Form is changed.

### US-8.3: Delete or Deactivate a Customer Order Form

#### AC-8.3.1: Successfully delete unused Form

**Given** a Customer Order Form exists  
**And** no Customer Orders reference it  
**And** the user is authenticated as an Administrator  
**When** the user requests deletion  
**Then** the system deletes the Customer Order Form and its default Form Items  
**And** no Customer Order is affected.

#### AC-8.3.2: Prevent deletion of referenced Form

**Given** a Customer Order Form is referenced by an existing Customer Order  
**And** the user is authenticated as a Manager  
**When** the user requests deletion  
**Then** the system rejects the request  
**And** the Form and Customer Order remain unchanged.

#### AC-8.3.3: Deactivate Customer Order Form

**Given** an active Customer Order Form exists  
**And** the user is authenticated as a Manager  
**When** the user marks the Form as inactive  
**Then** the system saves the inactive status  
**And** the Form remains available for historical reference  
**And** the Form cannot be selected when preparing new Customer Orders.

#### AC-8.3.4: Reject unauthorized Form deletion

**Given** a Customer Order Form exists  
**And** the user is authenticated as a Driver  
**When** the user attempts to delete the Form  
**Then** the system denies the operation  
**And** the Form remains unchanged.

#### AC-8.3.5: Reject deletion of nonexistent Form

**Given** no Customer Order Form exists with the requested Form ID  
**And** the user is authenticated as an Administrator  
**When** the user requests deletion of that Form  
**Then** the system rejects the request  
**And** no Form is changed.

### US-8.4: Maintain Customer Order Form Items

#### AC-8.4.1: Add Item to Form

**Given** an active Customer Order Form exists  
**And** an active Individual Item exists  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user adds the Item with a default quantity of 12 units  
**Then** the system saves the Form Item  
**And** stores the default quantity as 12 individual units.

#### AC-8.4.2: Reject inactive Item

**Given** an active Customer Order Form exists  
**And** an Individual Item is inactive  
**When** an authorized user attempts to add the Item to the Form  
**Then** the system rejects the request  
**And** no invalid Form Item is created.

#### AC-8.4.3: Reject invalid default quantity

**Given** a Customer Order Form exists  
**And** the user is authorized to maintain Form Items  
**When** the user attempts to add an Item with a default quantity of zero  
**Then** the system rejects the request  
**And** no Form Item is created.

#### AC-8.4.4: Reject duplicate Item on Form

**Given** a Customer Order Form already contains Item A  
**When** an authorized user attempts to add Item A again  
**Then** the system rejects the duplicate entry  
**And** the existing Form Item remains unchanged.

#### AC-8.4.5: Use Form to Prepare Customer Order

**Given** an active Customer Order Form contains valid default Items and quantities  
**And** its Customer is active  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user selects the Form to prepare a Customer Order  
**Then** the system creates a new draft Customer Order  
**And** copies the applicable Customer and Item information into the draft  
**And** allows the user to review and change the quantities before acceptance  
**And** does not automatically accept or submit the order.

---

## Data Ownership

### Customer Order Form and Form Items

**Owner:** Feature 8 — Maintain Customer Order Forms.

Feature 8 owns:
- `formId`
- `formCode`
- `formName`
- `customerId` reference on the template
- Default ordering instructions
- `isActive` status
- Form Item records
- Default quantities in individual units

Feature 8 creates, validates, updates, deactivates, and deletes eligible templates and their default Items.

### Customer Master Data

**Owner:** Feature 6 — Maintain Customers.

Feature 8 reads Customer identity and active status. It does not change Customer master records.

### Individual Item Master Data

**Owner:** Feature 4 — Maintain Individual Item.

Feature 8 reads Item identity and active status. It does not change Item descriptions, prices, UPCs, or other Item master data.

### Customer Orders

**Owner:** Feature 12 — Customer Order receipt and processing.

Feature 12 owns:
- Actual Customer Order records
- Actual Order line Items
- Ordered quantities and prices
- Order acceptance and submission
- Order status and subsequent processing

Feature 8 supplies template defaults. Feature 12 creates the draft Order, copies applicable data, and controls acceptance.

The optional `sourceFormId` records the originating template.

### User and Authorization Data

**Owner:** Shared authentication and authorization services.

Feature 8 checks user roles but does not maintain accounts, passwords, or role definitions.

### Data Integrity Rules

- Form IDs are unique and immutable.
- Form Codes are unique and nonempty.
- Form Names are nonempty.
- Customer references must be valid.
- Form Item references must be valid.
- Each `(formId, itemId)` combination must be unique.
- Default quantities must be positive integers.
- Inactive Items cannot be added to active forms.
- Inactive forms cannot be selected for new Orders.
- Forms referenced by Customer Orders cannot be deleted.
- Changes to templates cannot automatically change existing Orders.
- Related changes must be transactional to prevent partial saves.

---

## API Requirements

**Design status:** Proposed API contracts. Final endpoint naming must follow the project's API conventions.

**Base resource:** `/api/customer-order-forms`

### API-8.1: List Customer Order Forms

**Method:** GET  
**Endpoint:** `/api/customer-order-forms`

**Purpose:** List and search existing templates.

**Authorization:** Authorized office personnel.

**Query parameters:**
- `formCode`
- `formName`
- `customerId`
- `isActive`

**Successful response:** `200 OK`

**Rules:**
- Allow searching and filtering.
- Display inactive forms to authorized users for historical reference.
- Do not change records during search.

**Traceability:** FR-003 through FR-008, FR-021 through FR-023.

### API-8.2: Create Customer Order Form

**Method:** POST  
**Endpoint:** `/api/customer-order-forms`

**Purpose:** Create a reusable template.

**Authorization:** Customer Service Clerk or Manager.

**Example request:**

    {
      "formCode": "COF001",
      "formName": "Weekly Store Order",
      "customerId": 101,
      "instructions": "Prepare for Friday delivery",
      "isActive": true
    }

**Successful response:** `201 Created`

**Validation:**
- Form Code must be unique and nonempty.
- Form Name must be nonempty.
- Customer must exist.
- New active forms cannot reference inactive Customers.
- Form ID is generated automatically.
- Unauthorized requests are rejected.

**Error responses:**
- `400 Bad Request` for invalid input.
- `401 Unauthorized` for missing authentication.
- `403 Forbidden` for insufficient permissions.
- `404 Not Found` for nonexistent Customer references.
- `409 Conflict` for duplicate Form Codes.

**Traceability:** US-8.1; FR-001 through FR-008; AC-8.1.1 through AC-8.1.6.

### API-8.3: Get Customer Order Form

**Method:** GET  
**Endpoint:** `/api/customer-order-forms/{formId}`

**Purpose:** Retrieve form details and default Items.

**Authorization:** Authorized office personnel.

**Successful response:** `200 OK`

**Returned information:**
- Form ID
- Form Code
- Form Name
- Customer
- Instructions
- Active Status
- Default Form Items and quantities

**Error responses:**
- `401 Unauthorized`
- `403 Forbidden`
- `404 Not Found`

### API-8.4: Update Customer Order Form

**Method:** PUT  
**Endpoint:** `/api/customer-order-forms/{formId}`

**Purpose:** Update template information.

**Authorization:** Customer Service Clerk or Manager.

**Successful response:** `200 OK`

**Validation:**
- Form must exist.
- Form ID cannot change.
- Form Code must remain unique.
- Form Name cannot be empty.
- Customer reference must remain valid.
- Invalid updates must preserve previous values.
- Existing Customer Orders must remain unchanged.

**Error responses:**
- `400 Bad Request`
- `401 Unauthorized`
- `403 Forbidden`
- `404 Not Found`
- `409 Conflict`

**Traceability:** US-8.2; FR-016 through FR-019, FR-034; AC-8.2.1 through AC-8.2.6.

### API-8.5: Change Form Status

**Method:** PATCH  
**Endpoint:** `/api/customer-order-forms/{formId}/status`

**Purpose:** Activate or deactivate a template.

**Authorization:** Manager or Administrator, subject to approved role rules.

**Example request:**

    {
      "isActive": false
    }

**Successful response:** `200 OK`

**Rules:**
- Form must exist.
- Deactivated forms remain available for historical reference.
- Inactive forms cannot be selected for new Orders.
- Reactivation must respect Customer active-status rules.

**Error responses:**
- `400 Bad Request`
- `401 Unauthorized`
- `403 Forbidden`
- `404 Not Found`
- `409 Conflict`

**Traceability:** US-8.3; FR-021 through FR-023; AC-8.3.3.

### API-8.6: Delete Customer Order Form

**Method:** DELETE  
**Endpoint:** `/api/customer-order-forms/{formId}`

**Purpose:** Delete an unused template.

**Authorization:** Manager or Administrator.

**Successful response:** `204 No Content`

**Validation:**
- Form must exist.
- No Customer Orders may reference the form.
- Delete the form and its default Form Items together.
- Reject deletion if any Customer Order references the form.
- Preserve existing records when deletion fails.
- Protect dependency checks against concurrent transactions.

**Error responses:**
- `401 Unauthorized`
- `403 Forbidden`
- `404 Not Found`
- `409 Conflict`

**Traceability:** US-8.3; FR-024 through FR-027; AC-8.3.1, AC-8.3.2, AC-8.3.4, AC-8.3.5.

### API-8.7: Add Form Item

**Method:** POST  
**Endpoint:** `/api/customer-order-forms/{formId}/items`

**Purpose:** Add a default Individual Item.

**Authorization:** Customer Service Clerk or Manager.

**Example request:**

    {
      "itemId": 201,
      "defaultQuantity": 12
    }

**Successful response:** `201 Created`

**Validation:**
- Form must exist.
- Individual Item must exist.
- Inactive Items cannot be added to active forms.
- Quantity must be a positive integer in individual units.
- Duplicate Items on the same form are rejected.

**Error responses:**
- `400 Bad Request`
- `401 Unauthorized`
- `403 Forbidden`
- `404 Not Found`
- `409 Conflict`

**Traceability:** US-8.4; FR-009 through FR-014, FR-020; AC-8.4.1 through AC-8.4.4.

### API-8.8: Update Form Item

**Method:** PUT  
**Endpoint:** `/api/customer-order-forms/{formId}/items/{formItemId}`

**Purpose:** Update a default Item quantity.

**Authorization:** Customer Service Clerk or Manager.

**Successful response:** `200 OK`

**Rules:**
- Form and Form Item must exist.
- Quantity must be a positive integer.
- Item reference must remain valid.
- Existing Customer Orders must not be changed.

**Traceability:** FR-012 through FR-014, FR-020, FR-034.

### API-8.9: Remove Form Item

**Method:** DELETE  
**Endpoint:** `/api/customer-order-forms/{formId}/items/{formItemId}`

**Purpose:** Remove an Item from a template.

**Authorization:** Customer Service Clerk or Manager.

**Successful response:** `204 No Content`

**Rules:**
- Form and Form Item must exist.
- Remove only the template entry.
- Previously created Customer Orders remain unchanged.

**Traceability:** FR-020, FR-034.

### API-8.10: Prepare Customer Order from Form

**Method:** POST  
**Endpoint:** `/api/customer-orders/drafts/from-form/{formId}`

**Purpose:** Prepare a new draft Customer Order using template defaults.

**Owner:** Feature 12 — Customer Order receipt and processing.

**Authorization:** Authorized office personnel.

**Successful response:** `201 Created`

**Rules:**
- Form must exist and be active.
- Customer must exist and be active.
- Applicable Items must be valid.
- Copy Customer and Item information into the draft.
- Copy default quantities in individual units.
- Allow authorized users to review and change the draft.
- Do not automatically accept or submit the Order.
- Do not change existing Customer Orders.

**Traceability:** FR-030 through FR-034; AC-8.4.5.

### Shared API Requirements

- Enforce authentication and role-based authorization.
- Validate required fields on the server.
- Enforce unique Form Codes.
- Validate Customer and Individual Item references.
- Reject duplicate Form Items.
- Require positive integer quantities.
- Preserve historical Customer Orders.
- Use database constraints and transactions for consistency.
- Prevent concurrent requests from bypassing uniqueness or deletion restrictions.
- Follow the project's established error-response conventions.

---

## Screen Requirements

**Design status:** Proposed screens; image files are not yet claimed as created.

### Screen UI-8A: Customer Order Form List

**Proposed image:** `docs/UI/customer-order-form-list.png`

**Purpose:** Search and select Customer Order Form templates.

**Displayed information:**
- Form Code
- Form Name
- Customer Name
- Active Status

**Actions:**
- Search
- Filter by Customer
- Filter by Active Status
- View
- Add
- Edit
- Delete
- Prepare Customer Order

**Rules:**
- Maintenance actions depend on user role.
- Inactive forms must be clearly identified.
- Inactive forms cannot be used for new Orders.

### Screen UI-8B: Add Customer Order Form

**Proposed image:** `docs/UI/customer-order-form-add.png`

**Purpose:** Create a template.

| Field | Control | Required |
|---|---|---|
| Form Code | Text input | Yes |
| Form Name | Text input | Yes |
| Customer | Customer selector | Yes |
| Instructions | Multiline text | No |
| Active Status | Checkbox | Yes |

**Actions:**
- Save
- Cancel

**Validation:**
- Unique Form Code
- Nonempty Form Code and Form Name
- Existing Customer
- Active Customer required for a new active form

### Screen UI-8C: Edit Customer Order Form

**Proposed image:** `docs/UI/customer-order-form-edit.png`

**Purpose:** Update an existing template.

**Fields:**
- Form ID (read-only)
- Form Code
- Form Name
- Customer
- Instructions
- Active Status

**Actions:**
- Save Changes
- Cancel
- Manage Form Items
- View related Customer Orders

**Rules:**
- Form ID remains unchanged.
- Invalid changes are rejected.
- Previously created Orders remain unchanged.

### Screen UI-8D: Maintain Customer Order Form Items

**Proposed image:** `docs/UI/customer-order-form-items.png`

**Purpose:** Maintain default Items and quantities.

**Displayed information:**
- Form Code
- Customer
- Item Number
- Item Description
- Item Status
- Default Quantity in Individual Units

**Actions:**
- Add Item
- Update Quantity
- Remove Item
- Save Changes
- Cancel

**Rules:**
- Item must exist.
- Inactive Items cannot be added to active forms.
- Quantities must be positive integers.
- Duplicate Items are rejected.
- Existing Customer Orders remain unchanged.

### Screen UI-8E: Customer Order Form Details

**Proposed image:** `docs/UI/customer-order-form-details.png`

**Purpose:** Display template information.

**Displayed information:**
- Form ID
- Form Code
- Form Name
- Customer
- Instructions
- Active Status
- Default Items
- Default Quantities

**Actions:**
- Edit, if authorized
- Prepare Customer Order, if eligible
- Return to Form List

### Screen UI-8F: Prepare Customer Order Preview

**Proposed image:** `docs/UI/customer-order-form-preview.png`

**Purpose:** Preview template defaults before preparing a Customer Order.

**Displayed information:**
- Selected Form
- Customer
- Instructions
- Item List
- Default Quantities in Individual Units

**Actions:**
- Prepare Draft
- Cancel

**Rules:**
- Form and Customer must be active.
- Applicable Items must be valid.
- Draft preparation must not automatically accept or submit an Order.
- Feature 12 owns Order acceptance and processing.

### Screen UI-8G: Delete or Deactivate Form

**Proposed image:** `docs/UI/customer-order-form-status.png`

**Purpose:** Confirm form deactivation or deletion.

**Displayed information:**
- Form Code
- Form Name
- Active Status
- Existing Customer Order references
- Deletion eligibility

**Actions:**
- Deactivate
- Delete, if eligible
- Cancel

**Rules:**
- Referenced forms cannot be deleted.
- Deactivated forms remain available for historical reference.
- Unauthorized actions are rejected.

### Role Permissions

| Role | View Forms | Add/Edit Forms | Maintain Form Items | Delete Forms |
|---|---|---|---|---|
| Customer Service Clerk | Yes | Yes | Yes | No |
| Manager | Yes | Yes | Yes | Yes, if eligible |
| Administrator | According to permissions | According to permissions | According to permissions | Yes, if eligible |
| Warehouse Worker | If authorized | No | No | No |
| Receiver | If authorized | No | No | No |
| Picker | If authorized | No | No | No |
| Driver | If authorized | No | No | No |

### Validation Messages

The UI must display clear feedback for:
- Duplicate Form Code
- Missing Form Code
- Missing Form Name
- Nonexistent Customer
- Inactive Customer
- Nonexistent Form
- Nonexistent Item
- Inactive Item
- Duplicate Form Item
- Invalid default quantity
- Unauthorized action
- Referenced form cannot be deleted
- Inactive form cannot be selected
- Successful creation, update, deactivation, or deletion

### Proposed UI Deliverables

- `docs/UI/customer-order-form-list.png`
- `docs/UI/customer-order-form-add.png`
- `docs/UI/customer-order-form-edit.png`
- `docs/UI/customer-order-form-items.png`
- `docs/UI/customer-order-form-details.png`
- `docs/UI/customer-order-form-preview.png`
- `docs/UI/customer-order-form-status.png`

These paths must be updated if the repository uses a different UI documentation structure.

---

## Definition of Done

### Requirements and Design

- [ ] All four original User Stories are retained.
- [ ] All thirty-five original Functional Requirements are retained.
- [ ] Assumptions are documented.
- [ ] Edge Cases are documented.
- [ ] Success Criteria are documented.
- [ ] All six Key Entities are documented.
- [ ] The original Initial Data Model is retained.
- [ ] All twenty-two original Gherkin acceptance scenarios are retained.
- [ ] Data Ownership is documented.
- [ ] API Requirements are documented.
- [ ] Screen Requirements are documented.
- [ ] Out-of-Scope functionality is documented.
- [ ] Pending clarifications are recorded.

### Customer Order Form Maintenance

- [ ] Authorized personnel can create forms.
- [ ] Form IDs are generated uniquely.
- [ ] Form Codes are unique.
- [ ] Form Names are required.
- [ ] Forms reference existing Customers.
- [ ] Active forms cannot be created for inactive Customers.
- [ ] Authorized users can edit forms.
- [ ] Form IDs remain unchanged during updates.
- [ ] Invalid updates preserve existing information.
- [ ] Managers and Administrators can delete unused forms.
- [ ] Referenced forms cannot be deleted.
- [ ] Forms can be deactivated.
- [ ] Inactive forms cannot be selected for new Orders.

### Form Item Maintenance

- [ ] Authorized personnel can add Form Items.
- [ ] Every Form Item references an existing Individual Item.
- [ ] Inactive Items cannot be added to active forms.
- [ ] Default quantities are positive integers in individual units.
- [ ] Duplicate Items on the same form are rejected.
- [ ] Authorized personnel can update default quantities.
- [ ] Authorized personnel can remove Form Items.

### Customer Order Integration

- [ ] Active forms can be selected to prepare Customer Orders.
- [ ] Customer and Item defaults are copied into new draft Orders.
- [ ] Draft quantities can be reviewed and modified.
- [ ] Draft preparation does not automatically accept or submit Orders.
- [ ] Editing forms does not modify existing Customer Orders.
- [ ] Feature 12 owns actual Customer Order processing.

### Security and Validation

- [ ] Role permissions are enforced.
- [ ] Warehouse Workers cannot modify forms.
- [ ] Receivers cannot modify forms.
- [ ] Pickers cannot modify forms.
- [ ] Drivers cannot modify forms.
- [ ] Required fields and references are validated on the backend.
- [ ] Concurrent operations cannot bypass uniqueness or deletion restrictions.

### Acceptance Testing

- [ ] AC-8.1.1 through AC-8.1.6 pass.
- [ ] AC-8.2.1 through AC-8.2.6 pass.
- [ ] AC-8.3.1 through AC-8.3.5 pass.
- [ ] AC-8.4.1 through AC-8.4.5 pass.
- [ ] Tests cover duplicate Form Codes.
- [ ] Tests cover invalid and inactive Customers.
- [ ] Tests cover invalid and inactive Items.
- [ ] Tests cover invalid quantities and duplicate Items.
- [ ] Tests cover authorization restrictions.
- [ ] Tests cover deletion dependencies.
- [ ] Tests confirm existing Customer Orders remain unchanged.

### Documentation and Review

- [ ] Feature 8 follows the required OC Speckit section order.
- [ ] Relevant design decisions are documented in `docs/ADRs/` as required.
- [ ] Relevant non-functional requirements are addressed in `docs/NFR/` as required.
- [ ] Customer Order Form relationships are reflected in relevant architecture diagrams.
- [ ] Required UI screen designs are created.
- [ ] UI image links use correct repository paths.
- [ ] Changes are committed to the `design-draft` branch.
- [ ] Changes are pushed to GitHub.

**Draft note:** These checkboxes describe work to complete or verify. Documenting a requirement does not mean the application, tests, or screen images have already been implemented.

---

## Out of Scope

Feature 8 does not include:

- Creating or editing Customer master records (Feature 6).
- Creating or editing Individual Item master records (Feature 4).
- Maintaining Item prices or inventory quantities.
- Accepting, submitting, or processing actual Customer Orders (Feature 12).
- Picking, packing, shipping, or delivering Customer Orders.
- Maintaining Supplier Order Forms or Supplier Orders.
- Maintaining Warehouse or Company master information.
- Managing User accounts, passwords, or authorization roles.
- Automatically accepting Customer Orders when a template is selected.
- Automatically modifying existing Customer Orders when a template changes.
- Deleting forms referenced by existing Customer Orders.
- Allowing Warehouse Workers, Receivers, Pickers, or Drivers to modify Customer Order Forms.

### Pending Clarifications

- **CL-8.1:** May an inactive form be created for an inactive Customer?
- **CL-8.2:** Can an existing form be reassigned to another Customer?
- **CL-8.3:** Should a form automatically become inactive when its Customer is deactivated?
- **CL-8.4:** May a form contain no default Items?
- **CL-8.5:** What happens when an Item already on a form becomes inactive?
- **CL-8.6:** Should draft creation exclude unavailable Items or display a warning requiring review?
- **CL-8.7:** Are default instructions copied into the actual Customer Order or only displayed during preparation?
- **CL-8.8:** Who may reactivate an inactive Customer Order Form?
- **CL-8.9:** Should Customer Order prices be calculated using current Item prices when the draft is created?
- **CL-8.10:** How should an existing draft be handled if the source form changes before Order acceptance?

These decisions must be coordinated with Features 4, 6, and 12 before implementation.
