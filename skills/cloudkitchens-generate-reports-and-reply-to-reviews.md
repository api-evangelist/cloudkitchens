---
name: Generate CloudKitchens reports and reply to reviews
description: Request an asynchronous report across stores and a time period, collect it when the report-generated webhook fires, and post an operator reply to a customer review.
api: openapi/cloudkitchens-public-api-openapi.yml
generated: '2026-08-01'
method: generated
source: openapi/cloudkitchens-public-api-openapi.yml + https://developer-guides.cloudkitchens.com/docs/reports-integration-operations/
operations:
  - generateReportMulti
  - getReportStatus
  - reviewReply
---

# Generate CloudKitchens reports and reply to reviews

Reporting is asynchronous and notification-driven. There are two documented shapes — with a
notification (the `reportGenerated` webhook) and without (poll the status endpoint). Prefer the
notification flow.

Run the authentication skill first. Every call needs `Authorization: Bearer <token>` and
`X-Store-Id`.

## 1. Request a report — `generateReportMulti`

`POST /v1/reports/generate`, scope `reports.generate_report`. Requests a report for one or more
stores over a time period. Returns a job id.

The published report types are the order report, order-items report, payout-transactions report, and
the ratings-and-reviews report.

## 2. Collect it

- **Preferred:** wait for the `reportGenerated` webhook, verify its `X-HMAC-SHA256` signature, then
  fetch the resource named by `metadata.resourceHref`.
- **Fallback:** `GET /v1/reports/{jobId}` — `getReportStatus`, scope `reports.generate_report`. Poll
  with exponential backoff. Reports over long periods take time; a tight poll loop will earn a 429.

## 3. Reply to a review — `reviewReply`

`POST /v1/reviews/reply`, scope `reviews.reply`. Posts an operator reply to a customer review.

**A review reply is customer-visible and public.** An agent should draft it and a human should
approve it — do not auto-post generated replies to real diners.

## Rules that always apply

- No idempotency key. A repeated `generateReportMulti` is a second job; a repeated `reviewReply` may
  produce a duplicate public reply.
- Financial data returned by the payout-transactions report is sensitive. Do not forward it to
  general-purpose model context without the operator's consent — see
  `agentic-access/cloudkitchens-agentic-access.yml`.
- 5XX may be retried with identical parameters; 4XX means fix the request.
