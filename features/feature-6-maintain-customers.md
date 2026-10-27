
# Feature: Maintain Customers

**Feature ID:** 6  
**Branch pattern:** `feature/6-maintain-customers`  
**Status:** Draft - Proposed Rules Pending Approval  
**Created:** 2026-09-28  
**Input:** The Warehouse Management System maintains information about store customers who order products from the company. Authorized office personnel can add, update, delete, or deactivate customer records. Customer information supports order processing, shipping, delivery planning, and delivery confirmation. The system preserves customer relationships and historical transaction records.

---

## User Stories

### US-6.1: Add a Customer

**As a** Customer Service Clerk or Manager  
**I want to** add a customer with identifying, contact, and delivery information  
**So that** the company can receive orders and deliver products to that customer.

**Priority:** P1  
**Independent test:** Create a customer with a unique Customer Number and valid required information, then verify that the record is saved.

### US-6.2: Edit a Customer

**As a** Customer Service Clerk or Manager  
**I want to** update customer contact and delivery information  
**So that** customer orders and deliveries use accurate information.

**Priority:** P1  
**Independent test:** Update an existing customer's phone number or delivery address and verify that the changes are saved.

### US-6.3: Delete or Deactivate a Customer

**As a** Manager or Administrator  
**I want to** delete an unused customer or deactivate a customer that no longer places orders  
**So that** obsolete customer records are not used for new transactions while historical orders and deliveries remain available.

**Priority:** P1  
**Independent test:** Verify that an unused customer can be deleted, while a customer associated with orders or delivery history is protected from deletion and can be deactivated.

### US-6.4: Maintain Customer Delivery Information

**As a** Customer Service Clerk or Manager  
**I want to** maintain a customer's delivery address and route assignment  
**So that** warehouse personnel can prepare shipments and organize customer deliveries.

**Priority:** P1  
**Independent test:** Assign a customer to an existing delivery route and verify that the customer's delivery information and route assignment are saved.

---

## Functional Requirements

- **FR-001:** The system MUST allow authorized Customer Service Clerks and Managers to create Customer records.
- **FR-002:** The system MUST assign a unique, system-generated Customer ID to each Customer.
- **FR-003:** The system MUST maintain a unique Customer Number used internally by the company.
- **FR-004:** The system MUST prevent duplicate Customer Numbers.
- **FR-005:** The system MUST maintain the Customer Name.
- **FR-006:** The system MUST maintain the Customer Business Address.
- **FR-007:** The system MUST maintain the Customer Delivery Address.
- **FR-008:** The system MUST maintain the Customer Phone Number.
- **FR-009:** The system MUST maintain the Customer Email Address.
- **FR-010:** The system MUST support recording a Customer Contact Person.
- **FR-011:** The system MUST require a nonempty Customer Number and Customer Name.
- **FR-012:** The system MUST require a nonempty Delivery Address for a Customer receiving deliveries.
- **FR-013:** The system MUST validate the format of a Customer Email Address when one is provided.
- **FR-014:** The system MUST validate Customer information before saving.
- **FR-015:** The system MUST reject invalid Customer information without changing existing records.
- **FR-016:** The system MUST allow authorized Customer Service Clerks and Managers to update existing Customer information.
- **FR-017:** The system MUST preserve the Customer ID when Customer information is updated.
- **FR-018:** The system MUST support searching for Customers by Customer Number or Customer Name.
- **FR-019:** The system MUST support associating a Customer with multiple Customer Orders.
- **FR-020:** Each Customer Order MUST reference the Customer who placed the order.
- **FR-021:** The system MUST support assigning Customers to Delivery Routes.
- **FR-022:** A Delivery Route MUST support multiple Customers.
- **FR-023:** The system MUST allow an authorized user to update a Customer's assigned Delivery Route.
- **FR-024:** The system MUST reject assignment to a Delivery Route that does not exist.
- **FR-025:** The system MUST maintain Customer information needed for shipping and delivery operations.
- **FR-026:** The system MUST support marking a Customer as active or inactive.
- **FR-027:** The system MUST prevent inactive Customers from being selected for new Customer Orders.
- **FR-028:** The system MUST preserve inactive Customer records for historical order and delivery reporting.
- **FR-029:** The system MUST allow authorized Managers and Administrators to delete a Customer only when no Customer Orders, delivery records, or other historical transactions reference the Customer and no active Delivery Route assignment remains.
- **FR-030:** The system MUST reject deletion when a Customer is referenced by Customer Orders, delivery history, or an active Delivery Route assignment.
- **FR-031:** The system MUST preserve Customer information when deletion is rejected.
- **FR-032:** The system MUST reject attempts to edit or delete a Customer that does not exist.
- **FR-033:** The system MUST restrict Customer creation and modification to authorized office personnel, including Customer Service Clerks and Managers.
- **FR-034:** Warehouse workers, receivers, pickers, and drivers MUST NOT modify Customer master information.
- **FR-035:** Authorized warehouse workers and drivers MUST be able to view Customer information needed for their assigned shipping or delivery operations.
- **FR-036:** The system MUST maintain Customer master information separately from Customer Orders, shipments, and deliveries.
- **FR-037:** The system MUST preserve relationships between Customers, Customer Orders, and Delivery Routes.

---

## Key Entities

### Customer

Represents a store or business that orders products from the warehouse company.

Each Customer has identifying information, contact details, delivery information, and an active status.

### Customer Order

Represents an order placed by a Customer for products supplied by the warehouse company.

Customer Order processing is defined in Feature 12.

### Delivery Route

Represents an organized route used to deliver shipments to Customers.

A Delivery Route can contain multiple Customers.

### Delivery

Represents the transportation and delivery of shipped products to a Customer.

Delivery processing and confirmation are defined in Feature 15.

### User

Represents an authenticated employee whose role determines whether Customer information can be maintained.

---

## Initial Data Model

### Customer

| Attribute | Type | Description |
|---|---|---|
| customerId | Integer | Unique, system-generated identifier; primary key |
| customerNumber | String | Unique internal Customer Number |
| name | String | Customer business or store name |
| businessAddress | String | Customer business address |
| deliveryAddress | String | Address where products are delivered |
| phone | String | Customer contact telephone number |
| email | String | Customer contact email address |
| contactPerson | String | Customer's primary contact person |
| deliveryRouteId | Integer | Optional foreign key referencing Delivery Route |
| isActive | Boolean | Indicates whether the Customer is active |

**Relationships:**
- One Customer can have multiple Customer Orders.
- A Customer can be assigned to a Delivery Route.
- A Customer can receive multiple Deliveries.
- Customer information is maintained independently of order and delivery history.

**Constraints:**
- customerId must be unique and cannot be changed.
- customerNumber must be unique and nonempty.
- name must be nonempty.
- deliveryAddress must be provided for Customers receiving deliveries.
- email must have a valid email format when provided.
- deliveryRouteId must reference an existing Delivery Route when assigned.
- A Customer referenced by historical transactions cannot be deleted.

### Customer Order

| Attribute | Type | Description |
|---|---|---|
| customerOrderId | Integer | Unique Customer Order identifier |
| customerId | Integer | Foreign key referencing Customer |

**Relationships:**
- Each Customer Order belongs to one Customer.
- One Customer can have multiple Customer Orders.
- Customer Order details are defined in Feature 12.

### Delivery Route

| Attribute | Type | Description |
|---|---|---|
| deliveryRouteId | Integer | Unique Delivery Route identifier |
| routeName | String | Name or identifier of the delivery route |

**Relationships:**
- One Delivery Route can be assigned to multiple Customers.
- Each Customer has zero or one default Delivery Route.
- Delivery route planning and execution are handled in Feature 15.

### Delivery

| Attribute | Type | Description |
|---|---|---|
| deliveryId | Integer | Unique Delivery identifier |
| customerId | Integer | Foreign key referencing Customer |
| deliveryRouteId | Integer | Foreign key referencing Delivery Route |

**Relationships:**
- Each Delivery is associated with a Customer.
- A Delivery may be assigned to a Delivery Route.
- Delivery details are defined in Feature 15.

### User

| Attribute | Type | Description |
|---|---|---|
| userId | Integer | Unique User identifier |
| role | String | Assigned authorization role |

**Relationships:**
- User roles determine who may create, update, deactivate, or delete Customer records.

---

## Gherkin AC

### US-6.1: Add a Customer

#### AC-6.1.1: Successfully create Customer

**Given** the user is authenticated as a Customer Service Clerk or Manager  
**When** the user enters a unique Customer Number, nonempty Customer Name, valid Delivery Address, and valid Customer information  
**And** saves the record  
**Then** the system creates the Customer  
**And** assigns a unique Customer ID  
**And** stores the Customer information.

#### AC-6.1.2: Reject duplicate Customer Number

**Given** a Customer exists with Customer Number "CUS001"  
**And** the user is authorized to maintain Customers  
**When** the user attempts to create another Customer with Customer Number "CUS001"  
**Then** the system rejects the request  
**And** the existing Customer remains unchanged.

#### AC-6.1.3: Reject missing Customer Name

**Given** the user is authorized to maintain Customers  
**When** the user attempts to create a Customer with an empty Name  
**Then** the system rejects the request  
**And** no Customer record is created.

#### AC-6.1.4: Reject missing Delivery Address

**Given** the user is creating a Customer that receives deliveries  
**When** the user submits the Customer without a Delivery Address  
**Then** the system rejects the request  
**And** no Customer record is created.

#### AC-6.1.5: Reject invalid Email Address

**Given** the user is authorized to maintain Customers  
**When** the user enters an invalid Email Address  
**And** attempts to save the Customer  
**Then** the system rejects the request  
**And** no Customer record is created.

#### AC-6.1.6: Reject unauthorized Customer creation

**Given** the user is authenticated as a Warehouse Worker  
**When** the user attempts to create a Customer  
**Then** the system denies the request  
**And** no Customer record is created.

### US-6.2: Edit a Customer

#### AC-6.2.1: Successfully update Customer

**Given** a Customer record exists  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user updates the Customer's Phone Number and Delivery Address with valid information  
**And** saves the changes  
**Then** the system stores the updated information  
**And** the Customer ID remains unchanged.

#### AC-6.2.2: Reject invalid Customer update

**Given** a Customer record exists  
**And** the user is authenticated as a Manager  
**When** the user removes the required Customer Name  
**And** attempts to save the changes  
**Then** the system rejects the update  
**And** the previously stored Customer information remains unchanged.

#### AC-6.2.3: Reject duplicate Customer Number during update

**Given** Customer A has Customer Number "CUS001"  
**And** Customer B has Customer Number "CUS002"  
**And** the user is authorized to maintain Customers  
**When** the user changes Customer B's Number to "CUS001"  
**Then** the system rejects the update  
**And** both original Customer Numbers remain unchanged.

#### AC-6.2.4: Reject unauthorized Customer modification

**Given** a Customer record exists  
**And** the user is authenticated as a Picker  
**When** the user attempts to modify Customer information  
**Then** the system denies the request  
**And** the Customer remains unchanged.

#### AC-6.2.5: Reject editing nonexistent Customer

**Given** no Customer exists with the requested Customer ID  
**And** the user is authenticated as a Manager  
**When** the user attempts to update that Customer  
**Then** the system rejects the request  
**And** no Customer record is changed.

### US-6.3: Delete or Deactivate a Customer

#### AC-6.3.1: Successfully delete unused Customer

**Given** a Customer exists  
**And** no Customer Orders, delivery records, or historical transactions reference it  
**And** no active Delivery Route assignment remains  
**And** the user is authenticated as an Administrator  
**When** the user requests Customer deletion  
**Then** the system deletes the Customer record  
**And** the Customer is no longer available in the Customer directory.

#### AC-6.3.2: Prevent deletion when Customer Orders exist

**Given** a Customer is referenced by one or more Customer Orders  
**And** the user is authenticated as a Manager  
**When** the user requests Customer deletion  
**Then** the system rejects the deletion  
**And** the Customer and its order history remain unchanged.

#### AC-6.3.3: Prevent deletion when Delivery history exists

**Given** a Customer is referenced by completed Delivery records  
**And** the user is authenticated as an Administrator  
**When** the user requests Customer deletion  
**Then** the system rejects the deletion  
**And** the Customer and its Delivery history remain unchanged.

#### AC-6.3.4: Deactivate Customer

**Given** an active Customer exists  
**And** the user is authenticated as a Manager  
**When** the user marks the Customer as inactive  
**Then** the system saves the inactive status  
**And** the Customer remains available for historical reporting  
**And** the Customer cannot be selected for new Customer Orders.

#### AC-6.3.5: Reject unauthorized Customer deletion

**Given** a Customer record exists  
**And** the user is authenticated as a Driver  
**When** the user attempts to delete the Customer  
**Then** the system denies the operation  
**And** the Customer remains unchanged.

#### AC-6.3.6: Reject deletion of nonexistent Customer

**Given** no Customer exists with the requested Customer ID  
**And** the user is authenticated as an Administrator  
**When** the user requests deletion of that Customer  
**Then** the system rejects the request  
**And** no Customer record is changed.

### US-6.4: Maintain Customer Delivery Information

#### AC-6.4.1: Assign Customer to Delivery Route

**Given** an active Customer exists  
**And** a Delivery Route exists  
**And** the user is authenticated as a Customer Service Clerk  
**When** the user assigns the Customer to the Delivery Route  
**Then** the system saves the route assignment  
**And** the Customer is associated with the selected Delivery Route.

#### AC-6.4.2: Change Customer Delivery Route

**Given** a Customer is assigned to Delivery Route A  
**And** Delivery Route B exists  
**And** the user is authenticated as a Manager  
**When** the user changes the Customer's default route to Delivery Route B  
**Then** the system updates the Customer's route assignment  
**And** the Customer is no longer assigned to Route A as its default route.

#### AC-6.4.3: Reject nonexistent Delivery Route

**Given** a Customer exists  
**And** the requested Delivery Route does not exist  
**When** an authorized user attempts to assign the Customer to that route  
**Then** the system rejects the assignment  
**And** the Customer's previous route assignment remains unchanged.

#### AC-6.4.4: Display Customer Delivery Information

**Given** an active Customer has a Delivery Address and an assigned Delivery Route  
**And** a Driver is authorized to view an assigned Delivery  
**When** the Driver views the Delivery details  
**Then** the system displays the Customer's delivery information needed for that Delivery  
**And** the Driver cannot modify the Customer master record.
