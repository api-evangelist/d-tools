# D-Tools

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

D-Tools Inc. builds estimation, system design, project management and field-service software for audio-visual, low-voltage, security and systems-integration contractors. Two products carry two distinct public APIs. D-Tools Cloud is the web-native platform, and its REST API (dtcloudapi.d-tools.cloud) exposes Clients, Products, Opportunities, Quotes, Projects, Change Orders, Purchase Orders, Service Contracts, Files and Time Entries with documented rate limits, webhooks and a downloadable Postman collection. D-Tools System Integrator (SI) is the on-premises/hosted Windows product; because SI itself has no directly reachable API, D-Tools operates a cloud middleware queue at api.d-tools.com/si where third parties publish projects, change orders, tasks, service orders, purchase orders, time sheets, product catalogs, clients and vendors to an SI user and subscribe to what that SI user exports. Both APIs publish machine-readable specifications: OpenAPI 3.1.1 for SI and OpenAPI 3.0.4 for Cloud.

**Areas:** av-integration · Systems Integration · Project Management · Estimation · Quoting · Field Service Management · Construction Technology · low-voltage · Product Catalog · ERP Integration · Vertical SaaS

## D-Tools on APIs.io

Everything profiled for D-Tools is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/d-tools/](https://apis.io/providers/d-tools/)** — or go straight to one of the APIs or properties below.

### APIs (27)

- [D-Tools Clients API](https://apis.io/apis/d-tools/d-tools-clients-api/) — The Clients API from D-Tools — 4 operation(s) for clients.
- [D-Tools Files API](https://apis.io/apis/d-tools/d-tools-files-api/) — The Files API from D-Tools — 1 operation(s) for files.
- [D-Tools Message API](https://apis.io/apis/d-tools/d-tools-message-api/) — The Message API from D-Tools — 2 operation(s) for message.
- [D-Tools Opportunities API](https://apis.io/apis/d-tools/d-tools-opportunities-api/) — The Opportunities API from D-Tools — 4 operation(s) for opportunities.
- [D-Tools Products API](https://apis.io/apis/d-tools/d-tools-products-api/) — The Products API from D-Tools — 5 operation(s) for products.
- [D-Tools Projects API](https://apis.io/apis/d-tools/d-tools-projects-api/) — The Projects API from D-Tools — 3 operation(s) for projects.
- [D-Tools Publish Clients API](https://apis.io/apis/d-tools/d-tools-publishclients-api/) — Allows an integration to update a client list to a SI user.
- [D-Tools Publish Product Catalogs API](https://apis.io/apis/d-tools/d-tools-publishproductcatalogs-api/) — Allows an integration to publish a product catalog to a SI user.
- [D-Tools Publish Projects API](https://apis.io/apis/d-tools/d-tools-publishprojects-api/) — Allows an integration to publish or update a project to a SI user.
- [D-Tools Publish Service Orders API](https://apis.io/apis/d-tools/d-tools-publishserviceorders-api/) — Allows an integration to publish a service order to a SI user.
- [D-Tools Publish Tasks API](https://apis.io/apis/d-tools/d-tools-publishtasks-api/) — Allows an integration to publish a task to a SI user.
- [D-Tools Publish Time Sheets API](https://apis.io/apis/d-tools/d-tools-publishtimesheets-api/) — Allows an integration to publish a time sheet to a SI user.
- [D-Tools Publish Vendors API](https://apis.io/apis/d-tools/d-tools-publishvendors-api/) — Allows an integration to update a vendor list to a SI user. d
- [D-Tools Quotes API](https://apis.io/apis/d-tools/d-tools-quotes-api/) — The Quotes API from D-Tools — 2 operation(s) for quotes.
- [D-Tools Service Contracts API](https://apis.io/apis/d-tools/d-tools-servicecontracts-api/) — The ServiceContracts API from D-Tools — 2 operation(s) for servicecontracts.
- [D-Tools Subscribe Clients API](https://apis.io/apis/d-tools/d-tools-subscribeclients-api/) — Allows an integration to subscribe to clients published by SI users.
- [D-Tools Subscribe Partial Projects API](https://apis.io/apis/d-tools/d-tools-subscribepartialprojects-api/) — Allows an integration to subscribe to partial projects published by SI users.
- [D-Tools Subscribe Product Catalogs API](https://apis.io/apis/d-tools/d-tools-subscribeproductcatalogs-api/) — Allows an integration to subscribe to product catalogs published by SI users.
- [D-Tools Subscribe Projects API](https://apis.io/apis/d-tools/d-tools-subscribeprojects-api/) — Allows an integration to subscribe to projects and change orders published by SI users.
- [D-Tools Subscribe Purchase Order API](https://apis.io/apis/d-tools/d-tools-subscribepurchaseorder-api/) — Allows an integration to subscribe to Purchase orders published by SI users.
- [D-Tools Subscribe Service Order API](https://apis.io/apis/d-tools/d-tools-subscribeserviceorder-api/) — Allows an integration to subscribe to Service orders published by SI users.
- [D-Tools Subscribe Service Plan API](https://apis.io/apis/d-tools/d-tools-subscribeserviceplan-api/) — Allows an integration to subscribe to Service plan published by SI users.
- [D-Tools Subscribe Task API](https://apis.io/apis/d-tools/d-tools-subscribetask-api/) — Allows an integration to subscribe to Tasks published by SI users.
- [D-Tools Subscribe Time Sheet API](https://apis.io/apis/d-tools/d-tools-subscribetimesheet-api/) — Allows an integration to subscribe to Time sheets published by SI users.
- [D-Tools Change Orders API](https://apis.io/apis/d-tools/d-tools-change-orders-api/) — The Change Orders API from D-Tools — 2 operation(s) for change orders.
- [D-Tools Purchase Orders API](https://apis.io/apis/d-tools/d-tools-purchase-orders-api/) — The Purchase Orders API from D-Tools — 2 operation(s) for purchase orders.
- [D-Tools Time Entries API](https://apis.io/apis/d-tools/d-tools-time-entries-api/) — The Time Entries API from D-Tools — 1 operation(s) for time entries.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [D Tools Cloud Webhooks](https://apis.io/asyncapis/d-tools/d-tools-cloud-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [d-tools-mcp.yml](https://apis.io/servers/d-tools/d-tools-mcp-yml/)

#### Collections (2)

Postman and Open Collection request collections.

- [D-Tools Cloud API](https://apis.io/collections/d-tools/open-d-tools-cloud-api/)
- [D-Tools SI API Documentation](https://apis.io/collections/d-tools/open-d-tools-si-api/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [D Tools Cloud Api Overlay](https://apis.io/overlays/d-tools/d-tools-cloud-api-overlay/)
- [D Tools Si Api Overlay](https://apis.io/overlays/d-tools/d-tools-si-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [D Tools Authentication](https://apis.io/security/d-tools/d-tools-authentication/)
- [D Tools Domain Security](https://apis.io/security/d-tools/d-tools-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [D Tools Plans Pricing](https://apis.io/plans/d-tools/d-tools-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [D Tools Rate Limits](https://apis.io/rate-limits/d-tools/d-tools-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.d-tools.com/)
- [Documentation](https://docs.d-tools.cloud/en/collections/7640732-cloud-api-documentation)
- [Getting started](https://docs.d-tools.cloud/en/articles/9344578-best-practices-for-developing-api-integrations)
- [API reference](https://dtcloudapi.d-tools.cloud/apidocs/index.html)
- [Pricing](https://www.d-tools.com/cloud-pricing)
- [Sign up](https://www.d-tools.com/cloud-free-trial)
- [Support](https://www.d-tools.com/support)
- [Blog](https://www.d-tools.com/resource-center)
- [Terms of service](https://www.d-tools.com/d-tools-software-terms-of-services)
- [Privacy policy](https://www.d-tools.com/privacy)
- [Status](https://status.d-tools.cloud/)

## API Evangelist rating

**Kin Score 54.5** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 51.2 |
| Contract governance | 4.5 |
| Operational transparency | 67.1 |
| Developer ergonomics | 45.8 |
| Access clarity | 76.3 |

**Agent readiness 29.4** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 24.5** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/d-tools/](https://apis.io/providers/d-tools/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for D-Tools: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/d-tools/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
