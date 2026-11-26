# VotingRollEntry

[Meetings, notice, eligibility and quorum](../../governance/meetings-and-notice.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique roll/person unless separate seats lawfully vote independently. Represent each distinct entitlement with an explicit seat key and policy. Non-voters have weight zero.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `roll_id` | MeetingRoll ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `person_id` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `eligibility` | vote/speak/observe/notice_only/ineligible | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `vote_weight` | decimal | Required when the record reaches its applicable state | [ratio](../value-conventions.md#ratio) |
| `seat_id` | OfficeTerm ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `representation_class` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `evidence_ref` | text | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `decision_reason` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `changed_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `decision_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### roll_id

The target is [MeetingRoll](MeetingRoll.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MeetingRoll·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MeetingRoll·MISSING | Queue the missing MeetingRoll mapping or reject the command before linking. |
| Wrong scope | MeetingRoll·B01 | Do not attach another church’s MeetingRoll without a supported exchange and local authority. |
| Target rename | Rename MeetingRoll·A01 after linking | The existing roll_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No roll_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligibility

Declared alternatives in owner order: `vote`, `speak`, `observe`, `notice_only`, `ineligible`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | vote | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_eligibility | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No eligibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### vote_weight

Use exact ratio, rate or weighting for `VotingRollEntry.vote_weight`. Carry the declared unit, direction and calculation precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 1.125 under named rate basis | Carry the declared unit, direction and calculation precision. |
| Malformed or unmapped | rate with unknown direction | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | 0.125 fraction and 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | reciprocal quoted in opposite currency direction | Require explicit direction and an approved conversion. |
| Financial document already issued | historical line after a rate-table correction | Retain the original rate, effective date and rounding basis. |
| Incomplete record | No vote_weight at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### seat_id

The target is [OfficeTerm](OfficeTerm.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OfficeTerm·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OfficeTerm·MISSING | Queue the missing OfficeTerm mapping or reject the command before linking. |
| Wrong scope | OfficeTerm·B01 | Do not attach another church’s OfficeTerm without a supported exchange and local authority. |
| Target rename | Rename OfficeTerm·A01 after linking | The existing seat_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No seat_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### representation_class

Use versioned classification or status code for `VotingRollEntry.representation_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active representation_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped representation_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No representation_class provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### evidence_ref

Use scoped or external reference for `VotingRollEntry.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No evidence_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision_reason

Use versioned classification or status code for `VotingRollEntry.decision_reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active decision_reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped decision_reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No decision_reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### changed_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing changed_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No changed_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### decision_at

Use unambiguous point in time for `VotingRollEntry.decision_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No decision_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AssemblyCredential](AssemblyCredential.md).`roll_entry_id` | VotingRollEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [NoticeService](NoticeService.md).`roll_entry_id` | VotingRollEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProxyMandate](ProxyMandate.md).`holder_entry_id` | VotingRollEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProxyMandate](ProxyMandate.md).`principal_entry_id` | VotingRollEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VotingEntitlement](VotingEntitlement.md).`exercising_entry_id` | VotingRollEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VotingEntitlement](VotingEntitlement.md).`represented_entry_id` | VotingRollEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
