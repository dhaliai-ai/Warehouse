
# Feature: Maintain Suppliers

**Feature ID:** 5  
**Branch pattern:** `feature/5-maintain-suppliers`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System maintains information about suppliers from whom the company purchases products. Authorized office personnel can add, edit, delete, or deactivate suppliers. Supplier records include identifying information, contact details, the account number assigned to the company by the supplier, and purchasing information. The system preserves supplier relationships and historical purchase orders.

---

## User Stories

### US-5.1: Add a Supplier

**As a** Purchasing Clerk or Manager  
**I want to** add a supplier with its identification and contact information  
**So that** the company can purchase products from that supplier.

**Priority:** P1  
**Independent test:** Create a supplier with a unique Supplier Number and valid required information, then verify that the record is saved.

### US-5.2: Edit a Supplier

**As a** Purchasing Clerk or Manager  
**I want to** update supplier contact information and purchasing details  
**So that** the company maintains accurate supplier records.

**Priority:** P1  
**Independent test:** Update an existing supplier's address, phone number, or account information and verify that the changes are saved.

### US-5.3: Delete or Deactivate a Supplier

**As a** Manager or Administrator  
**I want to** delete an unused supplier or deactivate a supplier that the company no longer purchases from  
**So that** obsolete suppliers are not used for new orders while historical purchasing records remain available.

**Priority:** P1  
**Independent test:** Verify that an unused supplier can be deleted, while a supplier referenced by purchase orders is protected from deletion and can be deactivated.

### US-5.4: Maintain Supplier Purchasing Information

**As a** Purchasing Clerk or Manager  
**I want to** maintain supplier account information, payment terms, and estimated shipping lead time  
**So that** purchasing personnel have the information needed to place and manage supplier orders.

**Priority:** P1  
**Independent test:** Save and update a supplier's purchasing information and verify that it is available when preparing supplier orders.

---

## Functional Requirements

- **FR-001:** The system MUST allow authorized Purchasing Clerks and Managers to create Supplier records.
- **FR-002:** The system MUST assign a unique, system-generated Supplier ID to each Supplier.
- **FR-003:** The system MUST maintain a unique Supplier Number used internally by the company.
- **FR-004:** The system MUST prevent duplicate Supplier Numbers.
- **FR-005:** The system MUST maintain the Supplier Name.
- **FR-006:** The system MUST maintain the Supplier Address.
- **FR-007:** The system MUST maintain the Supplier Phone Number.
- **FR-008:** The system MUST maintain the Supplier Email Address.
- **FR-009:** The system MUST maintain the account or customer number assigned to the company by the Supplier.
- **FR-010:** The system MUST keep the internal Supplier Number separate from the account number assigned by the Supplier.
- **FR-011:** The system MUST support recording Supplier payment terms.
- **FR-012:** The system MUST support recording estimated Supplier shipping lead time in days.
- **FR-013:** The system MUST require a nonempty Supplier Name and internal Supplier Number.
- **FR-014:** The system MUST validate the format of an Email Address when one is provided.
- **FR-015:** The system MUST reject a negative shipping lead time.
- **FR-016:** The system MUST validate Supplier information before saving.
- **FR-017:** The system MUST reject invalid Supplier information without changing existing records.
- **FR-018:** The system MUST allow authorized Purchasing Clerks and Managers to update existing Supplier information.
- **FR-019:** The system MUST preserve the Supplier ID when Supplier information is updated.
- **FR-020:** The system MUST support searching for a Supplier by Supplier Number or Supplier Name.
- **FR-021:** The system MUST support associating a Supplier with multiple Individual Items.
- **FR-022:** The system MUST support associating an Individual Item with multiple Suppliers.
- **FR-023:** The system MUST maintain Supplier-specific purchasing prices through Supplier Item relationships.
- **FR-024:** The system MUST support associating a Supplier with multiple Supplier Orders.
- **FR-025:** Each Supplier Order MUST reference the Supplier from whom products are ordered.
- **FR-026:** The system MUST support marking a Supplier as active or inactive.
- **FR-027:** The system MUST prevent inactive Suppliers from being selected for new Supplier Orders.
- **FR-028:** The system MUST preserve inactive Supplier records for historical purchasing reports.
- **FR-029:** The system MUST allow authorized Managers and Administrators to delete a Supplier only when no Supplier Orders or other historical transactions reference it and no Supplier Item relationships remain.
- **FR-030:** The system MUST reject deletion when a Supplier is referenced by Supplier Orders, historical transactions, or Supplier Item relationships.
- **FR-031:** The system MUST preserve Supplier information when deletion is rejected.
- **FR-032:** The system MUST reject attempts to edit or delete a Supplier that does not exist.
- **FR-033:** The system MUST restrict Supplier creation and modification to authorized office personnel, including Purchasing Clerks and Managers.
- **FR-034:** Warehouse workers, receivers, pickers, and drivers MUST NOT modify Supplier master information.
- **FR-035:** The system MUST maintain Supplier master information separately from Supplier Orders and Supplier Item purchasing prices.
- **FR-036:** The system MUST preserve relationships between Suppliers, Individual Items, and Supplier Orders.

---

## Key Entities

### Supplier

Represents a business from which the company purchases products.

Each Supplier has identifying information, contact details, purchasing information, and an active status.

### Individual Item

Represents a product purchased from Suppliers and sold to Customers.

Individual Item maintenance is defined in Feature 4.

### Supplier Item

Represents the purchasing relationship between a Supplier and an Individual Item.

The relationship stores the price charged by the Supplier for the Item.

### Supplier Order

Represents an order placed by the company with a Supplier.

Supplier Order creation is defined in Feature 9.

### User

Represents an authenticated employee whose role determines whether Supplier information may be maintained.

---

## Initial Data Model

### Supplier

| Attribute | Type | Description |
|---|---|---|
| supplierId | Integer | Unique, system-generated identifier; primary key |
| supplierNumber | String | Unique internal Supplier Number |
| name | String | Supplier business name; required |
| address | String | Supplier business address |
| phone | String | Supplier contact telephone number |
| email | String | Supplier contact email address |
| companyAccountNumber | String | Account or customer number assigned to the company by this Supplier |
| paymentTerms | String | Supplier payment terms |
| shippingLeadTimeDays | Integer | Estimated shipping lead time in days |
| isActive | Boolean | Indicates whether the Supplier is active |

**Relationships:**
- One Supplier can supply multiple Individual Items.
- One Supplier can have multiple Supplier Item relationships.
- One Supplier can have multiple Supplier Orders.

**Constraints:**
- supplierId must be unique and cannot be changed.
- supplierNumber must be unique and nonempty.
- name must be nonempty.
- email must have a valid email format when provided.
- shippingLeadTimeDays cannot be negative.
- A Supplier referenced by historical orders cannot be deleted.

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique Item identifier |

**Relationships:**
- An Individual Item can be supplied by multiple Suppliers.
- Item information is maintained in Feature 4.

### Supplier Item

| Attribute | Type | Description |
|---|---|---|
| supplierItemId | Integer | Unique Supplier Item relationship identifier |
| supplierId | Integer | Foreign key referencing Supplier |
| itemId | Integer | Foreign key referencing Individual Item |
| purchasePricePerCase | Decimal | Supplier's purchasing price per case |

**Relationships:**
- Each Supplier Item references one Supplier.
- Each Supplier Item references one Individual Item.
- A Supplier can supply multiple Items.
- An Item can be supplied by multiple Suppliers.

**Constraints:**
- The combination of supplierId and itemId must be unique.
- purchasePricePerCase cannot be negative.

### Supplier Order

| Attribute | Type | Description |
|---|---|---|
| supplierOrderId | Integer | Unique Supplier Order identifier |
| supplierId | Integer | Foreign key referencing Supplier |

**Relationships:**
- Each Supplier Order belongs to one Supplier.
- One Supplier can have multiple Supplier Orders.
- Supplier Order details are defined in Feature 9.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- User roles determine who may create, update, deactivate, or delete Supplier records.

---

## Gherkin AC

### US-5.1: Add a Supplier

#### AC-5.1.1: Successfully create Supplier

**Given** the user is authenticated as a Purchasing Clerk or Manager  
**When** the user enters a unique Supplier Number, nonempty Supplier Name, and valid Supplier information  
**And** saves the record  
**Then** the system creates the Supplier  
**And** assigns a unique Supplier ID  
**And** stores the Supplier information.

#### AC-5.1.2: Reject duplicate Supplier Number

**Given** a Supplier exists with Supplier Number "SUP001"  
**And** the user is authorized to maintain Suppliers  
**When** the user attempts to create another Supplier with Supplier Number "SUP001"  
**Then** the system rejects the request  
**And** the existing Supplier remains unchanged.

#### AC-5.1.3: Reject missing Supplier Name

**Given** the user is authorized to maintain Suppliers  
**When** the user attempts to create a Supplier with an empty Name  
**Then** the system rejects the request  
**And** no Supplier record is created.

#### AC-5.1.4: Reject invalid Email Address

**Given** the user is authorized to maintain Suppliers  
**When** the user enters an Email Address that does not meet the required email format  
**And** attempts to save the Supplier  
**Then** the system rejects the request  
**And** no Supplier record is created.

#### AC-5.1.5: Reject unauthorized Supplier creation

**Given** the user is authenticated as a Warehouse Worker  
**When** the user attempts to create a Supplier  
**Then** the system denies the request  
**And** no Supplier record is created.

### US-5.2: Edit a Supplier

#### AC-5.2.1: Successfully update Supplier

**Given** a Supplier record exists  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user updates the Supplier's Address and Phone Number with valid information  
**And** saves the changes  
**Then** the system stores the updated information  
**And** the Supplier ID remains unchanged.

#### AC-5.2.2: Reject invalid Supplier update

**Given** a Supplier record exists  
**And** the user is authenticated as a Manager  
**When** the user removes the required Supplier Name  
**And** attempts to save the changes  
**Then** the system rejects the update  
**And** the previously stored Supplier information remains unchanged.

#### AC-5.2.3: Reject duplicate Supplier Number during update

**Given** Supplier A has Supplier Number "SUP001"  
**And** Supplier B has Supplier Number "SUP002"  
**And** the user is authorized to maintain Suppliers  
**When** the user changes Supplier B's Number to "SUP001"  
**Then** the system rejects the update  
**And** both original Supplier Numbers remain unchanged.

#### AC-5.2.4: Reject unauthorized Supplier modification

**Given** a Supplier record exists  
**And** the user is authenticated as a Driver  
**When** the user attempts to modify Supplier information  
**Then** the system denies the request  
**And** the Supplier remains unchanged.

#### AC-5.2.5: Reject editing nonexistent Supplier

**Given** no Supplier exists with the requested Supplier ID  
**And** the user is authenticated as a Manager  
**When** the user attempts to update that Supplier  
**Then** the system rejects the request  
**And** no Supplier record is changed.

### US-5.3: Delete or Deactivate a Supplier

#### AC-5.3.1: Successfully delete unused Supplier

**Given** a Supplier exists  
**And** no Supplier Orders or historical transactions reference it  
**And** no Supplier Item relationships remain  
**And** the user is authenticated as an Administrator  
**When** the user requests Supplier deletion  
**Then** the system deletes the Supplier record  
**And** the Supplier is no longer available in the Supplier directory.

#### AC-5.3.2: Prevent deletion when Supplier Orders exist

**Given** a Supplier is referenced by one or more Supplier Orders  
**And** the user is authenticated as a Manager  
**When** the user requests Supplier deletion  
**Then** the system rejects the deletion  
**And** the Supplier and its order history remain unchanged.

#### AC-5.3.3: Prevent deletion when Supplier Item relationships exist

**Given** a Supplier is associated with one or more Individual Items  
**And** the user is authenticated as an Administrator  
**When** the user requests Supplier deletion  
**Then** the system rejects the deletion  
**And** the Supplier Item relationships remain unchanged.

#### AC-5.3.4: Deactivate Supplier

**Given** an active Supplier exists  
**And** the user is authenticated as a Manager  
**When** the user marks the Supplier as inactive  
**Then** the system saves the inactive status  
**And** the Supplier remains available for historical reporting  
**And** the Supplier cannot be selected for new Supplier Orders.

#### AC-5.3.5: Reject unauthorized Supplier deletion

**Given** a Supplier record exists  
**And** the user is authenticated as a Picker  
**When** the user attempts to delete the Supplier  
**Then** the system denies the request  
**And** the Supplier remains unchanged.

#### AC-5.3.6: Reject deletion of nonexistent Supplier

**Given** no Supplier exists with the requested Supplier ID  
**And** the user is authenticated as an Administrator  
**When** the user requests deletion of that Supplier  
**Then** the system rejects the request  
**And** no Supplier record is changed.

### US-5.4: Maintain Supplier Purchasing Information

#### AC-5.4.1: Save Supplier Account Number

**Given** an existing Supplier record  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user enters the Account Number assigned to the company by the Supplier  
**And** saves the changes  
**Then** the system stores the Account Number  
**And** keeps it separate from the internal Supplier Number.

#### AC-5.4.2: Update Supplier Payment Terms

**Given** an existing Supplier record  
**And** the user is authenticated as a Manager  
**When** the user changes the Supplier's Payment Terms  
**And** saves the changes  
**Then** the system stores the updated Payment Terms.

#### AC-5.4.3: Save Supplier Shipping Lead Time

**Given** an existing Supplier record  
**And** the user is authenticated as a Purchasing Clerk  
**When** the user enters a shipping lead time of 7 days  
**And** saves the changes  
**Then** the system stores the shipping lead time as 7 days.

#### AC-5.4.4: Reject negative Shipping Lead Time

**Given** an existing Supplier record  
**And** the user is authenticated as a Manager  
**When** the user attempts to set the shipping lead time to -3 days  
**Then** the system rejects the update  
**And** the previously stored shipping lead time remains unchanged.
