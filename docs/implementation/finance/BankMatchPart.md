# BankMatchPart

[Banking, cash and currencies](../../finance/treasury.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exactly one source per part, at least one from each side per match. Prevent two accepted matches consuming the same portion.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `match_id` | → BankMatch | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `statement_line_id` | → BankStatementLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `journal_line_id` | → JournalLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `amount_signed` | signed_money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### match_id

The target is [BankMatch](BankMatch.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | BankMatch·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | BankMatch·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | BankMatch·MISSING | Queue the missing BankMatch mapping or reject the command before linking. |
| Wrong scope | BankMatch·B01 | Do not attach another church’s BankMatch without a supported exchange and local authority. |
| Target rename | Rename BankMatch·A01 after linking | The existing match_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No match_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### statement_line_id

The target is [BankStatementLine](BankStatementLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | BankStatementLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | BankStatementLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | BankStatementLine·MISSING | Queue the missing BankStatementLine mapping or reject the command before linking. |
| Wrong scope | BankStatementLine·B01 | Do not attach another church’s BankStatementLine without a supported exchange and local authority. |
| Target rename | Rename BankStatementLine·A01 after linking | The existing statement_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No statement_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### journal_line_id

The target is [JournalLine](JournalLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | JournalLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | JournalLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | JournalLine·MISSING | Queue the missing JournalLine mapping or reject the command before linking. |
| Wrong scope | JournalLine·B01 | Do not attach another church’s JournalLine without a supported exchange and local authority. |
| Target rename | Rename JournalLine·A01 after linking | The existing journal_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No journal_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### amount_signed

Use exact monetary amount with currency for `BankMatchPart.amount_signed`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount_signed at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
