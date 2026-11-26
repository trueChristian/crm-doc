# RoundPlacement

[Agreements, service rounds and relief distribution](../../administration/community-programs.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique active placement for the application and round. Waiting for a session does not alter the caseworker's eligibility decision.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `round_id` | → AssistanceRound | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `application_id` | → AidApplication | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `award_id` | → AidAward optional | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `requested_units` | quantity | Required at applicable lifecycle step | [decimal](../value-conventions.md#decimal) |
| `offered_units` | quantity | Required at applicable lifecycle step | [decimal](../value-conventions.md#decimal) |
| `state` | waiting, offered, confirmed, withdrawn or expired | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `offer_expires_at` | optional instant | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `source_key` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [key](../value-conventions.md#key) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `RoundPlacement.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RoundPlacement·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### round_id

The target is [AssistanceRound](AssistanceRound.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AssistanceRound·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AssistanceRound·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AssistanceRound·MISSING | Queue the missing AssistanceRound mapping or reject the command before linking. |
| Wrong scope | AssistanceRound·B01 | Do not attach another church’s AssistanceRound without a supported exchange and local authority. |
| Target rename | Rename AssistanceRound·A01 after linking | The existing round_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No round_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### application_id

The target is [AidApplication](../people/AidApplication.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AidApplication·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AidApplication·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AidApplication·MISSING | Queue the missing AidApplication mapping or reject the command before linking. |
| Wrong scope | AidApplication·B01 | Do not attach another church’s AidApplication without a supported exchange and local authority. |
| Target rename | Rename AidApplication·A01 after linking | The existing application_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No application_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### award_id

The target is [AidAward](../people/AidAward.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AidAward·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AidAward·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AidAward·MISSING | Queue the missing AidAward mapping or reject the command before linking. |
| Wrong scope | AidAward·B01 | Do not attach another church’s AidAward without a supported exchange and local authority. |
| Target rename | Rename AidAward·A01 after linking | The existing award_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No award_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### requested_units

Use exact decimal measure for `RoundPlacement.requested_units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No requested_units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### offered_units

Use exact decimal measure for `RoundPlacement.offered_units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No offered_units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `waiting`, `offered`, `confirmed`, `withdrawn`, `expired`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | waiting | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### offer_expires_at

Use unambiguous point in time for `RoundPlacement.offer_expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No offer_expires_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_key

Use opaque identity or token for `RoundPlacement.source_key`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RoundPlacement·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Incomplete record | No source_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
