# RefundTaxAllocation

[After-sale service and accounting](../../commerce/settlement.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One row per returned original tax component and refund allocation. Sum to the allocation’s tax amount. Cumulative credits cannot exceed the eligible original component. A later refund uses the remaining original allocation, including document-level rounding, and credits the same jurisdiction and basis.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `refund_allocation_id` | ref RefundAllocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `quote_tax_id` | ref QuoteTax | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `original_applied_component_id` | ref FinanceAppliedTaxComponent | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `credited_component_id` | ref FinanceAppliedTaxComponent? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `tax_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `taxable_basis_credited` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `residual_adjustment` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### refund_allocation_id

The target is [RefundAllocation](RefundAllocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RefundAllocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | RefundAllocation·MISSING | Queue the missing RefundAllocation mapping or reject the command before linking. |
| Wrong scope | RefundAllocation·B01 | Do not attach another church’s RefundAllocation without a supported exchange and local authority. |
| Target rename | Rename RefundAllocation·A01 after linking | The existing refund_allocation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No refund_allocation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quote_tax_id

The target is [QuoteTax](QuoteTax.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | QuoteTax·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | QuoteTax·MISSING | Queue the missing QuoteTax mapping or reject the command before linking. |
| Wrong scope | QuoteTax·B01 | Do not attach another church’s QuoteTax without a supported exchange and local authority. |
| Target rename | Rename QuoteTax·A01 after linking | The existing quote_tax_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No quote_tax_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### original_applied_component_id

The target is [FinanceAppliedTaxComponent](../finance/FinanceAppliedTaxComponent.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceAppliedTaxComponent·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FinanceAppliedTaxComponent·MISSING | Queue the missing FinanceAppliedTaxComponent mapping or reject the command before linking. |
| Wrong scope | FinanceAppliedTaxComponent·B01 | Do not attach another church’s FinanceAppliedTaxComponent without a supported exchange and local authority. |
| Target rename | Rename FinanceAppliedTaxComponent·A01 after linking | The existing original_applied_component_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No original_applied_component_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### credited_component_id

The target is [FinanceAppliedTaxComponent](../finance/FinanceAppliedTaxComponent.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceAppliedTaxComponent·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FinanceAppliedTaxComponent·MISSING | Queue the missing FinanceAppliedTaxComponent mapping or reject the command before linking. |
| Wrong scope | FinanceAppliedTaxComponent·B01 | Do not attach another church’s FinanceAppliedTaxComponent without a supported exchange and local authority. |
| Target rename | Rename FinanceAppliedTaxComponent·A01 after linking | The existing credited_component_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No credited_component_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### tax_amount

Use exact monetary amount with currency for `RefundTaxAllocation.tax_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No tax_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `RefundTaxAllocation.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### taxable_basis_credited

Use exact monetary amount with currency for `RefundTaxAllocation.taxable_basis_credited`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No taxable_basis_credited at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### residual_adjustment

Use exact monetary amount with currency for `RefundTaxAllocation.residual_adjustment`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No residual_adjustment at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
