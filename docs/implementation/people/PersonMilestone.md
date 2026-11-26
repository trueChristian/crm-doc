# PersonMilestone

[Participation categories and personal milestones](../../people/participation-and-personal-milestones.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One person can have multiple milestones. Historical knowledge can be year-only. A repeatable milestone has a distinct occurrence or eligible interval; repeated imports of the same source occurrence create one record.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `definition_id` | → MilestoneDefinition | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `congregation_id` | → Congregation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `status` | enum(planned, proposed, verified, expired, superseded, withdrawn) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `achieved_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `achieved_year` | year? | Optional under owner conditions | [year](../value-conventions.md#year) |
| `date_precision` | enum(day, year, unknown) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `verified_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `verified_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `source_kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `source_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `evidence_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `supersedes_id` | → PersonMilestone? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `next_review_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `PersonMilestone.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PersonMilestone·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
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

### definition_id

The target is [MilestoneDefinition](MilestoneDefinition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MilestoneDefinition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MilestoneDefinition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MilestoneDefinition·MISSING | Queue the missing MilestoneDefinition mapping or reject the command before linking. |
| Wrong scope | MilestoneDefinition·B01 | Do not attach another church’s MilestoneDefinition without a supported exchange and local authority. |
| Target rename | Rename MilestoneDefinition·A01 after linking | The existing definition_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No definition_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### status

Declared alternatives in owner order: `planned`, `proposed`, `verified`, `expired`, `superseded`, `withdrawn`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | planned | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### achieved_on

Use civil calendar date for `PersonMilestone.achieved_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No achieved_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### achieved_year

Use civil year for `PersonMilestone.achieved_year`. Preserve year precision separately from month/day.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024 | Preserve year precision separately from month/day. |
| Malformed or unmapped | 2024.5 | Reject a fractional calendar year. |
| Date reported only as a year | 2024 with no month or day | Do not store 1 January as the actual day. |
| Date used to determine age eligibility | possible ages either side of the eligibility cutoff | Return a range or request verification if the answer depends on the day. |
| Cross-year comparison | interval spanning the civil new year | Compare known intervals and disclose uncertainty. |
| Absent in intake | No achieved_year provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### date_precision

Declared alternatives in owner order: `day`, `year`, `unknown`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | day | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_date_precision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No date_precision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### verified_at

Use unambiguous point in time for `PersonMilestone.verified_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No verified_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### verified_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing verified_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No verified_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_kind

Use versioned classification or status code for `PersonMilestone.source_kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active source_kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped source_kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No source_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_ref

Use scoped or external reference for `PersonMilestone.source_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified source_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped source_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No source_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### evidence_ref

Use scoped or external reference for `PersonMilestone.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### supersedes_id

The target is [PersonMilestone](PersonMilestone.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PersonMilestone·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PersonMilestone·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PersonMilestone·MISSING | Queue the missing PersonMilestone mapping or reject the command before linking. |
| Wrong scope | PersonMilestone·B01 | Do not attach another church’s PersonMilestone without a supported exchange and local authority. |
| Target rename | Rename PersonMilestone·A01 after linking | The existing supersedes_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No supersedes_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### next_review_on

Use civil calendar date for `PersonMilestone.next_review_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No next_review_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PersonMilestone](PersonMilestone.md).`supersedes_id` | PersonMilestone identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
