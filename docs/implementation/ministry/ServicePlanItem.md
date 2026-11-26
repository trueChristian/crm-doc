# ServicePlanItem

[Worship and music](../../ministry/worship.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Acyclic sections contain items and subitems. Kinds include welcome, prayer, reading, music, sermon, offering, communion, testimony, announcements and dismissal. Permit silence or an untimed item. A fixed start can expose a timing conflict.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `plan_id` | → ServicePlan | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `parent_id` | → ServicePlanItem? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `sequence` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `duration_minutes` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `fixed_local_start` | time? | Optional under owner conditions | [clock](../value-conventions.md#clock) |
| `lead_person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `visibility` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `content_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### plan_id

The target is [ServicePlan](ServicePlan.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ServicePlan·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ServicePlan·MISSING | Queue the missing ServicePlan mapping or reject the command before linking. |
| Wrong scope | ServicePlan·B01 | Do not attach another church’s ServicePlan without a supported exchange and local authority. |
| Target rename | Rename ServicePlan·A01 after linking | The existing plan_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No plan_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_id

The target is [ServicePlanItem](ServicePlanItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ServicePlanItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ServicePlanItem·MISSING | Queue the missing ServicePlanItem mapping or reject the command before linking. |
| Wrong scope | ServicePlanItem·B01 | Do not attach another church’s ServicePlanItem without a supported exchange and local authority. |
| Target rename | Rename ServicePlanItem·A01 after linking | The existing parent_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### sequence

Use whole-number measure for `ServicePlanItem.sequence`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No sequence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Use versioned classification or status code for `ServicePlanItem.kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `ServicePlanItem.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### duration_minutes

Use whole-number measure for `ServicePlanItem.duration_minutes`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No duration_minutes provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### fixed_local_start

Use local wall-clock time for `ServicePlanItem.fixed_local_start`. Preserve local clock time and associate the relevant zone and civil date when scheduling.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 09:30 local | Preserve local clock time and associate the relevant zone and civil date when scheduling. |
| Malformed or unmapped | 25:10 | Reject invalid clock hour. |
| Scheduled time in a skipped local hour | 02:30 during a local spring-forward gap | Use the recurrence owner’s stated gap rule. |
| Repeated local hour | 01:30 occurs twice on the declared local date | Resolve the occurrence explicitly before issuing reminders. |
| Midnight crossing | 23:50 start and 00:10 next-day end | Associate the correct service date and end date. |
| Absent in intake | No fixed_local_start provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### lead_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing lead_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No lead_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### visibility

Use versioned classification or status code for `ServicePlanItem.visibility`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active visibility code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped visibility code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No visibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### content_ref

Use scoped or external reference for `ServicePlanItem.content_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified content_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped content_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No content_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [MusicUse](MusicUse.md).`item_id` | ServicePlanItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServiceCue](ServiceCue.md).`item_id` | ServicePlanItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServicePlanItem](ServicePlanItem.md).`parent_id` | ServicePlanItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServiceRunEntry](ServiceRunEntry.md).`item_id` | ServicePlanItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
