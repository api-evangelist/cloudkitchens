---
name: Publish menus to CloudKitchens and suspend unavailable items
description: Upsert a store menu, track the asynchronous publish job to completion, push it to the right publish targets, and suspend or unsuspend individual menu entities when items go out of stock.
api: openapi/cloudkitchens-public-api-openapi.yml
generated: '2026-08-01'
method: generated
source: openapi/cloudkitchens-public-api-openapi.yml + https://developer-guides.cloudkitchens.com/docs/menu-integrations-operations/
operations:
  - getMenu
  - upsertMenu
  - getAsyncJobStatus
  - managerGetMenuPublishTargets
  - managerPublishMenu
  - menuSync
  - managerSuspendMenuEntities
  - managerUnsuspendMenuEntities
---

# Publish menus to CloudKitchens and suspend unavailable items

Menus are **asynchronous**. An upsert returns a job, not a published menu. Never assume success from
the 2xx on the upsert.

Run the authentication skill first. Every call needs `Authorization: Bearer <token>` and
`X-Store-Id`.

## 1. Read the current menu — `getMenu`

`GET /v1/menus`, scope `menus.read`. Always read before you write, so you are diffing rather than
overwriting a menu an operator edited in the CloudKitchens UI.

## 2. Upsert — `upsertMenu`

`POST /v1/menus`, scope `menus.upsert`. Submits the new menu state and returns a job id.

## 3. Track the job — `getAsyncJobStatus`

`GET /v1/menus/jobs/{jobId}`, scope `menus.async_job.read`. Poll with backoff, not in a tight loop —
per-endpoint rate limits apply per store per application. Do not report the menu as live until the
job reports completion.

## 4. Publish to targets — `managerGetMenuPublishTargets`, `managerPublishMenu`

- `GET /manager/menu/v1/menus/publish-targets` — `managerGetMenuPublishTargets`, scope
  `manager.menus`. Lists the channels the menu can be published to.
- `POST /manager/menu/v1/menus/publish` — `managerPublishMenu`, scope `manager.menus`. Publishes.
  This changes what customers can order on live storefronts — treat it as a consequential write.

`POST /manager/menu/v1/menus/menu-sync` — `menuSync`, scope `manager.menus` — triggers a sync when
your POS is the source of truth.

## 5. Suspend and unsuspend items — `managerSuspendMenuEntities`, `managerUnsuspendMenuEntities`

- `POST /manager/menu/v1/menus/entities/availability/suspend` — take an item, modifier, or category
  off sale (86'd) without republishing the whole menu.
- `POST /manager/menu/v1/menus/entities/availability/unsuspend` — put it back.

Both use scope `manager.menus`. This is the correct mechanism for stock-outs; do not re-upsert the
entire menu to hide one item.

## Webhooks to handle

CloudKitchens drives menu work through events: `sendMenu` (send the current menu state),
`menuPublish` (publish result), `upsertMenuHours`, and `updateMenuEntitiesAvailabilities`. Answer
each with the matching callback — `menuSendCallback`, `menuPublishCallback`, `menuUpsertHours`,
`updateMenuEntitiesAvailabilitiesCallback` — using the corresponding narrow scopes
(`menus.get_current`, `menus.publish`, `menus.upsert_hours`, `menus.entity_suspension`). Verify the
`X-HMAC-SHA256` signature on every delivery before acting on it. See
`asyncapi/cloudkitchens-webhooks.yml`.

## Rules that always apply

- No idempotency key. A repeated upsert is a second job, not a no-op — check job status before
  resubmitting.
- Poll with exponential backoff; 429 is returned until you drop below the threshold.
