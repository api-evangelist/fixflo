# Fixflo (fixflo)

Fixflo (a trading name of Tactile Limited, London, United Kingdom, acquired by Aareon in 2021) is a UK repairs, maintenance and compliance management platform for lettings agents, block managers and commercial property managers. Occupiers report issues through a guided fault tree, and Fixflo routes the work to contractors, tracks jobs, service programmes, warranties and invoices, and syncs the resulting records back into the agency CRM. It sits in the post-tenancy operations layer of the UK property value chain rather than the listings layer — the UK has no MLS and no RESO, so there is no industry-mandated machine-readable listing contract here and Fixflo makes no RESO claim. Its API posture is unusually open for the sector in one respect and closed in another. A genuinely public Stoplight developer portal at api-docs.fixflo.com publishes a complete OpenAPI 3.0 description of the v2 API (135 paths, 164 operations, 25 resource tags) that anyone can read and download without logging in, but actually calling it is licensed. Every use of the API is subject to the signed Fixflo Application Developer and API Licence Agreement, keys are issued by support after a review of the use case, and the runtime base URL is the customer's own per-tenant subdomain. Read the contract freely; sign an agreement to use it.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/fixflo/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/fixflo/refs/heads/main/apis.yml)

## Tags

- Real Estate
- United Kingdom
- Property Management
- PropTech
- Repairs and Maintenance
- Block Management
- Lettings
- Rentals
- Commercial Real Estate
- Contractors

## Timestamps

- **Created:** 2026-07-26
- **Modified:** 2026-07-26

## APIs

### Fixflo API v2

The Fixflo v2 REST API, described by a publicly downloadable OpenAPI 3.0 document on the Fixflo Stoplight developer portal. It exposes the repairs and maintenance domain — issues and issue drafts, properties, blocks and estates, agencies, agents, brands and teams, landlords, leaseholders, tenants and customers, contractors and contractor networks, assets and warranties, cost codes, service programmes, service agreements and service events, jobs, custom field configuration and webhook subscriptions. Authentication is a bearer token issued inside a Fixflo account (documented as OAuth2-aligned but deliberately not a full OAuth2 implementation); a separate OpenID Connect discovery document is served anonymously at api.fixflo.com. Production calls are made against the customer's own subdomain (`https://[subdomain].fixflo.com/api/v2`); the published server is the shared sandbox. Rate limiting is documented as not below 500 requests per minute, returning HTTP 429. Use of the API requires the signed Fixflo Application Developer and API Licence Agreement.

- **Human URL:** [https://api-docs.fixflo.com/](https://api-docs.fixflo.com/)
- **Base URL:** `https://api-sandbox.fixflo.com/api/v2`

#### Tags

- Agent
- Agency
- Asset
- Block
- Cost code
- Brand
- Contractor
- Estate
- FaultTree
- Issue
- Issue draft
- Landlord
- Leaseholder
- Property
- Service programme definition
- Team
- Tenant
- Warranty
- Webhook
- Contractor networks
- Customer
- Service Event
- Service Programme
- Service Agreement
- CustomFieldConfiguration

#### Properties

- [OpenAPI](openapi/fixflo-api-v2-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://api-docs.fixflo.com/)
- [API Reference](https://api-docs.fixflo.com/5aaf5f6f6bc52-fixflo)
- [Getting Started](https://api-docs.fixflo.com/72b66de24898e-welcome-to-fixflo)
- [Webhooks](https://api-docs.fixflo.com/5cc9374300b99-webhooks)
- [Authentication](authentication/fixflo-authentication.yml)
- [OpenID Connect Discovery](https://api.fixflo.com/.well-known/openid-configuration)
- [JWKS](https://api.fixflo.com/.well-known/jwks)
- [Overlay](overlays/fixflo-api-v2-overlay.yaml)
- [Conventions](conventions/fixflo-conventions.yml)
- [Error Catalog](errors/fixflo-problem-types.yml)
- [Data Model](data-model/fixflo-data-model.yml)
- [Sandbox](sandbox/fixflo-sandbox.yml)
- [Rate Limits](rate-limits/fixflo-rate-limits.yml)
- [Postman Collection](https://www.postman.com/fixflo/fixflo-public/collection/glxckcp/fixflo-docs)
- [SDK](https://www.nuget.org/packages/Fixflo.WebApi.Client.V2/)
- [Terms of Service](https://fixflostore.blob.core.windows.net/live-assets/SystemApplicationDeveloperAndAPILicenseAgreement.pdf)
- [Support](https://help.fixflo.com/support/solutions/articles/61000295569-api-faqs-commonly-asked-questions-when-creating-an-integration)

## Artifacts

Produced by the API Evangelist enrichment pipeline on 2026-07-26 from the public Fixflo
developer portal and the published OpenAPI. Nothing here is fabricated; absences (no
security.txt, no trust centre, no AsyncAPI, no MCP server, no CLI) are recorded as absences.

- [Authentication profile](authentication/fixflo-authentication.yml) — bearer token for the REST API, plus the separate application OIDC surface
- [OAuth scopes](scopes/fixflo-scopes.yml) — application-login scopes only; the REST API has none
- [Well-known documents](well-known/fixflo-well-known.yml) — OIDC discovery, RFC 8414 metadata, JWKS (raw files harvested)
- [Packages / SDKs](packages/fixflo-packages.yml) — one first-party .NET client on NuGet
- [API conventions](conventions/fixflo-conventions.yml) — auth, tenancy, natural-key upsert idempotency, pagination, locales, error envelope
- [Rate limits](rate-limits/fixflo-rate-limits.yml) — "not below 500 requests a minute", HTTP 429
- [Error catalog](errors/fixflo-problem-types.yml) — the eight documented error responses; not RFC 9457
- [Lifecycle](lifecycle/fixflo-lifecycle.yml) — URI-path versioning, v1 retired, status page, no SLA
- [Conformance](conformance/fixflo-conformance.yml) — what the contract does and does not conform to
- [Data model](data-model/fixflo-data-model.yml) — 96 relationships derived from the 67 schemas
- [Webhook / event surface](asyncapi/fixflo-webhooks.yml) — one event, ff-signature HMAC, retries; no AsyncAPI published
- [Sandbox](sandbox/fixflo-sandbox.yml) — real but provisioned on request; no published test values
- [Agent skills](skills/_index.yml) — five generated skills grounded in verified operationIds
- [MCP candidate tools](mcp/fixflo-mcp.yml) — derived; Fixflo publishes no MCP server
- [Agentic access contracts](agentic-access/fixflo-agentic-access.yml) — recommended `x-agentic-access` per operation
- [OpenAPI overlay](overlays/fixflo-api-v2-overlay.yaml) — our enhancements, applied without mutating the harvested spec
- [Domain security](security/fixflo-domain-security.yml) — TLS/HSTS/DNS probe results
- [llms.txt](llms/fixflo-llms.txt) — generated; Fixflo publishes none

## Common Properties

- [Website](https://www.fixflo.com/)
- [Documentation](https://api-docs.fixflo.com/)
- [API Reference](https://api-docs.fixflo.com/5aaf5f6f6bc52-fixflo)
- [Blog](https://www.fixflo.com/blog)
- [Integrations](https://www.fixflo.com/integrations)
- [Support Knowledge Base](https://help.fixflo.com/support/home)
- [Status Page](https://status.fixflo.com/)
- [Terms of Service](https://www.fixflo.com/legal-and-patents)
- [Privacy Policy](https://www.fixflo.com/privacy-policy)
- [GitHub Organization](https://github.com/Fixflo)
- [LinkedIn](https://www.linkedin.com/company/fixflo)
- [Twitter](https://twitter.com/Fixflo)

## Access Notes

- **Home market:** United Kingdom
- **RESO posture:** No RESO reference found. No RESO Web API or Data Dictionary certification, no RESO directory listing, no OData service root, no `$metadata` document, and no Universal Property Identifier (UPI). RESO is a US/Canadian MLS-centred regime and the UK has no MLS.
- **Access gate:** Licence agreement. The [Fixflo Application Developer and API Licence Agreement](https://fixflostore.blob.core.windows.net/live-assets/SystemApplicationDeveloperAndAPILicenseAgreement.pdf) must be signed before access is granted; keys are requested from `support@fixflo.com` with a described use case, and a Fixflo agency account is a prerequisite because tokens are generated from inside a live Fixflo system.
- **Open data:** None. Fixflo publishes no open dataset. The UK's open property data layer (HM Land Registry Price Paid Data, Ordnance Survey open products) sits entirely outside Fixflo.
- **Auth model:** HTTP `Authorization: Bearer [token]` (64-char token, "aligned with OAuth2 standards but the full range of OAuth2 functionality is not required and has not been implemented"). A real OpenID Connect discovery document for the Fixflo application login is served anonymously at `https://api.fixflo.com/.well-known/openid-configuration`.

## Maintainers

- Kin Lane — kin@apievangelist.com
