# JournalLineDimension

[Books, dimensions and double entry](../../finance/ledger.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique line/dimension kind where that kind is single-valued. Split lines for multi-ministry amounts.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `line_id` | → JournalLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `dimension_id` | → FinanceDimension | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### line_id

The target is [JournalLine](JournalLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | JournalLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | JournalLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | JournalLine·MISSING | Queue the missing JournalLine mapping or reject the command before linking. |
| Wrong scope | JournalLine·B01 | Do not attach another church’s JournalLine without a supported exchange and local authority. |
| Target rename | Rename JournalLine·A01 after linking | The existing line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### dimension_id

The target is [FinanceDimension](FinanceDimension.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceDimension·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FinanceDimension·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FinanceDimension·MISSING | Queue the missing FinanceDimension mapping or reject the command before linking. |
| Wrong scope | FinanceDimension·B01 | Do not attach another church’s FinanceDimension without a supported exchange and local authority. |
| Target rename | Rename FinanceDimension·A01 after linking | The existing dimension_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No dimension_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
