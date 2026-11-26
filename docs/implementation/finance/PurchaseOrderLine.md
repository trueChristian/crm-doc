# PurchaseOrderLine

[Purchasing, payables and reimbursements](../../finance/payables.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Prevent orders above approved authority. Substitutions, change orders and price variance need recorded tolerances or overrides.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `order_id` | → PurchaseOrder | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `request_line_id` | → PurchaseRequestLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `unit_price` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `tax_code_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `fund_id` | → Fund | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `account_id` | → LedgerAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `dimension_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### order_id

The target is [PurchaseOrder](PurchaseOrder.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PurchaseOrder·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | PurchaseOrder·MISSING | Queue the missing PurchaseOrder mapping or reject the command before linking. |
| Wrong scope | PurchaseOrder·B01 | Do not attach another church’s PurchaseOrder without a supported exchange and local authority. |
| Target rename | Rename PurchaseOrder·A01 after linking | The existing order_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No order_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### request_line_id

The target is [PurchaseRequestLine](PurchaseRequestLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PurchaseRequestLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | PurchaseRequestLine·MISSING | Queue the missing PurchaseRequestLine mapping or reject the command before linking. |
| Wrong scope | PurchaseRequestLine·B01 | Do not attach another church’s PurchaseRequestLine without a supported exchange and local authority. |
| Target rename | Rename PurchaseRequestLine·A01 after linking | The existing request_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No request_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### quantity

Use exact decimal measure for `PurchaseOrderLine.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit_price

Use exact decimal measure for `PurchaseOrderLine.unit_price`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No unit_price at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_code_ref

Use scoped or external reference for `PurchaseOrderLine.tax_code_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified tax_code_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped tax_code_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No tax_code_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### fund_id

The target is [Fund](Fund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Fund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Fund·MISSING | Queue the missing Fund mapping or reject the command before linking. |
| Wrong scope | Fund·B01 | Do not attach another church’s Fund without a supported exchange and local authority. |
| Target rename | Rename Fund·A01 after linking | The existing fund_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No fund_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### account_id

The target is [LedgerAccount](LedgerAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LedgerAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | LedgerAccount·MISSING | Queue the missing LedgerAccount mapping or reject the command before linking. |
| Wrong scope | LedgerAccount·B01 | Do not attach another church’s LedgerAccount without a supported exchange and local authority. |
| Target rename | Rename LedgerAccount·A01 after linking | The existing account_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No account_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### dimension_ref

Use scoped or external reference for `PurchaseOrderLine.dimension_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified dimension_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped dimension_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No dimension_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [GoodsReceiptLine](GoodsReceiptLine.md).`order_line_id` | PurchaseOrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupplierBillLine](SupplierBillLine.md).`order_line_id` | PurchaseOrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
