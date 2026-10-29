# ADR-004: Implement Role-Based Access Control

**Status:** Proposed  
**Date:** 2026-10-28  
**Project:** Warehouse Management System

## Context

The Warehouse Management System supports different types of employees, including managers, office clerks, warehouse workers, shipping clerks, and drivers.

Each employee has different responsibilities and should only access the functions necessary to perform their assigned duties.

For example, managers and authorized office clerks may maintain item master data, while warehouse workers and drivers must not modify item master data.

Without appropriate access controls, unauthorized users could change inventory information, modify business records, or access restricted operations.

## Decision

The Warehouse Management System will implement Role-Based Access Control (RBAC).

Each authenticated user will be assigned one or more authorized roles. Permissions will determine which functions and operations the user can perform.

The proposed roles and permissions include:

| Role | Authorized Functions |
|---|---|
| Manager | Manage warehouse operations, maintain master data, review reports, and approve authorized adjustments |
| Office Clerk | Maintain authorized business records, create and manage orders, and update permitted master data |
| Warehouse Worker | Receive shipments, put away inventory, pick orders, scan items, and perform authorized inventory movements |
| Shipping Clerk | Verify shipments, record shipping information, and manage authorized shipping operations |
| Driver | View assigned deliveries, record delivery outcomes, and report discrepancies |

Warehouse workers and drivers will not have permission to modify item master data.

The Warehouse Backend API will enforce permissions for every protected operation.

The user interface will display functions according to the user's role, but hiding a menu option will not replace backend authorization.

## Rationale

Role-Based Access Control was selected because the Warehouse Management System has clearly defined employee responsibilities.

RBAC supports the principle of least privilege by restricting access to only the operations required for each role.

Centralized authorization also improves security, consistency, and maintainability.

## Consequences

**Positive:**
- Prevents unauthorized modifications to warehouse information.
- Supports different menus for different employee roles.
- Reduces the risk of accidental or unauthorized changes.
- Allows administrators to manage permissions consistently.
- Supports accountability for sensitive operations.

**Negative:**
- Requires user authentication and role management.
- Permissions must be reviewed when new features are introduced.
- Incorrect role assignments could prevent legitimate work or allow unauthorized access.
- Authorization rules require thorough testing.

## Alternatives Considered

**Allow all authenticated users to access every function:** Rejected because it would violate the warehouse's access-control requirements.

**Use only frontend menu restrictions:** Rejected because users could potentially bypass the interface and send requests directly to the backend.

## Related Artifacts

- `docs/Arch_Diagrams/Warehouse-C4-System-Context.png`
- `docs/Arch_Diagrams/Warehouse-C4-Container.png`
- Warehouse feature specifications in `features/`.