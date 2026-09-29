# Feature: Maintain Company

**Feature ID:** 1  
**Branch pattern:** `feature/1-maintain-company`  
**Status:** Draft  
**Created:** 2026-09-25  
**Input:** The system represents one company; that single company record is added, edited, and deleted so company data stays accurate.

---

## User Stories

### US-1.1: Add the Company

**As a** [TBD: authorized role not specified]  
**I want to** add the company  
**So that** the one company the system represents is recorded

**Priority:** P1  
**Independent test:** With no company recorded, add the company with valid information and confirm it is saved.

### US-1.2: Edit the Company

**As a** [TBD: authorized role not specified]  
**I want to** edit the company  
**So that** the company record stays accurate

**Priority:** P1  
**Independent test:** Change the existing company and confirm the saved record shows the updated information.

### US-1.3: Delete the Company

**As a** [TBD: authorized role not specified]  
**I want to** delete the company  
**So that** the company record can be removed if it should no longer be kept

**Priority:** P1  
**Independent test:** Delete the existing company and confirm it is no longer kept.

---

## Functional Requirements

- **FR-001:** The system MUST represent exactly one company.
- **FR-002:** The system MUST allow the company to be added when no company record exists.
- **FR-003:** The system MUST allow the company to be edited when the company record exists.
- **FR-004:** The system MUST allow the company to be deleted when the company record exists.
- **FR-005:** The system MUST save the company when the information is valid.
- **FR-006:** The system MUST NOT save the company when the information is invalid.
- **FR-007:** The system MUST NOT keep more than one company record.
- **FR-008:** Company attributes are **TBD** because the interview and class notes do not specify Company fields.
- **FR-009:** Whether Company can be deleted when Warehouses already exist is **TBD**.
- **FR-010:** The authorized role for adding, editing, or deleting Company is **TBD**.
- **FR-011:** Behavior when Edit or Delete is attempted and no Company record exists is **TBD**.

---

## Key Entities

- **Company:** The single company represented by the system. Its exact attributes are **TBD**.
- **Warehouse:** A warehouse belonging to the Company. Warehouse maintenance is handled in Feature 2.

---

## Initial Data Model

### Company

Represents the single company maintained by the system.

**Attributes:**
- Company ID
- [TBD: Company attributes are not specified in the interview/class material]

**Relationships:**
- A Company can have one or more Warehouses.
- The effect of existing Warehouses on Company deletion is **TBD**.
- The system keeps at most one Company record.

### Warehouse

Represents a warehouse associated with the Company.

**Relationships:**
- A Warehouse belongs to the Company.
- Warehouse maintenance is handled separately in Feature 2.

---

## Gherkin AC

### US-1.1: Add the Company

#### AC-1.1.1: Company is saved successfully

**Given** no Company record exists  
**When** the Company is added with valid information  
**Then** the Company is saved successfully  
**And** the system has exactly one Company record

#### AC-1.1.2: Company is not saved when information is invalid

**Given** no Company record exists  
**When** the Company is added with invalid information  
**Then** the Company is not saved  
**And** the system still has no Company record

#### AC-1.1.3: Second Company is not saved

**Given** a Company record already exists  
**When** another Company is added  
**Then** the second Company is not saved  
**And** the system still has exactly one Company record

### US-1.2: Edit the Company

#### AC-1.2.1: Edited Company is saved successfully

**Given** the Company record exists  
**When** the Company is edited with valid information  
**Then** the Company is saved successfully  
**And** the record shows the updated information  
**And** the system still has exactly one Company record

#### AC-1.2.2: Invalid edited Company is not saved

**Given** the Company record exists  
**When** the Company is edited with invalid information  
**Then** the changes are not saved  
**And** the existing Company information remains unchanged

### US-1.3: Delete the Company

#### AC-1.3.1: Company is deleted successfully

**Given** the Company record exists  
**When** the Company is deleted  
**Then** the Company is no longer kept