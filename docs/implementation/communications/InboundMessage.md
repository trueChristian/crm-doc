# InboundMessage

[Delivery and responses](../../communications/delivery-and-responses.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Deduplicate inbound events. Apply a verifiable channel stop command promptly even when an individual's identity is ambiguous, at least to that destination under the applicable policy.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `thread_id` | ReplyThread ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `sender_endpoint_ref` | protected text | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `channel` | enum | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `provider_event_key` | opaque | Required when the record reaches its applicable state | [key](../value-conventions.md#key) |
| `received_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `body_restricted` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `attachments_manifest` | restricted list? | Optional under owner conditions | [list](../value-conventions.md#list) |
| `classified_as` | ordinary/opt_out/opt_in/help/unknown | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `handling_state` | pending/routed/resolved/quarantined | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### thread_id

The target is [ReplyThread](ReplyThread.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReplyThread·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ReplyThread·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ReplyThread·MISSING | Queue the missing ReplyThread mapping or reject the command before linking. |
| Wrong scope | ReplyThread·B01 | Do not attach another church’s ReplyThread without a supported exchange and local authority. |
| Target rename | Rename ReplyThread·A01 after linking | The existing thread_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No thread_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### sender_endpoint_ref

Use scoped or external reference for `InboundMessage.sender_endpoint_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified sender_endpoint_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped sender_endpoint_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No sender_endpoint_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### channel

Use versioned classification or status code for `InboundMessage.channel`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active channel code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped channel code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No channel at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### provider_event_key

Use opaque identity or token for `InboundMessage.provider_event_key`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | InboundMessage·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Incomplete record | No provider_event_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### received_at

Use unambiguous point in time for `InboundMessage.received_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No received_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### body_restricted

Use human-readable text for `InboundMessage.body_restricted`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered body_restricted in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No body_restricted provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### attachments_manifest

Use ordered collection or mathematical set for `InboundMessage.attachments_manifest`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Absent in intake | No attachments_manifest provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### classified_as

Declared alternatives in owner order: `ordinary`, `opt_out`, `opt_in`, `help`, `unknown`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ordinary | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_classified_as | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No classified_as at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### handling_state

Declared alternatives in owner order: `pending`, `routed`, `resolved`, `quarantined`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | pending | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_handling_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No handling_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
