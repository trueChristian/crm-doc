# FxValuationItem

[Banking, cash and currencies](../../finance/treasury.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Include eligible monetary open items and accounts. Historical cost and other measurement classes follow their own approved basis.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `run_id` | → FxValuationRun | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `item_source` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `ledger_account_id` | → LedgerAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `foreign_balance` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `prior_base` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `rate_id` | → CurrencyRate | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `revalued_base` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `adjustment_signed` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### run_id

The target is [FxValuationRun](FxValuationRun.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FxValuationRun·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FxValuationRun·MISSING | Queue the missing FxValuationRun mapping or reject the command before linking. |
| Wrong scope | FxValuationRun·B01 | Do not attach another church’s FxValuationRun without a supported exchange and local authority. |
| Target rename | Rename FxValuationRun·A01 after linking | The existing run_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No run_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### item_source

Use scoped or external reference for `FxValuationItem.item_source`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified item_source in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped item_source | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No item_source at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ledger_account_id

The target is [LedgerAccount](LedgerAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LedgerAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | LedgerAccount·MISSING | Queue the missing LedgerAccount mapping or reject the command before linking. |
| Wrong scope | LedgerAccount·B01 | Do not attach another church’s LedgerAccount without a supported exchange and local authority. |
| Target rename | Rename LedgerAccount·A01 after linking | The existing ledger_account_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No ledger_account_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### foreign_balance

Use exact decimal measure for `FxValuationItem.foreign_balance`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No foreign_balance at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prior_base

Use exact decimal measure for `FxValuationItem.prior_base`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No prior_base at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rate_id

The target is [CurrencyRate](CurrencyRate.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CurrencyRate·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | CurrencyRate·MISSING | Queue the missing CurrencyRate mapping or reject the command before linking. |
| Wrong scope | CurrencyRate·B01 | Do not attach another church’s CurrencyRate without a supported exchange and local authority. |
| Target rename | Rename CurrencyRate·A01 after linking | The existing rate_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No rate_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revalued_base

Use exact decimal measure for `FxValuationItem.revalued_base`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No revalued_base at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### adjustment_signed

Use exact decimal measure for `FxValuationItem.adjustment_signed`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No adjustment_signed at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
