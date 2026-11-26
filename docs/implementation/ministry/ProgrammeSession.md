# ProgrammeSession

[Programmes, hospitality and personal itineraries](../../ministry/programmes.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Access can be open, require general admission, require separate reservation, or be an authorized staff-only activity. An occurrence belongs once per programme. Reject cross-programme cycles in prerequisites.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `programme_id` | → MinistryProgramme | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `occurrence_id` | → EventOccurrence | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `track_id` | → ProgrammeTrack? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `access_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `choice_group` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `prerequisite_session_id` | → ProgrammeSession? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### programme_id

The target is [MinistryProgramme](MinistryProgramme.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryProgramme·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinistryProgramme·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinistryProgramme·MISSING | Queue the missing MinistryProgramme mapping or reject the command before linking. |
| Wrong scope | MinistryProgramme·B01 | Do not attach another church’s MinistryProgramme without a supported exchange and local authority. |
| Target rename | Rename MinistryProgramme·A01 after linking | The existing programme_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No programme_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### occurrence_id

The target is [EventOccurrence](EventOccurrence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EventOccurrence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EventOccurrence·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EventOccurrence·MISSING | Queue the missing EventOccurrence mapping or reject the command before linking. |
| Wrong scope | EventOccurrence·B01 | Do not attach another church’s EventOccurrence without a supported exchange and local authority. |
| Target rename | Rename EventOccurrence·A01 after linking | The existing occurrence_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No occurrence_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### track_id

The target is [ProgrammeTrack](ProgrammeTrack.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProgrammeTrack·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProgrammeTrack·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProgrammeTrack·MISSING | Queue the missing ProgrammeTrack mapping or reject the command before linking. |
| Wrong scope | ProgrammeTrack·B01 | Do not attach another church’s ProgrammeTrack without a supported exchange and local authority. |
| Target rename | Rename ProgrammeTrack·A01 after linking | The existing track_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No track_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### access_code

Use versioned classification or status code for `ProgrammeSession.access_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active access_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped access_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No access_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### choice_group

Use versioned classification or status code for `ProgrammeSession.choice_group`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active choice_group code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped choice_group code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No choice_group provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### prerequisite_session_id

The target is [ProgrammeSession](ProgrammeSession.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProgrammeSession·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProgrammeSession·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProgrammeSession·MISSING | Queue the missing ProgrammeSession mapping or reject the command before linking. |
| Wrong scope | ProgrammeSession·B01 | Do not attach another church’s ProgrammeSession without a supported exchange and local authority. |
| Target rename | Rename ProgrammeSession·A01 after linking | The existing prerequisite_session_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No prerequisite_session_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [HospitalityOffer](HospitalityOffer.md).`session_id` | ProgrammeSession identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProgrammeSelection](ProgrammeSelection.md).`session_id` | ProgrammeSession identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProgrammeSession](ProgrammeSession.md).`prerequisite_session_id` | ProgrammeSession identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
