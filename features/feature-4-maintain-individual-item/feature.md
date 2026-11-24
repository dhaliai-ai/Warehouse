
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

## Assumptions

- **A-001:** The company maintains a central Individual Item catalog used by its Warehouses.
- **A-002:** Every Individual Item has a unique, system-generated Item ID.
- **A-003:** Item Numbers or SKUs are unique across the company.
- **A-004:** Every Item has a nonempty Item Number and description.
- **A-005:** Selling prices are recorded per individual unit, as specified in the Initial Data Model.
- **A-006:** Supplier purchasing prices are recorded per case, as specified in the Supplier Item data model.
- **A-007:** Every Item has a positive integer quantity of units per case.
- **A-008:** An Item may have multiple registered UPCs, but a UPC cannot identify different Items.
- **A-009:** An Item may be purchased from multiple existing Suppliers.
- **A-010:** Supplier master records are maintained through Feature 5.
- **A-011:** Inventory balances are maintained through Feature 3 and are not edited through Item maintenance.
- **A-012:** Minimum and maximum stock levels are maintained for each Item.
- **A-013:** Replenishment evaluation uses stored Inventory quantities and quantities already on Supplier Orders.
- **A-014:** Only authorized office personnel, including Inventory Clerks and Managers, can create or modify Item master information.
- **A-015:** Managers and Administrators can delete Items only when no Inventory or historical transaction dependencies exist.
- **A-016:** Discontinued Items can be deactivated instead of deleted so historical references remain available.
- **A-017:** Inactive Items cannot be selected for new Supplier Orders or Customer Orders.
- **A-018:** Warehouse Workers, Receivers, Pickers, and Drivers can access relevant Item information only according to their assigned permissions.
- **A-019:** The system uses shared authentication and authorization functionality to identify Users and enforce roles.
- **A-020:** Item maintenance does not directly change stored Inventory quantities.
- **A-021:** Barcode scanning or manual UPC lookup can identify an Item through its registered UPC.
- **A-022:** Existing Supplier Orders and Customer Orders retain valid historical Item references even if an Item becomes inactive.

---

## Edge Cases

- **EC-001:** A User attempts to create an Item using an Item Number already assigned to another Item.
- **EC-002:** An Item Number or description is missing or contains only whitespace.
- **EC-003:** A User enters a negative selling price.
- **EC-004:** A User enters zero, a negative number, or a noninteger value for units per case.
- **EC-005:** A User enters a negative minimum or maximum stock level.
- **EC-006:** The minimum stock level exceeds the maximum stock level.
- **EC-007:** A User attempts to change an existing Item Number to another Item's number.
- **EC-008:** A User attempts to update or delete an Item that does not exist.
- **EC-009:** A Warehouse Worker, Receiver, Picker, or Driver attempts to modify Item master data.
- **EC-010:** A User attempts to assign a UPC already registered to another Item.
- **EC-011:** A User enters an empty UPC code.
- **EC-012:** A User scans a UPC that is not registered to any Item.
- **EC-013:** A User attempts to associate an Item with a Supplier that does not exist.
- **EC-014:** A User attempts to associate an Item with a Supplier using a negative purchasing price.
- **EC-015:** A User attempts to create a duplicate Supplier Item relationship.
- **EC-016:** An Item has multiple Suppliers with different purchasing prices.
- **EC-017:** A User attempts to delete an Item that has Inventory records.
- **EC-018:** A User attempts to delete an Item referenced by Supplier Orders, Customer Orders, or historical transactions.
- **EC-019:** A discontinued Item is deactivated while historical orders still reference it.
- **EC-020:** A User attempts to select an inactive Item for a new Supplier Order or Customer Order.
- **EC-021:** An Item's stock quantity is below its minimum level, but additional units are already on Supplier Order.
- **EC-022:** An Item's stored Inventory is sufficient, so replenishment is not required.
- **EC-023:** An authorized User updates an Item's description or price while preserving its original Item ID.
- **EC-024:** Two Users attempt to create Items with the same Item Number at nearly the same time.
- **EC-025:** Two Users attempt to assign the same UPC to different Items concurrently.
- **EC-026:** A User attempts to delete an Item while another transaction is creating an Inventory or order reference.
- **EC-027:** A Supplier relationship is changed while existing Supplier Orders reference the Item.
- **EC-028:** An Item is inactive but still needs to be displayed in historical reports.

---

## Success Criteria

- **SC-001:** Authorized Inventory Clerks and Managers can create Items with valid required information.
- **SC-002:** Every Item receives a unique, system-generated Item ID.
- **SC-003:** Duplicate Item Numbers are rejected during creation and update.
- **SC-004:** Missing descriptions and invalid prices, quantities per case, or stock levels are rejected.
- **SC-005:** Authorized Item updates preserve the original Item ID.
- **SC-006:** Items can be identified by their Item Number or registered UPC.
- **SC-007:** A UPC cannot be assigned to two different Items.
- **SC-008:** An Item can be associated with multiple Suppliers, each with its own purchasing price.
- **SC-009:** Supplier relationships referencing nonexistent Suppliers are rejected.
- **SC-010:** Replenishment evaluation considers stock levels, Inventory quantities, and quantities already on Supplier Order.
- **SC-011:** Inactive Items remain available for historical reporting but cannot be selected for new orders.
- **SC-012:** Items with Inventory or historical transaction references cannot be deleted.
- **SC-013:** Unused Items without dependencies can be deleted by authorized Managers or Administrators.
- **SC-014:** Warehouse Workers, Receivers, Pickers, and Drivers cannot modify Item master data.
- **SC-015:** Authorized operational Users can view the Item information required for their work.
- **SC-016:** Item master maintenance does not directly change Inventory balances.
- **SC-017:** Concurrent requests cannot create duplicate Item Numbers or conflicting UPC assignments.
- **SC-018:** All 25 original Gherkin acceptance scenarios pass their corresponding verification tests.
- **SC-019:** Item information remains consistent with Supplier, UPC, Inventory, and order references.
- **SC-020:** The Item maintenance screens enforce the same validation and permissions as the backend.

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

---

## Data Ownership

### Individual Item Master Data

**Owner:** Feature 4 — Maintain Individual Item.

Feature 4 owns the Individual Item master records used throughout the Warehouse Management System.

Feature 4 is responsible for:
- Creating Individual Item records.
- Generating unique Item IDs.
- Maintaining unique SKU or Item Numbers.
- Maintaining Item descriptions.
- Maintaining selling prices.
- Maintaining units per case.
- Maintaining minimum and maximum stock levels.
- Maintaining active and inactive status.
- Validating Item information before saving.
- Preventing unauthorized modifications.
- Preventing deletion when historical dependencies exist.

Other features may reference Individual Items but must not directly modify Item master data.

### UPC Data

**Owner:** Feature 4 — Maintain Individual Item.

Feature 4 owns UPC records and their relationships with Individual Items.

Feature 4 is responsible for:
- Associating UPCs with Items.
- Maintaining UPC barcode values.
- Identifying the packaging level associated with each barcode.
- Preventing duplicate UPC assignments across different Items.
- Supporting Item identification through barcode lookup.

Receiving, Put Away, picking, and other warehouse workflows may read UPC information but must not change UPC master records.

### Supplier Master Data

**Owner:** Feature 5 — Maintain Supplier.

Feature 5 owns Supplier master information.

Feature 4 uses existing Supplier records when associating Suppliers with Individual Items.

Feature 4 must not create, modify, or delete Supplier master records.

### Supplier Item Relationship Data

**Owner:** Feature 4 — Maintain Individual Item.

Feature 4 maintains the relationship between an Individual Item and its Suppliers.

The Supplier Item relationship contains:
- Supplier Item ID.
- Supplier ID.
- Item ID.
- Purchasing price per case.

The system must:
- Require an existing Supplier.
- Require an existing Individual Item.
- Prevent duplicate Supplier and Item relationships.
- Reject negative purchasing prices.
- Support multiple Suppliers for one Item.

Supplier Order workflows may read these relationships when selecting purchasing sources.

### Inventory Data

**Owner:** Feature 3 — Maintain Inventory.

Feature 3 owns Inventory balances and stock transaction history.

Feature 4 may read Inventory information when:
- Evaluating replenishment requirements.
- Checking whether an Item can be deleted.
- Displaying related Inventory information.

Feature 4 must not directly modify stored Inventory quantities.

### Supplier Order Data

**Owner:** Create Supplier Order functionality.

Supplier Order workflows reference Individual Items and Supplier Item relationships.

Feature 4 provides Item master information needed for purchasing.

Feature 4 must not directly change Supplier Order quantities or transaction records.

### Customer Order Data

**Owner:** Customer Order functionality.

Customer Order workflows reference Individual Items.

Feature 4 provides Item descriptions, identification information, selling prices, and active status.

Inactive Items must not be selected for new customer orders.

Historical orders must retain valid Item references.

### User and Authorization Data

**Owner:** Shared authentication and authorization functionality.

Feature 4 uses User roles to enforce access permissions.

**Inventory Clerks and Managers:**
- Create Individual Items.
- Edit Individual Item information.
- Maintain UPC relationships.
- Maintain Supplier Item relationships.

**Managers and Administrators:**
- Delete eligible unused Individual Items.

**Warehouse Workers, Receivers, Pickers, and Drivers:**
- View relevant Item information when authorized.
- Cannot modify Item master information.

### Data Consistency Rules

- Every Individual Item must have a unique Item ID.
- Every Item Number must be unique.
- Every UPC must identify only one Individual Item.
- Every Supplier Item relationship must reference valid Item and Supplier records.
- A Supplier and Item combination must not be duplicated.
- Item updates must preserve the original Item ID.
- Item master maintenance must not directly change Inventory balances.
- Inactive Items must remain available for historical reporting.
- Items referenced by Inventory or historical transactions must not be deleted.
- Concurrent requests must not bypass uniqueness or dependency checks.

---

## API Requirements

**Design status:** Proposed API contracts for Feature 4.

The endpoint names, request structures, and response codes below are proposed design decisions. They must follow the Warehouse project's established API conventions before implementation.

**Base resource:** `/api/items`

### API-4.1: List and Search Individual Items

**Method:** GET  
**Endpoint:** `/api/items`

**Purpose:** Retrieve Individual Item information.

**Authorization:** Authenticated Users with Item viewing permission.

**Proposed query parameters:**
- `itemNumber`
- `description`
- `isActive`

**Successful response:** `200 OK`

**Example response:**

    [
      {
        "itemId": 101,
        "itemNumber": "ITEM001",
        "description": "Bottled Water",
        "sellingPrice": 1.50,
        "unitsPerCase": 24,
        "minimumStock": 100,
        "maximumStock": 500,
        "isActive": true
      }
    ]

**Rules:**
- Users may search by Item Number or description.
- Authorized Users may view active and inactive Items.
- Operational Users receive read-only access.
- Viewing Item information must not modify Item records.

**Traceability:** FR-024, FR-026, FR-028, FR-035.

### API-4.2: Create Individual Item

**Method:** POST  
**Endpoint:** `/api/items`

**Purpose:** Create a new Individual Item.

**Authorization:** Inventory Clerk or Manager.

**Example request:**

    {
      "itemNumber": "ITEM001",
      "description": "Bottled Water",
      "sellingPrice": 1.50,
      "unitsPerCase": 24,
      "minimumStock": 100,
      "maximumStock": 500,
      "isActive": true
    }

**Successful response:** `201 Created`

**Validation:**
- Item Number must be nonempty.
- Item Number must be unique.
- Description must be nonempty.
- Selling price cannot be negative.
- Units per case must be a positive integer.
- Minimum and maximum stock levels cannot be negative.
- Minimum stock cannot exceed maximum stock.
- Item ID must be generated by the system.
- The request must not create or modify Inventory balances.

**Error responses:**
- `400 Bad Request` for invalid information.
- `401 Unauthorized` for missing authentication.
- `403 Forbidden` for insufficient permissions.
- `409 Conflict` for a duplicate Item Number.

**Traceability:** US-4.1; FR-001 through FR-007, FR-012, FR-013, FR-016 through FR-021, FR-033, FR-034; AC-4.1.1 through AC-4.1.7.

### API-4.3: Get Individual Item Details

**Method:** GET  
**Endpoint:** `/api/items/{itemId}`

**Purpose:** Retrieve an existing Individual Item by its ID.

**Authorization:** Authenticated Users with Item viewing permission.

**Successful response:** `200 OK`

**Displayed information:**
- Item ID.
- Item Number.
- Description.
- Selling price.
- Units per case.
- Minimum stock.
- Maximum stock.
- Active status.

**Error responses:**
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found` if the Item does not exist.

**Traceability:** FR-002 through FR-007, FR-012, FR-024, FR-026, FR-035.

### API-4.4: Update Individual Item

**Method:** PUT  
**Endpoint:** `/api/items/{itemId}`

**Purpose:** Update Item master information.

**Authorization:** Inventory Clerk or Manager.

**Example request:**

    {
      "itemNumber": "ITEM001",
      "description": "Bottled Drinking Water",
      "sellingPrice": 1.75,
      "unitsPerCase": 24,
      "minimumStock": 100,
      "maximumStock": 500,
      "isActive": true
    }

**Successful response:** `200 OK`

**Validation:**
- Item must exist.
- Item ID must remain unchanged.
- Item Number must remain unique.
- Description must be nonempty.
- Selling price must be nonnegative.
- Units per case must be positive.
- Stock levels must be nonnegative.
- Minimum stock must not exceed maximum stock.
- Unauthorized Users must be rejected.
- Invalid changes must not overwrite existing valid information.

**Error responses:**
- `400 Bad Request`.
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.
- `409 Conflict` for duplicate Item Numbers.

**Traceability:** US-4.2; FR-016 through FR-023, FR-032 through FR-034; AC-4.2.1 through AC-4.2.5.

### API-4.5: Deactivate or Reactivate Individual Item

**Method:** PATCH  
**Endpoint:** `/api/items/{itemId}/status`

**Purpose:** Change an Item's active status.

**Authorization:** Authorized Inventory Clerk or Manager, subject to approved status-change permissions.

**Example request:**

    {
      "isActive": false
    }

**Successful response:** `200 OK`

**Rules:**
- Item must exist.
- Inactive Items remain available for historical reporting.
- Inactive Items cannot be selected for new Supplier Orders or Customer Orders.
- Existing historical transactions must remain unchanged.
- The status change must not delete Inventory records.

**Error responses:**
- `400 Bad Request`.
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.

**Traceability:** US-4.3; FR-026 through FR-028; AC-4.3.4.

### API-4.6: Delete Individual Item

**Method:** DELETE  
**Endpoint:** `/api/items/{itemId}`

**Purpose:** Delete an unused Individual Item.

**Authorization:** Manager or Administrator.

**Successful response:** `204 No Content`

**Validation:**
- Item must exist.
- No Inventory record may reference the Item.
- No Supplier Order may reference the Item.
- No Customer Order may reference the Item.
- No other retained historical transaction may reference the Item.
- Concurrent transactions must not create references while deletion is being completed.
- Rejected deletion must preserve all existing Item information.

**Error responses:**
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.
- `409 Conflict` when dependencies prevent deletion.

**Traceability:** US-4.3; FR-029 through FR-032; AC-4.3.1 through AC-4.3.3, AC-4.3.5, AC-4.3.6.

### API-4.7: Add UPC to Individual Item

**Method:** POST  
**Endpoint:** `/api/items/{itemId}/upcs`

**Purpose:** Associate a UPC barcode with an existing Item.

**Authorization:** Inventory Clerk or Manager.

**Example request:**

    {
      "upcCode": "012345678905",
      "barcodeType": "Each"
    }

**Successful response:** `201 Created`

**Validation:**
- Item must exist.
- UPC must not be empty.
- UPC must not already identify another Item.
- UPC relationship must be saved consistently.
- Unauthorized Users must be rejected.

**Error responses:**
- `400 Bad Request`.
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.
- `409 Conflict` for conflicting UPC assignments.

**Traceability:** US-4.4; FR-008, FR-009, FR-025; AC-4.4.1, AC-4.4.2.

### API-4.8: Find Individual Item by UPC

**Method:** GET  
**Endpoint:** `/api/items/by-upc/{upcCode}`

**Purpose:** Identify an Item using a registered UPC barcode.

**Authorization:** Authenticated Users with Item viewing permission.

**Successful response:** `200 OK`

**Example response:**

    {
      "itemId": 101,
      "itemNumber": "ITEM001",
      "description": "Bottled Water",
      "upcCode": "012345678905",
      "barcodeType": "Each",
      "isActive": true
    }

**Rules:**
- UPC lookup must identify the correct Item.
- The result must not permit unauthorized editing.
- Inactive Items may remain identifiable for authorized historical or operational purposes.
- Order-creation workflows must separately enforce active status.

**Error responses:**
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found` for an unknown UPC.

**Traceability:** FR-008, FR-009, FR-025, FR-035; AC-4.4.3.

### API-4.9: Associate Item with Supplier

**Method:** POST  
**Endpoint:** `/api/items/{itemId}/suppliers`

**Purpose:** Create a Supplier Item purchasing relationship.

**Authorization:** Inventory Clerk or Manager.

**Example request:**

    {
      "supplierId": 201,
      "purchasePricePerCase": 18.00
    }

**Successful response:** `201 Created`

**Validation:**
- Item must exist.
- Supplier must exist.
- Supplier and Item relationship must not already exist.
- Purchase price per case cannot be negative.
- Supplier-specific pricing must be preserved.
- Multiple Suppliers may be associated with one Item.

**Error responses:**
- `400 Bad Request`.
- `401 Unauthorized`.
- `403 Forbidden`.
- `404 Not Found`.
- `409 Conflict` for a duplicate Supplier Item relationship.

**Traceability:** US-4.5; FR-010, FR-011, FR-017, FR-037; AC-4.5.1 through AC-4.5.4.

### API-4.10: View Item Supplier Relationships

**Method:** GET  
**Endpoint:** `/api/items/{itemId}/suppliers`

**Purpose:** Retrieve the Suppliers associated with an Item.

**Authorization:** Authenticated Users with the appropriate viewing permission.

**Successful response:** `200 OK`

**Example response:**

    [
      {
        "supplierItemId": 301,
        "supplierId": 201,
        "purchasePricePerCase": 18.00
      },
      {
        "supplierItemId": 302,
        "supplierId": 202,
        "purchasePricePerCase": 17.50
      }
    ]

**Rules:**
- Return the Supplier Item relationships for the requested Item.
- Preserve supplier-specific purchasing prices.
- Do not modify Supplier master data.

**Traceability:** FR-010, FR-011, FR-037; US-4.5.

### API-4.11: Evaluate Replenishment Need

**Method:** GET  
**Endpoint:** `/api/items/{itemId}/replenishment`

**Purpose:** Determine whether an Item requires replenishment.

**Authorization:** Authorized office personnel.

**Successful response:** `200 OK`

**Proposed response information:**
- Item ID.
- Minimum stock level.
- Maximum stock level.
- Current Inventory quantity.
- Quantity already on Supplier Order.
- Replenishment indicator.
- Suggested replenishment quantity, if the calculation is approved.

**Rules:**
- Use the Item's minimum and maximum stock levels.
- Consider Inventory quantities from Feature 3.
- Consider quantities already on Supplier Order.
- Do not automatically create a Supplier Order.
- Do not directly modify Inventory quantities.

**Pending clarification:** Confirm whether stock levels and replenishment calculations apply company-wide or separately to each Warehouse. Confirm which outstanding Supplier Order statuses contribute to the on-order quantity.

**Traceability:** FR-012 through FR-015.

### Shared API Design Rules

- The backend must enforce authentication and authorization.
- Item IDs must be generated by the system.
- Item Numbers must be unique.
- UPC codes must not identify different Items.
- Supplier Item relationships must not be duplicated.
- Monetary values must use an appropriate fixed-precision decimal representation.
- Invalid requests must not partially update Item records.
- Item deletion must preserve referential integrity.
- Inactive Items must remain available for historical reporting.
- Item master operations must not directly modify Inventory balances.
- Concurrent requests must respect database uniqueness constraints.
- API contracts must follow the existing Warehouse backend conventions.

---

## Screen Requirements
### UI Design

![Receiving Scan Screen](../../docs/ui/Handheld/Receiving%20Scan.png)
**Design status:** Proposed user-interface screens for Feature 4.

Screen images must be created and linked to the feature documentation.

### Screen UI-4A: Individual Item List

**Proposed image:** `docs/UI/item-list.png`

**Purpose:** Allow Users to search, view, and select Individual Items.

**Displayed information:**
- Item Number.
- Description.
- Selling price.
- Units per case.
- Minimum stock level.
- Maximum stock level.
- Active status.

**Actions:**
- Search by Item Number.
- Search by description.
- Filter active and inactive Items.
- View Item details.
- Add Item, if authorized.
- Edit Item, if authorized.
- Delete Item, if authorized.

**Rules:**
- Warehouse Workers, Receivers, Pickers, and Drivers must not have Item editing permissions.
- Unauthorized maintenance actions must be unavailable.
- Backend permissions must still be enforced.
- Inactive Items must be distinguishable from active Items.

### Screen UI-4B: Add Individual Item

**Proposed image:** `docs/UI/item-add.png`

**Purpose:** Create a new Individual Item.

**Fields:**

| Field | Control | Required |
|---|---|---|
| Item Number | Text input | Yes |
| Description | Text input | Yes |
| Selling Price | Decimal input | Yes |
| Units Per Case | Integer input | Yes |
| Minimum Stock | Integer input | Yes |
| Maximum Stock | Integer input | Yes |
| Active Status | Checkbox or selection | Yes |

**Actions:**
- Save.
- Cancel.

**Rules:**
- Item Number must be unique.
- Item Number and description cannot be empty.
- Selling price cannot be negative.
- Units per case must be greater than zero.
- Stock levels cannot be negative.
- Minimum stock cannot exceed maximum stock.
- Item ID is generated automatically.
- Only authorized Inventory Clerks and Managers can save a new Item.

### Screen UI-4C: Edit Individual Item

**Proposed image:** `docs/UI/item-edit.png`

**Purpose:** Modify an existing Individual Item.

**Fields:**
- Item ID (read-only).
- Item Number.
- Description.
- Selling price.
- Units per case.
- Minimum stock.
- Maximum stock.
- Active status.

**Actions:**
- Save Changes.
- Cancel.
- Open UPC Maintenance.
- Open Supplier Relationships.

**Rules:**
- Item ID must not change.
- Item Number uniqueness must be enforced.
- Invalid changes must not overwrite existing information.
- Only authorized office personnel may modify Item master data.
- Changing Item information must not directly change Inventory quantities.

### Screen UI-4D: Maintain Item UPCs

**Proposed image:** `docs/UI/item-upcs.png`

**Purpose:** Manage the UPC barcodes associated with an Individual Item.

**Displayed information:**
- Item Number.
- Item description.
- Existing UPC codes.
- Barcode type or packaging level.

**Fields:**
- UPC code.
- Barcode type.

**Actions:**
- Add UPC.
- View UPCs.
- Return to Item.

**Rules:**
- UPC codes cannot be empty.
- The same UPC cannot identify different Items.
- A valid UPC must identify the associated Item during scanning.
- Only authorized Inventory Clerks and Managers may maintain UPC information.

### Screen UI-4E: Maintain Item Suppliers

**Proposed image:** `docs/UI/item-suppliers.png`

**Purpose:** Associate an Individual Item with one or more Suppliers.

**Displayed information:**
- Item Number.
- Item description.
- Supplier.
- Purchase price per case.

**Fields:**
- Supplier selection.
- Purchase price per case.

**Actions:**
- Add Supplier Relationship.
- View Supplier Relationships.
- Return to Item.

**Rules:**
- Supplier must exist.
- Duplicate Supplier and Item relationships are not allowed.
- Purchase price cannot be negative.
- Different Suppliers may have different purchasing prices.
- Supplier master records are maintained through Feature 5.

### Screen UI-4F: Item Details

**Proposed image:** `docs/UI/item-details.png`

**Purpose:** Display Item information needed by authorized Users.

**Displayed information:**
- Item ID.
- Item Number.
- Description.
- Selling price, when permitted.
- Units per case.
- Registered UPCs.
- Active status.
- Relevant Supplier information, when permitted.

**Rules:**
- Operational Users have read-only access.
- The screen must not permit unauthorized modifications.
- Inactive Items may remain visible for historical or authorized operational purposes.

### Screen UI-4G: Replenishment Information

**Proposed image:** `docs/UI/item-replenishment.png`

**Purpose:** Display information used to determine whether an Item requires replenishment.

**Displayed information:**
- Item Number.
- Description.
- Minimum stock level.
- Maximum stock level.
- Current Inventory quantity.
- Quantity on Supplier Order.
- Replenishment indicator.

**Rules:**
- Inventory quantities come from Feature 3.
- Supplier Order quantities come from the Supplier Order workflow.
- The screen must not directly change Inventory balances.
- The screen must not automatically create Supplier Orders.

**Pending clarification:** Confirm whether replenishment is calculated for each Warehouse or across all Warehouses.

### Proposed Role Permissions

| Role | View Items | Add Items | Edit Items | Maintain UPCs | Maintain Supplier Relationships | Delete Items |
|---|---|---|---|---|---|---|
| Inventory Clerk | Yes | Yes | Yes | Yes | Yes | No |
| Manager | Yes | Yes | Yes | Yes | Yes | Yes, if eligible |
| Administrator | According to permissions | According to permissions | According to permissions | According to permissions | According to permissions | Yes, if eligible |
| Warehouse Worker | Read-only | No | No | No | No | No |
| Receiver | Read-only | No | No | No | No | No |
| Picker | Read-only | No | No | No | No | No |
| Driver | Read-only, if authorized | No | No | No | No | No |

### Validation and Feedback

The interface must provide understandable messages for:
- Duplicate Item Number.
- Missing required Item information.
- Negative selling price.
- Invalid units per case.
- Negative stock levels.
- Minimum stock exceeding maximum stock.
- Duplicate UPC assignment.
- Missing Supplier.
- Negative Supplier purchasing price.
- Duplicate Supplier Item relationship.
- Unauthorized Item maintenance.
- Item not found.
- Item deletion blocked by Inventory.
- Item deletion blocked by historical transactions.
- Successful Item creation or update.
- Successful Item deactivation.
- Successful UPC or Supplier association.

### UI Design Deliverables

Create and link these screen images:

- `docs/UI/item-list.png`
- `docs/UI/item-add.png`
- `docs/UI/item-edit.png`
- `docs/UI/item-upcs.png`
- `docs/UI/item-suppliers.png`
- `docs/UI/item-details.png`
- `docs/UI/item-replenishment.png`

These paths are proposed and must match the final repository documentation structure.

---

## Definition of Done

### Requirements and Design

- [ ] All five User Stories are documented.
- [ ] All thirty-seven Functional Requirements are retained.
- [ ] Assumptions are documented.
- [ ] Edge Cases are documented.
- [ ] Success Criteria are documented.
- [ ] Key Entities are identified.
- [ ] Initial Data Model is documented.
- [ ] All twenty-five original Gherkin acceptance scenarios are retained.
- [ ] Data Ownership is documented.
- [ ] API Requirements are documented.
- [ ] Screen Requirements are documented.
- [ ] Out-of-Scope functionality is identified.
- [ ] Outstanding clarifications are reviewed.

### Item Master Management

- [ ] Authorized Inventory Clerks and Managers can create Items.
- [ ] Every Item receives a unique, system-generated Item ID.
- [ ] Item Numbers are unique.
- [ ] Required Item information is validated.
- [ ] Negative selling prices are rejected.
- [ ] Units per case must be positive integers.
- [ ] Minimum and maximum stock levels are nonnegative.
- [ ] Minimum stock cannot exceed maximum stock.
- [ ] Authorized Users can update Item information.
- [ ] Item updates preserve the original Item ID.
- [ ] Invalid updates do not overwrite valid information.
- [ ] Item master maintenance does not directly modify Inventory balances.

### UPC Management

- [ ] An Item can have multiple UPC records.
- [ ] UPC codes cannot be empty.
- [ ] The same UPC cannot identify different Items.
- [ ] UPC lookup identifies the correct Item.
- [ ] Unauthorized Users cannot maintain UPC records.
- [ ] Concurrent UPC assignments cannot create conflicting relationships.

### Supplier Relationships

- [ ] An Item can be associated with multiple Suppliers.
- [ ] Supplier Item relationships reference existing Suppliers.
- [ ] Supplier Item relationships reference existing Items.
- [ ] Duplicate Supplier and Item relationships are prevented.
- [ ] Negative purchasing prices are rejected.
- [ ] Supplier-specific purchasing prices are preserved.
- [ ] Supplier master data remains owned by Feature 5.

### Item Status and Deletion

- [ ] Authorized Users can deactivate Items.
- [ ] Inactive Items cannot be selected for new Supplier Orders.
- [ ] Inactive Items cannot be selected for new Customer Orders.
- [ ] Inactive Items remain available for historical reporting.
- [ ] Items with Inventory records cannot be deleted.
- [ ] Items with historical transaction references cannot be deleted.
- [ ] Authorized Managers and Administrators can delete eligible unused Items.
- [ ] Unauthorized deletion attempts are rejected.
- [ ] Failed deletion does not change Item information.

### Authorization and Security

- [ ] Inventory Clerks and Managers can maintain Item information.
- [ ] Warehouse Workers cannot modify Item master data.
- [ ] Receivers cannot modify Item master data.
- [ ] Pickers cannot modify Item master data.
- [ ] Drivers cannot modify Item master data.
- [ ] Authorized operational Users can view relevant Item information.
- [ ] Backend authorization is enforced independently of UI controls.

### Replenishment

- [ ] Minimum and maximum stock levels are available for replenishment evaluation.
- [ ] Inventory quantities from Feature 3 are considered.
- [ ] Quantities already on Supplier Order are considered.
- [ ] Replenishment calculations do not directly change Inventory.
- [ ] Replenishment evaluation does not automatically create Supplier Orders.
- [ ] Warehouse-level versus company-level replenishment rules are clarified.

### Acceptance Testing

- [ ] AC-4.1.1 through AC-4.1.7 pass.
- [ ] AC-4.2.1 through AC-4.2.5 pass.
- [ ] AC-4.3.1 through AC-4.3.6 pass.
- [ ] AC-4.4.1 through AC-4.4.3 pass.
- [ ] AC-4.5.1 through AC-4.5.4 pass.
- [ ] Tests cover invalid Item information.
- [ ] Tests cover duplicate Item Numbers.
- [ ] Tests cover duplicate UPC assignments.
- [ ] Tests cover Supplier relationship validation.
- [ ] Tests cover inactive Item restrictions.
- [ ] Tests cover deletion with historical dependencies.
- [ ] Tests cover unauthorized operations.
- [ ] Tests cover concurrent uniqueness conflicts.

### Documentation and Review

- [ ] Feature 4 follows the required OC Speckit section structure.
- [ ] Relevant architecture decisions are documented in `docs/ADRs/`.
- [ ] Relevant non-functional requirements are addressed in `docs/NFR/`.
- [ ] Item master data and related components are represented in the C4 diagrams.
- [ ] Individual Item List screen image is created.
- [ ] Add Individual Item screen image is created.
- [ ] Edit Individual Item screen image is created.
- [ ] UPC Maintenance screen image is created.
- [ ] Supplier Relationships screen image is created.
- [ ] Item Details screen image is created.
- [ ] Replenishment screen image is created.
- [ ] Screen images are linked to Feature 4.
- [ ] Changes are committed to the `design-draft` branch.
- [ ] Changes are pushed to GitHub.

**Draft note:** These checkboxes identify required completion work. They do not indicate that implementation, testing, or screen-image creation has already occurred.

---

## Out of Scope

Feature 4 does not include:

- Creating or maintaining Company records.
- Creating or maintaining Warehouse master records.
- Creating or maintaining Supplier master records.
- Creating or maintaining Warehouse Locations.
- Maintaining physical Inventory balances.
- Recording Inventory counts, adjustments, or movements.
- Creating or receiving Supplier Orders.
- Confirming Putaway Movements.
- Performing warehouse picking or shipping.
- Creating or processing Customer Orders.
- Maintaining User accounts, passwords, or roles.
- Changing Inventory quantities directly through Item maintenance.
- Automatically creating Supplier Orders based on replenishment calculations.
- Deleting Items that have Inventory or historical transaction dependencies.
- Removing historical Item information when an Item is deactivated.
- Allowing Warehouse Workers, Receivers, Pickers, or Drivers to modify Item master data.
- Maintaining Supplier purchasing information outside the defined Supplier Item relationships.
- Managing advanced demand forecasting or financial inventory valuation.

### Pending Clarifications

- **CL-4.1:** Confirm whether minimum and maximum stock levels apply company-wide or separately to each Warehouse.
- **CL-4.2:** Confirm which outstanding Supplier Order statuses and quantities are included in replenishment calculations.
- **CL-4.3:** Confirm whether additional UPC barcode types or packaging conversion rules are required beyond the proposed Item and case barcode types.
- **CL-4.4:** Confirm whether selling price changes require an effective date or whether only the current selling price is maintained.
- **CL-4.5:** Confirm whether deactivated Items may still be processed in already-existing orders.

These decisions must be coordinated with Features 3 and 5 and the relevant Supplier Order, Receiving, Picking, and Customer Order workflows.
