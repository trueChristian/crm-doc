# IntegrationDeliveryAttempt

[Integrations, exports and event delivery](../../platform/exchange-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique subscription/event/attempt. Track success per subscriber, independently from business commit.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `subscription_id` | Ref(IntegrationSubscription) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `event_id` | Ref(DomainEvent) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `attempt_no` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `started_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `completed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `outcome` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `response_class` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `next_retry_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `receipt_ref` | ResourceRef? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### subscription_id

The target is [IntegrationSubscription](IntegrationSubscription.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | IntegrationSubscription·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | IntegrationSubscription·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | IntegrationSubscription·MISSING | Queue the missing IntegrationSubscription mapping or reject the command before linking. |
| Wrong scope | IntegrationSubscription·B01 | Do not attach another church’s IntegrationSubscription without a supported exchange and local authority. |
| Target rename | Rename IntegrationSubscription·A01 after linking | The existing subscription_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No subscription_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### event_id

The target is [DomainEvent](DomainEvent.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DomainEvent·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DomainEvent·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DomainEvent·MISSING | Queue the missing DomainEvent mapping or reject the command before linking. |
| Wrong scope | DomainEvent·B01 | Do not attach another church’s DomainEvent without a supported exchange and local authority. |
| Target rename | Rename DomainEvent·A01 after linking | The existing event_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No event_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### attempt_no

Use whole-number measure for `IntegrationDeliveryAttempt.attempt_no`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No attempt_no at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### started_at

Use unambiguous point in time for `IntegrationDeliveryAttempt.started_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No started_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### completed_at

Use unambiguous point in time for `IntegrationDeliveryAttempt.completed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No completed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### outcome

Use versioned classification or status code for `IntegrationDeliveryAttempt.outcome`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active outcome code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped outcome code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No outcome at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### response_class

Use versioned classification or status code for `IntegrationDeliveryAttempt.response_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active response_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped response_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No response_class provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### next_retry_at

Use unambiguous point in time for `IntegrationDeliveryAttempt.next_retry_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No next_retry_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### receipt_ref

Use scoped or external reference for `IntegrationDeliveryAttempt.receipt_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified receipt_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped receipt_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No receipt_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
