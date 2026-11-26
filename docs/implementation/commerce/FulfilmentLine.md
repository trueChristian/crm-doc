# FulfilmentLine

[Counter sales and fulfilment](../../commerce/fulfilment.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Across groups, total allocated cannot exceed ordered units less unallocated cancellations. Capture each entitlement or service completion separately from physical inventory.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `group_id` | ref FulfilmentGroup | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `order_line_id` | ref OrderLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `allocated_units` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `completed_units` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `cancelled_units` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `stock_reservation_id` | ref StockReservation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `access_grant_id` | ref AccessGrant? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `service_delivery_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### group_id

The target is [FulfilmentGroup](FulfilmentGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FulfilmentGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FulfilmentGroup·MISSING | Queue the missing FulfilmentGroup mapping or reject the command before linking. |
| Wrong scope | FulfilmentGroup·B01 | Do not attach another church’s FulfilmentGroup without a supported exchange and local authority. |
| Target rename | Rename FulfilmentGroup·A01 after linking | The existing group_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No group_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### order_line_id

The target is [OrderLine](OrderLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OrderLine·MISSING | Queue the missing OrderLine mapping or reject the command before linking. |
| Wrong scope | OrderLine·B01 | Do not attach another church’s OrderLine without a supported exchange and local authority. |
| Target rename | Rename OrderLine·A01 after linking | The existing order_line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No order_line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allocated_units

Use exact decimal measure for `FulfilmentLine.allocated_units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No allocated_units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### completed_units

Use exact decimal measure for `FulfilmentLine.completed_units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No completed_units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cancelled_units

Use exact decimal measure for `FulfilmentLine.cancelled_units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No cancelled_units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### stock_reservation_id

The target is [StockReservation](StockReservation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockReservation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | StockReservation·MISSING | Queue the missing StockReservation mapping or reject the command before linking. |
| Wrong scope | StockReservation·B01 | Do not attach another church’s StockReservation without a supported exchange and local authority. |
| Target rename | Rename StockReservation·A01 after linking | The existing stock_reservation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No stock_reservation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### access_grant_id

The target is [AccessGrant](AccessGrant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessGrant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AccessGrant·MISSING | Queue the missing AccessGrant mapping or reject the command before linking. |
| Wrong scope | AccessGrant·B01 | Do not attach another church’s AccessGrant without a supported exchange and local authority. |
| Target rename | Rename AccessGrant·A01 after linking | The existing access_grant_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No access_grant_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### service_delivery_ref

Use scoped or external reference for `FulfilmentLine.service_delivery_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified service_delivery_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped service_delivery_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No service_delivery_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [ShipmentLine](ShipmentLine.md).`fulfilment_line_id` | FulfilmentLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
