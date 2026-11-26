# ExerciseReview

[Continuity exercises, accountability and reunification](../../assurance/continuity-and-reunification.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Record measured outcomes, limitations, responsible owners, deadlines and retest results. Privacy review before distribution.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `exercise_id` | → ContinuityExercise | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `review_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `facilitator_id` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `goals_and_results` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `unresolved_counts` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `recovery_decision_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `safe_lessons` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `protected_appendix_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `action_refs` | → AssuranceFinding set | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `approved_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `published_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ExerciseReview.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ExerciseReview·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### exercise_id

The target is [ContinuityExercise](ContinuityExercise.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ContinuityExercise·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ContinuityExercise·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ContinuityExercise·MISSING | Queue the missing ContinuityExercise mapping or reject the command before linking. |
| Wrong scope | ContinuityExercise·B01 | Do not attach another church’s ContinuityExercise without a supported exchange and local authority. |
| Target rename | Rename ContinuityExercise·A01 after linking | The existing exercise_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No exercise_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### review_on

Use civil calendar date for `ExerciseReview.review_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No review_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### facilitator_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing facilitator_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No facilitator_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### goals_and_results

Use human-readable text for `ExerciseReview.goals_and_results`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered goals_and_results in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No goals_and_results at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unresolved_counts

Use whole-number measure for `ExerciseReview.unresolved_counts`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No unresolved_counts at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recovery_decision_ref

Use scoped or external reference for `ExerciseReview.recovery_decision_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified recovery_decision_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped recovery_decision_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No recovery_decision_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### safe_lessons

Use human-readable text for `ExerciseReview.safe_lessons`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered safe_lessons in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No safe_lessons at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### protected_appendix_ref

Use scoped or external reference for `ExerciseReview.protected_appendix_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified protected_appendix_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped protected_appendix_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No protected_appendix_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### action_refs

The target is [AssuranceFinding](AssuranceFinding.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AssuranceFinding·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AssuranceFinding·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AssuranceFinding·MISSING | Queue the missing AssuranceFinding mapping or reject the command before linking. |
| Wrong scope | AssuranceFinding·B01 | Do not attach another church’s AssuranceFinding without a supported exchange and local authority. |
| Target rename | Rename AssuranceFinding·A01 after linking | The existing action_refs keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No action_refs at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### published_at

Use unambiguous point in time for `ExerciseReview.published_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

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
