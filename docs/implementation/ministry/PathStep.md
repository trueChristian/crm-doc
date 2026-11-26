# PathStep

[Learning and formation](../../ministry/learning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One path has many steps. Dependencies use PathDependency. An optional activity cannot silently become mandatory after enrolment.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `path_id` | → FormationPath | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `label` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `curriculum_id` | → Curriculum? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `required` | bool | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `approval_role` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `completion_evidence` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### path_id

The target is [FormationPath](FormationPath.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FormationPath·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FormationPath·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FormationPath·MISSING | Queue the missing FormationPath mapping or reject the command before linking. |
| Wrong scope | FormationPath·B01 | Do not attach another church’s FormationPath without a supported exchange and local authority. |
| Target rename | Rename FormationPath·A01 after linking | The existing path_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No path_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### label

Use human-readable text for `PathStep.label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No label at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Use versioned classification or status code for `PathStep.kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### curriculum_id

The target is [Curriculum](Curriculum.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Curriculum·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Curriculum·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Curriculum·MISSING | Queue the missing Curriculum mapping or reject the command before linking. |
| Wrong scope | Curriculum·B01 | Do not attach another church’s Curriculum without a supported exchange and local authority. |
| Target rename | Rename Curriculum·A01 after linking | The existing curriculum_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No curriculum_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### required

Use explicit logical choice for `PathStep.required`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No required at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approval_role

Use versioned classification or status code for `PathStep.approval_role`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active approval_role code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped approval_role code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No approval_role provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### completion_evidence

Use versioned classification or status code for `PathStep.completion_evidence`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active completion_evidence code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped completion_evidence code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No completion_evidence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PathDependency](PathDependency.md).`requires_step_id` | PathStep identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PathDependency](PathDependency.md).`step_id` | PathStep identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PathStepResult](PathStepResult.md).`step_id` | PathStep identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
