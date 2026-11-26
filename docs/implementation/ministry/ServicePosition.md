# ServicePosition

[Volunteers and rotas](../../ministry/volunteers.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One ministry has many positions, such as driver, door steward or interpreter. Restrict changes to requirements after appointment and flag affected future assignments for review.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `group_id` | → MinistryGroup | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `responsibilities` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `skill_code` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `minimum_age` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `training_required` | bool | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `conflict_group` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `active` | bool | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### group_id

The target is [MinistryGroup](MinistryGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinistryGroup·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinistryGroup·MISSING | Queue the missing MinistryGroup mapping or reject the command before linking. |
| Wrong scope | MinistryGroup·B01 | Do not attach another church’s MinistryGroup without a supported exchange and local authority. |
| Target rename | Rename MinistryGroup·A01 after linking | The existing group_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No group_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `ServicePosition.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### responsibilities

Use human-readable text for `ServicePosition.responsibilities`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered responsibilities in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No responsibilities at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### skill_code

Use versioned classification or status code for `ServicePosition.skill_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active skill_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped skill_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No skill_code provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### minimum_age

Use whole-number measure for `ServicePosition.minimum_age`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No minimum_age provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### training_required

Use explicit logical choice for `ServicePosition.training_required`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No training_required at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### conflict_group

Use versioned classification or status code for `ServicePosition.conflict_group`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active conflict_group code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped conflict_group code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No conflict_group provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### active

Use explicit logical choice for `ServicePosition.active`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No active at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DutyShift](DutyShift.md).`position_id` | ServicePosition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PositionRequirement](PositionRequirement.md).`position_id` | ServicePosition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerApplication](VolunteerApplication.md).`position_id` | ServicePosition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
