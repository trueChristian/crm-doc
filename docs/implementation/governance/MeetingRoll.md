# MeetingRoll

[Meetings, notice, eligibility and quorum](../../governance/meetings-and-notice.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

A certified edition is immutable. Certification preserves the selection basis, governing rule and eligible denominator. Only one operative edition per meeting instant.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `meeting_id` | GovernanceMeeting ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `cutoff_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `built_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `certified_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `certified_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `edition` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `basis_description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `replaces_id` | MeetingRoll ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `state` | working/certified/superseded | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### meeting_id

The target is [GovernanceMeeting](GovernanceMeeting.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernanceMeeting·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GovernanceMeeting·MISSING | Queue the missing GovernanceMeeting mapping or reject the command before linking. |
| Wrong scope | GovernanceMeeting·B01 | Do not attach another church’s GovernanceMeeting without a supported exchange and local authority. |
| Target rename | Rename GovernanceMeeting·A01 after linking | The existing meeting_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No meeting_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cutoff_at

Use unambiguous point in time for `MeetingRoll.cutoff_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No cutoff_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### built_at

Use unambiguous point in time for `MeetingRoll.built_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No built_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### certified_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing certified_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No certified_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### certified_at

Use unambiguous point in time for `MeetingRoll.certified_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No certified_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### edition

Use revision number or opaque revision token for `MeetingRoll.edition`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No edition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### basis_description

Use human-readable text for `MeetingRoll.basis_description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered basis_description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No basis_description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### replaces_id

The target is [MeetingRoll](MeetingRoll.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MeetingRoll·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MeetingRoll·MISSING | Queue the missing MeetingRoll mapping or reject the command before linking. |
| Wrong scope | MeetingRoll·B01 | Do not attach another church’s MeetingRoll without a supported exchange and local authority. |
| Target rename | Rename MeetingRoll·A01 after linking | The existing replaces_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No replaces_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `working`, `certified`, `superseded`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | working | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DecisionRound](DecisionRound.md).`roll_id` | MeetingRoll identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MeetingRoll](MeetingRoll.md).`replaces_id` | MeetingRoll identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [QuorumCheck](QuorumCheck.md).`roll_id` | MeetingRoll identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VotingRollEntry](VotingRollEntry.md).`roll_id` | MeetingRoll identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
