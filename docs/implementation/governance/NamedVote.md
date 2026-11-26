# NamedVote

[Deliberation and voting](../../governance/deliberation-and-voting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Named ballots only. One effective choice per right for a single-choice round. Corrections before close are explicit and auditable. Multiple selections obey the contest limit.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `entitlement_id` | VotingEntitlement ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `choice` | yes/no/abstain/candidate | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `nominee_id` | Nomination ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `weight` | decimal | Required when the record reaches its applicable state | [ratio](../value-conventions.md#ratio) |
| `recorded_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `recorded_by` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `corrected_from_id` | NamedVote ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### entitlement_id

The target is [VotingEntitlement](VotingEntitlement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VotingEntitlement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | VotingEntitlement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | VotingEntitlement·MISSING | Queue the missing VotingEntitlement mapping or reject the command before linking. |
| Wrong scope | VotingEntitlement·B01 | Do not attach another church’s VotingEntitlement without a supported exchange and local authority. |
| Target rename | Rename VotingEntitlement·A01 after linking | The existing entitlement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No entitlement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### choice

Declared alternatives in owner order: `yes`, `no`, `abstain`, `candidate`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | yes | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_choice | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No choice at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### nominee_id

The target is [Nomination](Nomination.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Nomination·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Nomination·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Nomination·MISSING | Queue the missing Nomination mapping or reject the command before linking. |
| Wrong scope | Nomination·B01 | Do not attach another church’s Nomination without a supported exchange and local authority. |
| Target rename | Rename Nomination·A01 after linking | The existing nominee_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No nominee_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### weight

Use exact ratio, rate or weighting for `NamedVote.weight`. Carry the declared unit, direction and calculation precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 1.125 under named rate basis | Carry the declared unit, direction and calculation precision. |
| Malformed or unmapped | rate with unknown direction | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | 0.125 fraction and 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | reciprocal quoted in opposite currency direction | Require explicit direction and an approved conversion. |
| Financial document already issued | historical line after a rate-table correction | Retain the original rate, effective date and rounding basis. |
| Incomplete record | No weight at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recorded_at

Use unambiguous point in time for `NamedVote.recorded_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No recorded_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recorded_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing recorded_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No recorded_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### corrected_from_id

The target is [NamedVote](NamedVote.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NamedVote·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | NamedVote·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | NamedVote·MISSING | Queue the missing NamedVote mapping or reject the command before linking. |
| Wrong scope | NamedVote·B01 | Do not attach another church’s NamedVote without a supported exchange and local authority. |
| Target rename | Rename NamedVote·A01 after linking | The existing corrected_from_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No corrected_from_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason

Use human-readable text for `NamedVote.reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [NamedVote](NamedVote.md).`corrected_from_id` | NamedVote identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
