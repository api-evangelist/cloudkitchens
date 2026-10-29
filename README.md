# CloudKitchens

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

CloudKitchens, operated by City Storage Systems, builds and runs delivery-only "ghost kitchen" facilities and the restaurant technology stack that runs them, with sites across roughly 30 countries. For integration partners it publishes the CloudKitchens Public API — an OpenAPI 3.0.1 contract of 80 operations and 27 webhook events, secured with OAuth 2.0 across 29 scopes and two flows (client credentials and authorization code), backed by an OpenID Connect identity provider at iam.cloudkitchens.com. The API spans order injection and fulfillment, menu upsert and publishing, storefront pause/resume, delivery dispatch callbacks, finance and payout reporting, inventory, reviews, loyalty, and organization/brand/store pairing. Access is partner-gated rather than self-serve: applications, webhook endpoints, and stores are onboarded manually by a CloudKitchens Account Representative, who issues the Application ID and Client Secret for the production and staging environments and provisions the partner-specific API base URL.

**Areas:** Restaurant · Ghost Kitchens · Food Delivery · Order Management · Menu Management · Storefront · Delivery · Reporting · Loyalty · Real Estate

## CloudKitchens on APIs.io

Everything profiled for CloudKitchens is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/cloudkitchens/](https://apis.io/providers/cloudkitchens/)** — or go straight to one of the APIs or properties below.

### APIs (27)

- [CloudKitchens Account Pairing Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-account-pairing-endpoints-api/) — Endpoints to manage store onboarding and status
- [CloudKitchens Account Pairing Webhooks API](https://apis.io/apis/cloudkitchens/cloudkitchens-account-pairing-webhooks-api/) — Webhooks to manage store onboarding and status
- [CloudKitchens Auth Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-auth-endpoints-api/) — Endpoints to handle token management.
- [CloudKitchens Callback Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-callback-endpoints-api/) — Endpoints for callback management.
- [CloudKitchens Delivery Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-delivery-endpoints-api/) — Endpoints to manage delivery.
- [CloudKitchens Delivery Webhooks API](https://apis.io/apis/cloudkitchens/cloudkitchens-delivery-webhooks-api/) — Webhooks from the delivery domain.
- [CloudKitchens Direct Orders Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-direct-orders-endpoints-api/) — Endpoints to get orders directly.
- [CloudKitchens Finance Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-finance-endpoints-api/) — Endpoints to handle financial data.
- [CloudKitchens Inventory Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-inventory-endpoints-api/) — Endpoints to interact with product inventory.
- [CloudKitchens Manager Loyalty Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-manager-loyalty-endpoints-api/) — Endpoints to manage loyalty.
- [CloudKitchens Manager Menu Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-manager-menu-endpoints-api/) — Endpoints for applications managing menus related data and operations.
- [CloudKitchens Manager Order Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-manager-order-endpoints-api/) — Endpoints for applications that act on the merchant/store side of an order rather than as the ordering marketplace — typically Point-of-Sale (POS) systems,…
- [CloudKitchens Manager Orders Webhooks API](https://apis.io/apis/cloudkitchens/cloudkitchens-manager-orders-webhooks-api/) — Webhooks delivered to merchant-side applications (POS, BI, and reporting integrations) so they can react to changes in an order as it progresses through its…
- [CloudKitchens Manager Storefront Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-manager-storefront-endpoints-api/) — Endpoints for applications managing storefront related data and operations.
- [CloudKitchens Menus Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-menus-endpoints-api/) — Endpoints to manage menus.
- [CloudKitchens Menus Webhooks API](https://apis.io/apis/cloudkitchens/cloudkitchens-menus-webhooks-api/) — Webhooks from menus domain.
- [CloudKitchens Orders Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-orders-endpoints-api/) — Endpoints used by ordering marketplaces and other order sources to send orders to a store and keep them up to date. This domain lets an order source submit…
- [CloudKitchens Orders Webhooks API](https://apis.io/apis/cloudkitchens/cloudkitchens-orders-webhooks-api/) — Webhooks from orders domains.
- [CloudKitchens Organization Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-organization-endpoints-api/) — Endpoints to interact with with organizations/brands/stores and with integration connections.
- [CloudKitchens Ping Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-ping-endpoints-api/) — Endpoints to ping and test system authentication.
- [CloudKitchens Ping Webhooks API](https://apis.io/apis/cloudkitchens/cloudkitchens-ping-webhooks-api/) — Webhooks to ping and test the system integration.
- [CloudKitchens Reports Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-reports-endpoints-api/) — Endpoints to reports generation operations
- [CloudKitchens Reports Webhooks API](https://apis.io/apis/cloudkitchens/cloudkitchens-reports-webhooks-api/) — Webhooks from the reports generation operations
- [CloudKitchens Reviews Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-reviews-endpoints-api/) — Endpoints for review operations
- [CloudKitchens Storefront Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-storefront-endpoints-api/) — Endpoints to manage storefront state
- [CloudKitchens Storefront Webhooks API](https://apis.io/apis/cloudkitchens/cloudkitchens-storefront-webhooks-api/) — Webhooks from storefront domain.
- [CloudKitchens Market Intel Endpoints API](https://apis.io/apis/cloudkitchens/cloudkitchens-market-intel-endpoints-api/) — The Market Intel Endpoints API from CloudKitchens — 1 operation(s) for market intel endpoints.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Cloudkitchens Webhooks](https://apis.io/asyncapis/cloudkitchens/cloudkitchens-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [cloudkitchens-mcp.yml](https://apis.io/servers/cloudkitchens/cloudkitchens-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Cloudkitchens Agentic Access](https://apis.io/agentic-access/cloudkitchens/cloudkitchens-agentic-access/)

#### Collections (1)

Postman and Open Collection request collections.

- [Public API](https://apis.io/collections/cloudkitchens/open-cloudkitchens-public-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Cloudkitchens Public Api Overlay](https://apis.io/overlays/cloudkitchens/cloudkitchens-public-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Cloudkitchens Authentication](https://apis.io/security/cloudkitchens/cloudkitchens-authentication/)
- [Cloudkitchens Domain Security](https://apis.io/security/cloudkitchens/cloudkitchens-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Cloudkitchens Scopes](https://apis.io/scopes/cloudkitchens/cloudkitchens-scopes/)

#### Rate limits (1)

Published request limits.

- [Cloudkitchens Rate Limits](https://apis.io/rate-limits/cloudkitchens/cloudkitchens-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.cloudkitchens.com/)
- [Documentation](https://developer-guides.cloudkitchens.com/docs/)
- [Getting started](https://developer-guides.cloudkitchens.com/docs/onboard-application/)
- [API reference](https://developer-guides.cloudkitchens.com/api-reference/)
- [Support](https://support.cloudkitchens.com/)
- [Blog](https://cloudkitchens.com/blog)
- [Terms of service](https://cloudkitchens.com/terms-of-service/)
- [Privacy policy](https://cloudkitchens.com/privacy-policy)

## API Evangelist rating

**Kin Score 47.0** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 54.1 |
| Contract governance | 4.5 |
| Operational transparency | 39.5 |
| Developer ergonomics | 39.9 |
| Access clarity | 21.1 |

**Agent readiness 34.1** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | documented (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/cloudkitchens/](https://apis.io/providers/cloudkitchens/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for CloudKitchens: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/cloudkitchens/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
