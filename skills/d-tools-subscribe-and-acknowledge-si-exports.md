---
name: d-tools-subscribe-and-acknowledge-si-exports
description: >-
  Consume everything a D-Tools System Integrator user exports — projects, change orders, tasks, service orders,
  purchase orders, service plans, time sheets, product catalogs and clients — and acknowledge each one so it is
  not redelivered.
api: D-Tools System Integrator (SI) API
base_url: https://api.d-tools.com/si
generated: '2026-08-11'
method: generated
source: openapi/d-tools-si-api-openapi.yml, https://docs.d-tools.com/en/articles/9225625-d-tools-si-api-overview
operations:
  - GET /Subscribe/Projects
  - GET /Subscribe/Projects/{id}
  - GET /Subscribe/Projects/GetProjectByMessageId
  - PUT /Subscribe/Projects/MarkAsImported
  - PUT /Subscribe/Projects/MarkAsImportedByMessageId
  - GET /Subscribe/Tasks
  - PUT /Subscribe/Task/MarkAsImported
  - GET /Subscribe/ServiceOrders
  - PUT /Subscribe/ServiceOrders/MarkAsImported
  - GET /Subscribe/PurchaseOrders
  - PUT /Subscribe/PurchaseOrders/MarkAsImported
  - GET /Subscribe/ServicePlans
  - PUT /Subscribe/ServicePlans/MarkAsImported
  - GET /Subscribe/TimeSheets
  - PUT /Subscribe/TimeSheets/MarkAsImported
  - GET /Subscribe/ProductCatalogs
  - PUT /Subscribe/ProductCatalogs/MarkAsImported
  - GET /Subscribe/Clients
  - POST /Subscribe/Clients/MarkAsImported
note: >-
  The SI OpenAPI declares no operationId on any operation, so operations are identified by method and path — both
  taken verbatim from the specification.
---

# Subscribe to D-Tools SI exports

## The shape of this API

Every `/Subscribe/*` family is a **poll-and-acknowledge queue**, not a query interface. You read what an SI user
has exported, you process it, and you acknowledge it. If you skip the acknowledgement you will receive the same
records again on the next poll — forever.

## The loop

1. **Poll.** `GET /Subscribe/{Family}` with `includeImported=false`, `pageNumber` and `pageSize`.
   Nine families follow this shape: Projects, PartialProjects, Tasks, ServiceOrders, PurchaseOrders, ServicePlans,
   TimeSheets, ProductCatalogs, Clients.
2. **Process transactionally on your side.** Commit the record into your system before step 3. If step 3 fails you
   want a duplicate delivery, not a lost one.
3. **Acknowledge.** Call the matching `MarkAsImported` for that family. Note the shapes differ:
   Projects offers both `MarkAsImported` (by project id) and `MarkAsImportedByMessageId`; Clients uses
   `POST /Subscribe/Clients/MarkAsImported` and accepts **at most 100 client ids** per call.
4. **Repeat on a timer.** Use `publishedOnUnixTimeMs` as your watermark so you do not re-scan the whole backlog.

## Fetching one specific thing

- By entity id: `GET /Subscribe/Projects/{id}`, `GET /Subscribe/Tasks/{id}`,
  `GET /Subscribe/ServiceOrders/{id}`, `GET /Subscribe/PurchaseOrders/{id}`,
  `GET /Subscribe/ServicePlans/{id}`, `GET /Subscribe/TimeSheets/{id}`,
  `GET /Subscribe/ProductCatalogs/{id}`.
- By message id: `GET /Subscribe/Projects/GetProjectByMessageId`.
- Tasks for a project: `GET /Subscribe/Tasks/ByProject/{projectId}`.
- Bulk clients: `POST /Subscribe/Clients/ClientList` — also capped at **100 ids**.

## Shrinking large project payloads

`GET /Subscribe/Projects` accepts `aggregateBy` with any of `Item`, `Location`, `System`, `Phase`. Items collapse
into one row **only** when `TypeId`, `LaborType`, `Manufacturer`, `Model`, `PackageName`, `PartNumber`, `IsOfe`,
`IsNonBillable`, `UnitCost`, `UnitPrice`, `LaborHours`, `IsTaxable`, `TaxId` and `Vendor` all match exactly. Any
difference splits the row.

When reading quantities, use both fields SI v18 introduced:
`TotalQuantity = Item Quantity x Parent Item Quantity x Package Item Quantity x Solution Item Quantity`.
For bulk wire, `Quantity` = wire length x total quantity. For variable labor, `Quantity` = labor hours x total
quantity. For everything else, `Quantity` = `TotalQuantity`.

## Rules you must apply yourself

- **An empty result is ambiguous.** It means nothing has been *exported*, not that nothing exists. If a customer
  says data is missing, the first question is whether their SI automation scheme is exporting at all.
- **No error contract, no rate limits, no versioning.** See the publish skill — the same three gaps apply.
- **Acknowledge last, never first.** There is no transaction spanning the read and the acknowledgement.
