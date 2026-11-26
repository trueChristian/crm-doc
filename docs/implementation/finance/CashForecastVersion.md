# CashForecastVersion

[Budgeting, cost allocation and cash forecasting](../../finance/planning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Keep restricted, committed and available liquidity distinct. Cash date can differ from expense or revenue date.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `book_id` | → FinanceBook | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `as_of` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `horizon_end` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `interval` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `scenario` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `opening_available_cash` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `assumptions` | evidence | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `prepared_by_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### book_id

The target is [FinanceBook](FinanceBook.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceBook·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FinanceBook·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FinanceBook·MISSING | Queue the missing FinanceBook mapping or reject the command before linking. |
| Wrong scope | FinanceBook·B01 | Do not attach another church’s FinanceBook without a supported exchange and local authority. |
| Target rename | Rename FinanceBook·A01 after linking | The existing book_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No book_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### as_of

Use civil calendar date for `CashForecastVersion.as_of`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No as_of at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### horizon_end

Use civil calendar date for `CashForecastVersion.horizon_end`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No horizon_end at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### interval

Use versioned classification or status code for `CashForecastVersion.interval`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active interval code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped interval code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No interval at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scenario

Use versioned classification or status code for `CashForecastVersion.scenario`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active scenario code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped scenario code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No scenario at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### opening_available_cash

Use exact monetary amount with currency for `CashForecastVersion.opening_available_cash`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No opening_available_cash at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assumptions

Use scoped or external reference for `CashForecastVersion.assumptions`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified assumptions in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped assumptions | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No assumptions at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prepared_by_ref

Use scoped or external reference for `CashForecastVersion.prepared_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified prepared_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped prepared_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No prepared_by_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CashForecastFlow](CashForecastFlow.md).`version_id` | CashForecastVersion identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
