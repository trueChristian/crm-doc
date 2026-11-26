# SponsorReport

[Grant applications and reporting](../../development/grant-applications.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique report purpose/period/obligation. A report deadline is a sponsor obligation; it does not independently authorize expenditure or a financial draw.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `award_id` | ref GrantAward | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `milestone_id` | ref AwardMilestone | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `period_start` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `period_end` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `due_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `sponsor_time_zone` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `kind` | narrative/financial/outcome/final | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `owner_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `status` | draft/review/approved/submitted/changes_requested/accepted/overdue | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### award_id

The target is [GrantAward](../finance/GrantAward.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GrantAward·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GrantAward·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GrantAward·MISSING | Queue the missing GrantAward mapping or reject the command before linking. |
| Wrong scope | GrantAward·B01 | Do not attach another church’s GrantAward without a supported exchange and local authority. |
| Target rename | Rename GrantAward·A01 after linking | The existing award_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No award_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### milestone_id

The target is [AwardMilestone](../finance/AwardMilestone.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AwardMilestone·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AwardMilestone·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AwardMilestone·MISSING | Queue the missing AwardMilestone mapping or reject the command before linking. |
| Wrong scope | AwardMilestone·B01 | Do not attach another church’s AwardMilestone without a supported exchange and local authority. |
| Target rename | Rename AwardMilestone·A01 after linking | The existing milestone_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No milestone_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period_start

Use civil calendar date for `SponsorReport.period_start`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No period_start at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period_end

Use civil calendar date for `SponsorReport.period_end`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No period_end at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### due_at

Use unambiguous point in time for `SponsorReport.due_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No due_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sponsor_time_zone

Use human-readable text for `SponsorReport.sponsor_time_zone`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered sponsor_time_zone in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No sponsor_time_zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `narrative`, `financial`, `outcome`, `final`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | narrative | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### owner_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing owner_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No owner_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Declared alternatives in owner order: `draft`, `review`, `approved`, `submitted`, `changes_requested`, `accepted`, `overdue`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [ReportSubmissionEdition](ReportSubmissionEdition.md).`report_id` | SponsorReport identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SponsorReportItem](SponsorReportItem.md).`report_id` | SponsorReport identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
