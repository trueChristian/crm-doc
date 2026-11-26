# ResultCount

[Deliberation and voting](../../governance/deliberation-and-voting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One figure per option including abstain, blank, spoilt and challenged where meaningful. The total and used entitlements reconcile or the discrepancy has a documented ruling.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `round_id` | DecisionRound ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `option_key` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `count` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `source` | recorded_votes/manual_tellers/import | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `evidence_note` | restricted text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `certified_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `witnessed_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `certified_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### round_id

The target is [DecisionRound](DecisionRound.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DecisionRound·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DecisionRound·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DecisionRound·MISSING | Queue the missing DecisionRound mapping or reject the command before linking. |
| Wrong scope | DecisionRound·B01 | Do not attach another church’s DecisionRound without a supported exchange and local authority. |
| Target rename | Rename DecisionRound·A01 after linking | The existing round_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No round_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### option_key

Use versioned classification or status code for `ResultCount.option_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active option_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped option_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No option_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### count

Use exact decimal measure for `ResultCount.count`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No count at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source

Declared alternatives in owner order: `recorded_votes`, `manual_tellers`, `import`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | recorded_votes | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_source | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No source at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_note

Use restricted value or protected content reference for `ResultCount.evidence_note`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted evidence_note supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No evidence_note provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### certified_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing certified_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No certified_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### witnessed_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing witnessed_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No witnessed_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### certified_at

Use unambiguous point in time for `ResultCount.certified_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No certified_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
