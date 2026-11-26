# QuorumCheck

[Meetings, notice, eligibility and quorum](../../governance/meetings-and-notice.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Persist rule edition, contributing entitlements and attendance intervals or an immutable snapshot. Restrict access to individually named evidence.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `meeting_id` | GovernanceMeeting ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `roll_id` | MeetingRoll ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `item_id` | AgendaItem ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `measured_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `denominator` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `eligible_present` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `represented_proxies` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `recused` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `required` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `classes_result` | structured counts | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |
| `outcome` | met/lost/undetermined | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `certified_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `evidence_ref` | text | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### meeting_id

The target is [GovernanceMeeting](GovernanceMeeting.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernanceMeeting·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GovernanceMeeting·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GovernanceMeeting·MISSING | Queue the missing GovernanceMeeting mapping or reject the command before linking. |
| Wrong scope | GovernanceMeeting·B01 | Do not attach another church’s GovernanceMeeting without a supported exchange and local authority. |
| Target rename | Rename GovernanceMeeting·A01 after linking | The existing meeting_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No meeting_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### roll_id

The target is [MeetingRoll](MeetingRoll.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MeetingRoll·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MeetingRoll·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MeetingRoll·MISSING | Queue the missing MeetingRoll mapping or reject the command before linking. |
| Wrong scope | MeetingRoll·B01 | Do not attach another church’s MeetingRoll without a supported exchange and local authority. |
| Target rename | Rename MeetingRoll·A01 after linking | The existing roll_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No roll_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### item_id

The target is [AgendaItem](AgendaItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AgendaItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AgendaItem·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AgendaItem·MISSING | Queue the missing AgendaItem mapping or reject the command before linking. |
| Wrong scope | AgendaItem·B01 | Do not attach another church’s AgendaItem without a supported exchange and local authority. |
| Target rename | Rename AgendaItem·A01 after linking | The existing item_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No item_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### measured_at

Use unambiguous point in time for `QuorumCheck.measured_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No measured_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### denominator

Use exact decimal measure for `QuorumCheck.denominator`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No denominator at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligible_present

Use exact decimal measure for `QuorumCheck.eligible_present`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No eligible_present at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### represented_proxies

Use exact decimal measure for `QuorumCheck.represented_proxies`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No represented_proxies at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recused

Use exact decimal measure for `QuorumCheck.recused`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No recused at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### required

Use exact decimal measure for `QuorumCheck.required`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No required at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### classes_result

Use typed value or bounded compound record for `QuorumCheck.classes_result`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of classes_result matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for classes_result | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No classes_result at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### outcome

Declared alternatives in owner order: `met`, `lost`, `undetermined`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | met | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_outcome | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No outcome at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### evidence_ref

Use scoped or external reference for `QuorumCheck.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No evidence_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DecisionRound](DecisionRound.md).`quorum_id` | QuorumCheck identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
