# RoleCapability

[Accounts, representation and authorization](../../platform/identity-access.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique role/action/resource/rule combination. Explicit actions include discover, read, edit, approve, export and publish.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `role_id` | Ref(AccessRole) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `action_key` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `resource_type` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `fields` | set(code) | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `conditions` | structured rule | Required when the record reaches its applicable state | [rule](../value-conventions.md#rule) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### role_id

The target is [AccessRole](AccessRole.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessRole·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AccessRole·MISSING | Queue the missing AccessRole mapping or reject the command before linking. |
| Wrong scope | AccessRole·B01 | Do not attach another church’s AccessRole without a supported exchange and local authority. |
| Target rename | Rename AccessRole·A01 after linking | The existing role_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No role_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### action_key

Use versioned classification or status code for `RoleCapability.action_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active action_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped action_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No action_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### resource_type

Use versioned classification or status code for `RoleCapability.resource_type`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active resource_type code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped resource_type code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No resource_type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fields

Use ordered collection or mathematical set for `RoleCapability.fields`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No fields at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### conditions

Use versioned structured decision or expression for `RoleCapability.conditions`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for conditions | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in conditions | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No conditions at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
