# OccurrenceOverride

[Calendars and occurrences](../../ministry/calendar.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One effective override per field and revision. Cancelling a date retains a cancellation marker so expansion cannot recreate it.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `occurrence_id` | → EventOccurrence | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `field_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `replacement_value` | typed_value | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |
| `reason` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `changed_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `changed_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

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

### field_code

Use versioned classification or status code for `OccurrenceOverride.field_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active field_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped field_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No field_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### replacement_value

Use typed value or bounded compound record for `OccurrenceOverride.replacement_value`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of replacement_value matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for replacement_value | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No replacement_value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reason

Use human-readable text for `OccurrenceOverride.reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### changed_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing changed_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No changed_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### changed_at

Use unambiguous point in time for `OccurrenceOverride.changed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No changed_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
