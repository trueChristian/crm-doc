# AssistancePolicy

[Optional assistance with retrieval, drafting and translation](../../platform/assisted-intelligence.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

A denied purpose or class blocks processing before retrieval or transfer. A disabled capability leaves ordinary screens usable.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `capability_key` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `scope_ref` | ResourceRef | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `enabled` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `purpose_id` | Ref(DataPurpose) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `permitted_classes` | set(code) | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `allowed_operations` | set(code) | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `processing_boundary` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `retention_class` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `reviewer_role_ref` | Ref(AccessRole) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `edition` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### capability_key

Use versioned classification or status code for `AssistancePolicy.capability_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active capability_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped capability_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No capability_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scope_ref

Use scoped or external reference for `AssistancePolicy.scope_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified scope_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped scope_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No scope_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### enabled

Use explicit logical choice for `AssistancePolicy.enabled`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No enabled at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### permitted_classes

Use ordered collection or mathematical set for `AssistancePolicy.permitted_classes`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No permitted_classes at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allowed_operations

Use ordered collection or mathematical set for `AssistancePolicy.allowed_operations`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No allowed_operations at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### processing_boundary

Use versioned classification or status code for `AssistancePolicy.processing_boundary`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active processing_boundary code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped processing_boundary code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No processing_boundary at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### retention_class

Use versioned classification or status code for `AssistancePolicy.retention_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active retention_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped retention_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No retention_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reviewer_role_ref

The target is [AccessRole](AccessRole.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessRole·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AccessRole·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AccessRole·MISSING | Queue the missing AccessRole mapping or reject the command before linking. |
| Wrong scope | AccessRole·B01 | Do not attach another church’s AccessRole without a supported exchange and local authority. |
| Target rename | Rename AccessRole·A01 after linking | The existing reviewer_role_ref keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No reviewer_role_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### edition

Use whole-number measure for `AssistancePolicy.edition`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No edition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AssistanceRun](AssistanceRun.md).`policy_id` | AssistancePolicy identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
