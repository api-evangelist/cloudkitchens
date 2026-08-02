---
name: Inject orders into CloudKitchens and drive them to fulfillment
description: Send an order from an ordering channel into a CloudKitchens store, keep its status and payment/delivery information current, then confirm, prep, and fulfill it from the manager side.
api: openapi/cloudkitchens-public-api-openapi.yml
generated: '2026-08-01'
method: generated
source: openapi/cloudkitchens-public-api-openapi.yml + https://developer-guides.cloudkitchens.com/docs/orders-integrations-lifecycle/
operations:
  - createOrder
  - updateOrder
  - updateOrderStatus
  - updateOrderCustomerPayment
  - updateOrderDeliveryInfo
  - orderCreated
  - managerGetOrderFeed
  - getManagerOrder
  - requestOrderConfirmation
  - updateOrderPrepTime
  - markAsReadyToPickup
  - markAsFulfilled
  - requestOrderCancelation
  - publishError
---

# Inject orders into CloudKitchens and drive them to fulfillment

There are two sides to the order surface and they use different scopes. Pick the one that matches
your role before you write a line of code.

- **Order provider** (you are an ordering channel sending orders *in*): `orders.create`,
  `orders.update`.
- **Order manager** (you are a POS / kitchen system acting *on* orders): `manager.orders`.

Run the authentication skill first. Every call needs `Authorization: Bearer <token>` and
`X-Store-Id`.

## Provider side — push an order in

1. `POST /v1/orders` — `createOrder`, scope `orders.create`. Creates the order for the store named
   by `X-Store-Id`. **This is not idempotent.** If the call fails with a 5XX, retry with the exact
   same body; if it fails with a 4XX, fix the body — do not resend blindly, or you will create a
   duplicate order in a real kitchen.
2. `PUT /v1/orders/{orderId}` — `updateOrder`, scope `orders.update`. Amend an order already
   accepted.
3. `POST /v1/orders/{orderId}/status` — `updateOrderStatus`, scope `orders.update`. Advance the
   order's status.
4. `PUT /v1/orders/{orderId}/payments` — `updateOrderCustomerPayment`, scope `orders.update`.
5. `PUT /v1/orders/{orderId}/delivery` — `updateOrderDeliveryInfo`, scope `orders.update`.

Listen for the `intentToCancelOrder`, `orderStatusUpdate` and `posInjectionStateUpdate` webhooks so
you learn about cancellations and injection failures instead of polling.

## Manager side — work the order

1. `POST /manager/order/v1/orders/order-created` — `orderCreated`, scope `manager.orders`. Notify
   CloudKitchens that an order was created in your system.
2. `GET /manager/order/v1/orders` — `managerGetOrderFeed`, scope `manager.orders`. The order feed.
   Prefer the `orderCreate` / `orderUpdate` webhooks over polling this.
3. `GET /manager/order/v1/sources/{source}/orders/{orderId}` — `getManagerOrder`. Full detail.
4. `POST .../orders/{orderId}/confirm` — `requestOrderConfirmation`. Accept the order.
5. `POST .../orders/{orderId}/prep-time` — `updateOrderPrepTime`, scope `orders.update`. Publish a
   revised prep time so the courier is not dispatched early.
6. `POST .../orders/{orderId}/ready-to-pickup` — `markAsReadyToPickup`.
7. `POST .../orders/{orderId}/fulfill` — `markAsFulfilled`. Terminal.
8. `POST .../orders/{orderId}/cancel` — `requestOrderCancelation`. **Consequential and effectively
   irreversible** — a human should authorize a cancellation; never let an agent cancel autonomously.

## When webhook processing fails

`POST /v1/callback/error` — `publishError`, scope `callback.error.write`. Report the failed event
back to CloudKitchens rather than silently dropping it.

## Rules that always apply

- No idempotency key exists on this API. Treat every write as at-most-once and reconcile with
  `getManagerOrder` before retrying a write that may have landed.
- Confirm, ready-to-pickup, fulfill and cancel all have physical consequences in a real kitchen.
  See `agentic-access/cloudkitchens-agentic-access.yml` for the recommended execution contracts.
- 429 means back off. 4XX means fix the request. 5XX may be retried with identical parameters.
