---
name: Pause and resume CloudKitchens storefronts
description: Take a store's storefronts offline when the kitchen cannot accept orders, track the asynchronous pause/unpause request to completion, and report store availability and hours back to CloudKitchens.
api: openapi/cloudkitchens-public-api-openapi.yml
generated: '2026-08-01'
method: generated
source: openapi/cloudkitchens-public-api-openapi.yml + https://developer-guides.cloudkitchens.com/docs/storefront-integrations-operations/
operations:
  - pauseStorefronts
  - getPauseRequestStatus
  - unpauseStorefronts
  - getUnpauseRequestStatus
  - postStoreAvailabilityChange
---

# Pause and resume CloudKitchens storefronts

Pausing a storefront stops real customers from ordering. Resuming it exposes a kitchen that may not
be ready. Both are consequential operations — an agent should confirm with a human operator before
either, and must never pause or unpause on a schedule it inferred.

Run the authentication skill first. Every call needs `Authorization: Bearer <token>` and
`X-Store-Id`.

## 1. Pause — `pauseStorefronts`

`POST /manager/storefront/v1/storefront/pause`, scope `manager.storefront`. Returns a request id;
the pause is applied asynchronously.

## 2. Track it — `getPauseRequestStatus`

`GET /manager/storefront/v1/storefront/pause/request/{requestId}/status`, scope
`manager.storefront`. Poll with backoff until the request resolves. Do not tell the operator the
store is paused until the request confirms it.

## 3. Resume — `unpauseStorefronts` and `getUnpauseRequestStatus`

`POST /manager/storefront/v1/storefront/unpause` then
`GET /manager/storefront/v1/storefront/unpause/request/{requestId}/status`, both scope
`manager.storefront`.

## 4. Report availability back — `postStoreAvailabilityChange`

`POST /v1/storefront/availability`, scope `storefront.store_availability`. Use this when *your*
system is the source of truth for whether the store is open, and CloudKitchens has asked via the
`getStoreAvailability` webhook.

Related callbacks on the same surface: `postStoreHoursConfigurationChange`
(scope `storefront.store_hours_configuration`), `postPauseStoreEventResult` and
`postUnpauseStoreEventResult` (scope `storefront.store_pause_unpause`) — these answer the
`pauseStore`, `unpauseStore`, and `getStoreHoursConfiguration` webhooks.

## Rules that always apply

- No idempotency key. A duplicate pause request is a second request; check the status endpoint
  before resubmitting.
- Verify `X-HMAC-SHA256` on every inbound webhook before acting.
- 429 means back off — status polling is rate limited per store per application.
