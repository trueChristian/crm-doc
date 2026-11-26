# CountLine

[Inventory and custody](../../commerce/inventory.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique count key per session. Count zero is an observation, missing is uncounted. A posting creates a movement only for the approved variance.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `session_id` | ref CountSession | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `variant_id` | ref ProductVariant | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `lot_id` | ref StockLot? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `expected` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `counted` | quantity? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `recounted` | quantity? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `reason` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `movement_id` | ref StockMovement? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### session_id

The target is [CountSession](CountSession.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CountSession·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CountSession·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CountSession·MISSING | Queue the missing CountSession mapping or reject the command before linking. |
| Wrong scope | CountSession·B01 | Do not attach another church’s CountSession without a supported exchange and local authority. |
| Target rename | Rename CountSession·A01 after linking | The existing session_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No session_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### variant_id

The target is [ProductVariant](ProductVariant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProductVariant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProductVariant·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProductVariant·MISSING | Queue the missing ProductVariant mapping or reject the command before linking. |
| Wrong scope | ProductVariant·B01 | Do not attach another church’s ProductVariant without a supported exchange and local authority. |
| Target rename | Rename ProductVariant·A01 after linking | The existing variant_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No variant_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### lot_id

The target is [StockLot](StockLot.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLot·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockLot·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockLot·MISSING | Queue the missing StockLot mapping or reject the command before linking. |
| Wrong scope | StockLot·B01 | Do not attach another church’s StockLot without a supported exchange and local authority. |
| Target rename | Rename StockLot·A01 after linking | The existing lot_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No lot_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### expected

Use exact decimal measure for `CountLine.expected`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No expected at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### counted

Use exact decimal measure for `CountLine.counted`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No counted provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recounted

Use exact decimal measure for `CountLine.recounted`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No recounted provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason

Use versioned classification or status code for `CountLine.reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

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

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
