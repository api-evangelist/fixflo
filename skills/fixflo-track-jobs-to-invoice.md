---
name: Track a Fixflo repair from quote to completed job and invoice
description: Follow an issue through quoting, award, appointment, completion documents and invoice submission as a contractor or a job management system.
api: openapi/fixflo-api-v2-openapi.yml
generated: '2026-07-26'
method: generated
operations:
  - get-issues
  - get-issues-jobawarded
  - get-issues-jobcompleted
  - get-issues-closed
  - get-Issue-issueId-quotes
  - post-Issue-issueId-Quote
  - post-Issue-issueId-amendquote-quoteId
  - post-Issue-issueId-declinetoquote
  - post-Issue-issueId-declineJob
  - post-Issue-issueId-appointment
  - put-Issue-issueId-appointment
  - post-Issue-issueid-jobcompletiondetails
  - get-Issue-issueid-jobcompletiondetails
  - post-job-completion-document
  - get-job-completion-documents
  - post-issue-issueid-invoicedetails
  - get-invoice-details
  - submit-invoice
  - post-Issue-Id-Comment
---

# Track a Fixflo repair from quote to completed job and invoice

This is the contractor / job-management side of the Fixflo API — the "Contractor networks"
tag. It is the money path: quote, award, attend, evidence, invoice.

## Before you start

- `Authorization: Bearer [token]` on every call, against the agency's own subdomain host.
- Poll windows exist on the list operations (`CreatedSince`, `UpdatedSince`, `ClosedSince`,
  `JobCreatedSince` and their `*Before` pairs). Use them — do not re-read the whole set.
- Better still, subscribe to the `Issue state change` webhook and poll only to backfill.

## Steps

1. **Find work.** `get-issues` (`GET /Issues`) with a `CreatedSince`/`UpdatedSince` window,
   or the state-specific lists: `get-issues-jobawarded` (`GET /Issues/JobAwarded`),
   `get-issues-jobcompleted` (`GET /Issues/JobCompleted`), `get-issues-closed`
   (`GET /Issues/Closed`).
2. **Quote.** `post-Issue-issueId-Quote` (`POST /Issue/{issueId}/quote`) with `LineItems`.
   Amend with `post-Issue-issueId-amendquote-quoteId`. Read the current position with
   `get-Issue-issueId-quotes`. If you will not quote, say so explicitly with
   `post-Issue-issueId-declinetoquote` rather than going silent.
3. **Accept or decline the job.** Declining is
   `post-Issue-issueId-declineJob` (`POST /Issue/{issueId}/declinejob`) with a
   `JobDeclineReasonMessage`. `post-Issue-issueId-quoteinstead` offers a quote in place of
   accepting a fixed-price job.
4. **Schedule.** `post-Issue-issueId-appointment` (`POST /Issue/{issueId}/appointment`);
   cancel with `put-Issue-issueId-appointment`
   (`PUT /Issue/{issueId}/appointment/{appointmentId}/cancel`).
5. **Assign the engineer.** `post-Issue-issueid-jobjobber` (`POST /Issue/{issueid}/jobjobber`).
6. **Complete with evidence.** `post-Issue-issueid-jobcompletiondetails`
   (`POST /Issue/{issueid}/jobcompletiondetails`), then upload documents with
   `post-job-completion-document` (`POST /issue/{issueid}/completiondoc`) and compliance
   certificates with `post-Issue-issueId-completioncertificatedoc`. Read back with
   `get-job-completion-documents` / `get-Issue-issueid-jobcompletiondetails`; remove a
   mistake with `delete-job-completion-document`.
7. **Further works.** If the visit uncovers more, `post-Issue-issueId-createfurtherworks`
   and `post-Issue-issueId-quotefurtherworks` keep it attached to the same issue instead of
   opening a duplicate.
8. **Invoice.** `post-issue-issueid-invoicedetails` (`POST /issue/{issueid}/invoicedetails`)
   to set `InvoiceDetails` + `LineItem`s, `get-invoice-details` to confirm, then
   `submit-invoice` (`POST /issue/{issueid}/submitinvoice`).
9. **Talk to the agent.** `post-Issue-Id-Comment` (`POST /Issue/{issueId}/Comment`) and
   `post-Issue-issueId-contractornetworkcomment`; read the thread with
   `get-Issue-Id-Comments`.

## Rules

- **`submit-invoice` is the one call you must not blind-retry.** There is no
  `Idempotency-Key`. On a timeout, call `get-invoice-details` first and only resubmit if
  nothing landed.
- Quotes, appointments and completion documents are equally non-replay-safe — read back
  before retrying any `POST` in this flow.
- Errors arrive as the vendor `Envelope` (`HttpStatusCode`, `Errors[]`, `Messages[]`), not
  problem+json, and carry no stable error codes.
- Documents come back as blobs, base-64 or PDF; Fixflo explicitly puts malware scanning on
  the consumer.
- Currency and date presentation follow the agency locale (default `en-GB`); values in the
  API are UTC `yyyy-MM-ddTHH:mm:ss`.

## Related

- `asyncapi/fixflo-webhooks.yml` — `Issue state change` beats polling
- `errors/fixflo-problem-types.yml`
- `conventions/fixflo-conventions.yml`
