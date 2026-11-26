# Calendars and occurrences

A calendar serves congregational worship, funerals, classes, building work, private appointments and online gatherings. The source of truth for a dated activity is its occurrence. A recurring series supplies defaults. An organizer can change a single Sunday without altering attendance, reminders or reservations for other Sundays.

## Records

| Logical record | Fields | Cardinality and validation |
| --- | --- | --- |
| MinistryCalendar | `name text`, `congregation_id → Congregation?`, `campus_id → Campus?`, `owner_group_id → MinistryGroup?`, `default_zone zone`, `visibility code`, `approval_rule code` | A campus can operate several calendars. Public, member, group and private scopes are available. A combined calendar honors each item's scope. |
| EventSeries | `calendar_id → MinistryCalendar`, `organizer_id → Person`, `host_group_id → MinistryGroup?`, `title text`, `summary text`, `kind code`, `delivery_mode code`, `zone zone`, `first_local_date date`, `local_start time?`, `duration_minutes count?`, `all_day_length count?`, `visibility code`, `state code` | One-off activities have one occurrence. An all-day activity uses local dates and positive day count. Timed items use positive duration and named zone. Support in-person, online and hybrid. |
| RecurrenceRule | `series_id → EventSeries`, `frequency code`, `interval count`, `weekdays code_set?`, `month_days integer_set?`, `ordinal integer?`, `months integer_set?`, `until_date date?`, `max_occurrences count?`, `gap_policy code`, `fold_policy code` | One active revision per series. Daily, weekly, monthly or yearly repetitions. End by count, by inclusive local date or indefinitely. Positive interval. Define how to handle missing month days, clock changes and leap dates. |
| EventOccurrence | `series_id → EventSeries`, `original_local_key text`, `local_date date`, `starts_at instant?`, `ends_at instant?`, `all_day_end_date date?`, `venue_label text?`, `campus_id → Campus?`, `capacity count?`, `state code`, `published_revision count?`, `cancel_reason text?` | Unique original local slot per series, including a disambiguator for repeated clock times. Occurrence ID survives rescheduling. End is exclusive. Unlimited capacity is explicit by absent limit. Zero closes admission. |
| OccurrenceOverride | `occurrence_id → EventOccurrence`, `field_code code`, `replacement_value typed_value`, `reason text`, `changed_by → UserAccount`, `changed_at instant` | One effective override per field and revision. Cancelling a date retains a cancellation marker so expansion cannot recreate it. |
| EventPublication | `occurrence_id → EventOccurrence`, `audience code`, `title text`, `summary text`, `language code`, `approved_by → UserAccount?`, `publish_at instant?`, `withdraw_at instant?`, `state code` | Multiple language and audience versions allowed. Restrict exact locations, private meeting links and participants when appropriate. |
| EventAccessDetail | `occurrence_id → EventOccurrence`, `audience code`, `location_instructions text?`, `online_join_reference text?`, `accessibility_detail text?`, `valid_from instant?`, `valid_until instant?` | Support sign-language interpretation, quiet space, step-free access and transport instructions. Restrict participant-only connection details. |
| CalendarSubscription | `calendar_id → MinistryCalendar`, `account_id → UserAccount?`, `audience code`, `scope_filter code?`, `issued_at instant`, `expires_at instant?`, `revoked_at instant?` | Personal subscription is bound to an authorized account, revocable and limited to the same visible event fields. Warn that copies already downloaded can persist. |

## Publication flow

The organizer creates a draft, previews the first and last dates and checks conflicts with rooms, equipment, transport, speakers and shifts. A reviewer may return it for changes or approve a particular revision. Publication makes the approved fields visible to the designated audience at the selected instant. State proceeds from draft to proposed, approved, published, completed or cancelled. A significant change to an approved occurrence goes through review again. Staff can unpublish immediately when a venue or a protected person's details were exposed.

Schedule repeated events in the origin's named time zone. A 09:00 local service stays at 09:00 when its region changes its UTC offset. For a nonexistent local time, require the selected policy to skip, move forward or prompt. For a repeated local hour, select the earlier or later instant explicitly and show it in preview. A series may add an exceptional date or skip a holiday. On “this and following,” preserve past instances and retain references for already-booked future dates, offering an impact preview for incompatible changes. Indefinite series expand inside a bounded planning horizon extended on demand. An all-day item must preserve its local dates in a remote viewer's display.

## Handovers and failure handling

A published change records affected registration holders, staff shifts, bookings, tickets and scheduled notices. A coordinator sees a result for each dependency. A room booking conflict can move the occurrence into “changes pending” until resolved. A completed payment is addressed through the refund policy. A schedule update never posts a refund by itself. A cancellation releases future resource claims, stops unissued reminders and queues a cancellation message once per recipient and change. A remote communications outage leaves an actionable delivery backlog without undoing a calendar decision. Retrying the same occurrence revision cannot release a booking or issue a notice twice.

Expose a public calendar, a member calendar, a filtered “my events and duties” calendar and a staff collision view. Suppress hidden meeting titles, host names and addresses from availability responses. For an outsider a private room reservation may be displayed simply as unavailable.

| Acceptance case | Observable result |
| --- | --- |
| A choir meets each last Friday except in December | Preview includes the last actual Friday of every applicable month. Editing April changes one occurrence only. |
| A youth service moves from 09:00 to 10:30 after a family registers | The family retains one registration under the same occurrence. Old pending reminders are superseded and a change notice uses the new time. |
| A retreat runs Friday through Sunday as an all-day activity | It shows Friday, Saturday and Sunday locally with Monday as its exclusive boundary. |
| An organizer retries a failed batch calendar expansion | Each original slot has one occurrence. A previously cancelled holiday remains cancelled. |
| A confidential pastoral appointment occupies a room | A public visitor cannot infer the participants, purpose or joining instructions. |
