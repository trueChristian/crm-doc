# PaySlipLine

[Payroll, stipends and remittances](../../finance/payroll.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Fund and functional distributions must sum to the row totals. Keep employer costs, noncash benefits and employee deductions separate.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `slip_id` | → PaySlip | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `component_rule_id` | → PayComponentRule | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `source_input_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `units` | decimal? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `rate` | decimal? | Optional under owner conditions | [ratio](../value-conventions.md#ratio) |
| `basis` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `fund_id` | → Fund | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `cost_dimension_ref` | → FinanceDimension? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `year_to_date` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### slip_id

The target is [PaySlip](PaySlip.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PaySlip·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | PaySlip·MISSING | Queue the missing PaySlip mapping or reject the command before linking. |
| Wrong scope | PaySlip·B01 | Do not attach another church’s PaySlip without a supported exchange and local authority. |
| Target rename | Rename PaySlip·A01 after linking | The existing slip_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No slip_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### component_rule_id

The target is [PayComponentRule](PayComponentRule.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PayComponentRule·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | PayComponentRule·MISSING | Queue the missing PayComponentRule mapping or reject the command before linking. |
| Wrong scope | PayComponentRule·B01 | Do not attach another church’s PayComponentRule without a supported exchange and local authority. |
| Target rename | Rename PayComponentRule·A01 after linking | The existing component_rule_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No component_rule_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_input_ref

Use scoped or external reference for `PaySlipLine.source_input_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified source_input_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped source_input_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No source_input_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### units

Use exact decimal measure for `PaySlipLine.units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No units provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### rate

Use exact ratio, rate or weighting for `PaySlipLine.rate`. Carry the declared unit, direction and calculation precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 1.125 under named rate basis | Carry the declared unit, direction and calculation precision. |
| Malformed or unmapped | rate with unknown direction | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | 0.125 fraction and 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | reciprocal quoted in opposite currency direction | Require explicit direction and an approved conversion. |
| Financial document already issued | historical line after a rate-table correction | Retain the original rate, effective date and rounding basis. |
| Absent in intake | No rate provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### basis

Use exact monetary amount with currency for `PaySlipLine.basis`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount

Use exact monetary amount with currency for `PaySlipLine.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fund_id

The target is [Fund](Fund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Fund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Fund·MISSING | Queue the missing Fund mapping or reject the command before linking. |
| Wrong scope | Fund·B01 | Do not attach another church’s Fund without a supported exchange and local authority. |
| Target rename | Rename Fund·A01 after linking | The existing fund_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No fund_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cost_dimension_ref

The target is [FinanceDimension](FinanceDimension.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceDimension·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FinanceDimension·MISSING | Queue the missing FinanceDimension mapping or reject the command before linking. |
| Wrong scope | FinanceDimension·B01 | Do not attach another church’s FinanceDimension without a supported exchange and local authority. |
| Target rename | Rename FinanceDimension·A01 after linking | The existing cost_dimension_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No cost_dimension_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### year_to_date

Use exact monetary amount with currency for `PaySlipLine.year_to_date`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No year_to_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PayRemittancePart](PayRemittancePart.md).`slip_line_id` | PaySlipLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
