---
name: Authenticate with CloudKitchens and pair stores
description: Get an OAuth 2.0 token for a CloudKitchens Public API application, verify connectivity, then discover the organization's brands and stores and connect your integration to them.
api: openapi/cloudkitchens-public-api-openapi.yml
generated: '2026-08-01'
method: generated
source: openapi/cloudkitchens-public-api-openapi.yml + https://developer-guides.cloudkitchens.com/docs/onboard-application/
operations:
  - requestToken
  - ping
  - organizationGetOrganization
  - organizationListBrands
  - organizationListStores
  - organizationGetStore
  - organizationCreateConnection
  - organizationDeleteConnection
  - upsertStorelinkEventResultEndpoint
  - updateStoreStatusEndpoint
---

# Authenticate with CloudKitchens and pair stores

Every other CloudKitchens skill starts here. Do not attempt any call before you hold a valid token
and know which store the call acts on behalf of.

## Before you start

- The application must already be registered. This is a **manual, one-time** step performed by a
  CloudKitchens Account Representative — there is no self-serve signup. You receive an
  **Application ID** (formerly "Partner ID") and a **Client Secret** for *each* environment
  (production and staging).
- Scopes are granted by CloudKitchens' internal team and then enabled on the Application Settings
  page in the Developer Portal. If a call returns 403, the scope is not enabled — that is a
  provisioning task, not something to retry.
- The base URL is provisioned per partner. The spec calls it `{{public-api-url}}`.

## 1. Get a token — `requestToken`

`POST /v1/auth/token`, `Content-Type: application/x-www-form-urlencoded`.

For a server-to-server integration use `grant_type=client_credentials` with `client_id`,
`client_secret`, and the space-separated `scope` list you were granted. For acting on behalf of a
CloudKitchens user, run the authorization-code flow first
(`GET /v1/auth/oauth2/authorize` with `client_id`, `redirect_uri`, `response_type=code`, `scope`,
`state`) and exchange the returned `code` with `grant_type=authorization_code`.

The response carries `access_token`, `expires_in`, `scope`, `token_type`.

**Tokens are valid for 30 days.** Store and re-use them. Do not mint a token per request.

## 2. Verify connectivity — `ping`

`GET /v1/ping` with `Authorization: Bearer <access_token>` and `X-Store-Id: <store id>`.
Requires the `ping` scope. This is the safe smoke test — it is rate limited to a small number of
calls per store per application per minute (the published worked example is eight per minute), so do
not poll it.

## 3. Discover the organization — `organizationGetOrganization`, `organizationListBrands`, `organizationListStores`, `organizationGetStore`

These run under the **authorization-code** flow with the `organization.read` scope, because they read
data on behalf of a user.

- `GET /organization/v1/organization` — the organization.
- `GET /organization/v1/organization/brands` — its brands.
- `GET /organization/v1/organization/brands/{brandId}/stores` — the stores under a brand.
- `GET /organization/v1/organization/brands/{brandId}/stores/{storeId}` — one store.

## 4. Connect your integration to a store — `organizationCreateConnection`

`POST /organization/v1/organization/brands/{brandId}/stores/{storeId}/connection` with the
`organization.service_integration` scope. `organizationDeleteConnection` (`DELETE`, same path)
removes it. Deleting a connection stops the event flow for that store — confirm with the operator
before calling it.

## 5. Report store-link results — `upsertStorelinkEventResultEndpoint`, `updateStoreStatusEndpoint`

When CloudKitchens sends the `upsertStore` / `removeStore` / `fetchCredentials` account-pairing
webhooks, acknowledge the outcome:

- `POST /v1/stores` (`upsertStorelinkEventResultEndpoint`, scope `stores.manage`) — report the
  result of a store upsert and register your identifier for the store.
- `PUT /v1/stores/status` (`updateStoreStatusEndpoint`, scope `stores.manage`) — update the store's
  status.

## Rules that always apply

- `Authorization: Bearer <token>` on every resource call.
- `X-Store-Id` carries **your** identifier for the store; CloudKitchens translates it internally and
  validates that your application is associated with that store.
- **There is no idempotency key.** Retrying a write is not free. Retry only on 5XX, with the exact
  same parameters, and back off.
- A 401 on a token you believe is valid can be a transient internal error. Retry once with backoff,
  or request a new token. CloudKitchens deliberately does not disclose why authentication failed.
- 429 means you exceeded a limit (20 authenticated req/sec per IP; per-endpoint quotas per store per
  application). Back off; do not tighten the loop.

See `conventions/cloudkitchens-conventions.yml`, `scopes/cloudkitchens-scopes.yml`, and
`errors/cloudkitchens-problem-types.yml`.
