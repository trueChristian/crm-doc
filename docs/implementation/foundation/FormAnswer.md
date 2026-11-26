# FormAnswer

[Applying church policy to forms and approvals](../../foundation/configuration.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Enforce the question's type and cardinality. The question belongs to the submitted edition. Corrections have an amendment, reason and actor.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `submission_id` | → FormSubmission | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `question_id` | → FormQuestion | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `ordinal` | integer | Required at applicable lifecycle step | [integer](../value-conventions.md#integer) |
| `value` | typed | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `classification` | code | Required at applicable lifecycle step | [vocab](../value-conventions.md#vocab) |
| `source_language` | optional tag | Optional under owner conditions | [structured](../value-conventions.md#structured) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### submission_id

The target is [FormSubmission](../platform/FormSubmission.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FormSubmission·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FormSubmission·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FormSubmission·MISSING | Queue the missing FormSubmission mapping or reject the command before linking. |
| Wrong scope | FormSubmission·B01 | Do not attach another church’s FormSubmission without a supported exchange and local authority. |
| Target rename | Rename FormSubmission·A01 after linking | The existing submission_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No submission_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### question_id

The target is [FormQuestion](FormQuestion.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FormQuestion·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FormQuestion·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FormQuestion·MISSING | Queue the missing FormQuestion mapping or reject the command before linking. |
| Wrong scope | FormQuestion·B01 | Do not attach another church’s FormQuestion without a supported exchange and local authority. |
| Target rename | Rename FormQuestion·A01 after linking | The existing question_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No question_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ordinal

Use whole-number measure for `FormAnswer.ordinal`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No ordinal at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### value

Use typed value or bounded compound record for `FormAnswer.value`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of value matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for value | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### classification

Use versioned classification or status code for `FormAnswer.classification`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active classification code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped classification code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No classification at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_language

Use typed value or bounded compound record for `FormAnswer.source_language`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of source_language matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for source_language | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Absent in intake | No source_language provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
