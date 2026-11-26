# DutyAcknowledgement

[Operational readiness, interruptions and review](../../ministry/readiness.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

A changed instruction can require a new acknowledgement. Silence does not constitute receipt.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `briefing_id` | → OperationalBriefing | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `assignment_id` | → VolunteerAssignment | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `plan_version` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `acknowledged_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `method` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### briefing_id

The target is [OperationalBriefing](OperationalBriefing.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OperationalBriefing·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OperationalBriefing·MISSING | Queue the missing OperationalBriefing mapping or reject the command before linking. |
| Wrong scope | OperationalBriefing·B01 | Do not attach another church’s OperationalBriefing without a supported exchange and local authority. |
| Target rename | Rename OperationalBriefing·A01 after linking | The existing briefing_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No briefing_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### plan_version

Use whole-number measure for `DutyAcknowledgement.plan_version`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No plan_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### acknowledged_at

Use unambiguous point in time for `DutyAcknowledgement.acknowledged_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No acknowledged_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### method

Use versioned classification or status code for `DutyAcknowledgement.method`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active method code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped method code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
