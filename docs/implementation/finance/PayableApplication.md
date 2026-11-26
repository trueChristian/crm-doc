# PayableApplication

[Purchasing, payables and reimbursements](../../finance/payables.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exactly one payment or credit source. Limit applications to unpaid balance; clear withholding through its own payable and remittance.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `disbursement_id` | → Disbursement? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `supplier_credit_id` | → SupplierCredit? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `bill_id` | → SupplierBill | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `discount_taken` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `withholding` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `applied_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### disbursement_id

The target is [Disbursement](Disbursement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Disbursement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Disbursement·MISSING | Queue the missing Disbursement mapping or reject the command before linking. |
| Wrong scope | Disbursement·B01 | Do not attach another church’s Disbursement without a supported exchange and local authority. |
| Target rename | Rename Disbursement·A01 after linking | The existing disbursement_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No disbursement_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### supplier_credit_id

The target is [SupplierCredit](SupplierCredit.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SupplierCredit·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | SupplierCredit·MISSING | Queue the missing SupplierCredit mapping or reject the command before linking. |
| Wrong scope | SupplierCredit·B01 | Do not attach another church’s SupplierCredit without a supported exchange and local authority. |
| Target rename | Rename SupplierCredit·A01 after linking | The existing supplier_credit_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No supplier_credit_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### bill_id

The target is [SupplierBill](SupplierBill.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SupplierBill·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | SupplierBill·MISSING | Queue the missing SupplierBill mapping or reject the command before linking. |
| Wrong scope | SupplierBill·B01 | Do not attach another church’s SupplierBill without a supported exchange and local authority. |
| Target rename | Rename SupplierBill·A01 after linking | The existing bill_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No bill_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount

Use exact monetary amount with currency for `PayableApplication.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### discount_taken

Use exact monetary amount with currency for `PayableApplication.discount_taken`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No discount_taken at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### withholding

Use exact monetary amount with currency for `PayableApplication.withholding`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No withholding at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### applied_on

Use civil calendar date for `PayableApplication.applied_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No applied_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
