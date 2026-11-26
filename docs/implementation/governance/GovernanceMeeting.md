# GovernanceMeeting

[Meetings, notice, eligibility and quorum](../../governance/meetings-and-notice.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique body/sequence. Scheduled end follows start. Link the calendar occurrence for bookings and reminders. Governance owns eligibility and minutes. Record actual opening and closing as session events.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `body_id` | GoverningBody ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `charter_id` | CharterEdition ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `event_occurrence_id` | EventOccurrence ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `class` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `sequence` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `local_zone` | zone | Required when the record reaches its applicable state | [zone](../value-conventions.md#zone) |
| `scheduled_start` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `scheduled_end` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `venue` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `remote_join_instruction` | restricted text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `state` | draft/called/open/adjourned/closed/cancelled | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `reconvenes_id` | GovernanceMeeting ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `chair_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `secretary_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### body_id

The target is [GoverningBody](GoverningBody.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GoverningBody·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GoverningBody·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GoverningBody·MISSING | Queue the missing GoverningBody mapping or reject the command before linking. |
| Wrong scope | GoverningBody·B01 | Do not attach another church’s GoverningBody without a supported exchange and local authority. |
| Target rename | Rename GoverningBody·A01 after linking | The existing body_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No body_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### charter_id

The target is [CharterEdition](CharterEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CharterEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CharterEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CharterEdition·MISSING | Queue the missing CharterEdition mapping or reject the command before linking. |
| Wrong scope | CharterEdition·B01 | Do not attach another church’s CharterEdition without a supported exchange and local authority. |
| Target rename | Rename CharterEdition·A01 after linking | The existing charter_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No charter_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### event_occurrence_id

The target is [EventOccurrence](../ministry/EventOccurrence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EventOccurrence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EventOccurrence·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EventOccurrence·MISSING | Queue the missing EventOccurrence mapping or reject the command before linking. |
| Wrong scope | EventOccurrence·B01 | Do not attach another church’s EventOccurrence without a supported exchange and local authority. |
| Target rename | Rename EventOccurrence·A01 after linking | The existing event_occurrence_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No event_occurrence_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### class

Use versioned classification or status code for `GovernanceMeeting.class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `GovernanceMeeting.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sequence

Use human-readable text for `GovernanceMeeting.sequence`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered sequence in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No sequence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### local_zone

Use time zone with civil-time rules for `GovernanceMeeting.local_zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Incomplete record | No local_zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scheduled_start

Use unambiguous point in time for `GovernanceMeeting.scheduled_start`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No scheduled_start at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scheduled_end

Use unambiguous point in time for `GovernanceMeeting.scheduled_end`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No scheduled_end at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### venue

Use human-readable text for `GovernanceMeeting.venue`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered venue in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No venue provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### remote_join_instruction

Use restricted value or protected content reference for `GovernanceMeeting.remote_join_instruction`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted remote_join_instruction supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No remote_join_instruction provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `draft`, `called`, `open`, `adjourned`, `closed`, `cancelled`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reconvenes_id

The target is [GovernanceMeeting](GovernanceMeeting.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernanceMeeting·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GovernanceMeeting·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GovernanceMeeting·MISSING | Queue the missing GovernanceMeeting mapping or reject the command before linking. |
| Wrong scope | GovernanceMeeting·B01 | Do not attach another church’s GovernanceMeeting without a supported exchange and local authority. |
| Target rename | Rename GovernanceMeeting·A01 after linking | The existing reconvenes_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reconvenes_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### chair_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing chair_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No chair_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### secretary_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing secretary_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No secretary_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### revision

Use revision number or opaque revision token for `GovernanceMeeting.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

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
| [AgendaItem](AgendaItem.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssemblyCredential](AssemblyCredential.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceResponse](AttendanceResponse.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceAttachment](GovernanceAttachment.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceCycle](GovernanceCycle.md).`assembly_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceMeeting](GovernanceMeeting.md).`reconvenes_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MeetingNotice](MeetingNotice.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MeetingRoll](MeetingRoll.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MeetingSessionEvent](MeetingSessionEvent.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MeetingSessionEvent](MeetingSessionEvent.md).`next_meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteEdition](MinuteEdition.md).`confirmed_meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteEdition](MinuteEdition.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PresenceInterval](PresenceInterval.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProxyMandate](ProxyMandate.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [QuorumCheck](QuorumCheck.md).`meeting_id` | GovernanceMeeting identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
