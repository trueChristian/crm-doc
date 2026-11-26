# ServiceCue

[Worship and music](../../ministry/worship.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Technical or accessibility cue such as microphone change, interpretation handoff, visual announcement or caption start. Public orders exclude private cues.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `item_id` | → ServicePlanItem | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `team_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `sequence` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `trigger` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `instruction` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `responsible_assignment_id` | → VolunteerAssignment? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `attachment_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### item_id

The target is [ServicePlanItem](ServicePlanItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ServicePlanItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ServicePlanItem·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ServicePlanItem·MISSING | Queue the missing ServicePlanItem mapping or reject the command before linking. |
| Wrong scope | ServicePlanItem·B01 | Do not attach another church’s ServicePlanItem without a supported exchange and local authority. |
| Target rename | Rename ServicePlanItem·A01 after linking | The existing item_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No item_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### team_code

Use versioned classification or status code for `ServiceCue.team_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active team_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped team_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No team_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sequence

Use whole-number measure for `ServiceCue.sequence`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No sequence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### trigger

Use human-readable text for `ServiceCue.trigger`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered trigger in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No trigger at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### instruction

Use human-readable text for `ServiceCue.instruction`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered instruction in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No instruction at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### responsible_assignment_id

The target is [VolunteerAssignment](VolunteerAssignment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VolunteerAssignment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | VolunteerAssignment·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | VolunteerAssignment·MISSING | Queue the missing VolunteerAssignment mapping or reject the command before linking. |
| Wrong scope | VolunteerAssignment·B01 | Do not attach another church’s VolunteerAssignment without a supported exchange and local authority. |
| Target rename | Rename VolunteerAssignment·A01 after linking | The existing responsible_assignment_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No responsible_assignment_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### attachment_ref

Use scoped or external reference for `ServiceCue.attachment_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified attachment_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped attachment_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No attachment_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
