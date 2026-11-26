# InboundReceipt

[Integrations, exports and event delivery](../../platform/exchange-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique connection and sender message key. An existing key with a different payload enters quarantine.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `connection_id` | Ref(ConnectionProfile) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sender_message_key` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `contract_id` | Ref(InterfaceEdition) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `payload_digest` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `arrived_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `authenticity_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `business_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `result_ref` | ResourceRef? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `failure_key` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### connection_id

The target is [ConnectionProfile](ConnectionProfile.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ConnectionProfile·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ConnectionProfile·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ConnectionProfile·MISSING | Queue the missing ConnectionProfile mapping or reject the command before linking. |
| Wrong scope | ConnectionProfile·B01 | Do not attach another church’s ConnectionProfile without a supported exchange and local authority. |
| Target rename | Rename ConnectionProfile·A01 after linking | The existing connection_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No connection_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sender_message_key

Use human-readable text for `InboundReceipt.sender_message_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered sender_message_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No sender_message_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### contract_id

The target is [InterfaceEdition](InterfaceEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | InterfaceEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | InterfaceEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | InterfaceEdition·MISSING | Queue the missing InterfaceEdition mapping or reject the command before linking. |
| Wrong scope | InterfaceEdition·B01 | Do not attach another church’s InterfaceEdition without a supported exchange and local authority. |
| Target rename | Rename InterfaceEdition·A01 after linking | The existing contract_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No contract_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### payload_digest

Use integrity fingerprint or opaque verifier for `InboundReceipt.payload_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No payload_digest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### arrived_at

Use unambiguous point in time for `InboundReceipt.arrived_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No arrived_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authenticity_state

Use versioned classification or status code for `InboundReceipt.authenticity_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active authenticity_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped authenticity_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No authenticity_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### business_state

Use versioned classification or status code for `InboundReceipt.business_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active business_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped business_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No business_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### result_ref

Use scoped or external reference for `InboundReceipt.result_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified result_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped result_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No result_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### failure_key

Use versioned classification or status code for `InboundReceipt.failure_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active failure_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped failure_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No failure_key provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
