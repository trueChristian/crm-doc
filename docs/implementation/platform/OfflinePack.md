# OfflinePack

[Offline capture and synchronization](../../platform/offline-continuity.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One scope and purpose per pack. Permission and data freshness have independent cutoffs.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `device_id` | Ref(RegisteredDevice) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `activity_ref` | ResourceRef | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `prepared_for` | Ref(UserAccount) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `policy_revision` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `source_cutoff` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `permission_revision` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `permitted_operations` | set(code) | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `field_manifest` | set(code) | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `expires_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `last_ack_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### device_id

The target is [RegisteredDevice](RegisteredDevice.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RegisteredDevice·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RegisteredDevice·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RegisteredDevice·MISSING | Queue the missing RegisteredDevice mapping or reject the command before linking. |
| Wrong scope | RegisteredDevice·B01 | Do not attach another church’s RegisteredDevice without a supported exchange and local authority. |
| Target rename | Rename RegisteredDevice·A01 after linking | The existing device_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No device_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### activity_ref

Use scoped or external reference for `OfflinePack.activity_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified activity_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped activity_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No activity_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prepared_for

The target is [UserAccount](UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing prepared_for keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No prepared_for at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### policy_revision

Use whole-number measure for `OfflinePack.policy_revision`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No policy_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_cutoff

Use unambiguous point in time for `OfflinePack.source_cutoff`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No source_cutoff at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### permission_revision

Use whole-number measure for `OfflinePack.permission_revision`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No permission_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### permitted_operations

Use ordered collection or mathematical set for `OfflinePack.permitted_operations`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No permitted_operations at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### field_manifest

Use ordered collection or mathematical set for `OfflinePack.field_manifest`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No field_manifest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expires_at

Use unambiguous point in time for `OfflinePack.expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No expires_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### last_ack_at

Use unambiguous point in time for `OfflinePack.last_ack_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No last_ack_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Use versioned classification or status code for `OfflinePack.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [LocalChange](LocalChange.md).`pack_id` | OfflinePack identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OfflineItem](OfflineItem.md).`pack_id` | OfflinePack identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SyncAttempt](SyncAttempt.md).`pack_id` | OfflinePack identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TemporaryLink](TemporaryLink.md).`pack_id` | OfflinePack identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
