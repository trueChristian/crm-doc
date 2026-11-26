# CourseSession

[Learning and formation](../../ministry/learning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Connect lesson, teacher and attendance. A replacement session explicitly references the affected occurrence through its revision.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `offering_id` | → CourseOffering | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `occurrence_id` | → EventOccurrence | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `unit_id` | → LearningUnit? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `session_number` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `teacher_person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### offering_id

The target is [CourseOffering](CourseOffering.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CourseOffering·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CourseOffering·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CourseOffering·MISSING | Queue the missing CourseOffering mapping or reject the command before linking. |
| Wrong scope | CourseOffering·B01 | Do not attach another church’s CourseOffering without a supported exchange and local authority. |
| Target rename | Rename CourseOffering·A01 after linking | The existing offering_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No offering_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### unit_id

The target is [LearningUnit](LearningUnit.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LearningUnit·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | LearningUnit·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | LearningUnit·MISSING | Queue the missing LearningUnit mapping or reject the command before linking. |
| Wrong scope | LearningUnit·B01 | Do not attach another church’s LearningUnit without a supported exchange and local authority. |
| Target rename | Rename LearningUnit·A01 after linking | The existing unit_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No unit_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### session_number

Use whole-number measure for `CourseSession.session_number`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No session_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### teacher_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing teacher_person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No teacher_person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
