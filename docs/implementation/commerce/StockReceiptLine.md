# StockReceiptLine

[Inventory and custody](../../commerce/inventory.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Arrived equals accepted plus quarantined plus refused. One purchase line may have many receipt lines. Match accepted units, agreed price and supplier invoice before payment according to finance policy.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `receipt_id` | ref StockReceipt | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `purchase_line_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `variant_id` | ref ProductVariant | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `lot_id` | ref StockLot? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `expected_quantity` | quantity? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `arrived_quantity` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `accepted_quantity` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `quarantined_quantity` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `refused_quantity` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `discrepancy_reason` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### receipt_id

The target is [StockReceipt](StockReceipt.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockReceipt·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | StockReceipt·MISSING | Queue the missing StockReceipt mapping or reject the command before linking. |
| Wrong scope | StockReceipt·B01 | Do not attach another church’s StockReceipt without a supported exchange and local authority. |
| Target rename | Rename StockReceipt·A01 after linking | The existing receipt_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No receipt_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purchase_line_ref

Use scoped or external reference for `StockReceiptLine.purchase_line_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified purchase_line_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped purchase_line_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No purchase_line_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

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

### lot_id

The target is [StockLot](StockLot.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLot·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | StockLot·MISSING | Queue the missing StockLot mapping or reject the command before linking. |
| Wrong scope | StockLot·B01 | Do not attach another church’s StockLot without a supported exchange and local authority. |
| Target rename | Rename StockLot·A01 after linking | The existing lot_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No lot_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### expected_quantity

Use exact decimal measure for `StockReceiptLine.expected_quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No expected_quantity provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### arrived_quantity

Use exact decimal measure for `StockReceiptLine.arrived_quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No arrived_quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### accepted_quantity

Use exact decimal measure for `StockReceiptLine.accepted_quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No accepted_quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quarantined_quantity

Use exact decimal measure for `StockReceiptLine.quarantined_quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quarantined_quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### refused_quantity

Use exact decimal measure for `StockReceiptLine.refused_quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No refused_quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### discrepancy_reason

Use versioned classification or status code for `StockReceiptLine.discrepancy_reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active discrepancy_reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped discrepancy_reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No discrepancy_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
