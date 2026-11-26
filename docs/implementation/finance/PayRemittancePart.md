# PayRemittancePart

[Payroll, stipends and remittances](../../finance/payroll.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Prevent a slip-line liability being discharged twice. Report outstanding balance by authority and due date.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `remittance_id` | → PayRemittance | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `slip_line_id` | → PaySlipLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### remittance_id

The target is [PayRemittance](PayRemittance.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PayRemittance·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PayRemittance·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PayRemittance·MISSING | Queue the missing PayRemittance mapping or reject the command before linking. |
| Wrong scope | PayRemittance·B01 | Do not attach another church’s PayRemittance without a supported exchange and local authority. |
| Target rename | Rename PayRemittance·A01 after linking | The existing remittance_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No remittance_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### slip_line_id

The target is [PaySlipLine](PaySlipLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PaySlipLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PaySlipLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PaySlipLine·MISSING | Queue the missing PaySlipLine mapping or reject the command before linking. |
| Wrong scope | PaySlipLine·B01 | Do not attach another church’s PaySlipLine without a supported exchange and local authority. |
| Target rename | Rename PaySlipLine·A01 after linking | The existing slip_line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No slip_line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount

Use exact monetary amount with currency for `PayRemittancePart.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
