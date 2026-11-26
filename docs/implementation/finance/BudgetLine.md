# BudgetLine

[Budgeting, cost allocation and cash forecasting](../../finance/planning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique planning grain or explicit line identity for separate initiatives. Monthly splits sum to annual amount; use explicit residual allocation.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `version_id` | → BudgetVersion | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `period_id` | → FiscalPeriod | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `account_id` | → LedgerAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `fund_id` | → Fund | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `dimension_set` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `quantity` | decimal? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `unit_cost` | decimal? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `phasing_method` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `assumption_note` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `owner_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### version_id

The target is [BudgetVersion](BudgetVersion.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | BudgetVersion·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | BudgetVersion·MISSING | Queue the missing BudgetVersion mapping or reject the command before linking. |
| Wrong scope | BudgetVersion·B01 | Do not attach another church’s BudgetVersion without a supported exchange and local authority. |
| Target rename | Rename BudgetVersion·A01 after linking | The existing version_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No version_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period_id

The target is [FiscalPeriod](FiscalPeriod.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FiscalPeriod·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FiscalPeriod·MISSING | Queue the missing FiscalPeriod mapping or reject the command before linking. |
| Wrong scope | FiscalPeriod·B01 | Do not attach another church’s FiscalPeriod without a supported exchange and local authority. |
| Target rename | Rename FiscalPeriod·A01 after linking | The existing period_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No period_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### dimension_set

Use ordered collection or mathematical set for `BudgetLine.dimension_set`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No dimension_set at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quantity

Use exact decimal measure for `BudgetLine.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No quantity provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### unit_cost

Use exact decimal measure for `BudgetLine.unit_cost`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No unit_cost provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### amount

Use exact monetary amount with currency for `BudgetLine.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### phasing_method

Use versioned classification or status code for `BudgetLine.phasing_method`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active phasing_method code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped phasing_method code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No phasing_method provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### assumption_note

Use human-readable text for `BudgetLine.assumption_note`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered assumption_note in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No assumption_note provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### owner_ref

Use scoped or external reference for `BudgetLine.owner_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified owner_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped owner_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No owner_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [ProposalBudgetLine](../development/ProposalBudgetLine.md).`finance_budget_line_id` | BudgetLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
