---
name: Run planned maintenance and compliance programmes in Fixflo
description: Define service programmes, schedule and complete service events against properties and blocks, and keep assets and warranties current for compliance reporting.
api: openapi/fixflo-api-v2-openapi.yml
generated: '2026-07-26'
method: generated
operations:
  - post-serviceprogrammedef
  - get-serviceprogrammedef
  - get-serviceprogrammes
  - get-serviceprogrammes-by-property
  - get-serviceprogramme
  - get-ServiceEvents
  - get-ServiceEvent
  - get-Property-propertyId-ServiceProgramme-serviceProgrammeId-ServiceEvents
  - post-Property-propertyId-ServiceProgramme-serviceProgrammeId-ServiceEvent
  - post-Property-propertyId-ServiceProgramme-serviceProgramme-ServiceEvent-Complete
  - post-ServiceEvent-CreateRemedial
  - get-ServiceEvent-Media
  - post-Asset
  - put-Asset-id
  - get-Assets
  - post-warranty-add
  - post-warranty-save
---

# Run planned maintenance and compliance programmes in Fixflo

Reactive repairs are only half of Fixflo. The other half is planned, statutory work — gas
safety, electrical, fire — modelled as service programme definitions that generate dated
service events against a property or block.

## Steps

1. **Define the programme.** `post-serviceprogrammedef` (`POST /ServiceProgrammeDef`)
   creates the reusable definition (what the check is, how often, whether it is statutory).
   Read one with `get-serviceprogrammedef` (`GET /ServiceProgrammeDef`) and list them with
   `GET /ServiceProgrammeDefs` — whose operationId in the published spec is the malformed
   `get-serviceprogrammedefs?pg=-pg-&keyword=-keyword-&IsDisabled=-isDisabled`, so match on
   the path, not the id.
2. **See what is running.** `get-serviceprogrammes` (`GET /ServiceProgrammes`) across the
   agency, `get-serviceprogrammes-by-property`
   (`GET /Property/{propertyId}/ServiceProgrammes`) for one property, or
   `get-serviceprogramme` for one programme. A `ServiceProgramme` carries
   `MostRecentServiceEvent` and `MostRecentCompliantServiceEvent` — that pair is the
   compliance answer.
3. **Query the due list.** `get-ServiceEvents` (`GET /ServiceEvents`) supports
   `dueDateSince`/`dueDateBefore`, `completedDateSince`/`completedDateBefore`,
   `instructionDateSince`/`instructionDateBefore`, `complianceState`, `isStatutory` and
   `FailedOnly`. `FailedOnly` plus a due-date window is the overdue-compliance report.
4. **Raise an event.** `post-Property-propertyId-ServiceProgramme-serviceProgrammeId-ServiceEvent`
   (`POST /Property/{propertyId}/ServiceProgramme/{serviceProgrammeId}/ServiceEvent`) to
   schedule a visit; update it with the `{serviceEventId}` variant.
5. **Complete it.** `post-Property-propertyId-ServiceProgramme-serviceProgramme-ServiceEvent-Complete`
   with a `ServiceEventComplete` body. Certificates and photos attach as media — read them
   back with `get-ServiceEvent-Media` (`GET /ServiceEvent/{id}/Medias`).
6. **Fail and remediate.** When a check fails, `post-ServiceEvent-CreateRemedial`
   (`POST /ServiceEvent/CreateRemedial`) opens the remedial work as a linked issue rather
   than a disconnected new report — that link is what keeps the compliance audit trail
   intact.
7. **Keep the asset register current.** `post-Asset` / `put-Asset-id` for the appliance or
   plant the programme covers (`ExternalAssetRef` is your natural key), `get-Assets` to
   reconcile, and `post-warranty-add` / `post-warranty-save` for warranty cover.
   `post-Asset` is one of the few operations that declares a real `400`, and `put-Asset-id`
   a real `404` — handle both.

## Rules

- Service events hang off **either** a property or a block; a block-managed programme uses
  `BlockId`/`ExternalBlockRef`. Sending both keys inconsistently is the usual source of
  orphaned events.
- All dates are UTC `yyyy-MM-ddTHH:mm:ss`, dates `yyyy-MM-dd`. Compliance windows are
  date-sensitive — do not let a local timezone shift a due date across a day boundary.
- No `Idempotency-Key`. Read the event list back before retrying a create; a duplicated
  statutory event is worse than a missing one because it corrupts the compliance history.
- Errors return the vendor `Envelope` with free-text `Errors[]`; there is no compliance-
  specific error vocabulary.

## Related

- `data-model/fixflo-data-model.yml` — ServiceProgrammeDef → ServiceProgramme → ServiceEvent
- `conventions/fixflo-conventions.yml`
- `errors/fixflo-problem-types.yml`
