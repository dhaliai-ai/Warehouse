
# Feature: Maintain Supplier Order Forms

**Feature ID:** 7  
**Branch pattern:** `feature/7-maintain-supplier-order-forms`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System maintains reusable supplier order form templates used when preparing purchase orders for suppliers. Authorized purchasing personnel can create, update, deactivate, and delete unused forms. Each form defines the information required for supplier ordering, while actual purchase orders are created separately in Feature 9.

---

## User Stories

### US-7.1: Add a Supplier Order Form

**As a** Purchasing Clerk or Manager  
**I want to** create a supplier order form template  
**So that** purchase orders can be prepared using consistent supplier and item information.

**Priority:** P1  
**Independent test:** Create a form with a unique form code, name, and valid supplier association, then verify that it is saved.

### US-7.2: Edit a Supplier Order Form

**As a** Purchasing Clerk or Manager  
**I want to** update a supplier order form template  
**So that** future purchase orders use accurate and current ordering information.

**Priority:** P1  
**Independent test:** Update an existing form's name or default ordering instructions and verify that the changes are saved without modifying previously created purchase orders.

### US-7.3: Delete or Deactivate a Supplier Order Form

**As a** Manager or Administrator  
**I want to** delete an unused form or deactivate a form that is no longer needed  
**So that** obsolete forms are not used for new orders while existing purchase orders remain protected.

**Priority:** P1  
**Independent test:** Verify that an unused form can be deleted and that a form referenced by an existing purchase order cannot be deleted but can be deactivated.

### US-7.4: Maintain Supplier Order Form Items

**As a** Purchasing Clerk or Manager  
**I want to** maintain the items and default quantities on a supplier order form  
**So that** frequently purchased products can be included when preparing a new supplier order.

**Priority:** P1  
**Independent test:** Add an item and default case quantity to a form and verify that the item is available when creating a supplier order.

---

## Functional Requirements

- **FR-001:** The system MUST allow authorized Purchasing Clerks and Managers to create Supplier Order Form templates.
- **FR-002:** The system MUST assign a unique, system-generated Form ID to each Supplier Order Form.
- **FR-003:** The system MUST maintain a unique Form Code for each Supplier Order Form.
- **FR-004:** The system MUST maintain a nonempty Form Name.
- **FR-005:** The system MUST associate each Supplier Order Form with an existing Supplier.
- **FR-006:** The system MUST prevent creation of a form for a nonexistent Supplier.
- **FR-007:** The system MUST prevent creation of a new active form for an inactive Supplier.
- **FR-008:** The system MUST support multiple Supplier Order Forms for one Supplier.
- **FR-009:** The system MUST support adding Individual Items to a Supplier Order Form.
- **FR-010:** Each form item MUST reference an Individual Item available from the form's Supplier.
- **FR-011:** The system MUST maintain a default order quantity in cases for each form item.
- **FR-012:** Default order quantities MUST be positive integers.
- **FR-013:** The system MUST prevent duplicate entries for the same Individual Item within one form.
- **FR-014:** The system MUST support storing default ordering instructions on a form.
- **FR-015:** The system MUST allow authorized Purchasing Clerks and Managers to edit existing forms.
- **FR-016:** The system MUST validate form information before saving.
- **FR-017:** The system MUST reject invalid form information without changing existing records.
- **FR-018:** The system MUST preserve the Form ID when a form is updated.
- **FR-019:** The system MUST support adding, updating, and removing default form items.
- **FR-020:** The system MUST support marking a form as active or inactive.
- **FR-021:** The system MUST prevent inactive forms from being selected for new Supplier Orders.
- **FR-022:** The system MUST preserve forms referenced by existing Supplier Orders.
- **FR-023:** The system MUST allow authorized Managers and Administrators to delete a form only when no Supplier Orders reference it.
- **FR-024:** The system MUST reject deletion of a form referenced by an existing Supplier Order.
- **FR-025:** The system MUST preserve form information when deletion is rejected.
- **FR-026:** The system MUST reject attempts to edit or delete a form that does not exist.
- **FR-027:** The system MUST restrict form creation and modification to authorized purchasing personnel.
- **FR-028:** Warehouse workers, receivers, pickers, and drivers MUST NOT modify Supplier Order Forms.
- **FR-029:** The system MUST keep Supplier Order Form maintenance separate from actual Supplier Order creation.
- **FR-030:** The system MUST allow an active Supplier Order Form to be selected when preparing a new Supplier Order.
- **FR-031:** The system MUST copy applicable form defaults into a new Supplier Order without automatically submitting that order.
- **FR-032:** The system MUST allow authorized purchasing personnel to review and modify copied order details before submission.
- **FR-033:** Changes to a Supplier Order Form MUST NOT automatically modify Supplier Orders already created from that form.
- **FR-034:** The system MUST maintain relationships between Supplier Order Forms, Suppliers, Individual Items, and Supplier Orders.

---

## Assumptions

- **A-001:** Supplier Order Forms are reusable templates, not actual purchase orders.
- **A-002:** Every Supplier Order Form has a unique, system-generated Form ID and a unique Form Code.
- **A-003:** Form Code and Form Name are required.
- **A-004:** Each Supplier Order Form belongs to one existing Supplier.
- **A-005:** A Supplier may have multiple Supplier Order Forms.
- **A-006:** New active forms cannot be created for inactive Suppliers.
- **A-007:** Purchasing Clerks and Managers can create and update Supplier Order Forms.
- **A-008:** Managers and Administrators can delete forms when no Supplier Orders reference them.
- **A-009:** Warehouse Workers, Receivers, Pickers, and Drivers cannot modify Supplier Order Forms.
- **A-010:** A Supplier Order Form may contain multiple default Form Items.
- **A-011:** Each Form Item must reference an Individual Item available from the form's Supplier.
- **A-012:** Default order quantities are positive whole numbers measured in cases.
- **A-013:** The same Individual Item may appear only once on a particular form.
- **A-014:** Supplier master information is maintained in Feature 5.
- **A-015:** Individual Item and Supplier Item relationships are maintained in Feature 4.
- **A-016:** Actual Supplier Orders are created and maintained in Feature 9.
- **A-017:** A form may be used to prepare multiple Supplier Orders.
- **A-018:** Form defaults are copied into a new draft Supplier Order; they are not permanently linked as editable shared order lines.
- **A-019:** Changing a template does not change Supplier Orders already created from it.
- **A-020:** Inactive forms remain available for historical reference but cannot be selected for new Supplier Orders.
- **A-021:** Existing Supplier Orders preserve their original Supplier and order details.
- **A-022:** Authentication and authorization are enforced by shared system services.
- **A-023:** A new Supplier Order remains a draft until an authorized user reviews and submits it through Feature 9.

---

## Edge Cases

- **EC-001:** A user attempts to create a form with a duplicate Form Code.
- **EC-002:** A user attempts to create a form without a Form Code.
- **EC-003:** A user attempts to create a form without a Form Name.
- **EC-004:** A Form Code or Form Name contains only whitespace.
- **EC-005:** A user attempts to associate a form with a nonexistent Supplier.
- **EC-006:** A user attempts to create an active form for an inactive Supplier.
- **EC-007:** A Supplier has multiple forms with different Form Codes.
- **EC-008:** A Warehouse Worker attempts to create a form.
- **EC-009:** A Picker attempts to modify a form.
- **EC-010:** A Driver attempts to delete a form.
- **EC-011:** A user attempts to update a nonexistent form.
- **EC-012:** A user attempts to delete a nonexistent form.
- **EC-013:** A user attempts to change a Form Code to one already used by another form.
- **EC-014:** A user attempts to add an Item not supplied by the form's Supplier.
- **EC-015:** A user attempts to add an inactive Individual Item to an active form.
- **EC-016:** A user attempts to add an Item with zero or negative default case quantity.
- **EC-017:** A user attempts to enter a fractional case quantity.
- **EC-018:** A user attempts to add the same Individual Item twice to one form.
- **EC-019:** A user updates the default quantity of an existing Form Item.
- **EC-020:** A user removes an Item from a form.
- **EC-021:** A form is updated after Supplier Orders have already been created from it.
- **EC-022:** A user attempts to delete a form referenced by an existing Supplier Order.
- **EC-023:** A Manager deactivates a form referenced by historical Supplier Orders.
- **EC-024:** A user attempts to select an inactive form for a new Supplier Order.
- **EC-025:** A user selects an active form whose Supplier has subsequently become inactive.
- **EC-026:** A user selects a form containing an Item no longer available from its Supplier.
- **EC-027:** A user creates a draft Supplier Order from a form and changes the copied quantities before submission.
- **EC-028:** A user cancels preparation of a draft Supplier Order.
- **EC-029:** Two users attempt to create forms with the same Form Code simultaneously.
- **EC-030:** A form is deleted while another transaction attempts to create a Supplier Order referencing it.
- **EC-031:** Invalid form updates must leave existing form information unchanged.

---

## Success Criteria

- **SC-001:** Authorized Purchasing Clerks and Managers can create Supplier Order Forms.
- **SC-002:** Every form receives a unique, system-generated Form ID.
- **SC-003:** Form Codes remain unique and Form Names are required.
- **SC-004:** Forms can reference only existing Suppliers.
- **SC-005:** New active forms cannot be created for inactive Suppliers.
- **SC-006:** One Supplier can have multiple Supplier Order Forms.
- **SC-007:** Authorized users can update form details without changing the Form ID.
- **SC-008:** Form Items reference valid Individual Items available from the form's Supplier.
- **SC-009:** Default quantities are positive integers measured in cases.
- **SC-010:** Duplicate Items within one form are rejected.
- **SC-011:** Authorized users can add, update, and remove default Form Items.
- **SC-012:** Inactive forms cannot be selected for new Supplier Orders.
- **SC-013:** Forms referenced by existing Supplier Orders cannot be deleted.
- **SC-014:** Authorized Managers and Administrators can delete unused forms.
- **SC-015:** Changes to templates do not modify previously created Supplier Orders.
- **SC-016:** Selecting an active form copies valid defaults into a new draft Supplier Order.
- **SC-017:** Users can review and change copied details before submitting the Supplier Order.
- **SC-018:** Selecting a form never automatically submits a Supplier Order.
- **SC-019:** Unauthorized or invalid operations leave existing records unchanged.
- **SC-020:** Form maintenance remains separate from Supplier Order processing.
- **SC-021:** All 22 original Gherkin acceptance scenarios are covered by verification tests.
- **SC-022:** Screen and API behavior consistently enforce validation and permissions.

---

## Key Entities

### Supplier Order Form

Represents a reusable template containing supplier ordering information and default items.

A form can be active or inactive and may be used to prepare multiple Supplier Orders.

### Supplier Order Form Item

Represents an Individual Item included as a default entry on a Supplier Order Form.

Each form item identifies the product and its default order quantity in cases.

### Supplier

Represents the business from which the company purchases products.

Supplier information is maintained in Feature 5.

### Individual Item

Represents a product purchased from Suppliers and stored in warehouses.

Individual Item information is maintained in Feature 4.

### Supplier Item

Represents the relationship between a Supplier and an Individual Item, including the supplier-specific purchasing price.

### Supplier Order

Represents an actual purchase order placed with a Supplier.

Supplier Order creation is handled separately in Feature 9.

### User

Represents an authenticated employee whose role determines whether Supplier Order Forms may be maintained.

---

## Initial Data Model

### Supplier Order Form

| Attribute | Type | Description |
|---|---|---|
| formId | Integer | Unique, system-generated identifier; primary key |
| formCode | String | Unique Supplier Order Form code |
| formName | String | Name identifying the form |
| supplierId | Integer | Foreign key referencing Supplier |
| instructions | String | Default purchasing instructions |
| isActive | Boolean | Indicates whether the form is active |

**Relationships:**
- Each Supplier Order Form belongs to one Supplier.
- One Supplier can have multiple Supplier Order Forms.
- One Supplier Order Form can contain multiple Supplier Order Form Items.
- One Supplier Order Form can be used to prepare multiple Supplier Orders.

**Constraints:**
- formId must be unique and cannot be changed.
- formCode must be unique and nonempty.
- formName must be nonempty.
- supplierId must reference an existing Supplier.
- Forms referenced by Supplier Orders cannot be deleted.

### Supplier Order Form Item

| Attribute | Type | Description |
|---|---|---|
| formItemId | Integer | Unique form item identifier |
| formId | Integer | Foreign key referencing Supplier Order Form |
| itemId | Integer | Foreign key referencing Individual Item |
| defaultQuantityCases | Integer | Default quantity ordered in cases |

**Relationships:**
- Each Form Item belongs to one Supplier Order Form.
- Each Form Item references one Individual Item.
- One Supplier Order Form can contain multiple Form Items.

**Constraints:**
- The combination of formId and itemId must be unique.
- defaultQuantityCases must be greater than zero.
- The Individual Item must be available from the Supplier associated with the form.

### Supplier

| Attribute | Type | Description |
|---|---|---|
| supplierId | Integer | Unique Supplier identifier |
| isActive | Boolean | Indicates whether the Supplier is active |

**Relationships:**
- One Supplier can have multiple Supplier Order Forms.
- Supplier maintenance is defined in Feature 5.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Individual Item identifier |
| unitsPerCase | Integer | Number of individual units per case |

**Relationships:**
- An Individual Item can appear on multiple Supplier Order Forms.
- Item maintenance is defined in Feature 4.

### Supplier Item

| Attribute | Type | Description |
|---|---|---|
| supplierItemId | Integer | Unique Supplier Item relationship identifier |
| supplierId | Integer | Foreign key referencing Supplier |
| itemId | Integer | Foreign key referencing Individual Item |
| purchasePricePerCase | Decimal | Supplier's purchasing price per case |

**Relationships:**
- Supplier Item identifies which products can be purchased from a Supplier.
- Supplier-specific prices are maintained in Feature 4.

### Supplier Order

| Attribute | Type | Description |
|---|---|---|
| supplierOrderId | Integer | Unique Supplier Order identifier |
| supplierId | Integer | Foreign key referencing Supplier |
| sourceFormId | Integer | Optional reference to the form used to prepare the order |

**Relationships:**
- A Supplier Order belongs to one Supplier.
- A Supplier Order may be created using a Supplier Order Form.
- Actual order quantities and prices are stored on the Supplier Order and its order lines.
- Supplier Order creation is defined in Feature 9.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- User roles determine who can create, update, deactivate, or delete Supplier Order Forms.

---

## Gherkin AC

### US-7.1: Add a Supplier Order Form

#### AC-7.1.1: Successfully create Supplier Order Form

**Given** an active Supplier exists  
**And** the user is authenticated as a Purchasing Clerk or Manager  
**When** the user enters a unique Form Code, nonempty Form Name, and selects the Supplier  
**And** saves the form  
**Then** the system creates the Supplier Order Form  
**And** assigns a unique Form ID  
**And** associates the form with the selected Supplier.

#### AC-7.1.2: Reject duplicate Form Code

**Given** a Supplier Order Form exists with Form Code "SOF001"  
**And** the user is authorized to maintain forms  
**When** the user attempts to create another form with Form Code "SOF001"  
**Then** the system rejects the request  
**And** the existing form remains unchanged.

#### AC-7.1.3: Reject missing Form Name

**Given** the user is authorized to maintain forms  
**When** the user attempts to create a form with an empty Form Name  
**Then** the system rejects the request  
**And** no new form is created.

#### AC-7.1.4: Reject nonexistent Supplier

**Given** the requested Supplier does not exist  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user attempts to create a form for that Supplier  
**Then** the system rejects the request  
**And** no form is created.

#### AC-7.1.5: Reject inactive Supplier

**Given** a Supplier exists and is inactive  
**And** the user is authorized to maintain forms  
**When** the user attempts to create an active form for that Supplier  
**Then** the system rejects the request  
**And** no active form is created.

#### AC-7.1.6: Reject unauthorized Form creation

**Given** the user is authenticated as a Warehouse Worker  
**When** the user attempts to create a Supplier Order Form  
**Then** the system denies the operation  
**And** no form is created.

### US-7.2: Edit a Supplier Order Form

#### AC-7.2.1: Successfully update Supplier Order Form

**Given** a Supplier Order Form exists  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user updates the Form Name and ordering instructions  
**And** saves the changes  
**Then** the system stores the updated information  
**And** the Form ID remains unchanged.

#### AC-7.2.2: Reject invalid Form update

**Given** a Supplier Order Form exists  
**And** the user is authenticated as a Manager  
**When** the user removes the required Form Name  
**And** attempts to save the changes  
**Then** the system rejects the update  
**And** the previously stored form information remains unchanged.

#### AC-7.2.3: Reject duplicate Form Code during update

**Given** Form A has Form Code "SOF001"  
**And** Form B has Form Code "SOF002"  
**And** the user is authorized to maintain forms  
**When** the user changes Form B's code to "SOF001"  
**Then** the system rejects the update  
**And** both original Form Codes remain unchanged.

#### AC-7.2.4: Preserve existing Supplier Orders

**Given** a Supplier Order Form has already been used to create a Supplier Order  
**And** the user is authenticated as a Manager  
**When** the user updates the Form's default instructions  
**And** saves the changes  
**Then** the system updates the Form  
**And** the existing Supplier Order remains unchanged.

#### AC-7.2.5: Reject unauthorized Form modification

**Given** a Supplier Order Form exists  
**And** the user is authenticated as a Picker  
**When** the user attempts to modify the form  
**Then** the system denies the request  
**And** the form remains unchanged.

#### AC-7.2.6: Reject editing nonexistent Form

**Given** no Supplier Order Form exists with the requested Form ID  
**And** the user is authenticated as a Manager  
**When** the user attempts to update that form  
**Then** the system rejects the request  
**And** no form is changed.

### US-7.3: Delete or Deactivate a Supplier Order Form

#### AC-7.3.1: Successfully delete unused Form

**Given** a Supplier Order Form exists  
**And** no Supplier Orders reference it  
**And** the user is authenticated as an Administrator  
**When** the user requests deletion  
**Then** the system deletes the Supplier Order Form and its default Form Items  
**And** no Supplier Order is affected.

#### AC-7.3.2: Prevent deletion of referenced Form

**Given** a Supplier Order Form is referenced by an existing Supplier Order  
**And** the user is authenticated as a Manager  
**When** the user requests deletion  
**Then** the system rejects the request  
**And** the Form and Supplier Order remain unchanged.

#### AC-7.3.3: Deactivate Supplier Order Form

**Given** an active Supplier Order Form exists  
**And** the user is authenticated as a Manager  
**When** the user marks the Form as inactive  
**Then** the system saves the inactive status  
**And** the Form remains available for historical reference  
**And** the Form cannot be selected when creating new Supplier Orders.

#### AC-7.3.4: Reject unauthorized Form deletion

**Given** a Supplier Order Form exists  
**And** the user is authenticated as a Driver  
**When** the user attempts to delete the Form  
**Then** the system denies the operation  
**And** the Form remains unchanged.

#### AC-7.3.5: Reject deletion of nonexistent Form

**Given** no Supplier Order Form exists with the requested Form ID  
**And** the user is authenticated as an Administrator  
**When** the user requests deletion of that Form  
**Then** the system rejects the request  
**And** no Form is changed.

### US-7.4: Maintain Supplier Order Form Items

#### AC-7.4.1: Add Item to Form

**Given** an active Supplier Order Form exists  
**And** an active Individual Item is available from the Form's Supplier  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user adds the Item with a default quantity of 5 cases  
**Then** the system saves the Form Item  
**And** stores the default quantity as 5 cases.

#### AC-7.4.2: Reject Item not supplied by Supplier

**Given** a Supplier Order Form is associated with Supplier A  
**And** Item B is not associated with Supplier A  
**When** an authorized user attempts to add Item B to the Form  
**Then** the system rejects the request  
**And** no invalid Form Item is created.

#### AC-7.4.3: Reject invalid default quantity

**Given** a Supplier Order Form exists  
**And** the user is authorized to maintain form items  
**When** the user attempts to add an Item with a default quantity of zero cases  
**Then** the system rejects the request  
**And** no Form Item is created.

#### AC-7.4.4: Reject duplicate Item on Form

**Given** a Supplier Order Form already contains Item A  
**When** an authorized user attempts to add Item A again  
**Then** the system rejects the duplicate entry  
**And** the existing Form Item remains unchanged.

#### AC-7.4.5: Use Form to Prepare Supplier Order

**Given** an active Supplier Order Form contains valid default Items and quantities  
**And** its Supplier is active  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user selects the Form to prepare a new Supplier Order  
**Then** the system creates a new draft Supplier Order  
**And** copies the applicable Supplier and Item information into the draft  
**And** allows the user to review the quantities before submission  
**And** does not automatically submit the order.

---

## Data Ownership

### Supplier Order Form Data

**Owner:** Feature 7 — Maintain Supplier Order Forms.

Feature 7 owns:
- Supplier Order Form ID.
- Form Code.
- Form Name.
- Supplier association.
- Default ordering instructions.
- Active or Inactive status.
- Supplier Order Form Items.
- Default case quantities.

Feature 7 is responsible for creating, updating, deactivating, and deleting eligible templates.

### Supplier Master Data

**Owner:** Feature 5 — Maintain Suppliers.

Feature 7 references existing Suppliers and checks their active status.

Feature 7 must not create, edit, deactivate, or delete Supplier master records.

### Individual Item Data

**Owner:** Feature 4 — Maintain Individual Item.

Feature 7 references existing Individual Items when adding default Form Items.

Feature 7 must not directly modify Individual Item master information.

### Supplier Item Relationships

**Owner:** Feature 4 — Maintain Individual Item.

Supplier Item relationships determine which Individual Items are available from each Supplier.

Feature 7 validates Form Items against these relationships.

Supplier-specific purchasing prices remain maintained in Feature 4.

### Supplier Order Data

**Owner:** Feature 9 — Create Supplier Order.

Feature 9 owns:
- Actual Supplier Orders.
- Supplier Order line items.
- Actual ordered quantities.
- Actual purchasing prices.
- Supplier Order status.
- Submission of Supplier Orders.

Feature 7 supplies template defaults but does not submit or modify existing Supplier Orders.

The optional `sourceFormId` reference allows an order to identify the template from which it originated.

### User and Authorization Data

**Owner:** Shared authentication and authorization functionality.

Purchasing Clerks and Managers may create and update Supplier Order Forms.

Managers and Administrators may delete unused forms.

Warehouse Workers, Receivers, Pickers, and Drivers cannot modify Supplier Order Forms.

### Data Consistency Rules

- Form IDs are unique and immutable.
- Form Codes are unique.
- Every form references an existing Supplier.
- Every Form Item references an existing Individual Item.
- Every Form Item must be valid for the form's Supplier.
- Each Item appears only once per form.
- Default quantities are positive integers.
- Inactive forms cannot be selected for new Supplier Orders.
- Forms referenced by Supplier Orders cannot be deleted.
- Existing Supplier Orders remain unchanged when templates are updated.
- Concurrent operations must not bypass uniqueness or dependency checks.

---

## API Requirements

**Design status:** Proposed API contracts for Feature 7.

The endpoints below are proposed and must follow the Warehouse project's established API conventions.

**Base resource:** `/api/supplier-order-forms`

### API-7.1: List Supplier Order Forms

**Method:** GET  
**Endpoint:** `/api/supplier-order-forms`

**Purpose:** Retrieve and search Supplier Order Form templates.

**Authorization:** Authenticated Users with appropriate purchasing permissions.

**Query parameters:**
- `formCode`
- `formName`
- `supplierId`
- `isActive`

**Successful response:** `200 OK`

**Rules:**
- Allow searching and filtering forms.
- Include inactive forms for authorized historical lookup.
- Do not modify records during search.

**Traceability:** FR-003 through FR-008, FR-020 through FR-022.

### API-7.2: Create Supplier Order Form

**Method:** POST  
**Endpoint:** `/api/supplier-order-forms`

**Purpose:** Create a reusable Supplier Order Form.

**Authorization:** Purchasing Clerk or Manager.

**Example request:**

    {
      "formCode": "SOF001",
      "formName": "Weekly Grocery Order",
      "supplierId": 101,
      "instructions": "Deliver to receiving door",
      "isActive": true
    }

**Successful response:** `201 Created`

**Validation:**
- Form Code must be unique and nonempty.
- Form Name must be nonempty.
- Supplier must exist.
- New active forms cannot reference inactive Suppliers.
- Form ID is generated automatically.
- Unauthorized requests are rejected.

**Error responses:**
- `400 Bad Request` for invalid data.
- `401 Unauthorized` for missing authentication.
- `403 Forbidden` for insufficient permissions.
- `404 Not Found` for nonexistent Supplier references.
- `409 Conflict` for duplicate Form Codes.

**Traceability:** US-7.1; FR-001 through FR-008; AC-7.1.1 through AC-7.1.6.

### API-7.3: Get Supplier Order Form Details

**Method:** GET  
**Endpoint:** `/api/supplier-order-forms/{formId}`

**Purpose:** Retrieve an existing form and its default Items.

**Authorization:** Authorized purchasing personnel.

**Successful response:** `200 OK`

**Displayed information:**
- Form ID.
- Form Code.
- Form Name.
- Supplier.
- Instructions.
- Active Status.
- Form Items and default case quantities.

**Error responses:**
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.

### API-7.4: Update Supplier Order Form

**Method:** PUT  
**Endpoint:** `/api/supplier-order-forms/{formId}`

**Purpose:** Update form information.

**Authorization:** Purchasing Clerk or Manager.

**Successful response:** `200 OK`

**Validation:**
- Form must exist.
- Form ID must remain unchanged.
- Form Code must remain unique.
- Form Name cannot be empty.
- Supplier association must remain valid.
- Invalid updates must preserve previously stored information.
- Existing Supplier Orders must remain unchanged.

**Error responses:**
- `400 Bad Request`.
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.
- `409 Conflict`.

**Traceability:** US-7.2; FR-015 through FR-018, FR-033; AC-7.2.1 through AC-7.2.6.

### API-7.5: Change Form Status

**Method:** PATCH  
**Endpoint:** `/api/supplier-order-forms/{formId}/status`

**Purpose:** Activate or deactivate a form.

**Authorization:** Manager or Administrator, subject to approved status permissions.

**Example request:**

    {
      "isActive": false
    }

**Successful response:** `200 OK`

**Rules:**
- Form must exist.
- Inactive forms cannot be selected for new Supplier Orders.
- Historical references remain available.
- Reactivation must respect Supplier active-status rules.

**Error responses:**
- `400 Bad Request`.
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.
- `409 Conflict` when a required business rule is violated.

**Traceability:** US-7.3; FR-020 through FR-022; AC-7.3.3.

### API-7.6: Delete Supplier Order Form

**Method:** DELETE  
**Endpoint:** `/api/supplier-order-forms/{formId}`

**Purpose:** Delete an unused form.

**Authorization:** Manager or Administrator.

**Successful response:** `204 No Content`

**Validation:**
- Form must exist.
- No Supplier Orders may reference the form.
- Deletion removes the form and its default Form Items.
- Rejected deletion must preserve the form and its Items.
- Dependency checks must be protected against concurrent transactions.

**Error responses:**
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.
- `409 Conflict` when Supplier Orders reference the form.

**Traceability:** US-7.3; FR-023 through FR-026; AC-7.3.1, AC-7.3.2, AC-7.3.4, AC-7.3.5.

### API-7.7: Add Form Item

**Method:** POST  
**Endpoint:** `/api/supplier-order-forms/{formId}/items`

**Purpose:** Add a default Individual Item to a form.

**Authorization:** Purchasing Clerk or Manager.

**Example request:**

    {
      "itemId": 201,
      "defaultQuantityCases": 5
    }

**Successful response:** `201 Created`

**Validation:**
- Form must exist.
- Item must exist.
- Item must be available from the form's Supplier.
- Item must meet applicable active-status requirements.
- Default quantity must be a positive integer.
- The same Item cannot appear twice on one form.

**Error responses:**
- `400 Bad Request`.
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.
- `409 Conflict`.

**Traceability:** US-7.4; FR-009 through FR-013, FR-019; AC-7.4.1 through AC-7.4.4.

### API-7.8: Update Form Item

**Method:** PUT  
**Endpoint:** `/api/supplier-order-forms/{formId}/items/{formItemId}`

**Purpose:** Update a default Form Item.

**Authorization:** Purchasing Clerk or Manager.

**Successful response:** `200 OK`

**Rules:**
- Form and Form Item must exist.
- Quantity must remain a positive integer.
- Item and Supplier relationships must remain valid.
- Existing Supplier Orders must not be changed.

**Traceability:** FR-011 through FR-013, FR-019, FR-033.

### API-7.9: Remove Form Item

**Method:** DELETE  
**Endpoint:** `/api/supplier-order-forms/{formId}/items/{formItemId}`

**Purpose:** Remove a default Item from a form.

**Authorization:** Purchasing Clerk or Manager.

**Successful response:** `204 No Content`

**Rules:**
- Form and Form Item must exist.
- Only the template entry is removed.
- Previously created Supplier Orders remain unchanged.

**Traceability:** FR-019, FR-033.

### API-7.10: Prepare Supplier Order from Form

**Method:** POST  
**Endpoint:** `/api/supplier-orders/drafts/from-form/{formId}`

**Purpose:** Prepare a new draft Supplier Order using form defaults.

**Owner:** Feature 9 — Create Supplier Order.

**Authorization:** Authorized purchasing personnel.

**Successful response:** `201 Created`

**Rules:**
- Form must exist and be active.
- Supplier must be active.
- Applicable Form Items must be valid.
- Copy Supplier and Item information into the new draft.
- Copy default quantities into the draft.
- Allow the User to review and modify the draft.
- Do not automatically submit the Supplier Order.
- Do not change previously created Supplier Orders.

**Traceability:** FR-029 through FR-033; AC-7.4.5.

### Shared API Rules

- Enforce authentication and authorization.
- Validate all required fields.
- Enforce unique Form Codes.
- Validate Supplier and Item references.
- Reject duplicate Form Items.
- Require positive integer case quantities.
- Preserve historical Supplier Orders.
- Use transactional writes for related form changes.
- Prevent concurrent operations from bypassing constraints.
- Follow the project's existing API naming and error-response conventions.

---

## Screen Requirements

**Design status:** Proposed screen specifications for Feature 7.

Screen images should be created and linked to the feature documentation.

### Screen UI-7A: Supplier Order Form List

**Proposed image:** `docs/UI/supplier-order-form-list.png`

**Purpose:** Search and select Supplier Order Forms.

**Displayed information:**
- Form Code.
- Form Name.
- Supplier Name.
- Active Status.

**Actions:**
- Search Forms.
- Filter by Supplier.
- Filter by Active Status.
- View Form.
- Add Form.
- Edit Form.
- Delete Form.
- Prepare Supplier Order.

**Rules:**
- Maintenance actions are restricted by role.
- Inactive forms must be clearly identified.
- Inactive forms cannot be selected for new Supplier Orders.

### Screen UI-7B: Add Supplier Order Form

**Proposed image:** `docs/UI/supplier-order-form-add.png`

**Purpose:** Create a Supplier Order Form.

**Fields:**

| Field | Control | Required |
|---|---|---|
| Form Code | Text input | Yes |
| Form Name | Text input | Yes |
| Supplier | Supplier selector | Yes |
| Instructions | Multiline text | No |
| Active Status | Checkbox | Yes |

**Actions:**
- Save.
- Cancel.

**Rules:**
- Form Code must be unique.
- Form Name must be nonempty.
- Supplier must exist.
- New active forms cannot use inactive Suppliers.
- Form ID is generated by the system.

### Screen UI-7C: Edit Supplier Order Form

**Proposed image:** `docs/UI/supplier-order-form-edit.png`

**Purpose:** Update form information.

**Fields:**
- Form ID (read-only).
- Form Code.
- Form Name.
- Supplier.
- Default Instructions.
- Active Status.

**Actions:**
- Save Changes.
- Cancel.
- Manage Form Items.
- View Related Supplier Orders.

**Rules:**
- Form ID remains unchanged.
- Form Code remains unique.
- Invalid updates are rejected.
- Existing Supplier Orders remain unchanged.

### Screen UI-7D: Maintain Form Items

**Proposed image:** `docs/UI/supplier-order-form-items.png`

**Purpose:** Manage default Items and case quantities.

**Displayed information:**
- Form Code.
- Supplier.
- Individual Item Number.
- Individual Item Description.
- Default Quantity in Cases.

**Actions:**
- Add Item.
- Update Quantity.
- Remove Item.
- Save Changes.
- Cancel.

**Rules:**
- Item must be available from the form's Supplier.
- Default quantity must be a positive integer.
- Duplicate Items are rejected.
- Supplier Item purchasing prices remain owned by Feature 4.
- Previously created Supplier Orders remain unchanged.

### Screen UI-7E: Supplier Order Form Details

**Proposed image:** `docs/UI/supplier-order-form-details.png`

**Purpose:** Display form information and default Items.

**Displayed information:**
- Form ID.
- Form Code.
- Form Name.
- Supplier.
- Instructions.
- Active Status.
- Default Form Items.
- Default Case Quantities.

**Actions:**
- Edit, if authorized.
- Prepare Supplier Order, if eligible.
- Return to Form List.

### Screen UI-7F: Prepare Supplier Order Preview

**Proposed image:** `docs/UI/supplier-order-form-preview.png`

**Purpose:** Preview template defaults before creating a draft Supplier Order.

**Displayed information:**
- Selected Form.
- Supplier.
- Default Instructions.
- Item List.
- Default Case Quantities.

**Actions:**
- Prepare Draft.
- Cancel.

**Rules:**
- Form and Supplier must be active.
- Applicable Items must be valid.
- Preparing a draft does not submit an order.
- Actual order editing and submission belong to Feature 9.

### Screen UI-7G: Delete or Deactivate Form

**Proposed image:** `docs/UI/supplier-order-form-status.png`

**Purpose:** Confirm form deactivation or deletion.

**Displayed information:**
- Form Code.
- Form Name.
- Active Status.
- Existing Supplier Order references.
- Deletion eligibility.

**Actions:**
- Deactivate.
- Delete, if eligible.
- Cancel.

**Rules:**
- Referenced forms cannot be deleted.
- Deactivated forms remain available for historical reference.
- Unauthorized operations are rejected.

### Role Permissions

| Role | View Forms | Add/Edit Forms | Maintain Form Items | Delete Forms |
|---|---|---|---|---|
| Purchasing Clerk | Yes | Yes | Yes | No |
| Manager | Yes | Yes | Yes | Yes, if eligible |
| Administrator | According to permissions | According to permissions | According to permissions | Yes, if eligible |
| Warehouse Worker | If authorized | No | No | No |
| Receiver | If authorized | No | No | No |
| Picker | If authorized | No | No | No |
| Driver | If authorized | No | No | No |

### Validation and Feedback

The UI must display clear messages for:
- Duplicate Form Code.
- Missing Form Code.
- Missing Form Name.
- Nonexistent Supplier.
- Inactive Supplier.
- Nonexistent Form.
- Invalid Form Item.
- Item not available from Supplier.
- Duplicate Form Item.
- Zero or negative default quantity.
- Unauthorized operation.
- Referenced Form cannot be deleted.
- Inactive Form cannot be used for new Supplier Orders.
- Successful creation, update, deactivation, or deletion.

### Proposed UI Deliverables

- `docs/UI/supplier-order-form-list.png`
- `docs/UI/supplier-order-form-add.png`
- `docs/UI/supplier-order-form-edit.png`
- `docs/UI/supplier-order-form-items.png`
- `docs/UI/supplier-order-form-details.png`
- `docs/UI/supplier-order-form-preview.png`
- `docs/UI/supplier-order-form-status.png`

These paths must match the final repository structure.

---

## Definition of Done

### Requirements and Design

- [ ] All four User Stories are documented.
- [ ] All thirty-four original Functional Requirements are retained.
- [ ] Assumptions are documented.
- [ ] Edge Cases are documented.
- [ ] Success Criteria are documented.
- [ ] Key Entities are documented.
- [ ] Initial Data Model is documented.
- [ ] All twenty-two original Gherkin acceptance scenarios are retained.
- [ ] Data Ownership is documented.
- [ ] API Requirements are documented.
- [ ] Screen Requirements are documented.
- [ ] Out-of-Scope functionality is documented.
- [ ] Pending clarifications are recorded.

### Form Maintenance

- [ ] Authorized Users can create Supplier Order Forms.
- [ ] Form IDs are generated uniquely.
- [ ] Form Codes are unique.
- [ ] Form Names are required.
- [ ] Forms reference existing Suppliers.
- [ ] Active forms cannot be created for inactive Suppliers.
- [ ] Authorized Users can update existing forms.
- [ ] Form IDs remain unchanged during updates.
- [ ] Invalid updates preserve existing information.
- [ ] Authorized Managers and Administrators can delete unused forms.
- [ ] Referenced forms cannot be deleted.
- [ ] Forms can be deactivated.
- [ ] Inactive forms cannot be selected for new Supplier Orders.

### Form Item Maintenance

- [ ] Authorized Users can add Form Items.
- [ ] Items must be available from the form's Supplier.
- [ ] Default quantities are positive integers.
- [ ] Duplicate Items on one form are rejected.
- [ ] Authorized Users can update default quantities.
- [ ] Authorized Users can remove Form Items.
- [ ] Supplier Item purchasing prices remain owned by Feature 4.

### Supplier Order Integration

- [ ] Active forms can be selected for preparing Supplier Orders.
- [ ] Form defaults are copied into new draft Supplier Orders.
- [ ] Draft quantities can be reviewed and modified.
- [ ] Preparing a draft does not automatically submit an order.
- [ ] Updating a form does not modify existing Supplier Orders.
- [ ] Feature 9 owns actual Supplier Order creation and submission.

### Security and Validation

- [ ] Role permissions are enforced.
- [ ] Warehouse Workers cannot modify forms.
- [ ] Receivers cannot modify forms.
- [ ] Pickers cannot modify forms.
- [ ] Drivers cannot modify forms.
- [ ] Backend validation protects required fields and references.
- [ ] Concurrent operations cannot bypass uniqueness or deletion restrictions.

### Acceptance Testing

- [ ] AC-7.1.1 through AC-7.1.6 pass.
- [ ] AC-7.2.1 through AC-7.2.6 pass.
- [ ] AC-7.3.1 through AC-7.3.5 pass.
- [ ] AC-7.4.1 through AC-7.4.5 pass.
- [ ] Tests cover duplicate Form Codes.
- [ ] Tests cover invalid Suppliers.
- [ ] Tests cover invalid Form Items.
- [ ] Tests cover default quantity validation.
- [ ] Tests cover authorization restrictions.
- [ ] Tests cover deletion dependencies.
- [ ] Tests verify existing Supplier Orders remain unchanged.

### Documentation and Review

- [ ] Feature 7 follows the required OC Speckit section structure.
- [ ] Relevant design decisions are documented in `docs/ADRs/`.
- [ ] Relevant non-functional requirements are addressed in `docs/NFR/`.
- [ ] Supplier Order Form relationships are reflected in the relevant C4 diagrams.
- [ ] Required UI screen designs are created.
- [ ] UI screen images are linked using correct repository paths.
- [ ] Changes are committed to the `design-draft` branch.
- [ ] Changes are pushed to GitHub.

**Draft note:** The checklist describes required work and verification. It does not mean that implementation, testing, or screen images have already been completed.

---

## Out of Scope

Feature 7 does not include:

- Creating or maintaining Supplier master records.
- Creating or maintaining Individual Item master records.
- Maintaining Supplier Item purchasing prices.
- Creating or modifying actual Supplier Orders outside the draft preparation integration.
- Submitting Supplier Orders.
- Receiving products from Suppliers.
- Updating Inventory quantities.
- Performing Put Away, Picking, or Shipping.
- Maintaining Customer Orders.
- Maintaining Warehouse or Company master information.
- Managing User accounts, passwords, or authorization roles.
- Automatically submitting purchase orders when a form is selected.
- Automatically changing existing Supplier Orders when a form is updated.
- Deleting forms referenced by existing Supplier Orders.
- Allowing Warehouse Workers, Receivers, Pickers, or Drivers to modify Supplier Order Forms.

### Pending Clarifications

- **CL-7.1:** Can an inactive form be created for an inactive Supplier?
- **CL-7.2:** Can an existing form be reassigned to a different Supplier, and what happens to its Form Items?
- **CL-7.3:** Should a form be allowed to remain active when its Supplier becomes inactive?
- **CL-7.4:** Should the system allow a form with no default Items?
- **CL-7.5:** Should a form automatically exclude Items that are no longer active or available from its Supplier when preparing an order?
- **CL-7.6:** Are default ordering instructions copied into the Supplier Order or only displayed during preparation?
- **CL-7.7:** Who may reactivate a previously inactive Supplier Order Form?
- **CL-7.8:** Should form defaults include purchasing prices, or should Feature 9 retrieve current Supplier Item prices when creating a draft?

These decisions must be coordinated with Features 4, 5, and 9 before implementation.
