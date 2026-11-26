# AvailabilityWindow

[Volunteers and rotas](../../ministry/volunteers.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Available, preferred or unavailable. A dated unavailability overrides a recurring preference. Split overnight ranges at the local boundary when checking conflicts.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `starts_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `ends_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `weekdays` | code_set? | Optional under owner conditions | [list](../value-conventions.md#list) |
| `local_start` | time? | Optional under owner conditions | [clock](../value-conventions.md#clock) |
| `local_end` | time? | Optional under owner conditions | [clock](../value-conventions.md#clock) |
| `zone` | zone | Required when the record reaches its applicable state | [zone](../value-conventions.md#zone) |
| `priority` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

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

### kind

Use versioned classification or status code for `AvailabilityWindow.kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### starts_on

Use civil calendar date for `AvailabilityWindow.starts_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No starts_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ends_on

Use civil calendar date for `AvailabilityWindow.ends_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No ends_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### weekdays

Use ordered collection or mathematical set for `AvailabilityWindow.weekdays`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Absent in intake | No weekdays provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### local_start

Use local wall-clock time for `AvailabilityWindow.local_start`. Preserve local clock time and associate the relevant zone and civil date when scheduling.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 09:30 local | Preserve local clock time and associate the relevant zone and civil date when scheduling. |
| Malformed or unmapped | 25:10 | Reject invalid clock hour. |
| Scheduled time in a skipped local hour | 02:30 during a local spring-forward gap | Use the recurrence owner’s stated gap rule. |
| Repeated local hour | 01:30 occurs twice on the declared local date | Resolve the occurrence explicitly before issuing reminders. |
| Midnight crossing | 23:50 start and 00:10 next-day end | Associate the correct service date and end date. |
| Absent in intake | No local_start provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### local_end

Use local wall-clock time for `AvailabilityWindow.local_end`. Preserve local clock time and associate the relevant zone and civil date when scheduling.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 09:30 local | Preserve local clock time and associate the relevant zone and civil date when scheduling. |
| Malformed or unmapped | 25:10 | Reject invalid clock hour. |
| Scheduled time in a skipped local hour | 02:30 during a local spring-forward gap | Use the recurrence owner’s stated gap rule. |
| Repeated local hour | 01:30 occurs twice on the declared local date | Resolve the occurrence explicitly before issuing reminders. |
| Midnight crossing | 23:50 start and 00:10 next-day end | Associate the correct service date and end date. |
| Absent in intake | No local_end provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### zone

Use time zone with civil-time rules for `AvailabilityWindow.zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Incomplete record | No zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### priority

Use whole-number measure for `AvailabilityWindow.priority`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No priority at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
