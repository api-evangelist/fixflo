---
name: Sync a property portfolio from a CRM into Fixflo
description: Upsert estates, blocks, properties, landlords and tenants into Fixflo from an external property management system using external references as the natural key.
api: openapi/fixflo-api-v2-openapi.yml
generated: '2026-07-26'
method: generated
operations:
  - post-estate
  - post-Block
  - post-property
  - post-Property-UpdateAddress
  - post-Landlord
  - post-LandlordProperty
  - post-LandlordPropertyJoin
  - post-Tenant
  - post-Tenant-Id-Property
  - get-Property-Search
  - get-property
  - get-propertyaddress-search
  - get-estates
  - get-blocks
---

# Sync a property portfolio from a CRM into Fixflo

This is the flow behind Fixflo's ~40 CRM integrations. It works because Fixflo's create
endpoints are **upserts keyed on your own external reference**, not blind inserts.

## Before you start

- `Authorization: Bearer [token]`, per-agency token, per-agency subdomain host.
- Decide your external reference scheme first and never change it. `ExternalEstateRef`,
  `ExternalBlockRef`, `ExternalPropertyRef`, `ExternalLandlordRef`, `ExternalRef` (agents,
  contractors, landlords, tenants) — each **must be unique within the agency**. This is the
  only durable join between your system and Fixflo, because Fixflo GUIDs are tenant-scoped.

## Steps — build top down

1. **Estates.** `post-estate` (`POST /Estate`) — create or update, keyed on
   `ExternalEstateRef`. Read back with `get-estates` (paged via `Pg`).
2. **Blocks.** `post-Block` (`POST /Block`) with `EstateId` or `ExternalEstateRef` to place
   the block in its estate, plus `LandlordId`/`ExternalLandlordRef` where the block is
   landlord-owned. List with `get-blocks`.
3. **Properties.** `post-property` (`POST /Property`) — "Update or create a property. If the
   PropertyId has a value > 0 and the property entity exists the property will be updated.
   If the ExternalPropertyRef value is set this value must be unique." Set `BlockId` for
   block-managed stock. Correct an address later with `post-Property-UpdateAddress`.
4. **Landlords and their properties.** `post-Landlord` (`POST /Landlord`), then join with
   `post-LandlordProperty` (`POST /LandlordProperty`) or `post-LandlordPropertyJoin`
   (`POST /LandlordPropertyJoin`) when you are joining by external reference on both sides.
   Unjoin with `post-LandlordProperty-Delete` / `post-LandlordPropertyJoin-Delete`.
5. **Tenants.** `post-Tenant` (`POST /Tenant`), then `post-Tenant-Id-Property`
   (`POST /Tenant/{Id}/Property`) to place the tenant at a property. Remove a tenancy with
   `delete-Tenant-Id-Property-PropertId`.
6. **Verify.** `get-Property-Search` (`GET /Property/Search`) and `get-property`
   (`GET /Property`, which accepts `ExternalPropertyRef`) to confirm what landed;
   `get-propertyaddress-search` for address-level reconciliation.

## Rules

- **Upsert, do not re-create.** Always send the external reference. A create with no `Id`
  and no external reference is the one call that will duplicate on retry.
- **Address hygiene.** `post-propertyaddress-merge` and `post-propertyaddress-split` exist
  for reconciling duplicated address records — use them rather than deleting stock.
- **Pagination is inconsistent.** Some collections page on `Pg` (integer), some on `Page`
  (string), most are unpaged. When the response is a `PrevNextPager`, follow `NextURL`
  rather than recomputing page numbers.
- **Deletes are mostly soft.** Many collections expose an `IsDeleted` filter; treat records
  as tombstoned rather than gone.
- **Right to erasure.** `post-Tenant-Id-Anonymise` (`POST /Tenant/{Id}/Anonymise`) is the
  documented anonymisation path for a tenant. Use it for GDPR erasure instead of deleting.
- **Rate limit** is documented as not below 500 requests/minute → `429`. Batch a portfolio
  sync with your own throttle and resume by external reference, not by page number.

## Related

- `conventions/fixflo-conventions.yml` — the external-reference upsert contract in full
- `data-model/fixflo-data-model.yml` — Estate → Block → Property → Tenant/Landlord edges
