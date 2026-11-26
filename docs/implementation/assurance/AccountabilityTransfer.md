# AccountabilityTransfer

[Continuity exercises, accountability and reunification](../../assurance/continuity-and-reunification.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Two distinct cohorts in one activation. Dispatch changes the current disposition to in_transfer. Receipt closes the source assignment and establishes a present entry in the destination exactly once. Timeouts route to the coordinator, without automatically counting an unresolved arrival.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `exercise_id` | → ContinuityExercise | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `subject_entry_id` | → AccountabilityEntry | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `source_cohort_id` | → AccountabilityCohort | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `destination_cohort_id` | → AccountabilityCohort | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `dispatched_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `dispatched_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `acknowledged_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `acknowledged_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `status` | enum(dispatched, acknowledged, discrepancy, corrected) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `operation_key` | text | Required when the record reaches its applicable state | [operation](../value-conventions.md#operation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `AccountabilityTransfer.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccountabilityTransfer·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
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
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ContinuityExercise·MISSING | Queue the missing ContinuityExercise mapping or reject the command before linking. |
| Wrong scope | ContinuityExercise·B01 | Do not attach another church’s ContinuityExercise without a supported exchange and local authority. |
| Target rename | Rename ContinuityExercise·A01 after linking | The existing exercise_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No exercise_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### subject_entry_id

The target is [AccountabilityEntry](AccountabilityEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccountabilityEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AccountabilityEntry·MISSING | Queue the missing AccountabilityEntry mapping or reject the command before linking. |
| Wrong scope | AccountabilityEntry·B01 | Do not attach another church’s AccountabilityEntry without a supported exchange and local authority. |
| Target rename | Rename AccountabilityEntry·A01 after linking | The existing subject_entry_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No subject_entry_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_cohort_id

The target is [AccountabilityCohort](AccountabilityCohort.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccountabilityCohort·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AccountabilityCohort·MISSING | Queue the missing AccountabilityCohort mapping or reject the command before linking. |
| Wrong scope | AccountabilityCohort·B01 | Do not attach another church’s AccountabilityCohort without a supported exchange and local authority. |
| Target rename | Rename AccountabilityCohort·A01 after linking | The existing source_cohort_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No source_cohort_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### destination_cohort_id

The target is [AccountabilityCohort](AccountabilityCohort.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccountabilityCohort·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AccountabilityCohort·MISSING | Queue the missing AccountabilityCohort mapping or reject the command before linking. |
| Wrong scope | AccountabilityCohort·B01 | Do not attach another church’s AccountabilityCohort without a supported exchange and local authority. |
| Target rename | Rename AccountabilityCohort·A01 after linking | The existing destination_cohort_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No destination_cohort_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### dispatched_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing dispatched_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No dispatched_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### dispatched_at

Use unambiguous point in time for `AccountabilityTransfer.dispatched_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No dispatched_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### acknowledged_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing acknowledged_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No acknowledged_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### acknowledged_at

Use unambiguous point in time for `AccountabilityTransfer.acknowledged_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No acknowledged_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### status

Declared alternatives in owner order: `dispatched`, `acknowledged`, `discrepancy`, `corrected`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | dispatched | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### operation_key

Use operation identity for exactly-once business effects for `AccountabilityTransfer.operation_key`. Bind the key to the original material inputs and outcome; retain it throughout the replay window.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | KEY-007 with original inputs | Bind the key to the original material inputs and outcome; retain it throughout the replay window. |
| Malformed or unmapped | KEY-007 with changed material inputs | Reject conflicting reuse and reconcile against the first accepted or in-flight operation. |
| Duplicate after successful commit | two equivalent submissions using KEY-007 | Return the original business receipt with no second payment, membership change, booking or notice. |
| Timeout before outcome is known | provider accepted work but acknowledgement delayed | Look up or reconcile the pending operation before issuing a replacement. |
| A genuine correction has a new key | COR-008 points to original KEY-007 | Link the correction to the original effect and apply its ordinary authorization and reversal rules. |
| Incomplete record | No operation_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
