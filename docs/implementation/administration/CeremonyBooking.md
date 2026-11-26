# CeremonyBooking

[Weddings, funerals, memorials and cemetery administration](../../administration/life-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Real-time room availability belongs to the resource register. At completion, record the appropriate rite once and link it to this booking.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `request_id` | → CeremonyRequest | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `event_occurrence_ref` | → EventOccurrence | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `purpose` | rehearsal, service, reception or graveside | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `resource_booking_refs` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [list](../value-conventions.md#list) |
| `fee_or_waiver_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `agreed_at` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [instant](../value-conventions.md#instant) |
| `cancellation_terms_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `CeremonyBooking.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CeremonyBooking·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### request_id

The target is [CeremonyRequest](CeremonyRequest.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CeremonyRequest·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CeremonyRequest·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CeremonyRequest·MISSING | Queue the missing CeremonyRequest mapping or reject the command before linking. |
| Wrong scope | CeremonyRequest·B01 | Do not attach another church’s CeremonyRequest without a supported exchange and local authority. |
| Target rename | Rename CeremonyRequest·A01 after linking | The existing request_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No request_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### event_occurrence_ref

The target is [EventOccurrence](../ministry/EventOccurrence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EventOccurrence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EventOccurrence·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EventOccurrence·MISSING | Queue the missing EventOccurrence mapping or reject the command before linking. |
| Wrong scope | EventOccurrence·B01 | Do not attach another church’s EventOccurrence without a supported exchange and local authority. |
| Target rename | Rename EventOccurrence·A01 after linking | The existing event_occurrence_ref keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No event_occurrence_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose

Declared alternatives in owner order: `rehearsal`, `service`, `reception`, `graveside`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | rehearsal | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_purpose | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### resource_booking_refs

Use ordered collection or mathematical set for `CeremonyBooking.resource_booking_refs`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No resource_booking_refs at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fee_or_waiver_ref

Use scoped or external reference for `CeremonyBooking.fee_or_waiver_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fee_or_waiver_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped fee_or_waiver_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No fee_or_waiver_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### agreed_at

Use unambiguous point in time for `CeremonyBooking.agreed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No agreed_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cancellation_terms_ref

Use scoped or external reference for `CeremonyBooking.cancellation_terms_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified cancellation_terms_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped cancellation_terms_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No cancellation_terms_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
