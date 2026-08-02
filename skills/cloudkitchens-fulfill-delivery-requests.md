---
name: Serve CloudKitchens delivery requests as a delivery provider
description: Answer CloudKitchens delivery webhooks as a courier network — quote a delivery, accept or cancel it, keep its status current, and report processing failures back.
api: openapi/cloudkitchens-public-api-openapi.yml
generated: '2026-08-01'
method: generated
source: openapi/cloudkitchens-public-api-openapi.yml + https://developer-guides.cloudkitchens.com/docs/delivery-integrations-operations/
operations:
  - requestDeliveryQuoteCallback
  - acceptDeliveryCallback
  - updateDeliveryRequestCallback
  - updateDeliveryStatus
  - cancelDeliveryCallback
  - deliveryCallbackError
---

# Serve CloudKitchens delivery requests as a delivery provider

This surface is **callback-shaped**: CloudKitchens sends you a webhook, you answer it with the
matching endpoint. Every operation here uses the single `delivery.provider` scope, except the error
callback.

Run the authentication skill first. Every call needs `Authorization: Bearer <token>` and
`X-Store-Id`.

## The flow

1. **`requestDeliveryQuotes` webhook** → answer with `requestDeliveryQuoteCallback`
   (`POST /v1/delivery/{deliveryReferenceId}/quotes`). Return your quotes for the delivery.
2. **`acceptDelivery` webhook** → answer with `acceptDeliveryCallback`
   (`POST /v1/delivery/{deliveryReferenceId}/accept`). You have committed a courier at this point.
3. **`updateDeliveryRequest` webhook** → answer with `updateDeliveryRequestCallback`
   (`POST /v1/delivery/{deliveryReferenceId}/update`) when the request changes.
4. **Status, continuously** — `updateDeliveryStatus`
   (`PUT /v1/delivery/{deliveryReferenceId}/status`). Push every courier state transition. Do not
   make CloudKitchens poll you.
5. **`cancelDelivery` webhook** → answer with `cancelDeliveryCallback`
   (`POST /v1/delivery/{deliveryReferenceId}/cancel`).

## When you cannot process an event

`POST /v1/delivery/callback/error` — `deliveryCallbackError`, scope `callback.error.write`. Report
the failure rather than dropping it; CloudKitchens has no other way to learn your side failed.

## Rules that always apply

- Verify the `X-HMAC-SHA256` header on every inbound webhook before acting. Compute HMAC-SHA256 over
  the raw body with your endpoint secret, base64-encode it, and compare. Reference implementations
  in Python, Java, JavaScript, C# and PHP are published in the webhook authentication guide.
- Acknowledge every webhook with HTTP 200 and an empty body.
- Accepting and cancelling a delivery dispatch real couriers to real addresses. These are
  physical-consequence operations — see `agentic-access/cloudkitchens-agentic-access.yml`.
- No idempotency key exists. Reconcile before retrying an accept or cancel.
