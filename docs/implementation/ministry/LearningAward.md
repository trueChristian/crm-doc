# LearningAward

[Learning and formation](../../ministry/learning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exactly one completion source. Unique serial within the organization. Reprinting preserves serial and any withdrawal. Public verification, if offered, discloses the minimum approved information.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `enrolment_id` | → LearningEnrolment? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `participation_id` | → PathParticipation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `serial` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `issued_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `expires_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `withdrawn_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `issuer_id` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### enrolment_id

The target is [LearningEnrolment](LearningEnrolment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LearningEnrolment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | LearningEnrolment·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | LearningEnrolment·MISSING | Queue the missing LearningEnrolment mapping or reject the command before linking. |
| Wrong scope | LearningEnrolment·B01 | Do not attach another church’s LearningEnrolment without a supported exchange and local authority. |
| Target rename | Rename LearningEnrolment·A01 after linking | The existing enrolment_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No enrolment_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### participation_id

The target is [PathParticipation](PathParticipation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PathParticipation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PathParticipation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PathParticipation·MISSING | Queue the missing PathParticipation mapping or reject the command before linking. |
| Wrong scope | PathParticipation·B01 | Do not attach another church’s PathParticipation without a supported exchange and local authority. |
| Target rename | Rename PathParticipation·A01 after linking | The existing participation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No participation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### title

Use human-readable text for `LearningAward.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### serial

Use human-readable text for `LearningAward.serial`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered serial in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No serial at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### issued_on

Use civil calendar date for `LearningAward.issued_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No issued_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expires_on

Use civil calendar date for `LearningAward.expires_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No expires_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### withdrawn_on

Use civil calendar date for `LearningAward.withdrawn_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No withdrawn_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### issuer_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing issuer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No issuer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
