# Quality attributes

App-wide non-functional targets for **this** product.

**Teaching policy:** Specs say *what* to build. This table says *how good* the system should be. Only **Accepted** rows (and feature **Requirements (FR-00N)** / **Success Criteria (SC-00N)**) constrain implementation. **Deferred** is the quality backlog / example. **Out of scope** is what not to build. See [`.cursor/rules/quality-attributes.mdc`](../../.cursor/rules/quality-attributes.mdc).

## Column meanings

| Column | Meaning |
|--------|---------|
| **Target** | Measure or bar — prefer a **number**. Illustrative until Status is **Accepted** and tests enforce it. |
| **Approach** | How the target is realized or limited |
| **Status** | **Accepted** / **Accepted (minimal)** / **Deferred** / **Out of scope** (see below) |
| **Links** | ADR (why), Cursor rule (how), code path, or **—** |

## Status values

| Status | Meaning |
|--------|---------|
| **Accepted** | In force — do not regress |
| **Accepted (minimal)** | Thin bar in force — do not expand |
| **Deferred** | Documented example — not a coding requirement unless a feature spec says so |
| **Out of scope** | Do not invent |

## Links column

| Link type | When |
|-----------|------|
| ADR | Approach decision |
| Cursor rule | Day-to-day agent/code constraint |
| Code path | Concrete implementation |
| **—** | No artifact yet |

| Attribute | Target | Approach | How we verify | Status | Links |
|-----------|--------|----------|---------------|--------|-------|
| **Security and Authorization** | Proposed: **100%** of protected API routes require authentication; **0** unauthorized cross-warehouse accesses in authorization tests; **0** unauthorized item-master modifications in permission tests | Backend RBAC and warehouse assignments; HTTPS for deployed frontend-to-backend communication; salted password hashing | Authentication, authorization, and cross-warehouse permission tests | Deferred | [ADR-0002](../adr/0002-rest-api.md), [ADR-0004](../adr/0004-role-based-access.md), [ADR-0008](../adr/0008-cross-warehouse-data-isolation.md) |
| **Performance** | Proposed: ≥ **95%** of ordinary user requests complete within **2 s**; ≥ **95%** of barcode validations complete within **1 s**; standard warehouse reports complete within **10 s** on an agreed test dataset; ≥ **50** concurrent users under the proposed initial workload | Three-tier Vue / Express / MySQL architecture with a REST `/api` | Load testing and response-time measurements (not yet executed as an Accepted bar) | Deferred | [ADR-0001](../adr/0001-three-tier-architecture.md), [ADR-0002](../adr/0002-rest-api.md), [ADR-0003](../adr/0003-relational-database.md) |
| **Warehouse Operational Throughput** | Proposed initial target: ≥ **30** confirmed scan operations per minute per active scanning device during a controlled test; measure receiving and picking scan-processing throughput separately | Count only system-confirmed scans; exclude physical travel and manual exception-resolution time; document workload, device, network, and test dataset | Repeatable warehouse workflow tests and load tests | Deferred | [ADR-0005](../adr/0005-barcode-scanning.md), [ADR-0010](../adr/0010-barcode-error-handling.md) |
| **Inventory Accuracy** | Proposed: ≥ **99.5%** agreement between recorded and physically counted quantities in a controlled inventory audit, measured as the percentage of audited item-location records whose recorded quantities exactly match physical counts | Relational warehouse-scoped inventory records and transactional updates; physical accuracy also depends on operational procedures and employee compliance | Controlled receiving, putaway, picking, shipping, and inventory reconciliation scenarios | Deferred | [ADR-0003](../adr/0003-relational-database.md), [ADR-0007](../adr/0007-company-multi-warehouse.md), [ADR-0009](../adr/0009-inventory-transaction-integrity.md) |
| **Inventory Transaction Integrity** | Proposed: **0** partially committed inventory transactions in failure tests; **0** duplicate inventory changes when the same operation identifier is submitted repeatedly; **0** unauthorized negative inventory quantities; traceability for successful inventory-changing operations | MySQL InnoDB transactions, database constraints, concurrency controls, and operation identifiers | Rollback, concurrent-update, duplicate-submission, and database integration tests | Deferred | [ADR-0003](../adr/0003-relational-database.md), [ADR-0008](../adr/0008-cross-warehouse-data-isolation.md), [ADR-0009](../adr/0009-inventory-transaction-integrity.md), [ADR-0010](../adr/0010-barcode-error-handling.md) |
| **Barcode Accuracy and Error Handling** | Proposed: reject **100%** of known invalid, unknown, mismatched, and unauthorized location barcodes in the defined test cases; **0** inventory modifications from rejected barcode operations | Distinguish individual-item UPCs, case-level barcodes, and storage-location barcodes; validate case quantities from item packaging information; backend barcode validation; understandable error and correction messages | Defined barcode error test cases; confirm rejected scans do not change inventory | Deferred | [ADR-0005](../adr/0005-barcode-scanning.md), [ADR-0010](../adr/0010-barcode-error-handling.md) |
| **Handheld Device Reliability** | Proposed: preserve **100%** of confirmed inventory transactions during simulated network and device interruptions; **0** unconfirmed operations incorrectly displayed as completed in interruption tests | Online-first architecture; recover confirmed task progress after reconnecting; prevent duplicate inventory changes during retries | Simulated interruption, reconnect, and retry tests | Deferred | [ADR-0006](../adr/0006-paperless-workflows.md), [ADR-0009](../adr/0009-inventory-transaction-integrity.md), [ADR-0010](../adr/0010-barcode-error-handling.md) |
| **Availability** | Proposed: **99.5%** monthly availability, excluding approved maintenance | Three-tier deployment of the web application, backend API, and database | Service availability monitoring (not a measured result) | Deferred | [ADR-0001](../adr/0001-three-tier-architecture.md) |
| **Backup and Recovery** | Proposed: database backups at least **once daily**; verify backup completion and periodically test restoration | Relational database backup and restore procedures; no recovery-time or recovery-point objective is established | Backup-completion checks and periodic restore tests | Deferred | [ADR-0003](../adr/0003-relational-database.md), [ADR-0009](../adr/0009-inventory-transaction-integrity.md) |
| **Observability and Auditability** | Proposed: record **all** successful inventory-changing transactions with responsible user, warehouse, item, quantity, operation type, and timestamp; log unexpected application errors without exposing passwords, tokens, or other secrets | Inventory transaction history plus application error logging | Transaction-history inspection and controlled failure tests | Deferred | [ADR-0009](../adr/0009-inventory-transaction-integrity.md), [ADR-0010](../adr/0010-barcode-error-handling.md) |
| **Usability** | Proposed: role-appropriate navigation; understandable confirmation and validation messages; routine receiving, putaway, and picking on compatible handheld devices; routine warehouse task lists shall not require printing | Paperless, role-based warehouse workflows | Representative warehouse user-acceptance scenarios | Deferred | [ADR-0004](../adr/0004-role-based-access.md), [ADR-0005](../adr/0005-barcode-scanning.md), [ADR-0006](../adr/0006-paperless-workflows.md) |
| **Accessibility (a11y)** | Proposed: aim **WCAG 2.2 AA** for primary web workflows | Keyboard navigation, contrast, and labeling on primary web screens; do not claim accessibility compliance before testing | Keyboard, contrast, labeling, and accessibility testing | Deferred | — |
| **Maintainability** | **100%** Gherkin scenarios mapped before merge; `npm test` green | Cursor rules + feature specs as source of truth; separate presentation, business logic, and data access; keep API and feature reference documentation current | Merge checklist; `npm test` | Accepted | [ADR-0001](../adr/0001-three-tier-architecture.md), [ADR-0002](../adr/0002-rest-api.md), [framework.md](../../features/framework.md), [quality-attributes.mdc](../../.cursor/rules/quality-attributes.mdc) |
| **Scalability** | Proposed: support additional warehouses in the same company without a separate application deployment; keep warehouse-specific inventory and operational records | Centralized application with company/warehouse data model; independent scaling of presentation, application, and data tiers where appropriate | Multi-warehouse design review and capacity testing | Deferred | [ADR-0001](../adr/0001-three-tier-architecture.md), [ADR-0007](../adr/0007-company-multi-warehouse.md) |
| **Compatibility** | Proposed: approved desktop browsers, compatible warehouse scanning devices, and approved handheld screen sizes | Device-agnostic barcode workflows; do not invent specific scanner hardware models | Browser and device compatibility testing | Deferred | [ADR-0005](../adr/0005-barcode-scanning.md), [ADR-0010](../adr/0010-barcode-error-handling.md) |
| **Internationalization (i18n)** | **1** locale | Multilingual functionality is not in initial scope | N/A | Out of scope | — |
| **Offline Processing** | Full offline inventory transaction processing and synchronization are not in the initial implementation | Online-first confirmation of inventory-changing operations; driver offline recording remains an unresolved business requirement | N/A for full offline sync; do not invent an offline platform | Out of scope | [ADR-0010](../adr/0010-barcode-error-handling.md) |

Numerical values in **Deferred** rows are **proposed targets**, not measured system performance. They do **not** override mandatory feature **Requirements (FR-00N)** / **Success Criteria (SC-00N)**. A **Deferred** row is not **Accepted** until review and matching verification exist.

---

## Feature-local NFRs

If only one feature needs a bar:

1. Put it in that feature’s **Requirements (FR-00N)** or **Success Criteria (SC-00N)**.
2. Add Gherkin when tests must prove it.
3. Optionally link from a row here (“see Feature N **FR-00N** / **SC-00N**”).

See [feature spec template](../../features/framework.md#feature-spec-template) in the teaching repo.

---

## Changing a bar

1. Edit **Target**, **Approach**, **Status**, **Links**. Prefer a number in **Target**.
2. **Approach** change → [ADR](../adr/README.md); add to **Links**.
3. Agent coding constraint → `.cursor/rules/`; add to **Links**.
4. API/schema change → `features/reference/` in the same feature PR ([Agent implementation request](../../features/framework.md#agent-implementation-request)).
5. **Deferred** → **Accepted** only with matching verification.
