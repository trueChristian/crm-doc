# PaySlip

[Payroll, stipends and remittances](../../finance/payroll.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique run/engagement; run can pay many workers. A worker sees only their own released slip. Independent access for payroll auditor.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `run_id` | → PayrollRun | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `engagement_id` | → PayrollEngagement | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `gross` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `taxable_base` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `employee_deductions` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `net_cash` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `employer_cost` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `statement_evidence` | ? | Optional under owner conditions | [structured](../value-conventions.md#structured) |
| `payment_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `statement_status` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### run_id

The target is [PayrollRun](PayrollRun.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PayrollRun·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PayrollRun·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PayrollRun·MISSING | Queue the missing PayrollRun mapping or reject the command before linking. |
| Wrong scope | PayrollRun·B01 | Do not attach another church’s PayrollRun without a supported exchange and local authority. |
| Target rename | Rename PayrollRun·A01 after linking | The existing run_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No run_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### engagement_id

The target is [PayrollEngagement](PayrollEngagement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PayrollEngagement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PayrollEngagement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PayrollEngagement·MISSING | Queue the missing PayrollEngagement mapping or reject the command before linking. |
| Wrong scope | PayrollEngagement·B01 | Do not attach another church’s PayrollEngagement without a supported exchange and local authority. |
| Target rename | Rename PayrollEngagement·A01 after linking | The existing engagement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No engagement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### gross

Use exact monetary amount with currency for `PaySlip.gross`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No gross at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### taxable_base

Use exact monetary amount with currency for `PaySlip.taxable_base`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No taxable_base at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### employee_deductions

Use exact monetary amount with currency for `PaySlip.employee_deductions`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No employee_deductions at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### net_cash

Use exact monetary amount with currency for `PaySlip.net_cash`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No net_cash at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### employer_cost

Use exact monetary amount with currency for `PaySlip.employer_cost`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No employer_cost at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### statement_evidence

Use typed value or bounded compound record for `PaySlip.statement_evidence`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of statement_evidence matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for statement_evidence | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Absent in intake | No statement_evidence provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### payment_ref

Use scoped or external reference for `PaySlip.payment_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified payment_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped payment_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No payment_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### statement_status

Use versioned classification or status code for `PaySlip.statement_status`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active statement_status code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped statement_status code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No statement_status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PaySlipLine](PaySlipLine.md).`slip_id` | PaySlip identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
