# AllocationResult

[Budgeting, cost allocation and cash forecasting](../../finance/planning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Target shares sum to pool. Finance can drill to source lines without disclosing confidential payroll or care information to every budget holder.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `run_id` | → AllocationRun | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `target_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `driver_id` | → AllocationDriver | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `contributing_source_refs` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### run_id

The target is [AllocationRun](AllocationRun.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AllocationRun·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AllocationRun·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AllocationRun·MISSING | Queue the missing AllocationRun mapping or reject the command before linking. |
| Wrong scope | AllocationRun·B01 | Do not attach another church’s AllocationRun without a supported exchange and local authority. |
| Target rename | Rename AllocationRun·A01 after linking | The existing run_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No run_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### target_ref

Use scoped or external reference for `AllocationResult.target_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified target_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped target_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No target_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount

Use exact monetary amount with currency for `AllocationResult.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### driver_id

The target is [AllocationDriver](AllocationDriver.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AllocationDriver·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AllocationDriver·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AllocationDriver·MISSING | Queue the missing AllocationDriver mapping or reject the command before linking. |
| Wrong scope | AllocationDriver·B01 | Do not attach another church’s AllocationDriver without a supported exchange and local authority. |
| Target rename | Rename AllocationDriver·A01 after linking | The existing driver_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No driver_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### contributing_source_refs

Use ordered collection or mathematical set for `AllocationResult.contributing_source_refs`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No contributing_source_refs at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
