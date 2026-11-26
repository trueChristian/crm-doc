# DocketExchange

[Complaints, whistleblowing and grievances](../../assurance/complaints-and-grievances.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Support anonymous follow-up, controlled interviews, document requests, independent witness accounts and receipt tracking. Routine email/notifications contain only approved neutral language and secure retrieval instructions.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `docket_id` | → ReviewDocket | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sender_role` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `recipient_scope` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `sent_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `delivery_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `ack_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `body_ref` | protected ID | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `redaction_version` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `purpose` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `DocketExchange.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DocketExchange·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### docket_id

The target is [ReviewDocket](ReviewDocket.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReviewDocket·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ReviewDocket·MISSING | Queue the missing ReviewDocket mapping or reject the command before linking. |
| Wrong scope | ReviewDocket·B01 | Do not attach another church’s ReviewDocket without a supported exchange and local authority. |
| Target rename | Rename ReviewDocket·A01 after linking | The existing docket_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No docket_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sender_role

Use versioned classification or status code for `DocketExchange.sender_role`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active sender_role code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped sender_role code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No sender_role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recipient_scope

Use versioned classification or status code for `DocketExchange.recipient_scope`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active recipient_scope code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped recipient_scope code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No recipient_scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sent_at

Use unambiguous point in time for `DocketExchange.sent_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No sent_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delivery_state

Use versioned classification or status code for `DocketExchange.delivery_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active delivery_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped delivery_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No delivery_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ack_at

Use unambiguous point in time for `DocketExchange.ack_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No ack_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### body_ref

Use scoped or external reference for `DocketExchange.body_ref`. Resolve against the permitted kind, owning namespace and purpose.
Field access: enforce the declared protection on reads, search, previews, exports and audit evidence as well as the underlying resource value.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified body_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped body_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No body_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### redaction_version

Use human-readable text for `DocketExchange.redaction_version`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered redaction_version in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No redaction_version provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### purpose

Use versioned classification or status code for `DocketExchange.purpose`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active purpose code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped purpose code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Use the minimum evidence allowed by the selected anonymous, pseudonymous or identified mode. A permitted operator may be accountable for receiving or reviewing work without collecting the identity of a protected subject. Keep safe-channel, identity and case evidence apart from releasable totals and narratives; apply the original permissions to the verification evidence.
