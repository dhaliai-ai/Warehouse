
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

## Assumptions

- **A-001:** Customer Service Clerks and Managers maintain Customer master records; Managers and Administrators may delete eligible records.
- **A-002:** Customer IDs are generated by the system; Customer Numbers are unique company-wide.
- **A-003:** Business and Delivery Addresses are separate; a Delivery Address is required for Customers receiving deliveries.
- **A-004:** A Customer has zero or one default Delivery Route; one route may serve multiple Customers.
- **A-005:** Delivery Routes exist before assignment. Feature 15 manages route planning and actual deliveries.
- **A-006:** Feature 12 owns Customer Orders; Feature 15 owns Delivery records.
- **A-007:** Deactivation blocks new Customer Orders but preserves existing orders and delivery history.
- **A-008:** Authorized warehouse personnel and drivers may read only the Customer details needed for assigned work.
- **A-009:** The system enforces permissions on the server, not only by hiding screen controls.
- **A-010:** Existing orders and deliveries retain their historical records when Customer master details change; how delivery addresses are snapshotted needs confirmation.

---

## Edge Cases

- **EC-001:** Duplicate Customer Number on create or update, including simultaneous requests.
- **EC-002:** Missing or whitespace-only Customer Number or Name.
- **EC-003:** Missing Delivery Address for a Customer receiving deliveries.
- **EC-004:** Invalid optional Email Address.
- **EC-005:** Editing or deleting a nonexistent Customer.
- **EC-006:** Warehouse Worker, Picker, Receiver, or Driver attempts unauthorized modification.
- **EC-007:** Assigning a nonexistent Delivery Route; previous assignment must remain unchanged.
- **EC-008:** Reassigning a Customer between existing routes or leaving the default route unassigned.
- **EC-009:** Deleting a Customer with Orders, Delivery records, other history, or an active route assignment.
- **EC-010:** Deactivating a Customer with existing orders or deliveries.
- **EC-011:** Selecting an inactive Customer for a new Order.
- **EC-012:** Updating the delivery address while a Delivery is in progress.
- **EC-013:** Driver requests information for a Delivery not assigned to them.
- **EC-014:** Concurrent creation of an Order or Delivery reference during Customer deletion.
- **EC-015:** Invalid updates must leave all previously stored fields unchanged.

---

## Success Criteria

- **SC-001:** Authorized personnel can create and edit Customers with validated required fields.
- **SC-002:** Customer IDs remain stable and Customer Numbers remain unique.
- **SC-003:** Customers can be found by Customer Number or Name.
- **SC-004:** Existing Delivery Routes can be assigned and reassigned; nonexistent routes are rejected.
- **SC-005:** Customer Orders, Deliveries, and route references remain consistent.
- **SC-006:** Inactive Customers are excluded from new Orders but remain in historical reports.
- **SC-007:** Customers with protected dependencies cannot be deleted; eligible Customers can be deleted by authorized roles.
- **SC-008:** Warehouse personnel and Drivers have operation-specific read access, not master-data edit access.
- **SC-009:** Invalid or unauthorized requests do not change stored records.
- **SC-010:** All 21 original Gherkin acceptance scenarios are covered by verification tests.

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

---

## Data Ownership

| Data | Owning feature | Feature 6 responsibility |
|---|---|---|
| Customer master (ID, Number, Name, addresses, contacts, status) | Feature 6 | Create, validate, update, deactivate, delete when eligible |
| Customer default Delivery Route assignment (`deliveryRouteId`) | Feature 6 | Assign an existing route; validate reference |
| Delivery Route definitions and delivery planning | Feature 15 | Read available routes; never create routes here |
| Customer Orders | Feature 12 | Provide Customer reference and active status; do not edit Orders |
| Deliveries and delivery confirmation | Feature 15 | Provide Customer delivery details; do not edit Delivery history |
| User authentication and roles | Shared authorization service | Enforce permissions on every operation |

**Integrity rules:** Customer Numbers must be unique; Customer Orders and Deliveries must reference existing Customers. Deletion is blocked by historical references or an active route assignment. Existing transactions must not be silently rewritten when Customer master information changes. Database constraints and transactional checks must protect against concurrent requests.

---

## API Requirements

**Proposed contracts:** Endpoint names and status codes must be reconciled with the project's established API conventions before implementation.

| ID | Method and endpoint | Purpose | Allowed roles |
|---|---|---|---|
| API-6.1 | `GET /api/customers?customerNumber=&name=&isActive=` | Search/list Customers | Authorized viewers |
| API-6.2 | `GET /api/customers/{customerId}` | View Customer details | Authorized viewers |
| API-6.3 | `POST /api/customers` | Create Customer | Customer Service Clerk, Manager |
| API-6.4 | `PUT /api/customers/{customerId}` | Update Customer master data | Customer Service Clerk, Manager |
| API-6.5 | `PATCH /api/customers/{customerId}/status` | Activate/deactivate Customer | Manager, Administrator (proposed; confirm) |
| API-6.6 | `DELETE /api/customers/{customerId}` | Delete unused Customer | Manager, Administrator |
| API-6.7 | `PUT /api/customers/{customerId}/delivery-route` | Assign/change default Delivery Route | Customer Service Clerk, Manager |
| API-6.8 | `GET /api/delivery-routes` | Select an existing route (owned by Feature 15) | Authorized viewers |

### Request and Response Data

**Create/Update Customer example:**

```json
{
  "customerNumber": "CUS001",
  "name": "North Store",
  "businessAddress": "100 Market Street",
  "deliveryAddress": "200 Receiving Road",
  "phone": "555-0100",
  "email": "store@example.com",
  "contactPerson": "Receiving Manager",
  "deliveryRouteId": 12,
  "isActive": true
}
```

The server generates `customerId` on creation. An update retains the existing `customerId`. A route assignment request may use `{"deliveryRouteId":12}`; the route must exist.

### Validation and Errors

- Require nonempty `customerNumber` and `name` (after trimming whitespace).
- Require nonempty `deliveryAddress` when the Customer receives deliveries.
- Validate `email` format when supplied; prevent duplicate `customerNumber`.
- Reject nonexistent Customers and Delivery Routes; preserve prior route assignment on failure.
- Block deletion when Customer Orders, Deliveries, historical transactions, or an active route assignment exist.
- Reject unauthorized modifications and inactive Customer selection when creating new Orders (enforced by Feature 12).
- Use `201 Created` for creation, `200 OK` for reads/updates, `204 No Content` for deletion; `400` for invalid input, `401` for unauthenticated, `403` for forbidden, `404` for missing records, and `409` for uniqueness/dependency conflicts.
- Validate and enforce permissions on the backend; use atomic writes and database constraints to avoid partial updates and concurrency errors.

**Traceability:** FR-001–FR-037; AC-6.1.1–AC-6.4.4. Feature 12 enforces the new-order restriction; Feature 15 owns delivery execution and route definitions.

---

## Screen Requirements
### UI Design

![Warehouse Dashboard](../../docs/ui/WMS/Warehouse%20Dashboard.png)
**Design status:** Proposed screen specifications; screen images are deliverables, not yet claimed as created.

| Screen | Proposed image | Main content and actions |
|---|---|---|
| UI-6A Customer List | `docs/UI/customer-list.png` | Search by Number/Name; active filter; View, Add, Edit, Delete according to role |
| UI-6B Add Customer | `docs/UI/customer-add.png` | Number, Name, Business/Delivery Addresses, Phone, Email, Contact Person, default Route, Active status; Save/Cancel |
| UI-6C Edit Customer | `docs/UI/customer-edit.png` | Same editable fields; read-only Customer ID; Save/Cancel; validation errors |
| UI-6D Customer Details | `docs/UI/customer-details.png` | Read-only contact, delivery, status, route, and linked record summary |
| UI-6E Delivery Information | `docs/UI/customer-delivery.png` | Delivery Address, Contact Person, existing Route selector; Save/Cancel for authorized office roles |
| UI-6F Delete/Deactivate Confirmation | `docs/UI/customer-status.png` | Dependency warnings, deactivate option, confirmation; never bypass backend rules |

**UI rules:** Display required-field and email validation clearly. Show an error when the route does not exist, the Customer Number is duplicated, or deletion is blocked by history/route assignment. Drivers and assigned warehouse personnel see only the delivery details necessary for their tasks and cannot edit Customer master information. Inactive Customers remain visible for authorized historical lookup but are unavailable for new Customer Orders. Screen image paths must be adjusted to match the repository's actual layout.

---

## Definition of Done

### Design Draft

- [ ] All 14 required OC Speckit sections appear in order.
- [ ] All 4 original User Stories and 37 original Functional Requirements are retained.
- [ ] The original Initial Data Model and all 21 Gherkin scenarios are retained.
- [ ] Data ownership agrees with Features 12 and 15.
- [ ] API endpoints, validation, permissions, and error behavior are reviewed.
- [ ] Screen designs are created and linked using actual repository paths.
- [ ] Relevant C4 architecture diagrams, NFRs, and ADRs are updated or referenced as required by the assignment.
- [ ] Pending business-rule clarifications are recorded for approval.
- [ ] Draft is saved, committed, and pushed on the intended design branch.

### Implementation and Verification (not implied complete by the draft)

- [ ] Customer CRUD and active-status restrictions work for authorized roles.
- [ ] Uniqueness, required fields, email, and route-reference validation work.
- [ ] Protected Customer deletion and historical references are enforced.
- [ ] Warehouse and Driver access is read-only and limited to assigned operations.
- [ ] All 21 original acceptance scenarios pass.
- [ ] Concurrent writes do not bypass uniqueness or referential integrity.

---

## Out of Scope

- Creating or editing Customer Orders (Feature 12).
- Creating Delivery Route definitions or optimizing routes (Feature 15).
- Shipping, transportation, delivery confirmation, or editing historical Deliveries (Feature 15).
- Warehouse receiving, picking, putaway, and inventory adjustments.
- Maintaining Supplier or Individual Item master records.
- Managing user accounts, passwords, or role definitions.
- Billing, payment processing, credit limits, or customer loyalty programs.
- Automatically rewriting existing Orders or completed Deliveries after Customer master updates.
- Deleting Customers with protected historical references or active route assignments.

### Pending Clarifications

- **CL-6.1:** Must a Delivery Address be required at Customer creation, or only when deliveries are enabled?
- **CL-6.2:** Who may deactivate/reactivate Customers: only Managers/Administrators or also Customer Service Clerks?
- **CL-6.3:** Are Customer addresses stored as one string or structured street/city/state/postal fields?
- **CL-6.4:** Should an in-progress Delivery retain the original delivery address after Customer master information changes?
- **CL-6.5:** Can a Customer with no active route assignment be eligible for delivery, and how is that handled?
