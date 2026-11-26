# TemporaryLink

[Offline capture and synchronization](../../platform/offline-continuity.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique temporary key per pack. Link later submissions to the accepted canonical identity.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `pack_id` | Ref(OfflinePack) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `temporary_key` | opaque | Required when the record reaches its applicable state | [key](../value-conventions.md#key) |
| `canonical_ref` | ResourceRef | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `resolved_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### pack_id

The target is [OfflinePack](OfflinePack.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OfflinePack·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OfflinePack·MISSING | Queue the missing OfflinePack mapping or reject the command before linking. |
| Wrong scope | OfflinePack·B01 | Do not attach another church’s OfflinePack without a supported exchange and local authority. |
| Target rename | Rename OfflinePack·A01 after linking | The existing pack_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No pack_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### temporary_key

Use opaque identity or token for `TemporaryLink.temporary_key`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TemporaryLink·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Incomplete record | No temporary_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### canonical_ref

Use scoped or external reference for `TemporaryLink.canonical_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified canonical_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped canonical_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No canonical_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### resolved_at

Use unambiguous point in time for `TemporaryLink.resolved_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No resolved_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
