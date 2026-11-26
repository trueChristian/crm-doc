# ExportJob

[Integrations, exports and event delivery](../../platform/exchange-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One artifact per successful revision. Immutable job parameters bind the output to the request and user.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `requested_by` | Ref(UserAccount) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `contract_id` | Ref(InterfaceEdition) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `scope_ref` | ResourceRef | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `filter_snapshot` | structured rule | Required when the record reaches its applicable state | [rule](../value-conventions.md#rule) |
| `fields` | set(code) | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `purpose_id` | Ref(DataPurpose) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `as_of` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `row_count` | integer? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `artifact_ref` | ResourceRef? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `expires_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### requested_by

The target is [UserAccount](UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing requested_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No requested_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### scope_ref

Use scoped or external reference for `ExportJob.scope_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified scope_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped scope_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No scope_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### filter_snapshot

Use versioned structured decision or expression for `ExportJob.filter_snapshot`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for filter_snapshot | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in filter_snapshot | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No filter_snapshot at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fields

Use ordered collection or mathematical set for `ExportJob.fields`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No fields at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose_id

The target is [DataPurpose](DataPurpose.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DataPurpose·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DataPurpose·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DataPurpose·MISSING | Queue the missing DataPurpose mapping or reject the command before linking. |
| Wrong scope | DataPurpose·B01 | Do not attach another church’s DataPurpose without a supported exchange and local authority. |
| Target rename | Rename DataPurpose·A01 after linking | The existing purpose_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No purpose_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### as_of

Use unambiguous point in time for `ExportJob.as_of`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No as_of at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Use versioned classification or status code for `ExportJob.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### row_count

Use whole-number measure for `ExportJob.row_count`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No row_count provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### artifact_ref

Use scoped or external reference for `ExportJob.artifact_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified artifact_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped artifact_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No artifact_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### expires_at

Use unambiguous point in time for `ExportJob.expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No expires_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
