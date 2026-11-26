# StockCostApplication

[Inventory accounting and stock valuation](../../finance/inventory-accounting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Applied quantity and cost cannot exceed available amount. A final fractional residual consumes the exact remaining layer value. Retain record of the original basis for returns.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `outgoing_id` | → InventoryValuationEvent | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `layer_id` | → StockCostLayer | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `assigned_cost` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `correction_of_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### outgoing_id

The target is [InventoryValuationEvent](InventoryValuationEvent.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | InventoryValuationEvent·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | InventoryValuationEvent·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | InventoryValuationEvent·MISSING | Queue the missing InventoryValuationEvent mapping or reject the command before linking. |
| Wrong scope | InventoryValuationEvent·B01 | Do not attach another church’s InventoryValuationEvent without a supported exchange and local authority. |
| Target rename | Rename InventoryValuationEvent·A01 after linking | The existing outgoing_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No outgoing_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### layer_id

The target is [StockCostLayer](StockCostLayer.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockCostLayer·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockCostLayer·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockCostLayer·MISSING | Queue the missing StockCostLayer mapping or reject the command before linking. |
| Wrong scope | StockCostLayer·B01 | Do not attach another church’s StockCostLayer without a supported exchange and local authority. |
| Target rename | Rename StockCostLayer·A01 after linking | The existing layer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No layer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quantity

Use exact decimal measure for `StockCostApplication.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assigned_cost

Use exact monetary amount with currency for `StockCostApplication.assigned_cost`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No assigned_cost at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### correction_of_ref

Use scoped or external reference for `StockCostApplication.correction_of_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified correction_of_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped correction_of_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No correction_of_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
