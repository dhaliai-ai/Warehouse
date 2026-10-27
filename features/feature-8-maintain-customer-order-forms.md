
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
