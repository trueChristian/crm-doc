# ResolutionAction

[Minutes, resolutions and the archive](../../governance/minutes-and-resolutions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exactly one accountable owner at assignment. Dependencies must be acyclic. Store reassignment, deadlines and escalation history. Several actions can implement a single resolution.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `resolution_id` | Resolution ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `owner_person_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `owner_body_id` | GoverningBody ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `due_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `urgency` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `state` | proposed/assigned/in_progress/blocked/done/verified/cancelled | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `completion_evidence` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `reviewed_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `completed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `predecessor_id` | ResolutionAction ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### resolution_id

The target is [Resolution](Resolution.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Resolution·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Resolution·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Resolution·MISSING | Queue the missing Resolution mapping or reject the command before linking. |
| Wrong scope | Resolution·B01 | Do not attach another church’s Resolution without a supported exchange and local authority. |
| Target rename | Rename Resolution·A01 after linking | The existing resolution_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No resolution_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### description

Use human-readable text for `ResolutionAction.description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### owner_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing owner_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No owner_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### owner_body_id

The target is [GoverningBody](GoverningBody.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GoverningBody·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GoverningBody·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GoverningBody·MISSING | Queue the missing GoverningBody mapping or reject the command before linking. |
| Wrong scope | GoverningBody·B01 | Do not attach another church’s GoverningBody without a supported exchange and local authority. |
| Target rename | Rename GoverningBody·A01 after linking | The existing owner_body_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No owner_body_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_at

Use unambiguous point in time for `ResolutionAction.due_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No due_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### urgency

Use versioned classification or status code for `ResolutionAction.urgency`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active urgency code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped urgency code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No urgency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `proposed`, `assigned`, `in_progress`, `blocked`, `done`, `verified`, `cancelled`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | proposed | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### completion_evidence

Use human-readable text for `ResolutionAction.completion_evidence`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered completion_evidence in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No completion_evidence provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reviewed_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing reviewed_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reviewed_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### completed_at

Use unambiguous point in time for `ResolutionAction.completed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No completed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### predecessor_id

The target is [ResolutionAction](ResolutionAction.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ResolutionAction·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ResolutionAction·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ResolutionAction·MISSING | Queue the missing ResolutionAction mapping or reject the command before linking. |
| Wrong scope | ResolutionAction·B01 | Do not attach another church’s ResolutionAction without a supported exchange and local authority. |
| Target rename | Rename ResolutionAction·A01 after linking | The existing predecessor_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No predecessor_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [ResolutionAction](ResolutionAction.md).`predecessor_id` | ResolutionAction identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
