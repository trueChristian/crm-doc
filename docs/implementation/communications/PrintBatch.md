# PrintBatch

[Delivery and responses](../../communications/delivery-and-responses.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Batch covers the precise envelopes in a protected manifest. Reprints and returned letters have a reason, date and disposition.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `dispatch_id` | DispatchRequest ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `prepared_by` | UserAccount ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `prepared_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `destination_count` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `check_total` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `handover_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `received_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `destruction_due` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `state` | prepared/verified/handed_over/closed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### dispatch_id

The target is [DispatchRequest](DispatchRequest.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DispatchRequest·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DispatchRequest·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DispatchRequest·MISSING | Queue the missing DispatchRequest mapping or reject the command before linking. |
| Wrong scope | DispatchRequest·B01 | Do not attach another church’s DispatchRequest without a supported exchange and local authority. |
| Target rename | Rename DispatchRequest·A01 after linking | The existing dispatch_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No dispatch_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prepared_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing prepared_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No prepared_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prepared_at

Use unambiguous point in time for `PrintBatch.prepared_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No prepared_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### destination_count

Use whole-number measure for `PrintBatch.destination_count`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No destination_count at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### check_total

Use whole-number measure for `PrintBatch.check_total`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No check_total at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### handover_at

Use unambiguous point in time for `PrintBatch.handover_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No handover_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### received_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing received_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No received_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### destruction_due

Use civil calendar date for `PrintBatch.destruction_due`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No destruction_due provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `prepared`, `verified`, `handed_over`, `closed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | prepared | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
