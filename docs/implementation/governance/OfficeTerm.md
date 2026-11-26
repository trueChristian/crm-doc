# OfficeTerm

[Governing bodies, office terms and delegated authority](../../governance/bodies-and-terms.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

At most one active incumbent for a seat and instant. An incoming term can be accepted before inauguration. A vacancy is a gap in active terms. Restrict corrections to officer history.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `office_id` | Office ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `person_id` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `seat_number` | positive integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `start_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `end_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `state` | proposed/accepted/active/ended/void | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `mandate_record` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `acceptance_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `reason_ended` | enum? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `predecessor_term_id` | OfficeTerm ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### office_id

The target is [Office](Office.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Office·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Office·MISSING | Queue the missing Office mapping or reject the command before linking. |
| Wrong scope | Office·B01 | Do not attach another church’s Office without a supported exchange and local authority. |
| Target rename | Rename Office·A01 after linking | The existing office_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No office_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### seat_number

Use whole-number measure for `OfficeTerm.seat_number`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No seat_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### start_on

Use civil calendar date for `OfficeTerm.start_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No start_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### end_on

Use civil calendar date for `OfficeTerm.end_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No end_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `proposed`, `accepted`, `active`, `ended`, `void`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | proposed | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### mandate_record

Use human-readable text for `OfficeTerm.mandate_record`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered mandate_record in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No mandate_record at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### acceptance_at

Use unambiguous point in time for `OfficeTerm.acceptance_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No acceptance_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason_ended

Use versioned classification or status code for `OfficeTerm.reason_ended`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reason_ended code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reason_ended code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No reason_ended provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### predecessor_term_id

The target is [OfficeTerm](OfficeTerm.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OfficeTerm·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OfficeTerm·MISSING | Queue the missing OfficeTerm mapping or reject the command before linking. |
| Wrong scope | OfficeTerm·B01 | Do not attach another church’s OfficeTerm without a supported exchange and local authority. |
| Target rename | Rename OfficeTerm·A01 after linking | The existing predecessor_term_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No predecessor_term_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AssemblyPaperRequest](AssemblyPaperRequest.md).`owner_term_id` | OfficeTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AuthorityDelegation](AuthorityDelegation.md).`delegate_term_id` | OfficeTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AuthorityDelegation](AuthorityDelegation.md).`grantor_term_id` | OfficeTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceCycle](GovernanceCycle.md).`owner_term_id` | OfficeTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernancePolicy](GovernancePolicy.md).`owner_term_id` | OfficeTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceReview](GovernanceReview.md).`reviewer_term_id` | OfficeTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteAttestation](MinuteAttestation.md).`attesting_office_id` | OfficeTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OfficeTerm](OfficeTerm.md).`predecessor_term_id` | OfficeTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VotingRollEntry](VotingRollEntry.md).`seat_id` | OfficeTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
