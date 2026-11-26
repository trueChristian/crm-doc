# JournalLine

[Books, dimensions and double entry](../../finance/ledger.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique entry/sequence. Exactly one positive base amount per line, other side zero. Express direction by debit/credit and use a positive transaction amount. Zero-original/base-only rounding or valuation lines require a dedicated posting purpose.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `entry_id` | → JournalEntry | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sequence` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `account_id` | → LedgerAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `fund_id` | → Fund | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `debit_base` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `credit_base` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `transaction_currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `transaction_amount` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `fx_rate` | decimal | Required when the record reaches its applicable state | [ratio](../value-conventions.md#ratio) |
| `memo` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `due_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `counterparty_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `reconciliation_key` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### entry_id

The target is [JournalEntry](JournalEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | JournalEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | JournalEntry·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | JournalEntry·MISSING | Queue the missing JournalEntry mapping or reject the command before linking. |
| Wrong scope | JournalEntry·B01 | Do not attach another church’s JournalEntry without a supported exchange and local authority. |
| Target rename | Rename JournalEntry·A01 after linking | The existing entry_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No entry_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sequence

Use whole-number measure for `JournalLine.sequence`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No sequence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### account_id

The target is [LedgerAccount](LedgerAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LedgerAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | LedgerAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | LedgerAccount·MISSING | Queue the missing LedgerAccount mapping or reject the command before linking. |
| Wrong scope | LedgerAccount·B01 | Do not attach another church’s LedgerAccount without a supported exchange and local authority. |
| Target rename | Rename LedgerAccount·A01 after linking | The existing account_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No account_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fund_id

The target is [Fund](Fund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Fund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Fund·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Fund·MISSING | Queue the missing Fund mapping or reject the command before linking. |
| Wrong scope | Fund·B01 | Do not attach another church’s Fund without a supported exchange and local authority. |
| Target rename | Rename Fund·A01 after linking | The existing fund_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No fund_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### debit_base

Use exact decimal measure for `JournalLine.debit_base`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No debit_base at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### credit_base

Use exact decimal measure for `JournalLine.credit_base`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No credit_base at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### transaction_currency

Use monetary unit code for `JournalLine.transaction_currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No transaction_currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### transaction_amount

Use exact decimal measure for `JournalLine.transaction_amount`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No transaction_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fx_rate

Use exact ratio, rate or weighting for `JournalLine.fx_rate`. Carry the declared unit, direction and calculation precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 1.125 under named rate basis | Carry the declared unit, direction and calculation precision. |
| Malformed or unmapped | rate with unknown direction | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | 0.125 fraction and 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | reciprocal quoted in opposite currency direction | Require explicit direction and an approved conversion. |
| Financial document already issued | historical line after a rate-table correction | Retain the original rate, effective date and rounding basis. |
| Incomplete record | No fx_rate at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### memo

Use human-readable text for `JournalLine.memo`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered memo in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No memo provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_on

Use civil calendar date for `JournalLine.due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No due_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### counterparty_ref

Use scoped or external reference for `JournalLine.counterparty_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified counterparty_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped counterparty_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No counterparty_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reconciliation_key

Use human-readable text for `JournalLine.reconciliation_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered reconciliation_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No reconciliation_key provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AwardCost](AwardCost.md).`journal_line_id` | JournalLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BankMatchPart](BankMatchPart.md).`journal_line_id` | JournalLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [JournalLineDimension](JournalLineDimension.md).`line_id` | JournalLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OpeningJournalMap](OpeningJournalMap.md).`journal_line_ref` | JournalLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
