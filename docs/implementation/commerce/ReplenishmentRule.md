# ReplenishmentRule

[Inventory and custody](../../commerce/inventory.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Generate a reviewable purchase request using available stock, committed supply and demand. Unique open suggestion per rule and planning cycle.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `location_id` | ref StockLocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `variant_id` | ref ProductVariant | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `reorder_at` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `target` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `supplier_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `lead_time_days` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `order_multiple` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### location_id

The target is [StockLocation](StockLocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | StockLocation·MISSING | Queue the missing StockLocation mapping or reject the command before linking. |
| Wrong scope | StockLocation·B01 | Do not attach another church’s StockLocation without a supported exchange and local authority. |
| Target rename | Rename StockLocation·A01 after linking | The existing location_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No location_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### variant_id

The target is [ProductVariant](ProductVariant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProductVariant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ProductVariant·MISSING | Queue the missing ProductVariant mapping or reject the command before linking. |
| Wrong scope | ProductVariant·B01 | Do not attach another church’s ProductVariant without a supported exchange and local authority. |
| Target rename | Rename ProductVariant·A01 after linking | The existing variant_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No variant_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reorder_at

Use exact decimal measure for `ReplenishmentRule.reorder_at`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No reorder_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### target

Use exact decimal measure for `ReplenishmentRule.target`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No target at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### supplier_ref

Use scoped or external reference for `ReplenishmentRule.supplier_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified supplier_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped supplier_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No supplier_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### lead_time_days

Use whole-number measure for `ReplenishmentRule.lead_time_days`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No lead_time_days at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### order_multiple

Use exact decimal measure for `ReplenishmentRule.order_multiple`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No order_multiple at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
