# C4 architecture diagrams

**Branch:** `design-final`  
**Status:** Proposed design. These diagrams are not implemented infrastructure.

The Warehouse Management System is documented with the C4 model at three levels. Feature specifications authorize behavior. ADRs record technology and integrity choices. These diagrams show structure only.

## Diagrams

| Level | Purpose | Exported PNG | Editable Draw.io source |
|---|---|---|---|
| 1 — System Context | People and the software system | [Warehouse-C4-System-Context.png](./Warehouse-C4-System-Context.png) | [Warehouse-C4-System-Context.drawio](./Warehouse-C4-System-Context.drawio) |
| 2 — Containers | Web application, backend API, database | [Warehouse-C4-Container1.drawio.png](./Warehouse-C4-Container1.drawio.png) | [Warehouse-C4-Container.drawio](./Warehouse-C4-Container.drawio) |
| 3 — Components | Logical backend components for Features 1–19 | [Warehouse-C4-Component.drawio.png](./Warehouse-C4-Component.drawio.png) | [Warehouse-C4-Component.drawio](./Warehouse-C4-Component.drawio) |

The Level 2 PNG filename `Warehouse-C4-Container1.drawio.png` is retained so existing ADR and README links keep working.

Earlier exports are preserved under [original/](./original/).

Copies of the Draw.io sources also exist at the repository root (`Warehouse-C4-*.drawio`). Prefer the files in this folder.

### Scope

| In scope | Out of scope |
|---|---|
| Internal employees grouped by documented roles | Supplier or customer portals |
| One software system | Payment, invoicing, or carrier services |
| Three containers from ADR-0001–0003 | Extra microservices, brokers, load balancers |
| Logical backend components | One container per UI screen |
| Proposed Vue / Node / MySQL stack | Claim that the stack is deployed |

## Proposed technology choices

These match ADR-0001, ADR-0002, and ADR-0003. They are proposed, not proven in production.

| Container | Proposed technologies |
|---|---|
| Warehouse Web Application | Vue 3, Vuetify, Vite, Vue Router, Axios. Desktop and handheld browsers. |
| Warehouse Backend API | Node.js, Express, Sequelize. REST under `/api`. HTTPS JSON. |
| Warehouse Database | MySQL, InnoDB. Relational constraints and transactions. |

The web application does not connect to MySQL. Handheld barcode capture uses the device camera in the same web application (ADR-0005).

## Related ADRs

| ADR | How it appears in the diagrams |
|---|---|
| ADR-0001 Three-tier architecture | Level 2 containers |
| ADR-0002 REST API | Web application → backend HTTPS JSON `/api` |
| ADR-0003 Relational database | Backend → MySQL through Sequelize |
| ADR-0004 Role-based access | Level 1 people; Security component |
| ADR-0005 Barcode scanning | Handheld users of the web application |
| ADR-0006 Paperless workflows | System purpose; no paper systems as containers |
| ADR-0007 Company and multi-warehouse | Company/warehouse administration component |
| ADR-0008 Warehouse isolation | Security and warehouse access; backend-enforced |
| ADR-0009 Inventory transaction integrity | Receiving vs putaway vs pick vs ship vs deliver notes |
| ADR-0010 Barcode errors and reliability | Data access rejects unconfirmed or duplicate work |

## Inventory abstraction (Level 3)

The component diagram states the documented stored-inventory rule and does not try to draw every FR:

- Receiving records Quantity Received and does **not** increase stored bin inventory.
- Confirmed putaway **increases** stored inventory.
- Confirmed picking **decreases** stored inventory once.
- Shipping and delivery do **not** deduct stored inventory again.

Pending feature clarifications are not resolved here.

## Editing and export

1. Open a `.drawio` file in [diagrams.net](https://app.diagrams.net/) or the Draw.io desktop app.
2. Export PNG into this folder using the filenames in the table above if the diagram changes.
3. Keep `Warehouse-C4-Container1.drawio.png` as the Level 2 export name unless ADR links are updated in a separate change.

A diagrams.net CLI exporter was not available in this environment. PNG exports were produced from equivalent static layouts so the files remain readable in GitHub and Markdown. The `.drawio` XML is the editable source.

Level 1 PNG shows each person with a **Uses → WMS** relationship chip. The Draw.io source also has named connectors from each person to the software system. Level 2 PNG shows HTTPS and Sequelize relationships. Level 3 PNG states inventory rules in the caption; the Draw.io source includes the corresponding named edges.

## Remaining architecture clarifications

- ADRs remain **Proposed**, not Accepted.
- Feature specs still contain unresolved stakeholder items (layout, some receiving/shipping/delivery details, reporting data-quality placement). Diagrams do not decide those items.
- Whether picked units occupy a staging inventory balance is unspecified (ADR-0009).
- Inter-warehouse transfer as ordinary bin movement remains unresolved (Feature 3).
