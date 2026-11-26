# BillingAllocation

[Counter sales and fulfilment](../../commerce/fulfilment.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Match posted items to the frozen sale and tax snapshot. Deposit recognition and unearned revenue must follow the posting policy.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `sales_document_link_id` | ref SalesDocumentLink | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `order_line_id` | ref OrderLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `units` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `net` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `tax` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `gross` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### sales_document_link_id

The target is [SalesDocumentLink](SalesDocumentLink.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SalesDocumentLink·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SalesDocumentLink·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SalesDocumentLink·MISSING | Queue the missing SalesDocumentLink mapping or reject the command before linking. |
| Wrong scope | SalesDocumentLink·B01 | Do not attach another church’s SalesDocumentLink without a supported exchange and local authority. |
| Target rename | Rename SalesDocumentLink·A01 after linking | The existing sales_document_link_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No sales_document_link_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### order_line_id

The target is [OrderLine](OrderLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderLine·MISSING | Queue the missing OrderLine mapping or reject the command before linking. |
| Wrong scope | OrderLine·B01 | Do not attach another church’s OrderLine without a supported exchange and local authority. |
| Target rename | Rename OrderLine·A01 after linking | The existing order_line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No order_line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### units

Use exact decimal measure for `BillingAllocation.units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### net

Use exact monetary amount with currency for `BillingAllocation.net`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No net at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax

Use exact monetary amount with currency for `BillingAllocation.tax`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No tax at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### gross

Use exact monetary amount with currency for `BillingAllocation.gross`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No gross at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
