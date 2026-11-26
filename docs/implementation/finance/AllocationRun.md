# AllocationRun

[Budgeting, cost allocation and cash forecasting](../../finance/planning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Lock input snapshot, rates and rounding. A revision reverses or posts a traceable delta.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `rule_id` | → AllocationRule | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `period_id` | → FiscalPeriod | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `input_snapshot` | evidence | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `pool_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `approved_by_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `posting_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `reverses_run_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### rule_id

The target is [AllocationRule](AllocationRule.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AllocationRule·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AllocationRule·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AllocationRule·MISSING | Queue the missing AllocationRule mapping or reject the command before linking. |
| Wrong scope | AllocationRule·B01 | Do not attach another church’s AllocationRule without a supported exchange and local authority. |
| Target rename | Rename AllocationRule·A01 after linking | The existing rule_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No rule_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period_id

The target is [FiscalPeriod](FiscalPeriod.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FiscalPeriod·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FiscalPeriod·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FiscalPeriod·MISSING | Queue the missing FiscalPeriod mapping or reject the command before linking. |
| Wrong scope | FiscalPeriod·B01 | Do not attach another church’s FiscalPeriod without a supported exchange and local authority. |
| Target rename | Rename FiscalPeriod·A01 after linking | The existing period_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No period_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### input_snapshot

Use scoped or external reference for `AllocationRun.input_snapshot`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified input_snapshot in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped input_snapshot | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No input_snapshot at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### pool_amount

Use exact monetary amount with currency for `AllocationRun.pool_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No pool_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_by_ref

Use scoped or external reference for `AllocationRun.approved_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approved_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approved_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No approved_by_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### posting_ref

Use scoped or external reference for `AllocationRun.posting_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified posting_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped posting_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No posting_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reverses_run_ref

Use scoped or external reference for `AllocationRun.reverses_run_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified reverses_run_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped reverses_run_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No reverses_run_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AllocationResult](AllocationResult.md).`run_id` | AllocationRun identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
