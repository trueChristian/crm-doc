# RiteRecord

[Rites, milestones and register books](../../people/rites-and-milestones.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Store known date components only; preserve source wording and provenance. Shared-event records may reference an event without exposing private fields. One ceremony can serve more than one principal.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `definition_id` | → RiteDefinition | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `congregation_id` | → Congregation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `entry_kind` | enum(performed_here, attested_elsewhere, historical_transcription) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `date_precision` | enum(day, month, year, unknown) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `occurred_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `occurred_month` | integer? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `occurred_year` | year? | Optional under owner conditions | [year](../value-conventions.md#year) |
| `place_label` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `external_church_name` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `provenance` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `evidence_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `state` | enum(draft, pending_review, entered, corrected, void) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `recorded_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `verified_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `entered_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `supersedes_id` | → RiteRecord? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `RiteRecord.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiteRecord·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### definition_id

The target is [RiteDefinition](RiteDefinition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiteDefinition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RiteDefinition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RiteDefinition·MISSING | Queue the missing RiteDefinition mapping or reject the command before linking. |
| Wrong scope | RiteDefinition·B01 | Do not attach another church’s RiteDefinition without a supported exchange and local authority. |
| Target rename | Rename RiteDefinition·A01 after linking | The existing definition_id keeps the same identity and historic documents retain their original wording. |
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

### entry_kind

Declared alternatives in owner order: `performed_here`, `attested_elsewhere`, `historical_transcription`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | performed_here | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_entry_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No entry_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### date_precision

Declared alternatives in owner order: `day`, `month`, `year`, `unknown`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | day | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_date_precision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No date_precision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### occurred_on

Use civil calendar date for `RiteRecord.occurred_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No occurred_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### occurred_month

Use whole-number measure for `RiteRecord.occurred_month`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No occurred_month provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### occurred_year

Use civil year for `RiteRecord.occurred_year`. Preserve year precision separately from month/day.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024 | Preserve year precision separately from month/day. |
| Malformed or unmapped | 2024.5 | Reject a fractional calendar year. |
| Date reported only as a year | 2024 with no month or day | Do not store 1 January as the actual day. |
| Date used to determine age eligibility | possible ages either side of the eligibility cutoff | Return a range or request verification if the answer depends on the day. |
| Cross-year comparison | interval spanning the civil new year | Compare known intervals and disclose uncertainty. |
| Absent in intake | No occurred_year provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### place_label

Use human-readable text for `RiteRecord.place_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered place_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No place_label provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### external_church_name

Use human-readable text for `RiteRecord.external_church_name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered external_church_name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No external_church_name provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### provenance

Use human-readable text for `RiteRecord.provenance`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered provenance in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No provenance at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_ref

Use scoped or external reference for `RiteRecord.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `draft`, `pending_review`, `entered`, `corrected`, `void`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recorded_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing recorded_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No recorded_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### entered_at

Use unambiguous point in time for `RiteRecord.entered_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No entered_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### supersedes_id

The target is [RiteRecord](RiteRecord.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiteRecord·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RiteRecord·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RiteRecord·MISSING | Queue the missing RiteRecord mapping or reject the command before linking. |
| Wrong scope | RiteRecord·B01 | Do not attach another church’s RiteRecord without a supported exchange and local authority. |
| Target rename | Rename RiteRecord·A01 after linking | The existing supersedes_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No supersedes_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CertificateIssue](CertificateIssue.md).`rite_id` | RiteRecord identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RegisterEntry](RegisterEntry.md).`rite_id` | RiteRecord identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiteFieldValue](RiteFieldValue.md).`rite_id` | RiteRecord identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiteParticipant](RiteParticipant.md).`rite_id` | RiteRecord identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiteRecord](RiteRecord.md).`supersedes_id` | RiteRecord identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
