# ContactRestriction

[Recipients and channel policy](../../communications/recipients-and-channels.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Requires a target and typed scope. A verified safety block dominates automatic fallback. Restrict visibility of the reason and affected households.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `person_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `endpoint_id` | DeliveryEndpoint ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `scope` | all/purpose/channel/endpoint | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `purpose_id` | CommunicationPurpose ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `channel` | enum? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `reason` | unsafe_address/reassigned/complaint/invalid/deceased/personal_request | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `active_from` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `ends_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `authorized_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `protected_note` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### endpoint_id

The target is [DeliveryEndpoint](DeliveryEndpoint.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DeliveryEndpoint·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DeliveryEndpoint·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DeliveryEndpoint·MISSING | Queue the missing DeliveryEndpoint mapping or reject the command before linking. |
| Wrong scope | DeliveryEndpoint·B01 | Do not attach another church’s DeliveryEndpoint without a supported exchange and local authority. |
| Target rename | Rename DeliveryEndpoint·A01 after linking | The existing endpoint_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No endpoint_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### scope

Declared alternatives in owner order: `all`, `purpose`, `channel`, `endpoint`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | all | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_scope | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose_id

The target is [CommunicationPurpose](CommunicationPurpose.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CommunicationPurpose·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CommunicationPurpose·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CommunicationPurpose·MISSING | Queue the missing CommunicationPurpose mapping or reject the command before linking. |
| Wrong scope | CommunicationPurpose·B01 | Do not attach another church’s CommunicationPurpose without a supported exchange and local authority. |
| Target rename | Rename CommunicationPurpose·A01 after linking | The existing purpose_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No purpose_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### channel

Use versioned classification or status code for `ContactRestriction.channel`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active channel code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped channel code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No channel provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason

Declared alternatives in owner order: `unsafe_address`, `reassigned`, `complaint`, `invalid`, `deceased`, `personal_request`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | unsafe_address | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_reason | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### active_from

Use unambiguous point in time for `ContactRestriction.active_from`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No active_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ends_at

Use unambiguous point in time for `ContactRestriction.ends_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No ends_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### authorized_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing authorized_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No authorized_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### protected_note

Use human-readable text for `ContactRestriction.protected_note`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered protected_note in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No protected_note provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
