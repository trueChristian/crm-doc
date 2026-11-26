# CallAssignment

[Community communication](../../communications/community-communication.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique activation/intended person/contact purpose, unless a second call is a documented escalation. Prohibit cycles and self-assignment. Follow caller capacity and time windows.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `tree_id` | ContactTree ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `activation_key` | opaque | Required when the record reaches its applicable state | [key](../value-conventions.md#key) |
| `caller_person_id` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `intended_person_id` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `endpoint_id` | DeliveryEndpoint ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `parent_assignment_id` | CallAssignment ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `backup_caller_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `deadline_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `outcome` | pending/attempted/confirmed/no_answer/wrong_number/help_requested/skipped | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `outcome_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `note_restricted` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### tree_id

The target is [ContactTree](ContactTree.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ContactTree·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ContactTree·MISSING | Queue the missing ContactTree mapping or reject the command before linking. |
| Wrong scope | ContactTree·B01 | Do not attach another church’s ContactTree without a supported exchange and local authority. |
| Target rename | Rename ContactTree·A01 after linking | The existing tree_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No tree_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### activation_key

Use opaque identity or token for `CallAssignment.activation_key`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CallAssignment·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Incomplete record | No activation_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### caller_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing caller_person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No caller_person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### intended_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing intended_person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No intended_person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### endpoint_id

The target is [DeliveryEndpoint](DeliveryEndpoint.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DeliveryEndpoint·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | DeliveryEndpoint·MISSING | Queue the missing DeliveryEndpoint mapping or reject the command before linking. |
| Wrong scope | DeliveryEndpoint·B01 | Do not attach another church’s DeliveryEndpoint without a supported exchange and local authority. |
| Target rename | Rename DeliveryEndpoint·A01 after linking | The existing endpoint_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No endpoint_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_assignment_id

The target is [CallAssignment](CallAssignment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CallAssignment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | CallAssignment·MISSING | Queue the missing CallAssignment mapping or reject the command before linking. |
| Wrong scope | CallAssignment·B01 | Do not attach another church’s CallAssignment without a supported exchange and local authority. |
| Target rename | Rename CallAssignment·A01 after linking | The existing parent_assignment_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_assignment_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### backup_caller_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing backup_caller_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No backup_caller_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### deadline_at

Use unambiguous point in time for `CallAssignment.deadline_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No deadline_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### outcome

Declared alternatives in owner order: `pending`, `attempted`, `confirmed`, `no_answer`, `wrong_number`, `help_requested`, `skipped`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | pending | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_outcome | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No outcome at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### outcome_at

Use unambiguous point in time for `CallAssignment.outcome_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No outcome_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### note_restricted

Use human-readable text for `CallAssignment.note_restricted`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered note_restricted in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No note_restricted provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CallAssignment](CallAssignment.md).`parent_assignment_id` | CallAssignment identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
