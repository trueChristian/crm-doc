# AccountabilityCheck

[Operational readiness, interruptions and review](../../ministry/readiness.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Multiple reports per area with timestamp and scope. Distinguish actual roll-call, anonymous headcount and estimate. Unknown attendance requires an explicit uncertainty indicator.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `incident_id` | → OperationsIncident | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `session_id` | → SupervisedSession? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `group_id` | → MinistryGroup? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `responsible_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `checked_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `expected` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `accounted` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `unknown` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `basis` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `restricted_exception_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### incident_id

The target is [OperationsIncident](OperationsIncident.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OperationsIncident·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OperationsIncident·MISSING | Queue the missing OperationsIncident mapping or reject the command before linking. |
| Wrong scope | OperationsIncident·B01 | Do not attach another church’s OperationsIncident without a supported exchange and local authority. |
| Target rename | Rename OperationsIncident·A01 after linking | The existing incident_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No incident_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### session_id

The target is [SupervisedSession](SupervisedSession.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SupervisedSession·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | SupervisedSession·MISSING | Queue the missing SupervisedSession mapping or reject the command before linking. |
| Wrong scope | SupervisedSession·B01 | Do not attach another church’s SupervisedSession without a supported exchange and local authority. |
| Target rename | Rename SupervisedSession·A01 after linking | The existing session_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No session_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### group_id

The target is [MinistryGroup](MinistryGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MinistryGroup·MISSING | Queue the missing MinistryGroup mapping or reject the command before linking. |
| Wrong scope | MinistryGroup·B01 | Do not attach another church’s MinistryGroup without a supported exchange and local authority. |
| Target rename | Rename MinistryGroup·A01 after linking | The existing group_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No group_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### responsible_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing responsible_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No responsible_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### checked_at

Use unambiguous point in time for `AccountabilityCheck.checked_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No checked_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expected

Use whole-number measure for `AccountabilityCheck.expected`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No expected provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### accounted

Use whole-number measure for `AccountabilityCheck.accounted`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No accounted at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unknown

Use whole-number measure for `AccountabilityCheck.unknown`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No unknown provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### basis

Use versioned classification or status code for `AccountabilityCheck.basis`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active basis code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped basis code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### restricted_exception_ref

Use scoped or external reference for `AccountabilityCheck.restricted_exception_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified restricted_exception_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped restricted_exception_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No restricted_exception_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Use the minimum evidence allowed by the selected anonymous, pseudonymous or identified mode. A permitted operator may be accountable for receiving or reviewing work without collecting the identity of a protected subject. Keep safe-channel, identity and case evidence apart from releasable totals and narratives; apply the original permissions to the verification evidence.
