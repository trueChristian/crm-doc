# CarePlanAction

[Pastoral care, prayer and continuity](../../people/pastoral-care.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Distinguish agreed visits, meal support, accessibility accommodations and external referrals. Minimize shared task payload. Reject cyclic dependencies.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `case_id` | → CareCase | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `description` | restricted text | Required when the record reaches its applicable state | [protected](../value-conventions.md#protected) |
| `assigned_to` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `due_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `dependency_id` | → CarePlanAction? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `state` | enum(proposed, agreed, in_progress, completed, cancelled) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `completed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `review_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `CarePlanAction.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CarePlanAction·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### case_id

The target is [CareCase](CareCase.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CareCase·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CareCase·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CareCase·MISSING | Queue the missing CareCase mapping or reject the command before linking. |
| Wrong scope | CareCase·B01 | Do not attach another church’s CareCase without a supported exchange and local authority. |
| Target rename | Rename CareCase·A01 after linking | The existing case_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No case_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### description

Use restricted value or protected content reference for `CarePlanAction.description`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted description supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Incomplete record | No description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assigned_to

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing assigned_to keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No assigned_to provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_on

Use civil calendar date for `CarePlanAction.due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No due_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### dependency_id

The target is [CarePlanAction](CarePlanAction.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CarePlanAction·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CarePlanAction·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CarePlanAction·MISSING | Queue the missing CarePlanAction mapping or reject the command before linking. |
| Wrong scope | CarePlanAction·B01 | Do not attach another church’s CarePlanAction without a supported exchange and local authority. |
| Target rename | Rename CarePlanAction·A01 after linking | The existing dependency_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No dependency_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `proposed`, `agreed`, `in_progress`, `completed`, `cancelled`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | proposed | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### completed_at

Use unambiguous point in time for `CarePlanAction.completed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No completed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### review_on

Use civil calendar date for `CarePlanAction.review_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No review_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CarePlanAction](CarePlanAction.md).`dependency_id` | CarePlanAction identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
