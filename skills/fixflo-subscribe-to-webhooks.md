---
name: Subscribe to Fixflo webhooks and verify their signatures
description: Register a Fixflo webhook, verify the ff-signature HMAC, handle retries idempotently, and audit delivery activity.
api: openapi/fixflo-api-v2-openapi.yml
generated: '2026-07-26'
method: generated
operations:
  - get-webhook-subscribe
  - get-webhooks
  - get-webhook-activity
  - get-webhook-unsubscribe
---

# Subscribe to Fixflo webhooks and verify their signatures

Fixflo pushes one documented event today — `Issue state change` — but it pushes it with
real signing and a real retry policy, so the receiver has actual work to do.

## Steps

1. **Register.** `get-webhook-subscribe` (`POST /Webhook/Subscribe`) with your endpoint URL
   and the shared secret you will verify against. Use an HTTPS endpoint: Fixflo permits
   HTTP but explicitly advises against it.
2. **Allow-list the source.** Deliveries originate from the IP behind the CNAME
   `webhook.fixflo.com`. Open your firewall to that, not to the world.
3. **Verify every request** before acting on it:
   - Read the request body in its entirety, raw and unparsed.
   - HMAC-SHA256 the raw body with the secret configured for that webhook.
   - Hex-encode the digest and compare against the `ff-signature` header, whose value has
     the form `sha256={hash}`.
   - Reject on mismatch. Do not parse first and verify later.
4. **Handle the envelope.** The body is JSON with two top-level members: `action` (here,
   `"Issue state change"`) and `payload` (an `Issue` object — `Id`, `Updated`,
   `IssueTitle`, `FaultId`, `FaultNotes`, `IssueDraftMedia`, reporter contact fields and
   `Address`).
5. **Be idempotent.** Fixflo retries up to 6 times over roughly 10 minutes whenever the
   connection fails or you answer `5xx`. Fixflo's own guidance: "any logic carried out on
   the server is idempotent ... is still valid even though the same message may be received
   more than once." Key your handler on the issue `Id` + `Updated` timestamp.
6. **Answer fast, work later.** Return `2xx` as soon as the signature verifies and queue
   the work; a slow handler earns retries and duplicate deliveries.
7. **Audit.** `get-webhooks` (`GET /Webhooks`) lists the agency's subscriptions;
   `get-webhook-activity` (`GET /Webhook/Activity`) returns delivery activity for one
   webhook, 20 per page, most recent first — the place to look when something did not
   arrive.
8. **Clean up.** `get-webhook-unsubscribe` (`DELETE /Webhook/Unsubscribe`) when the
   integration is torn down.

## Rules

- **One event exists.** Verbatim from Fixflo: "So far, users can only subscribe to one
  event, but we will be adding more in future." Anything else in your design is
  speculation — poll the issue list operations for state you cannot get from this event.
- The payload is a snapshot, not a delta. Re-read `get-Issue` (`GET /Issue/{Id}`) if you
  need the full current record.
- No AsyncAPI document exists for this surface. The catalogued description lives in
  `asyncapi/fixflo-webhooks.yml`.
- Signature verification uses hex encoding, not base64 — a common integration bug here.

## Related

- `asyncapi/fixflo-webhooks.yml` — the full webhook catalogue
- `conventions/fixflo-conventions.yml` — idempotency and retry semantics
