---
name: d-tools-publish-a-project-to-si
description: >-
  Publish a new project into a D-Tools System Integrator user's queue, follow it with change orders, and confirm
  the SI desktop application actually applied it.
api: D-Tools System Integrator (SI) API
base_url: https://api.d-tools.com/si
generated: '2026-08-11'
method: generated
source: openapi/d-tools-si-api-openapi.yml, https://docs.d-tools.com/en/articles/9225625-d-tools-si-api-overview
operations:
  - POST /Publish/Projects
  - POST /Publish/Projects/Update
  - POST /Publish/Projects/NewChangeOrder
  - POST /Publish/Projects/ProjectComments
  - GET /Message/PublishedMessageStatus
  - GET /Message/PublishedMessagesStatus
note: >-
  The SI OpenAPI declares no operationId on any of its 56 operations, so operations are identified by method and
  path — both taken verbatim from the specification.
---

# Publish a project to D-Tools SI

## What this actually does

`POST /Publish/Projects` does **not** write into System Integrator. It enqueues the project on the D-Tools cloud
API server, where it waits until the SI desktop application pulls and applies it. A `200` means *accepted into the
queue*. Treat the publish and the apply as two separate events.

## Before you start

- You need an `X-DTSI-ApiKey` header on every call. The key is scoped to **one SI user and one integration** —
  integrating with five SI customers means five keys. Generate it in the SI Control Panel under *Manage
  Integrations*. Access requires the customer to be enrolled in D-Tools Software Assurance.
- There is no sandbox. Publish against a real SI user's queue or not at all.

## Steps

1. **Publish the project.** `POST /Publish/Projects` with the project body. Keep your own
   `IntegrationProjectId`/external identifier on the record — you will need it to correlate later.
2. **Capture the message id from the response.** This is the only handle you get on the enqueued item.
3. **Confirm it was applied.** `GET /Message/PublishedMessageStatus` for one message, or
   `GET /Message/PublishedMessagesStatus` for a batch. Do not treat the `200` from step 1 as completion — poll
   status until SI reports the message applied.
4. **Amend an existing project.** `POST /Publish/Projects/Update` for the project itself.
5. **Send a change order.** `POST /Publish/Projects/NewChangeOrder`. Pass your own `IntegrationChangeOrderId`.
   Reusing the same value updates the existing change order instead of creating a second one — this is the only
   upsert key anywhere in the API and it is the closest thing to idempotency the surface offers.
6. **Attach commentary if needed.** `POST /Publish/Projects/ProjectComments`.

## Rules you must apply yourself, because the contract does not

- **No idempotency.** There is no `Idempotency-Key`. A retry after a network timeout on step 1 can enqueue a
  second project. Persist the message id before retrying, and where the entity supports it prefer the
  `Integration*Id` upsert path (step 5) over a blind re-POST.
- **No error contract.** All 56 SI operations declare only a `200` response. Do not branch on documented error
  shapes — there are none. Handle any non-2xx as opaque, log the body verbatim, and back off.
- **No rate limits published** for the SI API. Be conservative; the Cloud API's documented ceiling is 120/minute
  and that is the only quantitative signal D-Tools gives anywhere.
- **No versioning.** SI paths carry no version segment, so you cannot pin. Re-fetch
  `https://api.d-tools.com/si/openapi/v1.json` on a schedule and diff it yourself.
- **Pick one system of record.** D-Tools explicitly advises against bidirectional project editing without clearly
  defined rules. Decide whether SI or your system owns project data, and make the other side read-only.
