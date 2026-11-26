# QuoteLine

[Prices, tax and delivery quotes](../../commerce/pricing.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Every line has one charge purpose. Keep the list of eligibility/pricing decisions that explain its amount.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `quote_id` | ref Quote | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `cart_line_id` | ref CartLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `component` | sale/delivery/gift | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `quantity` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `source_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `discount_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `net_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `tax_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `gross_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `promotion_ids` | set of ref Promotion | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### quote_id

The target is [Quote](Quote.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Quote·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Quote·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Quote·MISSING | Queue the missing Quote mapping or reject the command before linking. |
| Wrong scope | Quote·B01 | Do not attach another church’s Quote without a supported exchange and local authority. |
| Target rename | Rename Quote·A01 after linking | The existing quote_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No quote_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cart_line_id

The target is [CartLine](CartLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CartLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CartLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CartLine·MISSING | Queue the missing CartLine mapping or reject the command before linking. |
| Wrong scope | CartLine·B01 | Do not attach another church’s CartLine without a supported exchange and local authority. |
| Target rename | Rename CartLine·A01 after linking | The existing cart_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No cart_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### component

Declared alternatives in owner order: `sale`, `delivery`, `gift`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | sale | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_component | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No component at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quantity

Use exact decimal measure for `QuoteLine.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_amount

Use exact monetary amount with currency for `QuoteLine.source_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No source_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### discount_amount

Use exact monetary amount with currency for `QuoteLine.discount_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No discount_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### net_amount

Use exact monetary amount with currency for `QuoteLine.net_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No net_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_amount

Use exact monetary amount with currency for `QuoteLine.tax_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No tax_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### gross_amount

Use exact monetary amount with currency for `QuoteLine.gross_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No gross_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### promotion_ids

The target is [Promotion](Promotion.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Promotion·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Promotion·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Promotion·MISSING | Queue the missing Promotion mapping or reject the command before linking. |
| Wrong scope | Promotion·B01 | Do not attach another church’s Promotion without a supported exchange and local authority. |
| Target rename | Rename Promotion·A01 after linking | The existing promotion_ids keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No promotion_ids at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [OrderLine](OrderLine.md).`quote_line_id` | QuoteLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [QuoteTax](QuoteTax.md).`quote_line_id` | QuoteLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SalesTaxSelection](SalesTaxSelection.md).`quote_line_id` | QuoteLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
