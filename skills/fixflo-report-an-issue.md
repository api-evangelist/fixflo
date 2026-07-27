---
name: Report a repair issue through the Fixflo fault tree
description: Walk the Fixflo guided fault tree, build an issue draft with photos against a property, and commit it into a live repair issue.
api: openapi/fixflo-api-v2-openapi.yml
generated: '2026-07-26'
method: generated
operations:
  - get-faulttree-walk
  - post-IssueDraft
  - post-IssueDraftMedia-Id
  - post-issuedraft-asset-Id
  - post-IssueDraft-Commit
  - post-IssueDraft-Delete
  - get-Issue
  - get-issue-id-report
---

# Report a repair issue through the Fixflo fault tree

Fixflo does not accept free-text repair requests. An issue is classified by walking a
guided fault tree, assembled as a draft, and only then committed. Follow that order.

## Before you start

- Base URL is the customer's own host: `https://[their subdomain].fixflo.com/api/v2`. The
  published sandbox is `https://api-sandbox.fixflo.com/api/v2`. There is no shared
  production host.
- Send `Authorization: Bearer [token]` on every call. The token is a 64-character string
  the customer generates inside their own Fixflo account. There are no scopes — the token
  carries that user's privileges.
- HTTPS is mandatory; a non-TLS request fails with `401`.
- Stay under the documented rate limit (not below 500 requests/minute). A breach returns
  `429` with no `Retry-After`, so back off yourself.

## Steps

1. **Identify the property.** If you hold your own CRM key, look the property up by
   external reference rather than guessing a GUID — see the property sync skill. Fixflo
   GUIDs are tenant-scoped and mean nothing outside one agency account.
2. **Walk the fault tree.** Call `get-faulttree-walk` (`GET /FaultTree/Walk/{id}`) starting
   from the root and follow the returned branch nodes until you reach a leaf fault. Each
   response is a `FaultTreeBranch` carrying the current `Fault` node and its `Children`.
   Do not invent fault ids — the tree is the classification contract.
3. **Create the draft.** `post-IssueDraft` (`POST /IssueDraft`) with the resolved `FaultId`,
   the reporter's contact details, and either `PropertyId`/`BlockId` or
   `ExternalPropertyRef`/`ExternalBlockRef`.
4. **Attach evidence.** `post-IssueDraftMedia-Id` (`POST /IssueDraftMedia`) for photos and
   video, and `post-issuedraft-asset-Id` (`POST /IssueDraft/{Id}/Assets`) to link the
   appliance or asset the fault relates to. Read back with `get-issuedraftmedia` or
   `get-issuedraft-asset-Id` if you need to confirm what attached.
5. **Commit.** `post-IssueDraft-Commit` (`POST /IssueDraft/Commit`) turns the draft into a
   live issue. Nothing reaches the agency's workflow until this call succeeds.
6. **Confirm.** `get-Issue` (`GET /Issue/{Id}`) for the issue record, or
   `get-issue-id-report` (`GET /Issue/{Id}/Report`) for the PDF report. Binary and
   base-64 payloads are documented as untrusted — scan them.
7. **Abandon cleanly.** If the reporter drops out, `post-IssueDraft-Delete`
   (`POST /IssueDraft/Delete`) rather than leaving orphaned drafts.

## Rules

- **Retry with care.** There is no `Idempotency-Key` header. `post-IssueDraft` and
  `post-IssueDraft-Commit` are not replay-safe: a blind retry after a timeout can create a
  second draft or a second issue. Read back with `get-issuedraft` before retrying, and set
  your own external reference afterwards with `post-Issue-externalref`
  (`POST /Issue/{Id}/ExternalRef`) so duplicates are detectable — external refs must be
  unique per agency.
- **Dates are UTC**, formatted `yyyy-MM-ddTHH:mm:ss` (dates `yyyy-MM-dd`). Use locale-neutral
  formats in URL parameters.
- **Errors are not RFC 9457.** Failures come back as the vendor `Envelope`:
  `HttpStatusCode`, `HttpStatusCodeDesc`, `Errors[]`, `Messages[]` — free text, no stable
  error codes. See `errors/fixflo-problem-types.yml`.
- The spec declares only `2xx` responses on almost every operation. Treat `401`, `429` and
  `5xx` as possible on every call even though they are not in the contract.

## Related

- `conventions/fixflo-conventions.yml` — auth, pagination, idempotency, rate limits
- `asyncapi/fixflo-webhooks.yml` — subscribe to `Issue state change` instead of polling
- `data-model/fixflo-data-model.yml` — FaultTree → IssueDraft → Issue → Quote → Job
