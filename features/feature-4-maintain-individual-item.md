
# Feature: Maintain Individual Item

**Feature ID:** 4  
**Branch pattern:** `feature/4-maintain-individual-item`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System maintains the products purchased from suppliers, stored in warehouses, and sold to customers. Authorized office personnel maintain item numbers, descriptions, UPC barcodes, selling prices, supplier relationships, quantities per case, and minimum and maximum stock levels. The system prevents duplicate item numbers and preserves item history when products are discontinued.

---

## User Stories

### US-4.1: Add an Individual Item

**As an** Inventory Clerk or Manager  
**I want to** add a new item with its identifying and purchasing information  
**So that** the warehouse can purchase, receive, store, pick, and sell the item.

**Priority:** P1  
**Independent test:** Create an item with a unique item number and valid required information, then verify that it is saved.

### US-4.2: Edit an Individual Item

**As an** Inventory Clerk or Manager  
**I want to** update an item's description, UPCs, prices, supplier relationships, and stock levels  
**So that** product information remains accurate for warehouse operations.

**Priority:** P1  
**Independent test:** Update an existing item's information and verify that the changes are saved without changing its unique Item ID.

### US-4.3: Delete or Deactivate an Individual Item

**As a** Manager or Administrator  
**I want to** remove an unused item or deactivate a discontinued item  
**So that** obsolete products are no longer used in new transactions while historical records remain available.

**Priority:** P1  
**Independent test:** Verify that an unused item can be deleted, while an item referenced by inventory or historical orders is protected from deletion and can be deactivated.

### US-4.4: Maintain Item UPCs

**As an** Inventory Clerk or Manager  
**I want to** maintain the UPC barcodes associated with an item  
**So that** warehouse workers can identify products accurately during receiving and picking.

**Priority:** P1  
**Independent test:** Add a UPC to an existing item and verify that scanning or looking up the UPC identifies the correct item.

### US-4.5: Maintain Item Supplier Relationships

**As an** Inventory Clerk or Manager  
**I want to** associate an item with suppliers and their purchasing prices  
**So that** the company can purchase the same item from different suppliers when necessary.

**Priority:** P1  
**Independent test:** Associate an item with two existing suppliers and verify that each supplier has its own purchasing price.

---

## Functional Requirements

- **FR-001:** The system MUST allow authorized Inventory Clerks and Managers to create Individual Item records.
- **FR-002:** The system MUST assign a unique, system-generated Item ID to each Individual Item.
- **FR-003:** The system MUST maintain a unique SKU or Item Number for each Individual Item.
- **FR-004:** The system MUST prevent duplicate SKU or Item Numbers.
- **FR-005:** The system MUST maintain a description for each Individual Item.
- **FR-006:** The system MUST maintain the selling price of each Individual Item.
- **FR-007:** The system MUST maintain the number of individual units contained in a case for each Individual Item.
- **FR-008:** The system MUST support one or more UPC barcodes associated with an Individual Item.
- **FR-009:** The system MUST prevent the same UPC from being assigned to different Individual Items.
- **FR-010:** The system MUST support associating an Individual Item with multiple Suppliers.
- **FR-011:** The system MUST maintain the purchasing price for each Supplier and Individual Item relationship.
- **FR-012:** The system MUST maintain minimum and maximum stock levels for each Individual Item.
- **FR-013:** The system MUST require the minimum stock level to be less than or equal to the maximum stock level.
- **FR-014:** The system MUST support determining when an item requires replenishment based on its minimum and maximum stock levels.
- **FR-015:** The system MUST consider inventory quantity and quantities already on supplier order when evaluating replenishment needs.
- **FR-016:** The system MUST require a nonempty SKU or Item Number and item description.
- **FR-017:** The system MUST reject negative selling prices and negative supplier purchasing prices.
- **FR-018:** The system MUST require the quantity per case to be a positive integer.
- **FR-019:** The system MUST reject negative minimum or maximum stock levels.
- **FR-020:** The system MUST validate item information before saving.
- **FR-021:** The system MUST reject invalid item information without changing existing records.
- **FR-022:** The system MUST allow authorized Inventory Clerks and Managers to edit existing item information.
- **FR-023:** The system MUST preserve the Item ID when item information is updated.
- **FR-024:** The system MUST support identifying an item by its SKU or Item Number.
- **FR-025:** The system MUST support identifying an item by a registered UPC barcode.
- **FR-026:** The system MUST support marking an item as active or inactive.
- **FR-027:** The system MUST prevent inactive items from being selected for new supplier orders or customer orders.
- **FR-028:** The system MUST preserve inactive items for historical reporting and existing transaction records.
- **FR-029:** The system MUST allow authorized Managers and Administrators to delete an item only when no inventory records, supplier orders, customer orders, or other historical transactions reference it.
- **FR-030:** The system MUST reject deletion when an item is referenced by inventory or transaction history.
- **FR-031:** The system MUST preserve item information when deletion is rejected.
- **FR-032:** The system MUST reject attempts to edit or delete an item that does not exist.
- **FR-033:** The system MUST restrict item creation and modification to authorized office personnel, including Inventory Clerks and Managers.
- **FR-034:** Warehouse workers, receivers, pickers, and drivers MUST NOT modify Individual Item master information.
- **FR-035:** Authorized warehouse workers and drivers MUST be able to view item information needed for their assigned operations without changing it.
- **FR-036:** The system MUST maintain item master information separately from inventory quantities and transaction quantities.
- **FR-037:** The system MUST maintain relationships between Individual Items, Suppliers, UPCs, and Inventory records.

---

## Key Entities

### Individual Item

Represents a product that the company purchases from suppliers, stores in warehouses, and sells to customers.

Each item has a unique identifier, SKU or Item Number, description, selling price, quantity per case, stock levels, and active status.

### UPC

Represents a barcode associated with an Individual Item.

An item may have multiple UPCs, including different identifiers used during warehouse operations.

### Supplier

Represents a business that supplies products to the company.

Supplier master information is maintained in Feature 5.

### Supplier Item

Represents the purchasing relationship between a Supplier and an Individual Item.

This relationship stores the supplier-specific purchasing price.

### Inventory

Represents the quantity of an Individual Item stored in a Warehouse Location.

Inventory quantities are maintained in Feature 3.

### User

Represents an authenticated employee whose role determines whether item information can be maintained.

---

## Initial Data Model

### Individual Item

| Attribute | Type | Description |
|---|---|---|
| itemId | Integer | Unique, system-generated identifier; primary key |
| itemNumber | String | Unique SKU or Item Number; required |
| description | String | Item description; required |
| sellingPrice | Decimal | Selling price per individual unit |
| unitsPerCase | Integer | Number of individual units in one case |
| minimumStock | Integer | Minimum desired stock level |
| maximumStock | Integer | Maximum desired stock level |
| isActive | Boolean | Indicates whether the item is active |

**Relationships:**
- One Individual Item can have multiple UPC records.
- One Individual Item can be associated with multiple Suppliers through Supplier Item records.
- One Individual Item can have multiple Inventory records in different Warehouse Locations.
- One Individual Item can appear on supplier and customer order lines.

**Constraints:**
- itemId must be unique and cannot be changed.
- itemNumber must be unique and nonempty.
- description must be nonempty.
- sellingPrice cannot be negative.
- unitsPerCase must be greater than zero.
- minimumStock and maximumStock cannot be negative.
- minimumStock cannot exceed maximumStock.

### UPC

| Attribute | Type | Description |
|---|---|---|
| upcId | Integer | Unique UPC record identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| upcCode | String | Barcode value associated with the item |
| barcodeType | String | Identifies the barcode's packaging level, such as individual unit or case |

**Relationships:**
- Each UPC belongs to one Individual Item.
- One Individual Item can have multiple UPC records.

**Constraints:**
- A UPC code cannot be assigned to different Individual Items.
- A UPC code must not be empty.

### Supplier

| Attribute | Type | Description |
|---|---|---|
| supplierId | Integer | Unique Supplier identifier |

**Relationships:**
- A Supplier can provide multiple Individual Items.
- Supplier information is maintained in Feature 5.

### Supplier Item

| Attribute | Type | Description |
|---|---|---|
| supplierItemId | Integer | Unique Supplier Item relationship identifier |
| supplierId | Integer | Foreign key referencing Supplier |
| itemId | Integer | Foreign key referencing Individual Item |
| purchasePricePerCase | Decimal | Supplier's purchasing price per case |

**Relationships:**
- Each Supplier Item record references one Supplier and one Individual Item.
- An Individual Item can have multiple Supplier Item records.
- A Supplier can have multiple Supplier Item records.

**Constraints:**
- The combination of supplierId and itemId must be unique.
- purchasePricePerCase cannot be negative.

### Inventory

| Attribute | Type | Description |
|---|---|---|
| inventoryId | Integer | Unique Inventory record identifier |
| itemId | Integer | Foreign key referencing Individual Item |
| locationId | Integer | Foreign key referencing Warehouse Location |
| quantity | Integer | Quantity stored in individual units |

**Relationships:**
- One Individual Item can have Inventory in multiple locations.
- Inventory management is defined in Feature 3.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- User roles determine who can create, update, or delete Individual Item records.

---

## Gherkin AC

### US-4.1: Add an Individual Item

#### AC-4.1.1: Successfully create Individual Item

**Given** the user is authenticated as an Inventory Clerk or Manager  
**When** the user enters a unique Item Number, a nonempty description, a valid selling price, a positive quantity per case, and valid stock levels  
**And** saves the item  
**Then** the system creates the Individual Item  
**And** assigns a unique Item ID  
**And** stores the item information.

#### AC-4.1.2: Reject duplicate Item Number

**Given** an Individual Item exists with Item Number "ITEM001"  
**And** the user is authorized to maintain items  
**When** the user attempts to create another item with Item Number "ITEM001"  
**Then** the system rejects the request  
**And** the existing item remains unchanged.

#### AC-4.1.3: Reject missing required information

**Given** the user is authorized to maintain items  
**When** the user attempts to create an item with an empty description  
**Then** the system rejects the request  
**And** no new item is created.

#### AC-4.1.4: Reject invalid selling price

**Given** the user is authorized to maintain items  
**When** the user attempts to create an item with a selling price of -5.00  
**Then** the system rejects the request  
**And** no new item is created.

#### AC-4.1.5: Reject invalid quantity per case

**Given** the user is authorized to maintain items  
**When** the user attempts to create an item with zero units per case  
**Then** the system rejects the request  
**And** no new item is created.

#### AC-4.1.6: Reject invalid stock levels

**Given** the user is authorized to maintain items  
**When** the user attempts to create an item with a minimum stock level of 100 and a maximum stock level of 50  
**Then** the system rejects the request  
**And** no new item is created.

#### AC-4.1.7: Reject unauthorized item creation

**Given** the user is authenticated as a Warehouse Worker  
**When** the user attempts to create an Individual Item  
**Then** the system denies the operation  
**And** no item is created.

### US-4.2: Edit an Individual Item

#### AC-4.2.1: Successfully update item information

**Given** an Individual Item exists  
**And** the user is authenticated as a Manager  
**When** the user updates the item's description and selling price with valid values  
**And** saves the changes  
**Then** the system stores the updated information  
**And** the Item ID remains unchanged.

#### AC-4.2.2: Reject duplicate Item Number during update

**Given** Item A has Item Number "ITEM001"  
**And** Item B has Item Number "ITEM002"  
**And** the user is authorized to maintain items  
**When** the user changes Item B's Item Number to "ITEM001"  
**Then** the system rejects the update  
**And** both original Item Numbers remain unchanged.

#### AC-4.2.3: Reject invalid item update

**Given** an Individual Item exists with a valid selling price  
**And** the user is authorized to maintain items  
**When** the user changes its selling price to a negative value  
**Then** the system rejects the update  
**And** the previously stored selling price remains unchanged.

#### AC-4.2.4: Reject unauthorized item modification

**Given** an Individual Item exists  
**And** the user is authenticated as a Picker  
**When** the user attempts to modify the item's description  
**Then** the system denies the request  
**And** the item remains unchanged.

#### AC-4.2.5: Reject editing nonexistent Item

**Given** no Individual Item exists with the requested Item ID  
**And** the user is authenticated as a Manager  
**When** the user attempts to update that item  
**Then** the system rejects the request  
**And** no item is changed.

### US-4.3: Delete or Deactivate an Individual Item

#### AC-4.3.1: Successfully delete unused Item

**Given** an Individual Item exists  
**And** no Inventory records or historical transactions reference it  
**And** the user is authenticated as an Administrator  
**When** the user requests item deletion  
**Then** the system deletes the Individual Item  
**And** the item is no longer available in the item catalog.

#### AC-4.3.2: Prevent deletion when Inventory exists

**Given** an Individual Item has Inventory records  
**And** the user is authenticated as a Manager  
**When** the user requests item deletion  
**Then** the system rejects the deletion  
**And** the Individual Item and its Inventory remain unchanged.

#### AC-4.3.3: Prevent deletion when order history exists

**Given** an Individual Item is referenced by a Supplier Order or Customer Order  
**And** the user is authenticated as an Administrator  
**When** the user requests item deletion  
**Then** the system rejects the deletion  
**And** the Item and its order history remain unchanged.

#### AC-4.3.4: Deactivate discontinued Item

**Given** an active Individual Item exists  
**And** the user is authenticated as a Manager  
**When** the user marks the item as inactive  
**Then** the system saves the inactive status  
**And** the item remains available for historical reporting  
**And** the item cannot be selected for new orders.

#### AC-4.3.5: Reject unauthorized item deletion

**Given** an Individual Item exists  
**And** the user is authenticated as a Driver  
**When** the user attempts to delete the item  
**Then** the system denies the operation  
**And** the item remains unchanged.

#### AC-4.3.6: Reject deletion of nonexistent Item

**Given** no Individual Item exists with the requested Item ID  
**And** the user is authenticated as an Administrator  
**When** the user requests deletion of that item  
**Then** the system rejects the request  
**And** no item is changed.

### US-4.4: Maintain Item UPCs

#### AC-4.4.1: Add UPC to Item

**Given** an Individual Item exists  
**And** the user is authenticated as an Inventory Clerk  
**When** the user adds a new UPC code to the item  
**Then** the system associates the UPC with the item  
**And** the UPC can be used to identify that item.

#### AC-4.4.2: Reject duplicate UPC assigned to another Item

**Given** UPC "012345678905" is associated with Item A  
**And** the user is authorized to maintain items  
**When** the user attempts to assign the same UPC to Item B  
**Then** the system rejects the request  
**And** the UPC remains associated with Item A.

#### AC-4.4.3: Identify Item using UPC

**Given** an active Individual Item has a registered UPC  
**When** an authorized Warehouse Worker scans the UPC  
**Then** the system identifies the corresponding Individual Item  
**And** displays the item's information needed for the operation.

### US-4.5: Maintain Item Supplier Relationships

#### AC-4.5.1: Associate Item with Supplier

**Given** an Individual Item exists  
**And** an active Supplier exists  
**And** the user is authenticated as a Manager  
**When** the user associates the Supplier with the Item and enters a valid purchase price per case  
**Then** the system saves the Supplier Item relationship  
**And** the Supplier becomes available as a purchasing source for the Item.

#### AC-4.5.2: Associate Item with multiple Suppliers

**Given** an Individual Item exists  
**And** two active Suppliers exist  
**And** the user is authorized to maintain items  
**When** the user associates both Suppliers with the Item using their respective purchasing prices  
**Then** the system stores both Supplier Item relationships  
**And** each Supplier retains its own purchasing price.

#### AC-4.5.3: Reject nonexistent Supplier

**Given** an Individual Item exists  
**And** the requested Supplier does not exist  
**When** an authorized user attempts to associate the Supplier with the Item  
**Then** the system rejects the request  
**And** no Supplier Item relationship is created.

#### AC-4.5.4: Reject negative Supplier purchase price

**Given** an Individual Item and Supplier exist  
**When** an authorized user attempts to assign a purchase price per case of -10.00  
**Then** the system rejects the request  
**And** no invalid Supplier Item relationship is saved.
