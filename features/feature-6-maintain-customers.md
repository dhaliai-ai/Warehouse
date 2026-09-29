# Feature: Maintain Customers

**Feature ID:** 6  
**Branch pattern:** `feature/6-maintain-customers`  
**Status:** Draft  
**Created:** 2026-09-28  
**Input:** The system maintains information about customers who order products from the warehouse.

---

## User Stories

### US-6.1: Add a Customer

**As a** [TBD: authorized role not specified]  
**I want to** add a customer  
**So that** the warehouse can keep information about customers who order products

**Priority:** P1  
**Independent test:** Add a customer with valid information and confirm it is saved.

### US-6.2: Edit a Customer

**As a** [TBD: authorized role not specified]  
**I want to** edit a customer  
**So that** the customer's information stays accurate

**Priority:** P1  
**Independent test:** Change an existing customer's information and confirm the changes are saved.

### US-6.3: Delete a Customer

**As a** [TBD: authorized role not specified]  
**I want to** delete a customer  
**So that** a customer record that should no longer be kept can be removed

**Priority:** P1  
**Independent test:** Delete an existing customer and confirm it is no longer kept.

---

## Functional Requirements

- **FR-001:** The system MUST allow a Customer to be added.
- **FR-002:** The system MUST allow an existing Customer to be edited.
- **FR-003:** The system MUST allow an existing Customer to be deleted.
- **FR-004:** The system MUST maintain Customer information needed for warehouse operations.
- **FR-005:** The system MUST save a Customer when the information is valid.
- **FR-006:** The system MUST NOT save a Customer when the information is invalid.
- **FR-007:** The exact Customer attributes are **TBD** because they were not specified in the interview or class notes.
- **FR-008:** The authorized role for adding, editing, or deleting Customers is **TBD**.
- **FR-009:** A Customer MAY be associated with Customer Orders.
- **FR-010:** A Customer MAY be associated with a Delivery Route.
- **FR-011:** Behavior when Edit or Delete is attempted for a Customer that does not exist is **TBD**.
- **FR-012:** Behavior when a Customer is deleted while associated with a Customer Order or Delivery Route is **TBD**.

---

## Key Entities

- **Customer:** A customer who orders products from the warehouse.
- **Customer Order:** An order associated with a Customer.
- **Delivery Route:** A route that contains Customers for delivery.

---

## Initial Data Model

### Customer

Represents a Customer who orders products from the warehouse.

**Attributes:**
- [TBD: Customer attributes were not specified in the interview or class notes]

**Relationships:**
- A Customer may be associated with Customer Orders.
- A Customer may be associated with a Delivery Route.

### Customer Order

Represents an order received from a Customer.

**Relationships:**
- A Customer may have Customer Orders.
- Customer Order processing is handled separately in Feature 12.

### Delivery Route

Represents a route used to deliver orders to Customers.

**Relationships:**
- A Delivery Route may contain multiple Customers.
- A Customer may be associated with a Delivery Route.

---

## Gherkin AC

### US-6.1: Add a Customer

#### AC-6.1.1: Customer is saved

**Given** a Customer is being added  
**When** valid Customer information is entered and saved  
**Then** the system saves the Customer record

#### AC-6.1.2: Invalid Customer is not saved

**Given** a Customer is being added  
**When** invalid Customer information is entered  
**Then** the system does not save the Customer record

### US-6.2: Edit a Customer

#### AC-6.2.1: Customer changes are saved

**Given** an existing Customer record  
**When** the Customer information is changed with valid information  
**Then** the system saves the updated Customer information

#### AC-6.2.2: Invalid changes are not saved

**Given** an existing Customer record  
**When** invalid Customer information is entered  
**Then** the system does not save the invalid changes  
**And** the existing Customer information remains unchanged

### US-6.3: Delete a Customer

#### AC-6.3.1: Customer is deleted

**Given** an existing Customer record  
**When** the Customer is deleted  
**Then** the Customer record is removed

#### AC-6.3.2: Customer does not exist

**Given** no matching Customer record exists  
**When** an attempt is made to delete the Customer  
**Then** [TBD: behavior not specified in the interview or class notes]