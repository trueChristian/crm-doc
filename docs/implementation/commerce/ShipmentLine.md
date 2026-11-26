# ShipmentLine

[Counter sales and fulfilment](../../commerce/fulfilment.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Only shipped quantity issues stock. A partial dispatch leaves remaining units held, backordered or explicitly cancelled.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `shipment_id` | ref Shipment | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `fulfilment_line_id` | ref FulfilmentLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `quantity` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `movement_id` | ref StockMovement? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `serial_or_lot_id` | ref StockLot? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### shipment_id

The target is [Shipment](Shipment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Shipment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Shipment·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Shipment·MISSING | Queue the missing Shipment mapping or reject the command before linking. |
| Wrong scope | Shipment·B01 | Do not attach another church’s Shipment without a supported exchange and local authority. |
| Target rename | Rename Shipment·A01 after linking | The existing shipment_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No shipment_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fulfilment_line_id

The target is [FulfilmentLine](FulfilmentLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FulfilmentLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FulfilmentLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FulfilmentLine·MISSING | Queue the missing FulfilmentLine mapping or reject the command before linking. |
| Wrong scope | FulfilmentLine·B01 | Do not attach another church’s FulfilmentLine without a supported exchange and local authority. |
| Target rename | Rename FulfilmentLine·A01 after linking | The existing fulfilment_line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No fulfilment_line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quantity

Use exact decimal measure for `ShipmentLine.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### movement_id

The target is [StockMovement](StockMovement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockMovement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockMovement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockMovement·MISSING | Queue the missing StockMovement mapping or reject the command before linking. |
| Wrong scope | StockMovement·B01 | Do not attach another church’s StockMovement without a supported exchange and local authority. |
| Target rename | Rename StockMovement·A01 after linking | The existing movement_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No movement_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### serial_or_lot_id

The target is [StockLot](StockLot.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLot·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockLot·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockLot·MISSING | Queue the missing StockLot mapping or reject the command before linking. |
| Wrong scope | StockLot·B01 | Do not attach another church’s StockLot without a supported exchange and local authority. |
| Target rename | Rename StockLot·A01 after linking | The existing serial_or_lot_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No serial_or_lot_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
