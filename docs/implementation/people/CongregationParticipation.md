# CongregationParticipation

[Participation categories and personal milestones](../../people/participation-and-personal-milestones.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Separate many-to-many person/congregation episodes. Prevent overlaps in the same exclusive family and scope. Different participation families may coexist, and the person may retain memberships or roles elsewhere.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `congregation_id` | → Congregation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `campus_id` | → Campus? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `category_id` | → ParticipationCategory | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `effective_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `effective_until` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `recorded_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `recorded_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `source_kind` | enum(self_declared, staff_confirmed, imported) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `evidence_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `ending_reason` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `CongregationParticipation.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CongregationParticipation·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### person_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### congregation_id

The target is [Congregation](../foundation/Congregation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Congregation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Congregation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Congregation·MISSING | Queue the missing Congregation mapping or reject the command before linking. |
| Wrong scope | Congregation·B01 | Do not attach another church’s Congregation without a supported exchange and local authority. |
| Target rename | Rename Congregation·A01 after linking | The existing congregation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No congregation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### campus_id

The target is [Campus](../foundation/Campus.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Campus·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Campus·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Campus·MISSING | Queue the missing Campus mapping or reject the command before linking. |
| Wrong scope | Campus·B01 | Do not attach another church’s Campus without a supported exchange and local authority. |
| Target rename | Rename Campus·A01 after linking | The existing campus_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No campus_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### category_id

The target is [ParticipationCategory](ParticipationCategory.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ParticipationCategory·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ParticipationCategory·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ParticipationCategory·MISSING | Queue the missing ParticipationCategory mapping or reject the command before linking. |
| Wrong scope | ParticipationCategory·B01 | Do not attach another church’s ParticipationCategory without a supported exchange and local authority. |
| Target rename | Rename ParticipationCategory·A01 after linking | The existing category_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No category_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_from

Use civil calendar date for `CongregationParticipation.effective_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No effective_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_until

Use civil calendar date for `CongregationParticipation.effective_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No effective_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recorded_at

Use unambiguous point in time for `CongregationParticipation.recorded_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No recorded_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recorded_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing recorded_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No recorded_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_kind

Declared alternatives in owner order: `self_declared`, `staff_confirmed`, `imported`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | self_declared | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_source_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No source_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_ref

Use scoped or external reference for `CongregationParticipation.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### ending_reason

Use versioned classification or status code for `CongregationParticipation.ending_reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active ending_reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped ending_reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No ending_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### revision

Use revision number or opaque revision token for `CongregationParticipation.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
