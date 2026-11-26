# Delivery

[Delivery and responses](../../communications/delivery-and-responses.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exactly one individual recipient or publication target. Person route requires a permitted endpoint. One intended submission per dedupe key, including publication destination and edition. Retain the provider reference separately from a member identity.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `dispatch_id` | DispatchRequest ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `recipient_id` | DispatchRecipient ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `publication_target_id` | ChannelPublicationTarget ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `endpoint_id` | DeliveryEndpoint ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `channel` | enum | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `sender_id` | SenderIdentity ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `rendered_digest` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `route_order` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `dedupe_key` | opaque | Required when the record reaches its applicable state | [key](../value-conventions.md#key) |
| `state` | queued/held/submitting/unknown/accepted/delivered/failed/suppressed/cancelled/expired | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `queued_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `next_attempt_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `expires_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `reason` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### dispatch_id

The target is [DispatchRequest](DispatchRequest.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DispatchRequest·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DispatchRequest·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DispatchRequest·MISSING | Queue the missing DispatchRequest mapping or reject the command before linking. |
| Wrong scope | DispatchRequest·B01 | Do not attach another church’s DispatchRequest without a supported exchange and local authority. |
| Target rename | Rename DispatchRequest·A01 after linking | The existing dispatch_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No dispatch_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recipient_id

The target is [DispatchRecipient](DispatchRecipient.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DispatchRecipient·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DispatchRecipient·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DispatchRecipient·MISSING | Queue the missing DispatchRecipient mapping or reject the command before linking. |
| Wrong scope | DispatchRecipient·B01 | Do not attach another church’s DispatchRecipient without a supported exchange and local authority. |
| Target rename | Rename DispatchRecipient·A01 after linking | The existing recipient_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No recipient_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### publication_target_id

The target is [ChannelPublicationTarget](ChannelPublicationTarget.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ChannelPublicationTarget·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ChannelPublicationTarget·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ChannelPublicationTarget·MISSING | Queue the missing ChannelPublicationTarget mapping or reject the command before linking. |
| Wrong scope | ChannelPublicationTarget·B01 | Do not attach another church’s ChannelPublicationTarget without a supported exchange and local authority. |
| Target rename | Rename ChannelPublicationTarget·A01 after linking | The existing publication_target_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No publication_target_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### endpoint_id

The target is [DeliveryEndpoint](DeliveryEndpoint.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DeliveryEndpoint·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DeliveryEndpoint·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DeliveryEndpoint·MISSING | Queue the missing DeliveryEndpoint mapping or reject the command before linking. |
| Wrong scope | DeliveryEndpoint·B01 | Do not attach another church’s DeliveryEndpoint without a supported exchange and local authority. |
| Target rename | Rename DeliveryEndpoint·A01 after linking | The existing endpoint_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No endpoint_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### channel

Use versioned classification or status code for `Delivery.channel`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active channel code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped channel code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No channel at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sender_id

The target is [SenderIdentity](SenderIdentity.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SenderIdentity·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SenderIdentity·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SenderIdentity·MISSING | Queue the missing SenderIdentity mapping or reject the command before linking. |
| Wrong scope | SenderIdentity·B01 | Do not attach another church’s SenderIdentity without a supported exchange and local authority. |
| Target rename | Rename SenderIdentity·A01 after linking | The existing sender_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No sender_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rendered_digest

Use integrity fingerprint or opaque verifier for `Delivery.rendered_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No rendered_digest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### route_order

Use whole-number measure for `Delivery.route_order`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No route_order at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### dedupe_key

Use opaque identity or token for `Delivery.dedupe_key`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Delivery·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Incomplete record | No dedupe_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `queued`, `held`, `submitting`, `unknown`, `accepted`, `delivered`, `failed`, `suppressed`, `cancelled`, `expired`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | queued | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### queued_at

Use unambiguous point in time for `Delivery.queued_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No queued_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### next_attempt_at

Use unambiguous point in time for `Delivery.next_attempt_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No next_attempt_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### expires_at

Use unambiguous point in time for `Delivery.expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No expires_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason

Use versioned classification or status code for `Delivery.reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DeliveryAttempt](DeliveryAttempt.md).`delivery_id` | Delivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DeliveryException](DeliveryException.md).`delivery_id` | Delivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DeliveryObservation](DeliveryObservation.md).`delivery_id` | Delivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [NoticeService](../governance/NoticeService.md).`delivery_id` | Delivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReplyThread](ReplyThread.md).`origin_delivery_id` | Delivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
