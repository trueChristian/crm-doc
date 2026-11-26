# ContinuityExercise

[Continuity exercises, accountability and reunification](../../assurance/continuity-and-reunification.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exercise notifications and test rosters are clearly marked. Starting a live activation creates a separate record with new authorization; a drill cannot silently become live.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `plan_id` | → ContinuityPlan | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `type` | enum(tabletop, practice, activation) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `start_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `end_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `actual_or_drill` | enum(live, drill) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `authorized_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `coordinator_id` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `objective` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `scope_ref` | ID | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `status` | enum(preparing, active, demobilizing, closed, cancelled) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `termination_decision_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ContinuityExercise.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ContinuityExercise·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### plan_id

The target is [ContinuityPlan](ContinuityPlan.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ContinuityPlan·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ContinuityPlan·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ContinuityPlan·MISSING | Queue the missing ContinuityPlan mapping or reject the command before linking. |
| Wrong scope | ContinuityPlan·B01 | Do not attach another church’s ContinuityPlan without a supported exchange and local authority. |
| Target rename | Rename ContinuityPlan·A01 after linking | The existing plan_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No plan_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### type

Declared alternatives in owner order: `tabletop`, `practice`, `activation`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | tabletop | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_type | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### start_at

Use unambiguous point in time for `ContinuityExercise.start_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No start_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### end_at

Use unambiguous point in time for `ContinuityExercise.end_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No end_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### actual_or_drill

Declared alternatives in owner order: `live`, `drill`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | live | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_actual_or_drill | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No actual_or_drill at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authorized_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing authorized_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No authorized_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### coordinator_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing coordinator_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No coordinator_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### objective

Use human-readable text for `ContinuityExercise.objective`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered objective in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No objective at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scope_ref

Use scoped or external reference for `ContinuityExercise.scope_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified scope_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped scope_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No scope_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Declared alternatives in owner order: `preparing`, `active`, `demobilizing`, `closed`, `cancelled`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | preparing | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### termination_decision_ref

Use scoped or external reference for `ContinuityExercise.termination_decision_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified termination_decision_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped termination_decision_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No termination_decision_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccountabilityCohort](AccountabilityCohort.md).`exercise_id` | ContinuityExercise identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountabilityTransfer](AccountabilityTransfer.md).`exercise_id` | ContinuityExercise identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExerciseReview](ExerciseReview.md).`exercise_id` | ContinuityExercise identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FamilyContactAttempt](FamilyContactAttempt.md).`exercise_id` | ContinuityExercise identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReunificationDecision](ReunificationDecision.md).`exercise_id` | ContinuityExercise identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
