
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