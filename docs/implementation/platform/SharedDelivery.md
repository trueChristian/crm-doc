# SharedDelivery

[Organization provisioning, shared work and exit](../../platform/organization-lifecycle.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One explicitly scoped transfer. Recipient uses its own local identity keys. Maintain evidence for correction and agreed deletion notices.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `agreement_id` | Ref(SharingAgreement) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sender_subject_ref` | ResourceRef | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `exported_fields` | set(code) | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `sent_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `payload_digest` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `receiver_reference` | opaque? | Optional under owner conditions | [key](../value-conventions.md#key) |
| `accepted_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `recall_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### agreement_id

The target is [SharingAgreement](SharingAgreement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SharingAgreement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | SharingAgreement·MISSING | Queue the missing SharingAgreement mapping or reject the command before linking. |
| Wrong scope | SharingAgreement·B01 | Do not attach another church’s SharingAgreement without a supported exchange and local authority. |
| Target rename | Rename SharingAgreement·A01 after linking | The existing agreement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No agreement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sender_subject_ref

Use scoped or external reference for `SharedDelivery.sender_subject_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified sender_subject_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped sender_subject_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No sender_subject_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### exported_fields

Use ordered collection or mathematical set for `SharedDelivery.exported_fields`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No exported_fields at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sent_at

Use unambiguous point in time for `SharedDelivery.sent_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No sent_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### payload_digest

Use integrity fingerprint or opaque verifier for `SharedDelivery.payload_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No payload_digest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### receiver_reference

Use opaque identity or token for `SharedDelivery.receiver_reference`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SharedDelivery·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Absent in intake | No receiver_reference provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### accepted_at

Use unambiguous point in time for `SharedDelivery.accepted_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No accepted_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recall_state

Use versioned classification or status code for `SharedDelivery.recall_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active recall_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped recall_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No recall_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Use versioned classification or status code for `SharedDelivery.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
