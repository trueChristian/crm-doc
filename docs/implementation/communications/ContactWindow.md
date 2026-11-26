# ContactWindow

[Recipients and channel policy](../../communications/recipients-and-channels.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Windows can cross midnight. Define timezone source and transition policy. If no overlap is permitted before a deadline, surface an exception to the operator.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `person_id` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `purpose_id` | CommunicationPurpose ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `zone` | zone | Required when the record reaches its applicable state | [zone](../value-conventions.md#zone) |
| `weekdays` | day set | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `start_local` | time | Required when the record reaches its applicable state | [clock](../value-conventions.md#clock) |
| `end_local` | time | Required when the record reaches its applicable state | [clock](../value-conventions.md#clock) |
| `mode` | allow/quiet | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `effective_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `effective_until` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose_id

The target is [CommunicationPurpose](CommunicationPurpose.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CommunicationPurpose·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CommunicationPurpose·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CommunicationPurpose·MISSING | Queue the missing CommunicationPurpose mapping or reject the command before linking. |
| Wrong scope | CommunicationPurpose·B01 | Do not attach another church’s CommunicationPurpose without a supported exchange and local authority. |
| Target rename | Rename CommunicationPurpose·A01 after linking | The existing purpose_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No purpose_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### zone

Use time zone with civil-time rules for `ContactWindow.zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Incomplete record | No zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### weekdays

Use ordered collection or mathematical set for `ContactWindow.weekdays`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No weekdays at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### start_local

Use local wall-clock time for `ContactWindow.start_local`. Preserve local clock time and associate the relevant zone and civil date when scheduling.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 09:30 local | Preserve local clock time and associate the relevant zone and civil date when scheduling. |
| Malformed or unmapped | 25:10 | Reject invalid clock hour. |
| Scheduled time in a skipped local hour | 02:30 during a local spring-forward gap | Use the recurrence owner’s stated gap rule. |
| Repeated local hour | 01:30 occurs twice on the declared local date | Resolve the occurrence explicitly before issuing reminders. |
| Midnight crossing | 23:50 start and 00:10 next-day end | Associate the correct service date and end date. |
| Incomplete record | No start_local at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### end_local

Use local wall-clock time for `ContactWindow.end_local`. Preserve local clock time and associate the relevant zone and civil date when scheduling.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 09:30 local | Preserve local clock time and associate the relevant zone and civil date when scheduling. |
| Malformed or unmapped | 25:10 | Reject invalid clock hour. |
| Scheduled time in a skipped local hour | 02:30 during a local spring-forward gap | Use the recurrence owner’s stated gap rule. |
| Repeated local hour | 01:30 occurs twice on the declared local date | Resolve the occurrence explicitly before issuing reminders. |
| Midnight crossing | 23:50 start and 00:10 next-day end | Associate the correct service date and end date. |
| Incomplete record | No end_local at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### mode

Declared alternatives in owner order: `allow`, `quiet`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | allow | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_mode | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No mode at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_from

Use civil calendar date for `ContactWindow.effective_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No effective_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_until

Use civil calendar date for `ContactWindow.effective_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No effective_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
