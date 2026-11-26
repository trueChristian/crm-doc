# DeliveryObservation

[Delivery and responses](../../communications/delivery-and-responses.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Deduplicate provider/event key. Preserve late observations and contradictory evidence. Unverified reports cannot alter member preferences or a final status.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `delivery_id` | Delivery ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `attempt_id` | DeliveryAttempt ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `event_key` | opaque | Required when the record reaches its applicable state | [key](../value-conventions.md#key) |
| `kind` | accepted/delivered/read/failed/complaint/unsubscribe/returned | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `observed_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `received_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `verification_result` | verified/quarantined | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `source_ref` | protected text? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `redacted_detail` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### delivery_id

The target is [Delivery](Delivery.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Delivery·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Delivery·MISSING | Queue the missing Delivery mapping or reject the command before linking. |
| Wrong scope | Delivery·B01 | Do not attach another church’s Delivery without a supported exchange and local authority. |
| Target rename | Rename Delivery·A01 after linking | The existing delivery_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No delivery_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### attempt_id

The target is [DeliveryAttempt](DeliveryAttempt.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DeliveryAttempt·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | DeliveryAttempt·MISSING | Queue the missing DeliveryAttempt mapping or reject the command before linking. |
| Wrong scope | DeliveryAttempt·B01 | Do not attach another church’s DeliveryAttempt without a supported exchange and local authority. |
| Target rename | Rename DeliveryAttempt·A01 after linking | The existing attempt_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No attempt_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### event_key

Use opaque identity or token for `DeliveryObservation.event_key`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DeliveryObservation·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Incomplete record | No event_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `accepted`, `delivered`, `read`, `failed`, `complaint`, `unsubscribe`, `returned`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | accepted | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### observed_at

Use unambiguous point in time for `DeliveryObservation.observed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No observed_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### received_at

Use unambiguous point in time for `DeliveryObservation.received_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No received_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### verification_result

Declared alternatives in owner order: `verified`, `quarantined`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_verification_result | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No verification_result at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_ref

Use scoped or external reference for `DeliveryObservation.source_ref`. Resolve against the permitted kind, owning namespace and purpose.
Field access: enforce the declared protection on reads, search, previews, exports and audit evidence as well as the underlying resource value.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified source_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped source_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No source_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### redacted_detail

Use human-readable text for `DeliveryObservation.redacted_detail`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered redacted_detail in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No redacted_detail provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
