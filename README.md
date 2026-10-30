# Fixflo

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Fixflo (a trading name of Tactile Limited, London, United Kingdom, acquired by Aareon in 2021) is a UK repairs, maintenance and compliance management platform for lettings agents, block managers and commercial property managers. Occupiers report issues through a guided fault tree, and Fixflo routes the work to contractors, tracks jobs, service programmes, warranties and invoices, and syncs the resulting records back into the agency CRM. It sits in the post-tenancy operations layer of the UK property value chain rather than the listings layer — the UK has no MLS and no RESO, so there is no industry-mandated machine-readable listing contract here and Fixflo makes no RESO claim. Its API posture is unusually open for the sector in one respect and closed in another. A genuinely public Stoplight developer portal at api-docs.fixflo.com publishes a complete OpenAPI 3.0 description of the v2 API (135 paths, 164 operations, 25 resource tags) that anyone can read and download without logging in, but actually calling it is licensed. Every use of the API is subject to the signed Fixflo Application Developer and API Licence Agreement, keys are issued by support after a review of the use case, and the runtime base URL is the customer's own per-tenant subdomain. Read the contract freely; sign an agreement to use it.

**Areas:** Real Estate · United Kingdom · Property Management · PropTech · Repairs and Maintenance · Block Management · Lettings · Rentals · Commercial Real Estate · Contractors

## Fixflo on APIs.io

Everything profiled for Fixflo is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/fixflo/](https://apis.io/providers/fixflo/)** — or go straight to one of the APIs or properties below.

### APIs (24)

- [Fixflo Agency API](https://apis.io/apis/fixflo/fixflo-agency-api/) — The Agency API from Fixflo — 5 operation(s) for agency.
- [Fixflo Agent API](https://apis.io/apis/fixflo/fixflo-agent-api/) — The Agent API from Fixflo — 3 operation(s) for agent.
- [Fixflo Asset API](https://apis.io/apis/fixflo/fixflo-asset-api/) — The Asset API from Fixflo — 3 operation(s) for asset.
- [Fixflo Block API](https://apis.io/apis/fixflo/fixflo-block-api/) — The Block API from Fixflo — 4 operation(s) for block.
- [Fixflo Brand API](https://apis.io/apis/fixflo/fixflo-brand-api/) — The Brand API from Fixflo — 2 operation(s) for brand.
- [Fixflo Contractor API](https://apis.io/apis/fixflo/fixflo-contractor-api/) — The Contractor API from Fixflo — 5 operation(s) for contractor.
- [Fixflo Contractor networks API](https://apis.io/apis/fixflo/fixflo-contractor-networks-api/) — The Contractor networks API from Fixflo — 27 operation(s) for contractor networks.
- [Fixflo Cost code API](https://apis.io/apis/fixflo/fixflo-cost-code-api/) — The Cost code API from Fixflo — 2 operation(s) for cost code.
- [Fixflo Estate API](https://apis.io/apis/fixflo/fixflo-estate-api/) — The Estate API from Fixflo — 3 operation(s) for estate.
- [Fixflo Fault Tree API](https://apis.io/apis/fixflo/fixflo-faulttree-api/) — The FaultTree API from Fixflo — 1 operation(s) for faulttree.
- [Fixflo Issue API](https://apis.io/apis/fixflo/fixflo-issue-api/) — The Issue API from Fixflo — 11 operation(s) for issue.
- [Fixflo Issue draft API](https://apis.io/apis/fixflo/fixflo-issue-draft-api/) — The Issue draft API from Fixflo — 7 operation(s) for issue draft.
- [Fixflo Job API](https://apis.io/apis/fixflo/fixflo-job-api/) — The Job API from Fixflo — 1 operation(s) for job.
- [Fixflo Landlord API](https://apis.io/apis/fixflo/fixflo-landlord-api/) — The Landlord API from Fixflo — 8 operation(s) for landlord.
- [Fixflo Leaseholder API](https://apis.io/apis/fixflo/fixflo-leaseholder-api/) — The Leaseholder API from Fixflo — 9 operation(s) for leaseholder.
- [Fixflo Media API](https://apis.io/apis/fixflo/fixflo-media-api/) — The Media API from Fixflo — 3 operation(s) for media.
- [Fixflo Property API](https://apis.io/apis/fixflo/fixflo-property-api/) — The Property API from Fixflo — 15 operation(s) for property.
- [Fixflo Service Event API](https://apis.io/apis/fixflo/fixflo-service-event-api/) — The Service Event API from Fixflo — 7 operation(s) for service event.
- [Fixflo Service Programme API](https://apis.io/apis/fixflo/fixflo-service-programme-api/) — The Service Programme API from Fixflo — 4 operation(s) for service programme.
- [Fixflo Service programme definition API](https://apis.io/apis/fixflo/fixflo-service-programme-definition-api/) — The Service programme definition API from Fixflo — 2 operation(s) for service programme definition.
- [Fixflo Team API](https://apis.io/apis/fixflo/fixflo-team-api/) — The Team API from Fixflo — 2 operation(s) for team.
- [Fixflo Tenant API](https://apis.io/apis/fixflo/fixflo-tenant-api/) — The Tenant API from Fixflo — 7 operation(s) for tenant.
- [Fixflo Warranty API](https://apis.io/apis/fixflo/fixflo-warranty-api/) — The Warranty API from Fixflo — 3 operation(s) for warranty.
- [Fixflo Webhook API](https://apis.io/apis/fixflo/fixflo-webhook-api/) — The Webhook API from Fixflo — 4 operation(s) for webhook.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Fixflo Webhooks](https://apis.io/asyncapis/fixflo/fixflo-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [fixflo](https://apis.io/servers/fixflo/fixflo/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Fixflo Agentic Access](https://apis.io/agentic-access/fixflo/fixflo-agentic-access/)

#### Collections (1)

Postman and Open Collection request collections.

- [Fixflo](https://apis.io/collections/fixflo/open-fixflo-api-v2/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Fixflo Api V2 Overlay](https://apis.io/overlays/fixflo/fixflo-api-v2-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Fixflo Authentication](https://apis.io/security/fixflo/fixflo-authentication/)
- [Fixflo Domain Security](https://apis.io/security/fixflo/fixflo-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Fixflo Scopes](https://apis.io/scopes/fixflo/fixflo-scopes/)

#### Rate limits (1)

Published request limits.

- [Fixflo Rate Limits](https://apis.io/rate-limits/fixflo/fixflo-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.fixflo.com/)
- [Documentation](https://api-docs.fixflo.com/)
- [Getting started](https://api-docs.fixflo.com/72b66de24898e-welcome-to-fixflo)
- [API reference](https://api-docs.fixflo.com/5aaf5f6f6bc52-fixflo)
- [Pricing](https://www.fixflo.com/pricing)
- [Support](https://help.fixflo.com/support/solutions/articles/61000295569-api-faqs-commonly-asked-questions-when-creating-an-integration)
- [Blog](https://www.fixflo.com/blog)
- [Terms of service](https://www.fixflo.com/legal-and-patents)
- [Privacy policy](https://www.fixflo.com/privacy-policy)
- [GitHub](https://github.com/Fixflo)
- [Status](https://status.fixflo.com/)

## API Evangelist rating

**Kin Score 43.1** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 66.1 |
| Contract quality | 53.6 |
| Contract governance | 4.5 |
| Operational transparency | 39.5 |
| Developer ergonomics | 32.7 |
| Access clarity | 38.2 |

**Agent readiness 39.2** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | — |

**Regulatory alignment 34.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/fixflo/](https://apis.io/providers/fixflo/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Fixflo: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/fixflo/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
