# ProductCategory

[Catalogue and offers](../../commerce/catalogue.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique pair. Category membership never widens visibility.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `product_id` | ref Product | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `category_id` | ref Category | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `display_order` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### product_id

The target is [Product](Product.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Product·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Product·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Product·MISSING | Queue the missing Product mapping or reject the command before linking. |
| Wrong scope | Product·B01 | Do not attach another church’s Product without a supported exchange and local authority. |
| Target rename | Rename Product·A01 after linking | The existing product_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No product_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### category_id

The target is [Category](Category.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Category·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Category·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Category·MISSING | Queue the missing Category mapping or reject the command before linking. |
| Wrong scope | Category·B01 | Do not attach another church’s Category without a supported exchange and local authority. |
| Target rename | Rename Category·A01 after linking | The existing category_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No category_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### display_order

Use whole-number measure for `ProductCategory.display_order`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No display_order at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
