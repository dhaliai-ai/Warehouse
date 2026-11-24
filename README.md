# Warehouse Management System (WMS)

## Project Overview

The Warehouse Management System (WMS) is designed to manage and coordinate warehouse operations, including supplier orders, receiving, putaway, inventory management, customer orders, picking, shipping, and delivery.

The system supports a company operating multiple warehouses and provides centralized management of warehouse information while maintaining warehouse-specific inventory, storage locations, and operational transactions.

The primary goal is to improve inventory accuracy, operational efficiency, order fulfillment, and traceability through digital and barcode-driven workflows.

This project follows the OC Speckit Spec-Driven Development (SDD) methodology.

Specifications define **what** to build (`features/`). Cursor rules define **how** to build it (`.cursor/rules/`). Tests verify both.

## Project Objectives

- Support the management of multiple warehouses within a company.
- Maintain accurate item, supplier, customer, and inventory information.
- Automate supplier and customer order processing.
- Support barcode-based receiving, putaway, and picking.
- Reduce dependence on paper-based warehouse operations.
- Track inventory quantities and storage locations.
- Identify receiving, shipping, and delivery discrepancies.
- Provide operational reports for warehouse management.
- Enforce role-based access and warehouse-specific data restrictions.

## System Users and Responsibilities

| User Role | Responsibilities |
|---|---|
| Warehouse Manager | Manage warehouse operations, review reports, authorize adjustments, and oversee discrepancies. |
| Office Clerk | Maintain authorized master data and process supplier and customer orders. |
| Receiving Clerk | Receive supplier shipments, scan items, verify quantities, and identify discrepancies. |
| Warehouse Worker | Perform putaway, inventory movement, and assigned warehouse tasks. |
| Picker | Pick customer orders using digital instructions and barcode verification. |
| Shipping Clerk | Verify picked orders and coordinate outgoing shipments. |
| Driver | Access assigned delivery information, confirm deliveries, and report discrepancies. |

Access to functions and data shall be determined by the user's assigned role and authorized warehouse.

## Warehouse Domain Model

The proposed conceptual domain model, including workflows, ownership, and open design questions, is documented in [docs/warehouse-domain-model.md](docs/warehouse-domain-model.md).

The system is organized around the following business entities:

| Entity | Description |
|---|---|
| Company | Organization responsible for operating one or more warehouses. |
| Warehouse | Physical facility used to receive, store, and distribute inventory. |
| Storage Location | Identifiable warehouse location, including receiving doors, picking bins, and reserve storage. |
| Item | Product identified by an item number and associated barcode information. |
| Inventory | Quantity of an item stored at a specific warehouse location. |
| Supplier | Organization providing products to the warehouse. |
| Customer | Organization or store receiving products from the warehouse. |
| Supplier Order | Purchase order identifying products and quantities ordered from a supplier. |
| Customer Order | Order identifying products and quantities requested by a customer. |
| Inventory Transaction | Record of an inventory receipt, movement, adjustment, or shipment. |
| Shipment | Group of customer-order items prepared for distribution. |
| Delivery | Record of products delivered to a customer and any delivery discrepancies. |
| User | Authorized individual assigned system roles and warehouse access. |

## Core Warehouse Workflows

### Supplier Order and Receiving

1. An authorized office clerk creates a supplier order.
2. The receiving clerk identifies the arriving shipment and corresponding supplier order.
3. Products are scanned and received quantities are recorded.
4. Ordered and received quantities are compared.
5. Discrepancies are recorded and reviewed.
6. Received inventory becomes available for putaway.

### Putaway and Inventory Management

1. A warehouse worker receives a putaway assignment.
2. The system identifies an appropriate storage location.
3. The worker scans the item and destination location.
4. The system validates the movement.
5. Inventory quantities and locations are updated.
6. Inventory movements are recorded for traceability.

### Customer Order and Picking

1. An authorized clerk records a customer order.
2. The system identifies the required items and available inventory.
3. Picking tasks are assigned to warehouse workers.
4. Workers follow digital picking instructions.
5. Items and locations are verified using barcode scanning.
6. Picked orders are prepared for shipping.

### Shipping and Delivery

1. The shipping clerk verifies picked customer orders.
2. Orders are prepared for shipment.
3. Shipment information is recorded.
4. Drivers access their assigned delivery information.
5. Delivered quantities and discrepancies are recorded.
6. Management reviews shipment and delivery reports.

## Multi-Warehouse Support

The system shall support multiple warehouses belonging to a company.

- Each warehouse shall have a unique identifier.
- Storage locations shall belong to a specific warehouse.
- Inventory quantities shall be maintained by warehouse and storage location.
- Operational transactions shall identify the associated warehouse.
- Users shall access only warehouses and functions for which they are authorized.
- Warehouse-specific transactions shall not unintentionally modify inventory belonging to another warehouse.

Ordinary inter-warehouse inventory transfer as a routine bin-to-bin movement is **not fully specified**. Feature 3 leaves that question unresolved. This README does not approve a transfer workflow.

The initial design focuses on one company operating multiple warehouses. Support for independent tenant companies is an architecture decision requiring further review.

## Feature Specifications

The Warehouse Management System includes the following 19 features:

| Feature | Description |
|---|---|
| 1 | Maintain Company |
| 2 | Maintain Warehouses |
| 3 | Maintain Inventory |
| 4 | Maintain Individual Item |
| 5 | Maintain Suppliers |
| 6 | Maintain Customers |
| 7 | Maintain Supplier Order Forms |
| 8 | Maintain Customer Order Forms |
| 9 | Create Supplier Order |
| 10 | Receive Supplier Order |
| 11 | Put Away Received Items |
| 12 | Receive Customer Orders |
| 13 | Pick Customer Orders |
| 14 | Ship Customer Orders |
| 15 | Deliver Customer Orders |
| 16 | Out-of-Stock Items |
| 17 | Supplier Order Shipping Differences |
| 18 | Delivery Shipping Differences |
| 19 | Monthly Shipped Item Quantities |

Detailed specifications are maintained in the [Feature Catalog](features/README.md).

Each feature follows the OC Speckit specification format, including functional requirements, acceptance criteria, data ownership, API requirements, screen requirements, and Definition of Done.

## System Architecture

The proposed system uses a three-tier architecture:

1. **Presentation Layer:** Web-based user interface supporting desktop and compatible handheld devices.
2. **Application Layer:** Backend REST API responsible for business rules, authentication, authorization, and warehouse workflows.
3. **Data Layer:** Relational database responsible for persistent storage, data relationships, and transaction integrity.

Architecture decisions are documented in [Architecture Decision Records](docs/adr/README.md).

## Technology Stack

The following technology stack is inherited from the OC Speckit starter kit and represents the proposed implementation baseline.

| Layer | Technology |
|---|---|
| Frontend | Vue 3, Vuetify 4, Vite, vue-router, axios |
| Backend | Node.js, Express, Sequelize |
| Database | MySQL (InnoDB, proposed) |
| Backend Testing | Jest and supertest |
| Frontend Testing | Vitest and @vue/test-utils |
| UI Design | Figma |
| Architecture Diagrams | draw.io |
| Version Control | Git and GitHub |
| Development Environment | Cursor |

### Proposed Application Configuration

| Configuration | Value |
|---|---|
| Database name | warehouse |
| Frontend development port | 8082 |
| Backend development port | 3200 |
| API prefix | /api |

These are proposed implementation settings and must be verified against the application configuration before implementation.

## Nonfunctional Requirements

The system prioritizes the following quality attributes:

- Performance and warehouse operational throughput.
- Inventory accuracy and transaction integrity.
- Security and role-based authorization.
- Barcode scanning accuracy and error handling.
- Reliability and recovery from network interruptions.
- Usability on desktop and handheld warehouse devices.
- Scalability across multiple warehouses.
- Maintainability and requirements traceability.

Detailed quality targets and verification approaches are maintained in [Nonfunctional Requirements](docs/nfr/).

## Repository Documentation

| Directory or File | Purpose |
|---|---|
| [features/](features/) | Warehouse feature specifications. |
| [features/README.md](features/README.md) | Feature catalog and navigation. |
| [features/framework.md](features/framework.md) | OC Speckit specification framework. |
| [features/reference/](features/reference/) | Living API, schema, and business-rule references. |
| [docs/adr/](docs/adr/) | Architecture Decision Records. |
| [docs/warehouse-domain-model.md](docs/warehouse-domain-model.md) | Proposed warehouse domain model (entities, workflows, ownership). |
| [docs/nfr/](docs/nfr/) | Nonfunctional requirements and quality attributes. |
| [docs/ui/](docs/ui/) | Warehouse user interface designs. |
| [docs/Arch_Diagrams/](docs/Arch_Diagrams/) | C4 architecture diagrams. |
| [.cursor/rules/](.cursor/rules/) | Implementation standards and development rules. |
| [docs/STARTER-KIT.md](docs/STARTER-KIT.md) | OC Speckit starter-kit guidance. |

## Architecture Diagrams

The system architecture is represented using the C4 model. These diagrams are **proposed design**, not implemented infrastructure. Index, sources, and ADR mapping: [docs/Arch_Diagrams/README.md](docs/Arch_Diagrams/README.md).

- [Level 1 — System Context](docs/Arch_Diagrams/Warehouse-C4-System-Context.png)
- [Level 2 — Container Diagram](docs/Arch_Diagrams/Warehouse-C4-Container1.drawio.png)
- [Level 3 — Component Diagram](docs/Arch_Diagrams/Warehouse-C4-Component.drawio.png)

## User Interface Designs

User interface designs are maintained in [docs/ui/](docs/ui/).

Relevant UI images are linked from the Screen Requirements sections of individual feature specifications. The 112 required Screen IDs have design mockups under [docs/ui/](docs/ui/) (desktop) and [docs/ui/Handheld/](docs/ui/Handheld/) (handheld). These are design images, not implemented application screens. Inventory: [docs/ui/README.md](docs/ui/README.md).

## Branching Strategy

| Branch | Purpose |
|---|---|
| main | Reviewed and merged project specifications. |
| design-draft | Initial warehouse design and instructor feedback corrections. |
| design-final | Final warehouse design and architecture specifications. |
| dev | Future implementation integration. |
| feature/N-short-name | Future individual feature implementation. |

Changes shall be reviewed through GitHub pull requests before merging into the appropriate target branch.

## Development Approach

The project follows the OC Speckit Spec-Driven Development process:

1. Define and review feature specifications.
2. Document architecture decisions.
3. Establish measurable nonfunctional requirements.
4. Design user interfaces and system architecture.
5. Review acceptance criteria and data ownership.
6. Implement features according to approved specifications.
7. Verify behavior through automated and manual testing.
8. Maintain consistency between specifications, implementation, and reference documentation.

API, database schema, and business-rule reference documents shall be updated in the same pull request when related implementation changes occur.

## Future Implementation Setup

When application implementation begins, the OC Speckit starter-kit dependencies can be installed using:

```bash
npm install --prefix frontend
npm install --prefix backend
npm install
```

Configure the backend environment files, MySQL databases, database credentials, and authentication secret before running the application.

Run the automated tests using:

```bash
npm test
```

Start the backend and frontend in separate terminals:

```bash
cd backend
npm run dev
```

```bash
cd frontend
npm run dev
```

## Project Status

**Current Phase:** Warehouse System Design and Architecture Review.

The current project focuses on producing complete, consistent, and reviewable Warehouse Management System specifications using the OC Speckit framework. Application implementation is outside the scope of the current design assignment.

## Academic Information

**Course:** Software Engineering II

**Institution:** Oklahoma Christian University

**Instructor:** Prof. North

**Project:** Warehouse Management System