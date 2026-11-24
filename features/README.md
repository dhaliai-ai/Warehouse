# Feature Specifications

Spec-driven development (SDD) source of truth for **this** application.  
No application code may be written unless it maps to a requirement in one of these files.

This directory contains the **Warehouse Management System** product-specific feature specifications. Each numbered feature lives in its own folder as `feature.md`. These files authorize warehouse administration, inventory, purchasing, receiving, putaway, customer orders, picking, shipping, delivery, and reporting. They do **not** claim that those features have been implemented or tested.

**Methodology:** [framework.md](./framework.md) — how to write, trace, and ship feature specs.  
**Student guide (requirements):** [writing-feature-requirements.md](./writing-feature-requirements.md) — stories, FRs, initial data model, Gherkin AC.  
**Student guide (design):** [writing-feature-design.md](./writing-feature-design.md) — ownership, API, screens, test map, DoD, out of scope.  
**Student guide (living reference):** [reference/writing-living-reference.md](./reference/writing-living-reference.md) — update api / data-model / behavior in the same PR.

*(Examples in the writing guides often cite the OC CS Speckit Todo sample app — use them as patterns for your product.)*

**Sprints** live in your agile tool — they are **not** part of these specs.

## Feature catalog

| ID | File | Branch | Depends on |
|----|------|--------|------------|
| 1 | [Maintain Company](./feature-01-maintain-company/feature.md) | `feature/1-maintain-company` (proposed) | TBD |
| 2 | [Maintain Warehouses](./feature-02-maintain-warehouses/feature.md) | `feature/2-maintain-warehouses` (proposed) | TBD |
| 3 | [Maintain Inventory](./feature-03-maintain-inventory/feature.md) | `feature/3-maintain-inventory` (proposed) | TBD |
| 4 | [Maintain Individual Item](./feature-04-maintain-individual-item/feature.md) | `feature/4-maintain-individual-item` (proposed) | TBD |
| 5 | [Maintain Suppliers](./feature-05-maintain-suppliers/feature.md) | `feature/5-maintain-suppliers` (proposed) | TBD |
| 6 | [Maintain Customers](./feature-06-maintain-customers/feature.md) | `feature/6-maintain-customers` (proposed) | TBD |
| 7 | [Maintain Supplier Order Forms](./feature-07-maintain-supplier-order-forms/feature.md) | `feature/7-maintain-supplier-order-forms` (proposed) | TBD |
| 8 | [Maintain Customer Order Forms](./feature-08-maintain-customer-order-forms/feature.md) | `feature/8-maintain-customer-order-forms` (proposed) | TBD |
| 9 | [Create Supplier Order](./feature-09-create-supplier-order/feature.md) | `design-draft` (exists) | TBD |
| 10 | [Receive Supplier Order](./feature-10-receive-supplier-order/feature.md) | `design-draft` (exists) | TBD |
| 11 | [Put Away Received Items](./feature-11-put-away-received-items/feature.md) | `feature/11-put-away-received-items` (proposed) | 2, 3, 4, 9, 10 |
| 12 | [Receive Customer Orders](./feature-12-receive-customer-orders/feature.md) | `feature/12-receive-customer-orders` (proposed) | TBD |
| 13 | [Pick Customer Orders](./feature-13-pick-customer-orders/feature.md) | `feature/13-pick-customer-orders` (proposed) | TBD |
| 14 | [Ship Customer Orders](./feature-14-ship-customer-orders/feature.md) | `feature/14-ship-customer-orders` (proposed) | TBD |
| 15 | [Deliver Customer Orders](./feature-15-deliver-customer-orders/feature.md) | `feature/15-deliver-customer-orders` (proposed) | TBD |
| 16 | [Out of Stock Items](./feature-16-out-of-stock-items/feature.md) | `feature/16-items-out-of-stock` (proposed) | TBD |
| 17 | [Supplier Order Shipping Differences](./feature-17-supplier-order-shipping-differences/feature.md) | `feature/17-supplier-order-differences` (proposed) | TBD |
| 18 | [Delivery Shipping Differences](./feature-18-delivery-shipping-differences/feature.md) | `feature/18-delivery-shipment-differences` (proposed) | TBD |
| 19 | [Monthly Shipped Item Quantities](./feature-19-monthly-shipped-item-quantities/feature.md) | `feature/19-monthly-shipped-item-quantities` (proposed) | TBD |

**Branch names:** Values marked *(proposed)* are implementation branch names from each spec’s **Branch pattern** field. No `feature/N-*` implementation branches exist in this repository yet. Features 9 and 10 document **Branch:** `design-draft`, which exists as the current design documentation branch, not as a completed implementation branch.

**Depends on:** Only Feature 11 documents other-feature data ownership (Features 2, 3, 4, 9, and 10). Other specs do not establish a formal dependency list, so those cells are **TBD**.

New features: follow [framework.md](./framework.md#feature-spec-template) — **Status**, **Input**, **FR-00N**, **SC-00N**, **Key Entities**, Gherkin, **Agent implementation request**, **Definition of Done**.

**Branch roles:** `main` = scaffold-only starter kit · `dev` = integration · `feature/N-*` = feature work (branch from `dev`).

## Warehouse workflow coverage

Existing specifications grouped by warehouse operation. This table maps coverage; it does not add features or mark work complete.

| Workflow | Features |
|----------|----------|
| Company and warehouse administration | 1, 2 |
| Item and inventory management | 3, 4 |
| Supplier and customer management | 5, 6 |
| Purchasing and receiving | 7, 9, 10 |
| Putaway and storage | 11 |
| Customer order management | 8, 12 |
| Picking and fulfillment | 13 |
| Shipping and delivery | 14, 15 |
| Inventory exceptions and discrepancies | 3, 10, 16, 17, 18 |
| Reporting | 16, 17, 18, 19 |

## Living reference

Keep snapshots in sync when schema, API, or product rules change — **in the same PR as implementation** (required DoD; see [Merge checklist + Agility sync](./framework.md#merge-checklist--agility-sync)). Each `feature-N-*.md` includes an **Agent implementation request** block so Cursor updates reference during implementation ([framework.md](./framework.md#agent-implementation-request)). Spec evolution after merge: [prefer a new feature delta](./framework.md#spec-evolution-after-merge).

| File | Purpose |
|------|---------|
| [reference/README.md](./reference/README.md) | How to maintain reference docs |
| [reference/writing-living-reference.md](./reference/writing-living-reference.md) | Student guide — writing/updating living reference |
| [reference/data-model.md](./reference/data-model.md) | Current database tables (update in feature PR when schema changes) |
| [reference/api.md](./reference/api.md) | Current REST API (update in feature PR when API changes) |
| [reference/behavior.md](./reference/behavior.md) | Current product rules (update in feature PR when rules change) |

## Related

- Cursor rules: `.cursor/rules/`
- ADRs: `docs/adr/`
- Warehouse domain model: [docs/warehouse-domain-model.md](../docs/warehouse-domain-model.md)
- Quality attributes (NFRs): `docs/nfr/`
- Starter kit notes: `docs/STARTER-KIT.md`
