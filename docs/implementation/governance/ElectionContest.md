# ElectionContest

[Deliberation and voting](../../governance/deliberation-and-voting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Contest specifies the exact threshold, tie, vacancies and recount rules. Ranked methods require an adopted transfer and tie-break rule with round-level count details.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `item_id` | AgendaItem ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `office_id` | Office ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `seats_available` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `nomination_opens_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `nomination_closes_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `candidate_rule` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `method` | plurality/majority_runoff/approval/ranked | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `selection_limit` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `term_start` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `term_end` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `state` | nominations/ballot/count/certified/disputed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### item_id

The target is [AgendaItem](AgendaItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AgendaItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AgendaItem·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AgendaItem·MISSING | Queue the missing AgendaItem mapping or reject the command before linking. |
| Wrong scope | AgendaItem·B01 | Do not attach another church’s AgendaItem without a supported exchange and local authority. |
| Target rename | Rename AgendaItem·A01 after linking | The existing item_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No item_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### office_id

The target is [Office](Office.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Office·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Office·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Office·MISSING | Queue the missing Office mapping or reject the command before linking. |
| Wrong scope | Office·B01 | Do not attach another church’s Office without a supported exchange and local authority. |
| Target rename | Rename Office·A01 after linking | The existing office_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No office_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### seats_available

Use whole-number measure for `ElectionContest.seats_available`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No seats_available at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### nomination_opens_at

Use unambiguous point in time for `ElectionContest.nomination_opens_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No nomination_opens_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### nomination_closes_at

Use unambiguous point in time for `ElectionContest.nomination_closes_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No nomination_closes_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### candidate_rule

Use human-readable text for `ElectionContest.candidate_rule`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered candidate_rule in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No candidate_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### method

Declared alternatives in owner order: `plurality`, `majority_runoff`, `approval`, `ranked`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | plurality | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_method | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### selection_limit

Use whole-number measure for `ElectionContest.selection_limit`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No selection_limit at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### term_start

Use civil calendar date for `ElectionContest.term_start`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No term_start at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### term_end

Use civil calendar date for `ElectionContest.term_end`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No term_end provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `nominations`, `ballot`, `count`, `certified`, `disputed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | nominations | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DecisionRound](DecisionRound.md).`election_id` | ElectionContest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Nomination](Nomination.md).`contest_id` | ElectionContest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
