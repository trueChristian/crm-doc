# VotingEntitlement

[Deliberation and voting](../../governance/deliberation-and-voting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique round/represented right. A proxy holder casts separately for each authorized right. Secret ballot records cannot contain the entitlement id.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `round_id` | DecisionRound ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `represented_entry_id` | VotingRollEntry ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `exercising_entry_id` | VotingRollEntry ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `proxy_id` | ProxyMandate ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `issued_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `consumed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `revoked_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `weight` | decimal | Required when the record reaches its applicable state | [ratio](../value-conventions.md#ratio) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### round_id

The target is [DecisionRound](DecisionRound.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DecisionRound·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | DecisionRound·MISSING | Queue the missing DecisionRound mapping or reject the command before linking. |
| Wrong scope | DecisionRound·B01 | Do not attach another church’s DecisionRound without a supported exchange and local authority. |
| Target rename | Rename DecisionRound·A01 after linking | The existing round_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No round_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### represented_entry_id

The target is [VotingRollEntry](VotingRollEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VotingRollEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | VotingRollEntry·MISSING | Queue the missing VotingRollEntry mapping or reject the command before linking. |
| Wrong scope | VotingRollEntry·B01 | Do not attach another church’s VotingRollEntry without a supported exchange and local authority. |
| Target rename | Rename VotingRollEntry·A01 after linking | The existing represented_entry_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No represented_entry_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### exercising_entry_id

The target is [VotingRollEntry](VotingRollEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VotingRollEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | VotingRollEntry·MISSING | Queue the missing VotingRollEntry mapping or reject the command before linking. |
| Wrong scope | VotingRollEntry·B01 | Do not attach another church’s VotingRollEntry without a supported exchange and local authority. |
| Target rename | Rename VotingRollEntry·A01 after linking | The existing exercising_entry_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No exercising_entry_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### proxy_id

The target is [ProxyMandate](ProxyMandate.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProxyMandate·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ProxyMandate·MISSING | Queue the missing ProxyMandate mapping or reject the command before linking. |
| Wrong scope | ProxyMandate·B01 | Do not attach another church’s ProxyMandate without a supported exchange and local authority. |
| Target rename | Rename ProxyMandate·A01 after linking | The existing proxy_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No proxy_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### issued_at

Use unambiguous point in time for `VotingEntitlement.issued_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No issued_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### consumed_at

Use unambiguous point in time for `VotingEntitlement.consumed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No consumed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### revoked_at

Use unambiguous point in time for `VotingEntitlement.revoked_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No revoked_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### weight

Use exact ratio, rate or weighting for `VotingEntitlement.weight`. Carry the declared unit, direction and calculation precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 1.125 under named rate basis | Carry the declared unit, direction and calculation precision. |
| Malformed or unmapped | rate with unknown direction | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | 0.125 fraction and 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | reciprocal quoted in opposite currency direction | Require explicit direction and an approved conversion. |
| Financial document already issued | historical line after a rate-table correction | Retain the original rate, effective date and rounding basis. |
| Incomplete record | No weight at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [NamedVote](NamedVote.md).`entitlement_id` | VotingEntitlement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
