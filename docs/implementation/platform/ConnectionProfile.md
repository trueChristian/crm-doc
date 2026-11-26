# ConnectionProfile

[Integrations, exports and event delivery](../../platform/exchange-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Allow only approved endpoints and require a verified test connection before activation. Credentials are replaceable without changing the identity.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `principal_id` | Ref(IntegrationPrincipal) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `provider_kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `destination_ref` | protected address | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `environment` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `outbound_fields` | set(code) | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `credential_revision` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `enabled_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `egress_policy_ref` | ResourceRef | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### principal_id

The target is [IntegrationPrincipal](IntegrationPrincipal.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | IntegrationPrincipal·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | IntegrationPrincipal·MISSING | Queue the missing IntegrationPrincipal mapping or reject the command before linking. |
| Wrong scope | IntegrationPrincipal·B01 | Do not attach another church’s IntegrationPrincipal without a supported exchange and local authority. |
| Target rename | Rename IntegrationPrincipal·A01 after linking | The existing principal_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No principal_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### provider_kind

Use versioned classification or status code for `ConnectionProfile.provider_kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active provider_kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped provider_kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No provider_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### destination_ref

Use scoped or external reference for `ConnectionProfile.destination_ref`. Resolve against the permitted kind, owning namespace and purpose.
Field access: enforce the declared protection on reads, search, previews, exports and audit evidence as well as the underlying resource value.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified destination_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped destination_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No destination_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### environment

Use versioned classification or status code for `ConnectionProfile.environment`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active environment code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped environment code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No environment at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### outbound_fields

Use ordered collection or mathematical set for `ConnectionProfile.outbound_fields`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No outbound_fields at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### credential_revision

Use whole-number measure for `ConnectionProfile.credential_revision`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No credential_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### enabled_at

Use unambiguous point in time for `ConnectionProfile.enabled_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No enabled_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### egress_policy_ref

Use scoped or external reference for `ConnectionProfile.egress_policy_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified egress_policy_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped egress_policy_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No egress_policy_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [InboundReceipt](InboundReceipt.md).`connection_id` | ConnectionProfile identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IntegrationSubscription](IntegrationSubscription.md).`connection_id` | ConnectionProfile identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
