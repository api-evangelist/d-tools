---
name: d-tools-sync-cloud-clients-and-opportunities
description: >-
  Read and write D-Tools Cloud clients, opportunities, quotes and projects over the REST API, with the pagination,
  date-window and dual-credential rules the docs impose.
api: D-Tools Cloud API
base_url: https://dtcloudapi.d-tools.cloud
generated: '2026-08-11'
method: generated
source: >-
  openapi/d-tools-cloud-api-openapi.yml,
  https://docs.d-tools.cloud/en/collections/7640732-cloud-api-documentation
operations:
  - GET /api/v1/Clients/GetClients
  - GET /api/v1/Clients/GetClient
  - POST /api/v1/Clients/CreateClient
  - PUT /api/v1/Clients/UpdateClient
  - GET /api/v1/Opportunities/GetOpportunities
  - GET /api/v1/Opportunities/GetOpportunity
  - POST /api/v1/Opportunities/CreateOpportunity
  - PUT /api/v1/Opportunities/UpdateOpportunity
  - GET /api/v1/Quotes/GetQuotes
  - GET /api/v1/Quotes/GetQuote
  - GET /api/v1/Projects/GetProjects
  - GET /api/v1/Projects/GetProject
  - PUT /api/v1/Projects/UpdateProject
  - GET /api/v1/ChangeOrders/GetChangeOrders
  - GET /api/v1/PurchaseOrders/GetPurchaseOrders
  - GET /api/v1/ServiceContracts/GetServiceContracts
  - GET /api/v1/TimeEntries/GetTimeEntries
  - GET /api/v1/Products/GetProducts
  - PUT /api/v1/Products/UpdateProductPrices
note: >-
  The Cloud OpenAPI declares no operationId and no summary on any of its 26 operations, so operations are
  identified by method and path — both taken verbatim from the specification.
---

# Sync D-Tools Cloud clients, opportunities and projects

## Every request carries two credentials

Both headers, on every call, or you get `401`:

```
X-API-Key: <your tenant key>
Authorization: Basic <the fixed value D-Tools publishes in its authentication article>
```

The `X-API-Key` is generated in-app under *Settings > Integration > Developer > API Keys*. The `Authorization`
value is a single constant D-Tools publishes in its own public documentation and tells every customer to reuse
verbatim; it is identical across all tenants and provides no separation. Read it from
<https://docs.d-tools.cloud/en/articles/8756132-authentication> at build time — do not hard-code a copy from
anywhere else, and do not treat it as a secret you own. Only the `X-API-Key` is yours.

You may hold at most **5 active API keys** per account.

## Reading a list

`GET` list endpoints take `page`, `pageSize`, `sort`, `search` and `includeTotalCount`. Set
`includeTotalCount=true` on the first page so you know how far to paginate, then drop it. `GetClients` returns at
most **500** records per request.

For incremental sync use the date windows rather than re-scanning:
`fromCreatedDate` / `toCreatedDate` and `fromModifiedDate` / `toModifiedDate`. Store the high-water mark yourself.

## Writing

- Clients: `POST /api/v1/Clients/CreateClient`, then `PUT /api/v1/Clients/UpdateClient`.
- Opportunities: `POST /api/v1/Opportunities/CreateOpportunity`, then
  `PUT /api/v1/Opportunities/UpdateOpportunity`.
- Projects: `PUT /api/v1/Projects/UpdateProject` only — projects cannot be created over the API.
- Products: prices, barcodes and statuses are updatable
  (`UpdateProductPrices`, `UpdateProductBarcodes`, `UpdateProductStatuses`); the product itself is not creatable.
- Quotes, Change Orders, Purchase Orders, Service Contracts, Time Entries and Files are **read-only**.

## Errors

Non-2xx responses carry an ASP.NET Core `ProblemDetails` body (`type`, `title`, `status`, `detail`, `instance`)
served as `application/json`, not `application/problem+json` — do not content-negotiate on the problem type.

| Status | What it means | What to do |
|---|---|---|
| 400 | Missing or malformed query parameters | Fix the request; the body's `detail` names the field |
| 401 | Bad or missing credentials | Check both headers; check the key is still active and you are within 5 keys |
| 404 | Entity id does not exist on this tenant | Re-resolve the id |
| 409 | Conflict on a create/update | Declared in the spec, **undocumented by D-Tools** — log the body and treat as non-retryable |
| 500 | Server-side | Back off and retry |

## Rules you must apply yourself

- **No idempotency.** No `Idempotency-Key`, no dedupe window. A retried `CreateClient` after a timeout can create
  a duplicate. Search by your own external key before creating.
- **Rate limits are invisible at runtime.** 120 calls/minute and 10,000 calls/day per key are documented, but the
  API returns **no** `RateLimit-*` headers, no `Retry-After`, and declares no `429`. Count your own calls and
  throttle client-side; you will not be told you are close.
- **No request-id header**, so cross-system tracing has to be built on your side.
- **Webhooks are configured in the UI, not here.** They exist under the same Developer settings screen, but the
  event list, payload schema and signature scheme are unpublished — verify delivery yourself and do not assume you
  can authenticate the sender.
