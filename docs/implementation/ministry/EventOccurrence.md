# EventOccurrence

[Calendars and occurrences](../../ministry/calendar.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique original local slot per series, including a disambiguator for repeated clock times. Occurrence ID survives rescheduling. End is exclusive. Unlimited capacity is explicit by absent limit. Zero closes admission.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `series_id` | → EventSeries | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `original_local_key` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `local_date` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `starts_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `ends_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `all_day_end_date` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `venue_label` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `campus_id` | → Campus? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `capacity` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `published_revision` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `cancel_reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### series_id

The target is [EventSeries](EventSeries.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EventSeries·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EventSeries·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EventSeries·MISSING | Queue the missing EventSeries mapping or reject the command before linking. |
| Wrong scope | EventSeries·B01 | Do not attach another church’s EventSeries without a supported exchange and local authority. |
| Target rename | Rename EventSeries·A01 after linking | The existing series_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No series_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### original_local_key

Use human-readable text for `EventOccurrence.original_local_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered original_local_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No original_local_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### local_date

Use civil calendar date for `EventOccurrence.local_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No local_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### starts_at

Use unambiguous point in time for `EventOccurrence.starts_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No starts_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### ends_at

Use unambiguous point in time for `EventOccurrence.ends_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No ends_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### all_day_end_date

Use civil calendar date for `EventOccurrence.all_day_end_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No all_day_end_date provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### venue_label

Use human-readable text for `EventOccurrence.venue_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered venue_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No venue_label provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

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

### capacity

Use whole-number measure for `EventOccurrence.capacity`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No capacity provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Use versioned classification or status code for `EventOccurrence.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### published_revision

Use whole-number measure for `EventOccurrence.published_revision`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No published_revision provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### cancel_reason

Use human-readable text for `EventOccurrence.cancel_reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered cancel_reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No cancel_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AdmissionOption](AdmissionOption.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealChannel](../development/AppealChannel.md).`event_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceCount](AttendanceCount.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceRecord](AttendanceRecord.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CeremonyBooking](../administration/CeremonyBooking.md).`event_occurrence_ref` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChildCheckIn](ChildCheckIn.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CommunityDistribution](CommunityDistribution.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CourseSession](CourseSession.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DutyShift](DutyShift.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EquipmentReservation](EquipmentReservation.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EventAccessDetail](EventAccessDetail.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EventPublication](EventPublication.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EventRegistration](EventRegistration.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceMeeting](../governance/GovernanceMeeting.md).`event_occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryProgramme](MinistryProgramme.md).`main_occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OccurrenceOverride](OccurrenceOverride.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationalBriefing](OperationalBriefing.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationsIncident](OperationsIncident.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PartnershipAgreement](../development/PartnershipAgreement.md).`event_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProgrammeSession](ProgrammeSession.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RehearsalCall](RehearsalCall.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RoomBooking](RoomBooking.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServicePlan](ServicePlan.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupervisedSession](SupervisedSession.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TransportJourney](TransportJourney.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TripLeg](TripLeg.md).`occurrence_id` | EventOccurrence identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
