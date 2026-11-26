# RegistrationPlace

[Registration, tickets and attendance](../../ministry/registration.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

For named attendance, one place per attendee. Unnamed group allocations require a responsible contact and a positive quantity. For child sessions obtain a verified person record before admission.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `registration_id` | → EventRegistration | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `option_id` | → AdmissionOption | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `guest_label` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `quantity` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `hold_expires_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `confirmed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `cancelled_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### registration_id

The target is [EventRegistration](EventRegistration.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EventRegistration·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EventRegistration·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EventRegistration·MISSING | Queue the missing EventRegistration mapping or reject the command before linking. |
| Wrong scope | EventRegistration·B01 | Do not attach another church’s EventRegistration without a supported exchange and local authority. |
| Target rename | Rename EventRegistration·A01 after linking | The existing registration_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No registration_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### option_id

The target is [AdmissionOption](AdmissionOption.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AdmissionOption·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AdmissionOption·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AdmissionOption·MISSING | Queue the missing AdmissionOption mapping or reject the command before linking. |
| Wrong scope | AdmissionOption·B01 | Do not attach another church’s AdmissionOption without a supported exchange and local authority. |
| Target rename | Rename AdmissionOption·A01 after linking | The existing option_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No option_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### guest_label

Use human-readable text for `RegistrationPlace.guest_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered guest_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No guest_label provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### quantity

Use whole-number measure for `RegistrationPlace.quantity`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Use versioned classification or status code for `RegistrationPlace.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### hold_expires_at

Use unambiguous point in time for `RegistrationPlace.hold_expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No hold_expires_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### confirmed_at

Use unambiguous point in time for `RegistrationPlace.confirmed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No confirmed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### cancelled_at

Use unambiguous point in time for `RegistrationPlace.cancelled_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No cancelled_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AdmissionSaleUnit](AdmissionSaleUnit.md).`place_id` | RegistrationPlace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AdmissionSeat](AdmissionSeat.md).`place_id` | RegistrationPlace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AdmissionTicket](AdmissionTicket.md).`place_id` | RegistrationPlace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceRecord](AttendanceRecord.md).`place_id` | RegistrationPlace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChildCheckIn](ChildCheckIn.md).`place_id` | RegistrationPlace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProgrammeSelection](ProgrammeSelection.md).`general_place_id` | RegistrationPlace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProgrammeSelection](ProgrammeSelection.md).`session_place_id` | RegistrationPlace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RegistrationAnswer](RegistrationAnswer.md).`place_id` | RegistrationPlace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [WaitingEntry](WaitingEntry.md).`place_id` | RegistrationPlace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
