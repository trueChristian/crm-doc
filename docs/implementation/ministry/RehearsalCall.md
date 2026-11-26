# RehearsalCall

[Worship and music](../../ministry/worship.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Distinct rehearsal occurrence with its own reservations and availability checks. Schedules reference published material and its authorized audience.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `plan_id` | → ServicePlan | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `occurrence_id` | → EventOccurrence | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `team_id` | → MinistryGroup? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `instructions` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `published_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### plan_id

The target is [ServicePlan](ServicePlan.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ServicePlan·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ServicePlan·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ServicePlan·MISSING | Queue the missing ServicePlan mapping or reject the command before linking. |
| Wrong scope | ServicePlan·B01 | Do not attach another church’s ServicePlan without a supported exchange and local authority. |
| Target rename | Rename ServicePlan·A01 after linking | The existing plan_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No plan_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### team_id

The target is [MinistryGroup](MinistryGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinistryGroup·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinistryGroup·MISSING | Queue the missing MinistryGroup mapping or reject the command before linking. |
| Wrong scope | MinistryGroup·B01 | Do not attach another church’s MinistryGroup without a supported exchange and local authority. |
| Target rename | Rename MinistryGroup·A01 after linking | The existing team_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No team_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### instructions

Use human-readable text for `RehearsalCall.instructions`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered instructions in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No instructions provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### published_at

Use unambiguous point in time for `RehearsalCall.published_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No published_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
