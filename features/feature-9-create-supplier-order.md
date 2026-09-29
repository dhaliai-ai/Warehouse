# Feature: Create Supplier Order

**Feature ID:** 9  
**Branch pattern:** `feature/9-create-supplier-order`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system assists in creating a Supplier Order by identifying inventory that needs replenishment, calculating the quantity needed based on minimum and maximum inventory levels, and recording the order so it can later be identified and received.

---

## User Stories

### US-9.1: Identify Items Needing Replenishment

**As a** warehouse employee  
**I want to** identify items whose Quantity on Hand is below the minimum level  
**So that** inventory can be replenished before it runs out

**Priority:** P1  
**Independent test:** Confirm that an item below its minimum inventory level is identified as needing replenishment.

### US-9.2: Determine Quantity to Order

**As a** warehouse employee  
**I want to** determine how much inventory should be ordered  
**So that** the item's quantity can be brought toward its maximum inventory level

**Priority:** P1  
**Independent test:** Use the item's Inventory Quantity, quantity already on order, minimum, and maximum to determine the quantity needed.

### US-9.3: Create Supplier Order

**As a** warehouse employee  
**I want to** create a Supplier Order for the required items  
**So that** the products can be ordered from the Supplier

**Priority:** P1  
**Independent test:** Create a Supplier Order and confirm that the Supplier, items, and Quantity Ordered are recorded.

---

## Functional Requirements

- **FR-001:** The system MUST maintain a minimum and maximum inventory level used for replenishment.
- **FR-002:** The system MUST determine Quantity on Hand using Inventory Quantity plus Quantity already on order.
- **FR-003:** The system MUST identify when Quantity on Hand is below the minimum inventory level.
- **FR-004:** The system MUST determine the quantity needed to bring inventory toward the maximum inventory level.
- **FR-005:** The system MUST allow a Supplier Order to be created for items requiring replenishment.
- **FR-006:** The Supplier Order MUST be associated with a Supplier.
- **FR-007:** The system MUST record the items included in the Supplier Order.
- **FR-008:** The system MUST record Quantity Ordered for each item.
- **FR-009:** Quantity Ordered MUST remain separate from Quantity Received.
- **FR-010:** The system MUST preserve the Supplier Order so it can later be identified during the receiving process.
- **FR-011:** The Supplier Order MUST have an identifier that can be used when the order is later received.
- **FR-012:** The Supplier Order MUST have a status.
- **FR-013:** The exact Supplier Order status values are **TBD**.
- **FR-014:** Which Supplier Order statuses count toward quantity already on order is **TBD**.
- **FR-015:** The exact process used to electronically send the Supplier Order to the Supplier is **TBD**.
- **FR-016:** Behavior when an item requiring replenishment has no associated Supplier is **TBD**.
- **FR-017:** Behavior when minimum or maximum inventory information is missing or invalid is **TBD**.

---

## Key Entities

- **Supplier Order:** An order placed with a Supplier for items requiring replenishment.
- **Supplier Order Item:** An Individual Item included in a Supplier Order with its Quantity Ordered and Quantity Received.
- **Individual Item:** A product that may require replenishment.
- **Inventory:** The quantity of an Individual Item stored in a Warehouse Location.
- **Supplier:** The Supplier from whom products are ordered.

---

## Initial Data Model

### Supplier Order

Represents an order placed with a Supplier.

**Attributes:**
- PO Number / Order Identifier
- Status [exact values TBD]

**Relationships:**
- A Supplier Order is associated with a Supplier.
- A Supplier Order contains one or more Supplier Order Items.
- A Supplier Order is later used by the Receive Supplier Order process.

### Supplier Order Item

Represents an Individual Item included in a Supplier Order.

**Attributes:**
- Individual Item
- Quantity Ordered
- Quantity Received

**Relationships:**
- A Supplier Order contains one or more Supplier Order Items.
- Each Supplier Order Item refers to an Individual Item.
- Quantity Ordered remains separate from Quantity Received.

### Individual Item

Represents a product that may need replenishment.

**Relevant Attributes:**
- SKU / Item Number
- Description
- Minimum Inventory Level
- Maximum Inventory Level

**Relationships:**
- An Individual Item may be associated with a Supplier.
- An Individual Item may appear on multiple Supplier Orders.
- An Individual Item may exist as Inventory in one or more Warehouse Locations.

### Inventory

Represents an Individual Item quantity in a Warehouse Location.

**Relevant Attributes:**
- Individual Item
- Warehouse Location
- Quantity

**Relationships:**
- Inventory contributes to the current Inventory Quantity used when determining Quantity on Hand.

### Supplier

Represents the Supplier from whom products are ordered.

**Relationships:**
- A Supplier may supply Individual Items.
- A Supplier may have multiple Supplier Orders.

---

## Gherkin AC

### US-9.1: Identify Items Needing Replenishment

#### AC-9.1.1: Quantity on Hand is calculated

**Given** an Individual Item has Inventory Quantity and quantity already on order  
**When** the system determines Quantity on Hand  
**Then** the system uses Inventory Quantity plus quantity already on order

#### AC-9.1.2: Item is below minimum

**Given** an Individual Item has a defined minimum inventory level  
**When** Quantity on Hand is below the minimum  
**Then** the system identifies the item as needing replenishment

#### AC-9.1.3: Item is not below minimum

**Given** an Individual Item has a defined minimum inventory level  
**When** Quantity on Hand is equal to or greater than the minimum  
**Then** the item does not meet the minimum-level condition for replenishment

### US-9.2: Determine Quantity to Order

#### AC-9.2.1: Replenishment quantity is determined

**Given** Quantity on Hand is below the minimum inventory level  
**And** the item has a maximum inventory level  
**When** the system determines the replenishment quantity  
**Then** the quantity is calculated to bring inventory toward the maximum level

#### AC-9.2.2: Existing orders are considered

**Given** some quantity of the item is already on order  
**When** the system determines whether additional inventory is needed  
**Then** the quantity already on order is included in Quantity on Hand

### US-9.3: Create Supplier Order

#### AC-9.3.1: Supplier Order is created

**Given** one or more items require replenishment  
**When** the warehouse employee creates a Supplier Order  
**Then** the system records the Supplier  
**And** records the items and Quantity Ordered

#### AC-9.3.2: Ordered and Received quantities remain separate

**Given** a Supplier Order has been created  
**When** the order is later processed  
**Then** Quantity Ordered remains separate from Quantity Received

#### AC-9.3.3: Supplier Order is available for receiving

**Given** a Supplier Order has been created and preserved in the system  
**When** its shipment later arrives  
**Then** the Supplier Order can be identified for the receiving process

#### AC-9.3.4: Item has no Supplier

**Given** an item requires replenishment  
**When** no Supplier is associated with the item  
**Then** [TBD: behavior not specified in the interview or class notes]