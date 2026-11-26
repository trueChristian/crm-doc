# PathStepResult

[Learning and formation](../../ministry/learning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Satisfied, exempted, deferred, in review or incomplete. A waiver has an authorizer and scope.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `participation_id` | → PathParticipation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `step_id` | → PathStep | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `evidence_id` | → LearningEvidence? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `approved_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `decided_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### participation_id

The target is [PathParticipation](PathParticipation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PathParticipation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PathParticipation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PathParticipation·MISSING | Queue the missing PathParticipation mapping or reject the command before linking. |
| Wrong scope | PathParticipation·B01 | Do not attach another church’s PathParticipation without a supported exchange and local authority. |
| Target rename | Rename PathParticipation·A01 after linking | The existing participation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No participation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### step_id

The target is [PathStep](PathStep.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PathStep·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PathStep·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PathStep·MISSING | Queue the missing PathStep mapping or reject the command before linking. |
| Wrong scope | PathStep·B01 | Do not attach another church’s PathStep without a supported exchange and local authority. |
| Target rename | Rename PathStep·A01 after linking | The existing step_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No step_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_id

The target is [LearningEvidence](LearningEvidence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LearningEvidence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | LearningEvidence·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | LearningEvidence·MISSING | Queue the missing LearningEvidence mapping or reject the command before linking. |
| Wrong scope | LearningEvidence·B01 | Do not attach another church’s LearningEvidence without a supported exchange and local authority. |
| Target rename | Rename LearningEvidence·A01 after linking | The existing evidence_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No evidence_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Use versioned classification or status code for `PathStepResult.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing approved_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No approved_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### decided_on

Use civil calendar date for `PathStepResult.decided_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No decided_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason

Use human-readable text for `PathStepResult.reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
