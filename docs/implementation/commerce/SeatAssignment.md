# SeatAssignment

[Subscriptions, grants and playback](../../commerce/access.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One beneficiary per live seat, up to plan maximum. Household relationship alone is insufficient to assign or inspect another person's access.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `grant_id` | ref AccessGrant | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `seat_number` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `beneficiary_account_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `effective_from` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `effective_until` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `assigned_by` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `eligibility_evidence_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### grant_id

The target is [AccessGrant](AccessGrant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessGrant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AccessGrant·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AccessGrant·MISSING | Queue the missing AccessGrant mapping or reject the command before linking. |
| Wrong scope | AccessGrant·B01 | Do not attach another church’s AccessGrant without a supported exchange and local authority. |
| Target rename | Rename AccessGrant·A01 after linking | The existing grant_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No grant_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### seat_number

Use whole-number measure for `SeatAssignment.seat_number`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No seat_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### beneficiary_account_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing beneficiary_account_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No beneficiary_account_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_from

Use unambiguous point in time for `SeatAssignment.effective_from`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No effective_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_until

Use unambiguous point in time for `SeatAssignment.effective_until`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No effective_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### assigned_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing assigned_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No assigned_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligibility_evidence_ref

Use scoped or external reference for `SeatAssignment.eligibility_evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified eligibility_evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped eligibility_evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No eligibility_evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
