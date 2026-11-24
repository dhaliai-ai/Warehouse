# Warehouse UI design inventory

**Branch:** `design-final`  
**Status:** Batches 1–7 complete. These are design mockups, not implemented application screens. All 112 required Screen IDs have dedicated images after visual inspection.  
**Source of truth:** Screen Requirements in `features/feature-*/feature.md`  
**Existing files:** preserved under `docs/ui/` (this inventory does not rename or move them)

This document lists every screen, dialog, form, and handheld interface **explicitly named** in the nineteen feature specifications. It does not add screens, buttons, or fields that the specs do not require.

Proposed files for **new** mockups use lowercase kebab-case under `docs/ui/`. The repository folder is `docs/ui/`.

**Status values**

| Status | Meaning |
|---|---|
| Complete | Existing image shows the required screen (fields, actions, and purpose match) |
| Partially complete | Existing image is related but omits required content or mixes extra/unspecified content |
| Missing | No matching image file |
| Incorrectly linked | A feature embeds an existing image that is not that screen |
| Reusable | Shared chrome or a pattern that several screens may follow; not a substitute for a required screen |

---

## Inventory

| Feature | Screen ID | Screen Name | Interface Type | Image Path | Status |
|---|---|---|---|---|---|
| 1 | UI-1 | Company Maintenance | Desktop | `docs/ui/company-maintenance.png` (exists/view). States: `docs/ui/company-maintenance-empty.png`, `docs/ui/company-maintenance-add.png`, `docs/ui/company-maintenance-edit.png`, `docs/ui/company-maintenance-saving.png`, `docs/ui/company-maintenance-delete.png`. Original retained: `docs/ui/Maintain Company.png` | Complete |
| 2 | UI-2A | Warehouse List | Desktop | `docs/ui/warehouse-list.png`. States: `docs/ui/warehouse-list-empty.png`, `docs/ui/warehouse-list-delete.png`. Original retained: `docs/ui/Maintain Warehouse.png` | Complete |
| 2 | UI-2B | Warehouse Add/Edit | Desktop | `docs/ui/warehouse-add.png` (add/empty), `docs/ui/warehouse-edit.png` (edit). Original retained: `docs/ui/Maintain Warehouse.png` | Complete |
| 3 | UI-3A | Inventory List | Desktop | `docs/ui/inventory-list.png`. Empty: `docs/ui/inventory-list-empty.png` | Complete |
| 3 | UI-3B | Add Inventory Balance | Desktop | `docs/ui/inventory-add.png` | Complete |
| 3 | UI-3C | Physical Inventory Count | Desktop | `docs/ui/inventory-count.png` | Complete |
| 3 | UI-3D | Inventory Adjustment | Desktop | `docs/ui/inventory-adjustment.png` | Complete |
| 3 | UI-3E | Move Inventory | Desktop | `docs/ui/inventory-movement.png` | Complete |
| 3 | UI-3F | Inventory History | Desktop | `docs/ui/inventory-history.png` | Complete |
| 3 | UI-3G | Awaiting Put Away | Desktop | `docs/ui/inventory-awaiting-putaway.png` | Complete |
| 4 | UI-4A | Individual Item List | Desktop | `docs/ui/item-list.png`. Delete blocked: `docs/ui/item-list-delete.png` | Complete |
| 4 | UI-4B | Add Individual Item | Desktop | `docs/ui/item-add.png` | Complete |
| 4 | UI-4C | Edit Individual Item | Desktop | `docs/ui/item-edit.png` | Complete |
| 4 | UI-4D | Maintain Item UPCs | Desktop | `docs/ui/item-upcs.png` | Complete |
| 4 | UI-4E | Maintain Item Suppliers | Desktop | `docs/ui/item-suppliers.png` | Complete |
| 4 | UI-4F | Item Details | Desktop | `docs/ui/item-details.png` | Complete |
| 4 | UI-4G | Replenishment Information | Desktop | `docs/ui/item-replenishment.png` | Complete |
| 5 | UI-5A | Supplier List | Desktop | `docs/ui/supplier-list.png`. Delete blocked: `docs/ui/supplier-list-delete.png` | Complete |
| 5 | UI-5B | Add Supplier | Desktop | `docs/ui/supplier-add.png` | Complete |
| 5 | UI-5C | Edit Supplier | Desktop | `docs/ui/supplier-edit.png` | Complete |
| 5 | UI-5D | Supplier Details | Desktop | `docs/ui/supplier-details.png` | Complete |
| 5 | UI-5E | Supplier Purchasing Information | Desktop | `docs/ui/supplier-purchasing.png` | Complete |
| 5 | UI-5F | Supplier Relationships | Desktop | `docs/ui/supplier-relationships.png` | Complete |
| 6 | UI-6A | Customer List | Desktop | `docs/ui/customer-list.png` | Complete |
| 6 | UI-6B | Add Customer | Desktop | `docs/ui/customer-add.png` | Complete |
| 6 | UI-6C | Edit Customer | Desktop | `docs/ui/customer-edit.png` | Complete |
| 6 | UI-6D | Customer Details | Desktop | `docs/ui/customer-details.png` | Complete |
| 6 | UI-6E | Delivery Information | Desktop | `docs/ui/customer-delivery.png`. Driver: `docs/ui/customer-delivery-driver.png` | Complete |
| 6 | UI-6F | Delete/Deactivate Confirmation | Desktop dialog | `docs/ui/customer-status.png` | Complete |
| 7 | UI-7A | Supplier Order Form List | Desktop | `docs/ui/supplier-order-form-list.png`. Empty: `docs/ui/supplier-order-form-list-empty.png`. Unauthorized: `docs/ui/supplier-order-form-list-unauthorized.png` | Complete |
| 7 | UI-7B | Add Supplier Order Form | Desktop | `docs/ui/supplier-order-form-add.png` | Complete |
| 7 | UI-7C | Edit Supplier Order Form | Desktop | `docs/ui/supplier-order-form-edit.png` | Complete |
| 7 | UI-7D | Maintain Form Items | Desktop | `docs/ui/supplier-order-form-items.png` | Complete |
| 7 | UI-7E | Supplier Order Form Details | Desktop | `docs/ui/supplier-order-form-details.png` | Complete |
| 7 | UI-7F | Prepare Supplier Order Preview | Desktop | `docs/ui/supplier-order-form-preview.png`. Inactive blocked: `docs/ui/supplier-order-form-preview-blocked.png` | Complete |
| 7 | UI-7G | Delete or Deactivate Form | Desktop dialog | `docs/ui/supplier-order-form-status.png` (referenced, delete blocked). Unused eligible: `docs/ui/supplier-order-form-status-unused.png` | Complete |
| 8 | UI-8A | Customer Order Form List | Desktop | `docs/ui/customer-order-form-list.png`. Empty: `docs/ui/customer-order-form-list-empty.png`. Unauthorized: `docs/ui/customer-order-form-list-unauthorized.png` | Complete |
| 8 | UI-8B | Add Customer Order Form | Desktop | `docs/ui/customer-order-form-add.png` | Complete |
| 8 | UI-8C | Edit Customer Order Form | Desktop | `docs/ui/customer-order-form-edit.png` | Complete |
| 8 | UI-8D | Maintain Customer Order Form Items | Desktop | `docs/ui/customer-order-form-items.png` | Complete |
| 8 | UI-8E | Customer Order Form Details | Desktop | `docs/ui/customer-order-form-details.png` | Complete |
| 8 | UI-8F | Prepare Customer Order Preview | Desktop | `docs/ui/customer-order-form-preview.png`. Inactive blocked: `docs/ui/customer-order-form-preview-blocked.png` | Complete |
| 8 | UI-8G | Delete or Deactivate Form | Desktop dialog | `docs/ui/customer-order-form-status.png` (referenced, delete blocked). Unused eligible: `docs/ui/customer-order-form-status-unused.png` | Complete |
| 9 | UI-9A | Replenishment Recommendations | Desktop | `docs/ui/supplier-replenishment.png` | Complete |
| 9 | UI-9B | Create Supplier Order | Desktop | `docs/ui/supplier-order-create.png` | Complete |
| 9 | UI-9C | Review and Submit Supplier Order | Desktop | `docs/ui/supplier-order-review.png` | Complete |
| 9 | UI-9D | Supplier Order List | Desktop | `docs/ui/supplier-order-list.png` | Complete |
| 9 | UI-9E | Supplier Order Details | Desktop | `docs/ui/supplier-order-details.png` | Complete |
| 9 | UI-9F | Receiving PO Lookup | Desktop / receiving station | `docs/ui/supplier-order-receiving-lookup.png` | Complete |
| 9 | UI-9G | Supplier Order Audit History | Desktop | `docs/ui/supplier-order-audit.png` | Complete |
| 9 | UI-9H | Purchasing Exceptions | Desktop | `docs/ui/supplier-purchasing-exceptions.png` | Complete |
| 10 | UI-10A | Supplier Order Lookup | Handheld / receiving | `docs/ui/Handheld/receive-supplier-order-lookup.png`. Unknown PO: `docs/ui/Handheld/receive-supplier-order-lookup-unknown.png` | Complete |
| 10 | UI-10B | Receiving Warehouse and Door | Handheld / receiving | `docs/ui/Handheld/receive-supplier-order-door.png`. Mismatch: `docs/ui/Handheld/receive-supplier-order-door-mismatch.png` | Complete |
| 10 | UI-10C | Scan Received Items | Handheld | `docs/ui/Handheld/receive-supplier-order-scan.png`. Invalid: `docs/ui/Handheld/receive-supplier-order-scan-invalid.png`. Unconfirmed: `docs/ui/Handheld/receive-supplier-order-scan-connection.png`. Original retained: `docs/ui/Handheld/Receiving Scan.png` | Complete |
| 10 | UI-10D | Receiving Discrepancy Review | Handheld / receiving | `docs/ui/Handheld/receive-supplier-order-discrepancies.png` | Complete |
| 10 | UI-10E | Complete Receiving | Handheld / receiving | `docs/ui/Handheld/receive-supplier-order-complete.png`. Approval missing: `docs/ui/Handheld/receive-supplier-order-complete-blocked.png` | Complete |
| 10 | UI-10F | Supplier Order Receiving Closure | Desktop / receiving | `docs/ui/receive-supplier-order-close.png` | Complete |
| 10 | UI-10G | Receiving History | Desktop | `docs/ui/receive-supplier-order-history.png` | Complete |
| 11 | UI-11A | Available Putaway Assignments | Handheld | `docs/ui/Handheld/putaway-assignments.png`. Empty: `docs/ui/Handheld/putaway-assignments-empty.png` | Complete |
| 11 | UI-11B | Putaway Assignment Details | Handheld | `docs/ui/Handheld/putaway-assignment-details.png` | Complete |
| 11 | UI-11C | Putaway Sequence | Handheld | `docs/ui/Handheld/putaway-sequence.png` | Complete |
| 11 | UI-11D | Item UPC Verification | Handheld | `docs/ui/Handheld/putaway-item-verify.png`. Incorrect item: `docs/ui/Handheld/putaway-item-verify-error.png` | Complete |
| 11 | UI-11E | Destination Bin Verification | Handheld | `docs/ui/Handheld/putaway-bin-verify.png`. Incorrect location: `docs/ui/Handheld/putaway-bin-verify-error.png` | Complete |
| 11 | UI-11F | Confirm Putaway Quantity | Handheld | `docs/ui/Handheld/putaway-quantity.png`. Unconfirmed: `docs/ui/Handheld/putaway-quantity-unconfirmed.png` | Complete |
| 11 | UI-11G | Alternative Storage Location | Handheld | `docs/ui/Handheld/putaway-alternative-location.png` | Complete |
| 11 | UI-11H | Blocked Putaway Instruction | Handheld | `docs/ui/Handheld/putaway-blocked.png` | Complete |
| 11 | UI-11I | Putaway Assignment Completion | Handheld | `docs/ui/Handheld/putaway-completion.png`. Outstanding remaining: `docs/ui/Handheld/putaway-completion-blocked.png` | Complete |
| 11 | UI-11J | Putaway Movement History | Desktop | `docs/ui/putaway-history.png` | Complete |
| 12 | SCREEN-12.1 | Customer Order List | Desktop | `docs/ui/customer-order-list.png`. Empty: `docs/ui/customer-order-list-empty.png` | Complete |
| 12 | SCREEN-12.2 | Customer Order Entry and Edit | Desktop | `docs/ui/customer-order-entry.png` | Complete |
| 12 | SCREEN-12.3 | Customer Order Detail | Desktop | `docs/ui/customer-order-detail.png` | Complete |
| 12 | SCREEN-12.4 | Release Customer Order Confirmation | Desktop dialog | `docs/ui/customer-order-release.png` | Complete |
| 12 | SCREEN-12.5 | Cancel Customer Order Confirmation | Desktop dialog | `docs/ui/customer-order-cancel.png` | Complete |
| 13 | SCREEN-13.1 | Available Picking Work | Handheld | `docs/ui/Handheld/picking-available-work.png`. Empty: `docs/ui/Handheld/picking-available-work-empty.png` | Complete |
| 13 | SCREEN-13.2 | Picking Assignment Overview | Handheld | `docs/ui/Handheld/picking-assignment.png` | Complete |
| 13 | SCREEN-13.3 | Picking Instruction | Handheld | `docs/ui/Handheld/picking-instruction.png`. Unconfirmed: `docs/ui/Handheld/picking-unconfirmed.png`. Original retained: `docs/ui/Handheld/Picking Scan.png` | Complete |
| 13 | SCREEN-13.4 | Barcode Verification | Handheld | `docs/ui/Handheld/picking-barcode-verify.png`. Location error: `docs/ui/Handheld/picking-barcode-location-error.png`. Item error: `docs/ui/Handheld/picking-barcode-item-error.png` | Complete |
| 13 | SCREEN-13.5 | Picking Shortage | Handheld | `docs/ui/Handheld/picking-shortage.png` | Complete |
| 13 | SCREEN-13.6 | Picking Completion | Handheld | `docs/ui/Handheld/picking-completion.png` | Complete |
| 13 | SCREEN-13.7 | Supervisor Shortage Review | Desktop | `docs/ui/picking-shortage-review.png` | Complete |
| 13 | SCREEN-13.8 | Picking History | Desktop | `docs/ui/picking-history.png` | Complete |
| 14 | SCREEN-14.1 | Available Customer Orders for Shipping | Desktop | `docs/ui/shipping-available-orders.png` | Complete |
| 14 | SCREEN-14.2 | Shipment Preparation | Desktop / shipping station | `docs/ui/shipping-preparation.png` | Complete |
| 14 | SCREEN-14.3 | Shipment Item Verification | Handheld / shipping station | `docs/ui/Handheld/shipping-item-verify.png`. Incorrect item: `docs/ui/Handheld/shipping-item-verify-error.png` | Complete |
| 14 | SCREEN-14.4 | Shipment Quantity Confirmation | Handheld / shipping station | `docs/ui/Handheld/shipping-quantity.png` | Complete |
| 14 | SCREEN-14.5 | Shipment Packaging and Labeling | Desktop / shipping station | `docs/ui/shipping-packaging.png` | Complete |
| 14 | SCREEN-14.6 | Shipment Completion | Desktop / shipping station | `docs/ui/shipping-completion.png` | Complete |
| 14 | SCREEN-14.7 | Shipping Exception Review | Desktop | `docs/ui/shipping-exceptions.png` | Complete |
| 14 | SCREEN-14.8 | Shipment History | Desktop | `docs/ui/shipping-history.png` | Complete |
| 15 | SCREEN-15.1 | Assigned Deliveries | Handheld | `docs/ui/Handheld/delivery-assigned.png`. Empty: `docs/ui/Handheld/delivery-assigned-empty.png` | Complete |
| 15 | SCREEN-15.2 | Delivery Details | Handheld | `docs/ui/Handheld/delivery-details.png` | Complete |
| 15 | SCREEN-15.3 | Record Quantity Delivered | Handheld | `docs/ui/Handheld/delivery-quantity.png` | Complete |
| 15 | SCREEN-15.4 | Delivery Discrepancy Entry | Handheld | `docs/ui/Handheld/delivery-discrepancy.png` | Complete |
| 15 | SCREEN-15.5 | Delivery Outcome Confirmation | Handheld | `docs/ui/Handheld/delivery-outcome.png` | Complete |
| 15 | SCREEN-15.6 | Delivery Assignment Administration | Desktop | `docs/ui/delivery-assignment-admin.png` | Complete |
| 15 | SCREEN-15.7 | Delivery Reassignment | Desktop | `docs/ui/delivery-reassignment.png` | Complete |
| 15 | SCREEN-15.8 | Delivery History | Desktop | `docs/ui/delivery-history.png` | Complete |
| 15 | SCREEN-15.9 | Delivery Discrepancy Review | Desktop | `docs/ui/delivery-discrepancy-review.png` | Complete |
| 16 | SCREEN-16.1 | Out-of-Stock Report | Desktop | `docs/ui/report-out-of-stock.png` | Complete |
| 16 | SCREEN-16.2 | Out-of-Stock Record Details | Desktop | `docs/ui/report-out-of-stock-details.png` | Complete |
| 16 | SCREEN-16.3 | Empty Results and Historical Data Warning | Desktop (state / message) | `docs/ui/report-out-of-stock-empty.png`. Invalid: `docs/ui/report-out-of-stock-invalid.png`. Unauthorized: `docs/ui/report-out-of-stock-unauthorized.png`. Incomplete history warning is on SCREEN-16.1 | Complete |
| 17 | SCREEN-17.1 | Supplier Difference Report | Desktop | `docs/ui/report-supplier-differences.png` | Complete |
| 17 | SCREEN-17.2 | Supplier Difference Details | Desktop | `docs/ui/report-supplier-difference-details.png` | Complete |
| 17 | SCREEN-17.3 | Empty Results and Data Quality Messages | Desktop (state / message) | `docs/ui/report-supplier-differences-empty.png`. Invalid: `docs/ui/report-supplier-differences-invalid.png`. Provisional: `docs/ui/report-supplier-differences-provisional.png`. Unauthorized: `docs/ui/report-supplier-differences-unauthorized.png` | Complete |
| 18 | SCREEN-18.1 | Delivery Difference Report | Desktop | `docs/ui/report-delivery-differences.png`. Incomplete history: `docs/ui/report-delivery-differences-incomplete.png` | Complete |
| 18 | SCREEN-18.2 | Delivery Difference Details | Desktop | `docs/ui/report-delivery-difference-details.png` | Complete |
| 18 | SCREEN-18.3 | Delivery History | Desktop | `docs/ui/report-delivery-history.png` (reporting; not Feature 15 `delivery-history.png`) | Complete |
| 18 | SCREEN-18.4 | Empty Results and Validation Messages | Desktop (state / message) | `docs/ui/report-delivery-differences-empty.png`. Invalid: `docs/ui/report-delivery-differences-invalid.png`. Pending: `docs/ui/report-delivery-differences-pending.png`. Unauthorized: `docs/ui/report-delivery-differences-unauthorized.png` | Complete |
| 19 | SCREEN-19.1 | Monthly Shipping Report | Desktop | `docs/ui/report-monthly-shipping.png` | Complete |
| 19 | SCREEN-19.2 | Monthly Item Shipment Details | Desktop | `docs/ui/report-monthly-shipping-details.png` | Complete |
| 19 | SCREEN-19.3 | Monthly Shipping Data-Quality View | Desktop | `docs/ui/report-monthly-shipping-data-quality.png` | Complete |
| 19 | SCREEN-19.4 | Empty Results and Validation Messages | Desktop (state / message) | `docs/ui/report-monthly-shipping-empty.png`. Missing month: `docs/ui/report-monthly-shipping-missing-month.png`. Missing year: `docs/ui/report-monthly-shipping-missing-year.png`. Invalid month: `docs/ui/report-monthly-shipping-invalid-month.png`. Invalid year: `docs/ui/report-monthly-shipping-invalid-year.png`. Unauthorized: `docs/ui/report-monthly-shipping-unauthorized.png`. Warehouse denied: `docs/ui/report-monthly-shipping-warehouse-denied.png` | Complete |

**Unmapped existing files (not a required Screen ID)**

| File | Classification |
|---|---|
| `docs/ui/Warehouse Dashboard.png` | Not specified as a feature screen. Incorrectly linked from Feature 6. Treat as shared navigation chrome only. |
| `docs/ui/WMS/Reusable UI Components.png` | Reusable across multiple features (buttons and status chips). Not a screen. |

**Count:** 112 required screens (including specified empty-result / message screens and confirmation dialogs with their own Screen IDs). Feature 1 delete confirmation is a **state of UI-1**, not a separate Screen ID.

---

## Existing image review

Visual inspection of the seven files was performed. None is **Complete** for a required Screen ID.

### `docs/ui/Maintain Company.png` — Feature 1 UI-1 — Partially complete

**Matches:** Desktop maintenance layout; Company name, address, phone, email; Edit / Save / Cancel; success and invalid-email feedback; Manager-style user.

**Gaps vs Screen Requirements:** Spec fields are Company ID, Company Name, Address, Phone, Email. The mock splits address into street/city/state/postal, adds Contact name, Contact role, Active, Organization profile, and primary warehouse. No Add-when-empty state, no Delete, no deletion confirmation.

**Linked correctly** from Feature 1. Proposed `docs/ui/company-maintenance.png` is still required if the deliverable must match spec fields exactly.

### `docs/ui/Maintain Warehouse.png` — Feature 2 UI-2A and UI-2B — Partially complete

**Matches:** List of warehouses with search, status, Add warehouse, selected-record edit, Save / Cancel, Company shown as organization.

**Gaps:** One image covers both required screens. List columns omit Phone; uses Warehouse number rather than Warehouse Code. No Delete or deletion confirmation. Extra Manager and Operating zone fields are not in UI-2B. Address is required in the mock; spec Address is optional.

### `docs/ui/Maintain Items and Suppliers.png` — Features 3, 4, 5 — Partially complete / incorrectly linked

**Visible content:** Item register (number, description, UPC, primary supplier, on-hand, status), Add item / Add supplier, selected item edit, selected supplier edit.

**Feature 3:** Incorrectly linked. This is item/supplier master data, not Inventory List, count, adjustment, movement, history, or awaiting putaway.

**Feature 4:** Partially reusable for UI-4A/UI-4C/UI-4E only. Missing selling price, units per case, min stock, dedicated Add Item, UPC maintenance, item details, replenishment.

**Feature 5:** Partial supplier edit pane only. No supplier list, purchasing information, or relationships screens.

### `docs/ui/Warehouse Dashboard.png` — Feature 6 — Incorrectly linked

Dashboard tiles and warehouse activity. Feature 6 requires Customer List, Add/Edit, Details, Delivery Information, and Delete/Deactivate. None of those appear.

### `docs/ui/Handheld/Receiving Scan.png` — original Figma receiving mock — retained

**Matches:** Handheld receiving chrome; PO; item; expected vs received; UPC scan; quantity; confirm receipt.

**Gaps vs Feature 10 spec:** Uses reams/pallets rather than ordered/previous/session/cumulative units; does not distinguish Individual vs Case UPC conversion. Dedicated UI-10C mockup is `docs/ui/Handheld/receive-supplier-order-scan.png`. This original file was not overwritten.

### `docs/ui/Handheld/Picking Scan.png` — original Figma picking mock — retained

**Matches:** Handheld picking chrome; source bin; item; requested vs picked; UPC scan; quantity.

**Gaps vs Feature 13:** Uses reams and SO-1183; combines instruction and scan. Dedicated SCREEN-13.3 and SCREEN-13.4 mockups are `picking-instruction.png` and `picking-barcode-verify.png`. This original file was not overwritten.

### `docs/ui/WMS/Reusable UI Components.png` — Reusable

Cancel button and Active / Inactive / Mock data / In Progress chips. Use as a visual language reference. Not a feature screen.

---

## Screen requirements extract (by feature)

Roles, fields, and actions below are copied from Screen Requirements only.

### Feature 1 — Maintain Company

| ID | Purpose | Roles | Fields | Actions | Validation / feedback | Device | Image |
|---|---|---|---|---|---|---|---|
| UI-1 | Create, view, update, or delete the single Company | Manager, Administrator (full); other roles view if authorized | Company ID (read-only), Name (required), Address, Phone, Email | Add (only if none exists), Edit, Save, Cancel, Delete (confirm) | Required name; duplicate company; not found; unauthorized; warehouses or history block delete; success/error | Desktop | Existing partial `Maintain Company.png` |

### Feature 2 — Maintain Warehouses

| ID | Purpose | Roles | Fields / columns | Actions | Validation | Device | Image |
|---|---|---|---|---|---|---|---|
| UI-2A | View and select warehouses | Manager, Administrator maintain; others view if authorized | Code, Name, Address, Phone, Status | Add, Edit, Delete (confirm), Close/Back | Empty list; delete blocked by inventory or history | Desktop | Combined partial `Maintain Warehouse.png` |
| UI-2B | Create or update warehouse | Same | ID (read-only), Company (read-only), Code, Name, Address, Phone, Active | Save, Cancel | Required code/name; unique code; company must exist | Desktop | Combined partial |

### Feature 3 — Maintain Inventory

UI-3A List (search/filter item, location, warehouse; view qty). UI-3B Add balance. UI-3C Physical count. UI-3D Adjustment (reason). UI-3E Move (source, destination, qty). UI-3F History. UI-3G Awaiting put away. Roles: inventory clerks / managers per spec. All desktop. All missing except wrong link to items/suppliers mock.

### Feature 4 — Maintain Individual Item

UI-4A List (item number, description, selling price, units per case, min stock, status). UI-4B Add. UI-4C Edit. UI-4D UPCs. UI-4E Item–supplier links. UI-4F Details. UI-4G Replenishment. Office roles. Desktop. Receiving Scan link is incorrect.

### Feature 5 — Maintain Suppliers

UI-5A List. UI-5B Add. UI-5C Edit. UI-5D Details. UI-5E Purchasing (account, terms, lead time). UI-5F Relationships. Purchasing Clerk / Manager / Administrator. Desktop. All missing as dedicated screens.

### Feature 6 — Maintain Customers

UI-6A List (search number/name, active filter, View/Add/Edit/Delete). UI-6B/C Add/Edit (number, name, business/delivery addresses, phone, email, contact, default route, active; ID read-only on edit). UI-6D Details. UI-6E Delivery information. UI-6F Delete/deactivate with dependency warnings. Office maintain; drivers/warehouse read-only delivery as specified. Desktop. Dashboard link is incorrect.

### Feature 7 and 8 — Order forms

UI-7A–UI-7G and UI-8A–UI-8G are complete after visual inspection. Parallel list / add / edit / form items / details / preview / delete-or-deactivate. Office purchasing (7) and customer-service (8). Desktop. Separate files; supplier vs customer entities differ. CL-7.1–CL-7.8 and CL-8.1–CL-8.10 remain unresolved.

### Feature 9 — Create Supplier Order

UI-9A–UI-9H are complete after visual inspection. Desktop purchasing. PD-9.1–PD-9.7 remain unresolved. Feature 7 forms are optional inputs; Feature 4 owns live Supplier Item prices; Feature 10 owns receiving.

### Feature 10 — Receive Supplier Order

UI-10A–UI-10G are complete after visual inspection. Handheld lookup, door, scan, discrepancy, and complete; desktop close and history. CL-10.1–CL-10.7 remain unresolved. Receiving records Quantity Received and does not increase stored bin inventory.

### Feature 11 — Put Away

UI-11A–UI-11J are complete after visual inspection. Handheld through completion; desktop movement history. Screen design clarifications remain unresolved. Stored inventory increases only after a confirmed Putaway Movement.

### Feature 12 — Receive Customer Orders

SCREEN-12.1–12.5 are complete after visual inspection. Desktop office entry. Feature 8 forms are optional inputs. Out-of-stock reporting is Feature 16, not a Feature 12 screen field.

### Feature 13 — Pick Customer Orders

SCREEN-13.1–13.8 are complete after visual inspection. Handheld through completion; desktop shortage review and history. Stored inventory decreases only on confirmed pick. Replenishment is request-only.

### Feature 14 — Ship Customer Orders

SCREEN-14.1–14.8 are complete after visual inspection. No shipping-door or carrier fields (not in Screen Requirements). Shipping does not deduct stored inventory.

### Feature 15 — Deliver Customer Orders

SCREEN-15.1–15.9 are complete after visual inspection. Driver handheld for 15.1–15.5; office desktop for assignment, reassignment, history, discrepancy review. Delivery does not deduct stored inventory.

### Features 16–19 — Reports

SCREEN-16.1–16.3, SCREEN-17.1–17.3, SCREEN-18.1–18.4, and SCREEN-19.1–19.4 are complete after visual inspection. Desktop reporting only. Empty, invalid, unauthorized, provisional, pending, and data-quality states are separate files where the spec required those messages. Feature 18 SCREEN-18.3 is reporting history (`report-delivery-history.png`), not Feature 15 operational history. Clarifications on Figma layout and whether Feature 19 data-quality is a separate screen remain unresolved.

---

## Legitimate reuse (do not omit required function)

| Pattern | Screens that may share a layout | Must stay distinct |
|---|---|---|
| Desktop shell (nav, header, user chip) | All office screens | Dashboard is not a substitute for list/forms |
| Component kit | Buttons, Active/Inactive, In Progress | `Reusable UI Components.png` is chrome only |
| Master-data list + search | UI-2A, 3A, 4A, 5A, 6A, 7A, 8A, 9D, 12.1 | Different columns and filters |
| Add / edit form | UI-2B, 4B/4C, 5B/5C, 6B/6C, 7B/7C, 8B/8C, 12.2 | Different fields; add vs edit (ID read-only) |
| Read-only details | UI-4F, 5D, 6D, 7E, 8E, 9E, 12.3 | Different entities |
| Confirm / deactivate dialog | UI-1 delete state, UI-6F, 7G, 8G, 12.4, 12.5 | Different copy and blockers |
| Handheld scan + quantity | UI-10C, 11D–11F, 13.3–13.4, 14.3–14.4, 15.3 | Receiving vs putaway vs pick vs ship vs deliver |
| History / audit | UI-3F, 9G, 10G, 11J, 13.8, 14.8, 15.8, 18.3 | Different filters and columns |
| Exception / discrepancy | UI-9H, 10D, 11H, 13.5, 13.7, 14.7, 15.4, 15.9 | Different workflows |
| Filtered report | 16.1, 17.1, 18.1, 19.1 | Different metrics; 16–19 are not one report |
| Feature 7 vs 8 order forms | Same screen sequence | Separate files; supplier vs customer forms |

Do **not** combine: inventory vs item master; Feature 3 movement vs Feature 11 putaway; Feature 9F vs Feature 10A (related PO lookup, different owners); Feature 15.8 vs Feature 18.3 without checking each spec’s columns.

---

## Recommended design batches

### Batch 1 — Company and warehouse (Features 1–2)

**Done (mockups, not application screens).** UI-1, UI-2A, and UI-2B are complete after visual inspection. Original `Maintain Company.png` and `Maintain Warehouse.png` were not overwritten.

Generated:

- `docs/ui/company-maintenance.png`
- `docs/ui/company-maintenance-empty.png`
- `docs/ui/company-maintenance-add.png`
- `docs/ui/company-maintenance-edit.png`
- `docs/ui/company-maintenance-saving.png`
- `docs/ui/company-maintenance-delete.png`
- `docs/ui/warehouse-list.png`
- `docs/ui/warehouse-list-empty.png`
- `docs/ui/warehouse-list-delete.png`
- `docs/ui/warehouse-add.png`
- `docs/ui/warehouse-edit.png`

### Batch 2 — Inventory and items (Features 3–4)

**Done (mockups, not application screens).** UI-3A–UI-3G and UI-4A–UI-4G are complete after visual inspection. Incorrect Feature 3 and Feature 4 embeddings were replaced in the specs. Original `Maintain Items and Suppliers.png` and `Handheld/Receiving Scan.png` were not deleted.

Generated:

- `docs/ui/inventory-list.png`
- `docs/ui/inventory-list-empty.png`
- `docs/ui/inventory-add.png`
- `docs/ui/inventory-count.png`
- `docs/ui/inventory-adjustment.png`
- `docs/ui/inventory-movement.png`
- `docs/ui/inventory-history.png`
- `docs/ui/inventory-awaiting-putaway.png`
- `docs/ui/item-list.png`
- `docs/ui/item-list-delete.png`
- `docs/ui/item-add.png`
- `docs/ui/item-edit.png`
- `docs/ui/item-upcs.png`
- `docs/ui/item-suppliers.png`
- `docs/ui/item-details.png`
- `docs/ui/item-replenishment.png`

### Batch 3 — Suppliers and customers (Features 5–6)

**Done (mockups, not application screens).** UI-5A–UI-5F and UI-6A–UI-6F are complete after visual inspection. Feature 6 no longer embeds the Warehouse Dashboard. Original `Warehouse Dashboard.png` was not deleted. CL-5.1–CL-5.6 and CL-6.1–CL-6.5 remain unresolved on the mockups.

Generated:

- `docs/ui/supplier-list.png`
- `docs/ui/supplier-list-delete.png`
- `docs/ui/supplier-add.png`
- `docs/ui/supplier-edit.png`
- `docs/ui/supplier-details.png`
- `docs/ui/supplier-purchasing.png`
- `docs/ui/supplier-relationships.png`
- `docs/ui/customer-list.png`
- `docs/ui/customer-add.png`
- `docs/ui/customer-edit.png`
- `docs/ui/customer-details.png`
- `docs/ui/customer-delivery.png`
- `docs/ui/customer-delivery-driver.png`
- `docs/ui/customer-status.png`

### Batch 4 — Order forms (Features 7–8)

**Done (mockups, not application screens).** UI-7A–UI-7G and UI-8A–UI-8G are complete after visual inspection. CL-7.1–CL-7.8 and CL-8.1–CL-8.10 remain unresolved on the mockups.

Generated:

- `docs/ui/supplier-order-form-list.png`
- `docs/ui/supplier-order-form-list-empty.png`
- `docs/ui/supplier-order-form-list-unauthorized.png`
- `docs/ui/supplier-order-form-add.png`
- `docs/ui/supplier-order-form-edit.png`
- `docs/ui/supplier-order-form-items.png`
- `docs/ui/supplier-order-form-details.png`
- `docs/ui/supplier-order-form-preview.png`
- `docs/ui/supplier-order-form-preview-blocked.png`
- `docs/ui/supplier-order-form-status.png`
- `docs/ui/supplier-order-form-status-unused.png`
- `docs/ui/customer-order-form-list.png`
- `docs/ui/customer-order-form-list-empty.png`
- `docs/ui/customer-order-form-list-unauthorized.png`
- `docs/ui/customer-order-form-add.png`
- `docs/ui/customer-order-form-edit.png`
- `docs/ui/customer-order-form-items.png`
- `docs/ui/customer-order-form-details.png`
- `docs/ui/customer-order-form-preview.png`
- `docs/ui/customer-order-form-preview-blocked.png`
- `docs/ui/customer-order-form-status.png`
- `docs/ui/customer-order-form-status-unused.png`

### Batch 5 — Purchasing, receiving, putaway (Features 9–11)

**Done (mockups, not application screens).** UI-9A–UI-9H, UI-10A–UI-10G, and UI-11A–UI-11J are complete after visual inspection. Original `docs/ui/Handheld/Receiving Scan.png` was not overwritten. PD-9.x, CL-10.x, and Feature 11 screen-design clarifications remain unresolved.

Generated desktop:

- `docs/ui/supplier-replenishment.png`
- `docs/ui/supplier-order-create.png`
- `docs/ui/supplier-order-review.png`
- `docs/ui/supplier-order-list.png`
- `docs/ui/supplier-order-details.png`
- `docs/ui/supplier-order-receiving-lookup.png`
- `docs/ui/supplier-order-audit.png`
- `docs/ui/supplier-purchasing-exceptions.png`
- `docs/ui/receive-supplier-order-close.png`
- `docs/ui/receive-supplier-order-history.png`
- `docs/ui/putaway-history.png`

Generated handheld:

- `docs/ui/Handheld/receive-supplier-order-lookup.png`
- `docs/ui/Handheld/receive-supplier-order-lookup-unknown.png`
- `docs/ui/Handheld/receive-supplier-order-door.png`
- `docs/ui/Handheld/receive-supplier-order-door-mismatch.png`
- `docs/ui/Handheld/receive-supplier-order-scan.png`
- `docs/ui/Handheld/receive-supplier-order-scan-invalid.png`
- `docs/ui/Handheld/receive-supplier-order-scan-connection.png`
- `docs/ui/Handheld/receive-supplier-order-discrepancies.png`
- `docs/ui/Handheld/receive-supplier-order-complete.png`
- `docs/ui/Handheld/receive-supplier-order-complete-blocked.png`
- `docs/ui/Handheld/putaway-assignments.png`
- `docs/ui/Handheld/putaway-assignments-empty.png`
- `docs/ui/Handheld/putaway-assignment-details.png`
- `docs/ui/Handheld/putaway-sequence.png`
- `docs/ui/Handheld/putaway-item-verify.png`
- `docs/ui/Handheld/putaway-item-verify-error.png`
- `docs/ui/Handheld/putaway-bin-verify.png`
- `docs/ui/Handheld/putaway-bin-verify-error.png`
- `docs/ui/Handheld/putaway-quantity.png`
- `docs/ui/Handheld/putaway-quantity-unconfirmed.png`
- `docs/ui/Handheld/putaway-alternative-location.png`
- `docs/ui/Handheld/putaway-blocked.png`
- `docs/ui/Handheld/putaway-completion.png`
- `docs/ui/Handheld/putaway-completion-blocked.png`

### Batch 6 — Customer orders, picking, shipping, delivery (Features 12–15)

**Done (mockups, not application screens).** SCREEN-12.1–12.5, SCREEN-13.1–13.8, SCREEN-14.1–14.8, and SCREEN-15.1–15.9 are complete after visual inspection. Original `docs/ui/Handheld/Picking Scan.png` was not overwritten. Feature 12–15 pending clarifications remain unresolved.

Generated desktop:

- `docs/ui/customer-order-list.png`
- `docs/ui/customer-order-list-empty.png`
- `docs/ui/customer-order-entry.png`
- `docs/ui/customer-order-detail.png`
- `docs/ui/customer-order-release.png`
- `docs/ui/customer-order-cancel.png`
- `docs/ui/picking-shortage-review.png`
- `docs/ui/picking-history.png`
- `docs/ui/shipping-available-orders.png`
- `docs/ui/shipping-preparation.png`
- `docs/ui/shipping-packaging.png`
- `docs/ui/shipping-completion.png`
- `docs/ui/shipping-exceptions.png`
- `docs/ui/shipping-history.png`
- `docs/ui/delivery-assignment-admin.png`
- `docs/ui/delivery-reassignment.png`
- `docs/ui/delivery-history.png`
- `docs/ui/delivery-discrepancy-review.png`

Generated handheld:

- `docs/ui/Handheld/picking-available-work.png`
- `docs/ui/Handheld/picking-available-work-empty.png`
- `docs/ui/Handheld/picking-assignment.png`
- `docs/ui/Handheld/picking-instruction.png`
- `docs/ui/Handheld/picking-unconfirmed.png`
- `docs/ui/Handheld/picking-barcode-verify.png`
- `docs/ui/Handheld/picking-barcode-location-error.png`
- `docs/ui/Handheld/picking-barcode-item-error.png`
- `docs/ui/Handheld/picking-shortage.png`
- `docs/ui/Handheld/picking-completion.png`
- `docs/ui/Handheld/shipping-item-verify.png`
- `docs/ui/Handheld/shipping-item-verify-error.png`
- `docs/ui/Handheld/shipping-quantity.png`
- `docs/ui/Handheld/delivery-assigned.png`
- `docs/ui/Handheld/delivery-assigned-empty.png`
- `docs/ui/Handheld/delivery-details.png`
- `docs/ui/Handheld/delivery-quantity.png`
- `docs/ui/Handheld/delivery-discrepancy.png`
- `docs/ui/Handheld/delivery-outcome.png`

### Batch 7 — Exceptions and reporting (Features 16–19)

**Done (mockups, not application screens).** SCREEN-16.1–16.3, SCREEN-17.1–17.3, SCREEN-18.1–18.4, and SCREEN-19.1–19.4 are complete after visual inspection. Batches 1–6 files were not overwritten.

Generated:

- `docs/ui/report-out-of-stock.png`
- `docs/ui/report-out-of-stock-details.png`
- `docs/ui/report-out-of-stock-empty.png`
- `docs/ui/report-out-of-stock-invalid.png`
- `docs/ui/report-out-of-stock-unauthorized.png`
- `docs/ui/report-supplier-differences.png`
- `docs/ui/report-supplier-difference-details.png`
- `docs/ui/report-supplier-differences-empty.png`
- `docs/ui/report-supplier-differences-invalid.png`
- `docs/ui/report-supplier-differences-provisional.png`
- `docs/ui/report-supplier-differences-unauthorized.png`
- `docs/ui/report-delivery-differences.png`
- `docs/ui/report-delivery-differences-incomplete.png`
- `docs/ui/report-delivery-difference-details.png`
- `docs/ui/report-delivery-history.png`
- `docs/ui/report-delivery-differences-empty.png`
- `docs/ui/report-delivery-differences-invalid.png`
- `docs/ui/report-delivery-differences-pending.png`
- `docs/ui/report-delivery-differences-unauthorized.png`
- `docs/ui/report-monthly-shipping.png`
- `docs/ui/report-monthly-shipping-details.png`
- `docs/ui/report-monthly-shipping-data-quality.png`
- `docs/ui/report-monthly-shipping-empty.png`
- `docs/ui/report-monthly-shipping-missing-month.png`
- `docs/ui/report-monthly-shipping-missing-year.png`
- `docs/ui/report-monthly-shipping-invalid-month.png`
- `docs/ui/report-monthly-shipping-invalid-year.png`
- `docs/ui/report-monthly-shipping-unauthorized.png`
- `docs/ui/report-monthly-shipping-warehouse-denied.png`

---

## Totals

| Metric | Count |
|---|---|
| Required screens (explicit Screen IDs) | **112** |
| Existing original image files (preserved) | **7** |
| New Batch 1 mockup files | **11** (UI-1 plus empty, add, edit, saving, and delete-confirmation states) |
| New Batch 2 mockup files | **16** |
| New Batch 3 mockup files | **14** (12 Screen IDs plus supplier delete-blocked and driver delivery states) |
| New Batch 4 mockup files | **22** (14 Screen IDs plus empty, unauthorized, inactive-preview, and unused-delete states) |
| New Batch 5 mockup files | **35** (25 Screen IDs plus unknown PO, warehouse mismatch, scan errors, blocked completion, empty putaway, verify errors, unconfirmed movement) |
| New Batch 6 mockup files | **37** (30 Screen IDs plus empty lists, scan errors, unconfirmed pick, and empty assigned deliveries) |
| New Batch 7 mockup files | **29** (14 Screen IDs plus empty, invalid, unauthorized, provisional, pending, incomplete-history, missing-month/year, invalid month/year, and warehouse-denied states) |
| Complete required screens | **112** (Features 1–19) |
| Partially complete required screens | **0** |
| Incorrectly linked embeddings | **0** |
| Missing dedicated mockups | **0** |
| Newly generated PNG files (Batches 1–7, including verification states) | **164** |
| Original Figma image files (preserved, not overwritten) | **7** |
| Unmapped extras | Dashboard; reusable component sheet |
| Reuse opportunities | Desktop shell; list/search; add/edit; details; confirm dialogs; handheld scan+qty; history; report+empty state; Feature 7/8 form sequence |

**These files are design mockups, not implemented application screens.** All 112 required Screen IDs have been visually inspected against Screen Requirements. Spec clarifications remain unresolved and were not decided in mockups. C4 diagrams are a separate deliverable.

### Final verification notes

- UI-1 **Saving** is an explicit Screen State: `docs/ui/company-maintenance-saving.png`.
- SCREEN-18.1 incomplete Shipment/Delivery history warning: `docs/ui/report-delivery-differences-incomplete.png`.
- SCREEN-19.4 missing-year, invalid-month, and invalid-year messages have dedicated files; missing-month is unchanged.
- Markdown embeddings use `docs/ui/` and `docs/ui/Handheld/`.
- Original Figma files remain: `Maintain Company.png`, `Maintain Warehouse.png`, `Maintain Items and Suppliers.png`, `Warehouse Dashboard.png`, `Handheld/Receiving Scan.png`, `Handheld/Picking Scan.png`, `WMS/Reusable UI Components.png`.
