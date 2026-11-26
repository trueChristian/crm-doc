# MinuteEdition

[Minutes, resolutions and the archive](../../governance/minutes-and-resolutions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique meeting/book/edition and unique issued book/record number. The digest covers exact content, annex manifest and revision. Edits after approval require a separately authorized correction.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `book_id` | MinuteBook ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `meeting_id` | GovernanceMeeting ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `edition` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `record_number` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `state` | draft/review/approved/superseded | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `prepared_by` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `prepared_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `prior_id` | MinuteEdition ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `confirmed_meeting_id` | GovernanceMeeting ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `confirmed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `approved_snapshot_digest` | text? | Optional under owner conditions | [digest](../value-conventions.md#digest) |
| `correction_rationale` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### book_id

The target is [MinuteBook](MinuteBook.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinuteBook·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinuteBook·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinuteBook·MISSING | Queue the missing MinuteBook mapping or reject the command before linking. |
| Wrong scope | MinuteBook·B01 | Do not attach another church’s MinuteBook without a supported exchange and local authority. |
| Target rename | Rename MinuteBook·A01 after linking | The existing book_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No book_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### edition

Use whole-number measure for `MinuteEdition.edition`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No edition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### record_number

Use human-readable text for `MinuteEdition.record_number`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered record_number in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No record_number provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `draft`, `review`, `approved`, `superseded`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prepared_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing prepared_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No prepared_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prepared_at

Use unambiguous point in time for `MinuteEdition.prepared_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No prepared_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prior_id

The target is [MinuteEdition](MinuteEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinuteEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinuteEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinuteEdition·MISSING | Queue the missing MinuteEdition mapping or reject the command before linking. |
| Wrong scope | MinuteEdition·B01 | Do not attach another church’s MinuteEdition without a supported exchange and local authority. |
| Target rename | Rename MinuteEdition·A01 after linking | The existing prior_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No prior_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### confirmed_meeting_id

The target is [GovernanceMeeting](GovernanceMeeting.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernanceMeeting·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GovernanceMeeting·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GovernanceMeeting·MISSING | Queue the missing GovernanceMeeting mapping or reject the command before linking. |
| Wrong scope | GovernanceMeeting·B01 | Do not attach another church’s GovernanceMeeting without a supported exchange and local authority. |
| Target rename | Rename GovernanceMeeting·A01 after linking | The existing confirmed_meeting_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No confirmed_meeting_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### confirmed_at

Use unambiguous point in time for `MinuteEdition.confirmed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No confirmed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approved_snapshot_digest

Use integrity fingerprint or opaque verifier for `MinuteEdition.approved_snapshot_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Absent in intake | No approved_snapshot_digest provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### correction_rationale

Use human-readable text for `MinuteEdition.correction_rationale`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered correction_rationale in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No correction_rationale provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [GovernanceAttachment](GovernanceAttachment.md).`edition_id` | MinuteEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteAttestation](MinuteAttestation.md).`edition_id` | MinuteEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteEdition](MinuteEdition.md).`prior_id` | MinuteEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteItem](MinuteItem.md).`edition_id` | MinuteEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OfficialExtract](OfficialExtract.md).`edition_id` | MinuteEdition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
