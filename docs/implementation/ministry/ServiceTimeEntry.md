# ServiceTimeEntry

[Volunteers and rotas](../../ministry/volunteers.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Measured minutes exclude breaks. Prevent negative durations and overlapping approved time for the same person. Estimate and approved hours are distinguishable.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `assignment_id` | → VolunteerAssignment | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `arrived_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `departed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `break_minutes` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `approved_minutes` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `reviewed_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `correction_of_id` | → ServiceTimeEntry? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### assignment_id

The target is [VolunteerAssignment](VolunteerAssignment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VolunteerAssignment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | VolunteerAssignment·MISSING | Queue the missing VolunteerAssignment mapping or reject the command before linking. |
| Wrong scope | VolunteerAssignment·B01 | Do not attach another church’s VolunteerAssignment without a supported exchange and local authority. |
| Target rename | Rename VolunteerAssignment·A01 after linking | The existing assignment_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No assignment_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### arrived_at

Use unambiguous point in time for `ServiceTimeEntry.arrived_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No arrived_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### departed_at

Use unambiguous point in time for `ServiceTimeEntry.departed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No departed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### break_minutes

Use whole-number measure for `ServiceTimeEntry.break_minutes`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No break_minutes at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_minutes

Use whole-number measure for `ServiceTimeEntry.approved_minutes`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No approved_minutes provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reviewed_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewed_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reviewed_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### correction_of_id

The target is [ServiceTimeEntry](ServiceTimeEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ServiceTimeEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ServiceTimeEntry·MISSING | Queue the missing ServiceTimeEntry mapping or reject the command before linking. |
| Wrong scope | ServiceTimeEntry·B01 | Do not attach another church’s ServiceTimeEntry without a supported exchange and local authority. |
| Target rename | Rename ServiceTimeEntry·A01 after linking | The existing correction_of_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No correction_of_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PartnershipDelivery](../development/PartnershipDelivery.md).`service_entry_id` | ServiceTimeEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServiceTimeEntry](ServiceTimeEntry.md).`correction_of_id` | ServiceTimeEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
