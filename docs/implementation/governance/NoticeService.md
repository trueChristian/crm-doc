# NoticeService

[Meetings, notice, eligibility and quorum](../../governance/meetings-and-notice.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One or more means per entitled party. Hand delivery and publication support witnessed evidence. The charter decides which evidence satisfies service.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `notice_id` | MeetingNotice ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `roll_entry_id` | VotingRollEntry ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `mode` | digital/post/hand/publication | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `delivery_id` | Delivery ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `dispatched_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `evidence_ref` | text? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `acknowledged_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `exception_reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `reviewed_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### notice_id

The target is [MeetingNotice](MeetingNotice.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MeetingNotice·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MeetingNotice·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MeetingNotice·MISSING | Queue the missing MeetingNotice mapping or reject the command before linking. |
| Wrong scope | MeetingNotice·B01 | Do not attach another church’s MeetingNotice without a supported exchange and local authority. |
| Target rename | Rename MeetingNotice·A01 after linking | The existing notice_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No notice_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### roll_entry_id

The target is [VotingRollEntry](VotingRollEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VotingRollEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | VotingRollEntry·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | VotingRollEntry·MISSING | Queue the missing VotingRollEntry mapping or reject the command before linking. |
| Wrong scope | VotingRollEntry·B01 | Do not attach another church’s VotingRollEntry without a supported exchange and local authority. |
| Target rename | Rename VotingRollEntry·A01 after linking | The existing roll_entry_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No roll_entry_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### mode

Declared alternatives in owner order: `digital`, `post`, `hand`, `publication`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | digital | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_mode | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No mode at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delivery_id

The target is [Delivery](../communications/Delivery.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Delivery·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Delivery·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Delivery·MISSING | Queue the missing Delivery mapping or reject the command before linking. |
| Wrong scope | Delivery·B01 | Do not attach another church’s Delivery without a supported exchange and local authority. |
| Target rename | Rename Delivery·A01 after linking | The existing delivery_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No delivery_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### dispatched_at

Use unambiguous point in time for `NoticeService.dispatched_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No dispatched_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### evidence_ref

Use scoped or external reference for `NoticeService.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### acknowledged_at

Use unambiguous point in time for `NoticeService.acknowledged_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No acknowledged_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### exception_reason

Use human-readable text for `NoticeService.exception_reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered exception_reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No exception_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reviewed_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing reviewed_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reviewed_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
