# Membership

[Membership, transfers and certified rolls](../../people/membership-and-rolls.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

A membership is a continuous affiliation in a congregation. A new episode after departure may link to the earlier one. Local roll numbers follow configured scope and reuse policy.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `congregation_id` | → Congregation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `local_roll_number` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `originating_application_id` | → MembershipApplication? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `first_effective_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `closed_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `supersedes_membership_id` | → Membership? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `record_status` | enum(valid, corrected_in_error) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `Membership.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Membership·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
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

### local_roll_number

Use human-readable text for `Membership.local_roll_number`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered local_roll_number in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No local_roll_number provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### originating_application_id

The target is [MembershipApplication](MembershipApplication.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MembershipApplication·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MembershipApplication·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MembershipApplication·MISSING | Queue the missing MembershipApplication mapping or reject the command before linking. |
| Wrong scope | MembershipApplication·B01 | Do not attach another church’s MembershipApplication without a supported exchange and local authority. |
| Target rename | Rename MembershipApplication·A01 after linking | The existing originating_application_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No originating_application_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### first_effective_on

Use civil calendar date for `Membership.first_effective_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No first_effective_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### closed_on

Use civil calendar date for `Membership.closed_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No closed_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### supersedes_membership_id

The target is [Membership](Membership.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Membership·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Membership·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Membership·MISSING | Queue the missing Membership mapping or reject the command before linking. |
| Wrong scope | Membership·B01 | Do not attach another church’s Membership without a supported exchange and local authority. |
| Target rename | Rename Membership·A01 after linking | The existing supersedes_membership_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No supersedes_membership_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### record_status

Declared alternatives in owner order: `valid`, `corrected_in_error`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | valid | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_record_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No record_status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revision

Use revision number or opaque revision token for `Membership.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [Membership](Membership.md).`supersedes_membership_id` | Membership identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipDecision](MembershipDecision.md).`membership_id` | Membership identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipPeriod](MembershipPeriod.md).`membership_id` | Membership identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
