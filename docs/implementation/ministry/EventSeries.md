# EventSeries

[Calendars and occurrences](../../ministry/calendar.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One-off activities have one occurrence. An all-day activity uses local dates and positive day count. Timed items use positive duration and named zone. Support in-person, online and hybrid.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `calendar_id` | → MinistryCalendar | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `organizer_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `host_group_id` | → MinistryGroup? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `summary` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `delivery_mode` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `zone` | zone | Required when the record reaches its applicable state | [zone](../value-conventions.md#zone) |
| `first_local_date` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `local_start` | time? | Optional under owner conditions | [clock](../value-conventions.md#clock) |
| `duration_minutes` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `all_day_length` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `visibility` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### calendar_id

The target is [MinistryCalendar](MinistryCalendar.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryCalendar·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinistryCalendar·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinistryCalendar·MISSING | Queue the missing MinistryCalendar mapping or reject the command before linking. |
| Wrong scope | MinistryCalendar·B01 | Do not attach another church’s MinistryCalendar without a supported exchange and local authority. |
| Target rename | Rename MinistryCalendar·A01 after linking | The existing calendar_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No calendar_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### organizer_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing organizer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organizer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### host_group_id

The target is [MinistryGroup](MinistryGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinistryGroup·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinistryGroup·MISSING | Queue the missing MinistryGroup mapping or reject the command before linking. |
| Wrong scope | MinistryGroup·B01 | Do not attach another church’s MinistryGroup without a supported exchange and local authority. |
| Target rename | Rename MinistryGroup·A01 after linking | The existing host_group_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No host_group_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### title

Use human-readable text for `EventSeries.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### summary

Use human-readable text for `EventSeries.summary`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered summary in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No summary at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Use versioned classification or status code for `EventSeries.kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delivery_mode

Use versioned classification or status code for `EventSeries.delivery_mode`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active delivery_mode code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped delivery_mode code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No delivery_mode at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### zone

Use time zone with civil-time rules for `EventSeries.zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Incomplete record | No zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### first_local_date

Use civil calendar date for `EventSeries.first_local_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No first_local_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### local_start

Use local wall-clock time for `EventSeries.local_start`. Preserve local clock time and associate the relevant zone and civil date when scheduling.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 09:30 local | Preserve local clock time and associate the relevant zone and civil date when scheduling. |
| Malformed or unmapped | 25:10 | Reject invalid clock hour. |
| Scheduled time in a skipped local hour | 02:30 during a local spring-forward gap | Use the recurrence owner’s stated gap rule. |
| Repeated local hour | 01:30 occurs twice on the declared local date | Resolve the occurrence explicitly before issuing reminders. |
| Midnight crossing | 23:50 start and 00:10 next-day end | Associate the correct service date and end date. |
| Absent in intake | No local_start provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### duration_minutes

Use whole-number measure for `EventSeries.duration_minutes`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No duration_minutes provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### all_day_length

Use whole-number measure for `EventSeries.all_day_length`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No all_day_length provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### visibility

Use versioned classification or status code for `EventSeries.visibility`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active visibility code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped visibility code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No visibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Use versioned classification or status code for `EventSeries.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [EventOccurrence](EventOccurrence.md).`series_id` | EventSeries identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecurrenceRule](RecurrenceRule.md).`series_id` | EventSeries identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
