# GroupRolePeriod

[Groups and participation](../../ministry/groups.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Roles can overlap when different. Same person's periods for the same role cannot overlap. Role and participation must belong to same group.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `participation_id` | → GroupParticipation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `role_id` | → GroupRole | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `from_date` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `until_date` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `appointed_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `basis` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### participation_id

The target is [GroupParticipation](GroupParticipation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GroupParticipation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GroupParticipation·MISSING | Queue the missing GroupParticipation mapping or reject the command before linking. |
| Wrong scope | GroupParticipation·B01 | Do not attach another church’s GroupParticipation without a supported exchange and local authority. |
| Target rename | Rename GroupParticipation·A01 after linking | The existing participation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No participation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### role_id

The target is [GroupRole](GroupRole.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GroupRole·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GroupRole·MISSING | Queue the missing GroupRole mapping or reject the command before linking. |
| Wrong scope | GroupRole·B01 | Do not attach another church’s GroupRole without a supported exchange and local authority. |
| Target rename | Rename GroupRole·A01 after linking | The existing role_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No role_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### from_date

Use civil calendar date for `GroupRolePeriod.from_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No from_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### until_date

Use civil calendar date for `GroupRolePeriod.until_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No until_date provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### appointed_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing appointed_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No appointed_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### basis

Use human-readable text for `GroupRolePeriod.basis`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered basis in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No basis provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
