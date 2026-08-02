# CloudKitchens

CloudKitchens, operated by City Storage Systems, builds and runs delivery-only "ghost kitchen"
facilities and the restaurant technology stack that runs them, across roughly 30 countries.

For integration partners it publishes the **CloudKitchens Public API** — an OpenAPI 3.0.1 contract of
**80 operations** and **27 webhook events**, secured with OAuth 2.0 across **29 scopes** and two
flows, backed by an OpenID Connect identity provider at `iam.cloudkitchens.com`. The API spans order
injection and fulfillment, menu upsert and publishing, storefront pause/resume, delivery dispatch
callbacks, finance and payout reporting, inventory, reviews, loyalty, and organization/brand/store
pairing.

Access is partner-gated rather than self-serve: applications, webhook endpoints and stores are
onboarded manually by a CloudKitchens Account Representative, who issues the Application ID and
Client Secret for production and staging and provisions the partner-specific API base URL.

## Developer surface

- Developer Portal — https://developer.cloudkitchens.com/
- Developer Documentation — https://developer-guides.cloudkitchens.com/docs/
- API Reference — https://developer-guides.cloudkitchens.com/api-reference/
- Support — https://support.cloudkitchens.com/
- Website — https://www.cloudkitchens.com/

## Artifacts

| Artifact | Path |
|---|---|
| OpenAPI 3.0.1 (harvested verbatim) | `openapi/cloudkitchens-public-api-openapi.yml` |
| API Evangelist overlay | `overlays/cloudkitchens-public-api-overlay.yaml` |
| Authentication profile | `authentication/cloudkitchens-authentication.yml` |
| OAuth scopes (29) | `scopes/cloudkitchens-scopes.yml` |
| OIDC discovery (verbatim) | `well-known/cloudkitchens-openid-configuration.json` |
| Well-known probe index | `well-known/cloudkitchens-well-known.yml` |
| API conventions | `conventions/cloudkitchens-conventions.yml` |
| Webhook event catalog (27) | `asyncapi/cloudkitchens-webhooks.yml` |
| Error catalog | `errors/cloudkitchens-problem-types.yml` |
| Rate limits | `rate-limits/cloudkitchens-rate-limits.yml` |
| Lifecycle + versioning | `lifecycle/cloudkitchens-lifecycle.yml` |
| Conformance | `conformance/cloudkitchens-conformance.yml` |
| Data model | `data-model/cloudkitchens-data-model.yml` |
| Sandbox / staging | `sandbox/cloudkitchens-sandbox.yml` |
| Packages (none published) | `packages/cloudkitchens-packages.yml` |
| MCP candidate (not published by CloudKitchens) | `mcp/cloudkitchens-mcp.yml` |
| Agentic access contracts | `agentic-access/cloudkitchens-agentic-access.yml` |
| Agent skills (6) | `skills/_index.yml` |
| Domain security | `security/cloudkitchens-domain-security.yml` |
| llms.txt | `llms/cloudkitchens-llms.txt` |

## Recorded negatives

Verified absent, not merely unsearched: no `security.txt`, no A2A agent card, no hosted MCP server,
no GraphQL surface, no AsyncAPI document, no official SDK/CLI/Postman collection, no status page, no
public changelog, no trust center or published certifications, no idempotency contract, and no
self-serve signup or published pricing for the Public API.

## Related

Otter (`all/otter/`) is the sibling restaurant-OS product under the same City Storage Systems parent.
The Public API captured here is served from CloudKitchens' own host
(`developer-guides.cloudkitchens.com`) and is the CloudKitchens-branded instance of that contract.
