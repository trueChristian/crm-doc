# OpeningItem

[Financial onboarding, cutover and handover](../../finance/cutover.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique migration/kind/legacy_id. Types include signed account balance, bill, invoice, pledge, grant balance, deposit/cheque in transit, asset, inventory layer, payroll/tax liability and deferred contract.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `migration_id` | → FinanceMigration | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `legacy_id` | text | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `parent_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `event_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `due_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `original_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `outstanding_amount` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `ledger_account_ref` | → LedgerAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `fund_ref` | → Fund | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `dimension_set` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `external_evidence` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `target_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `validation_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### migration_id

The target is [FinanceMigration](FinanceMigration.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceMigration·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FinanceMigration·MISSING | Queue the missing FinanceMigration mapping or reject the command before linking. |
| Wrong scope | FinanceMigration·B01 | Do not attach another church’s FinanceMigration without a supported exchange and local authority. |
| Target rename | Rename FinanceMigration·A01 after linking | The existing migration_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No migration_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Use versioned classification or status code for `OpeningItem.kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### legacy_id

Use scoped or external reference for `OpeningItem.legacy_id`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified legacy_id in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped legacy_id | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No legacy_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_ref

Use scoped or external reference for `OpeningItem.parent_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified parent_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped parent_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No parent_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### event_on

Use civil calendar date for `OpeningItem.event_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No event_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### due_on

Use civil calendar date for `OpeningItem.due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No due_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### original_amount

Use exact monetary amount with currency for `OpeningItem.original_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No original_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### outstanding_amount

Use exact monetary amount with currency for `OpeningItem.outstanding_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No outstanding_amount provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### ledger_account_ref

The target is [LedgerAccount](LedgerAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LedgerAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | LedgerAccount·MISSING | Queue the missing LedgerAccount mapping or reject the command before linking. |
| Wrong scope | LedgerAccount·B01 | Do not attach another church’s LedgerAccount without a supported exchange and local authority. |
| Target rename | Rename LedgerAccount·A01 after linking | The existing ledger_account_ref keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No ledger_account_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fund_ref

The target is [Fund](Fund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Fund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Fund·MISSING | Queue the missing Fund mapping or reject the command before linking. |
| Wrong scope | Fund·B01 | Do not attach another church’s Fund without a supported exchange and local authority. |
| Target rename | Rename Fund·A01 after linking | The existing fund_ref keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No fund_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### dimension_set

Use ordered collection or mathematical set for `OpeningItem.dimension_set`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No dimension_set at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### external_evidence

Use scoped or external reference for `OpeningItem.external_evidence`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified external_evidence in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped external_evidence | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No external_evidence provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### target_ref

Use scoped or external reference for `OpeningItem.target_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified target_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped target_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No target_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### validation_state

Use versioned classification or status code for `OpeningItem.validation_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active validation_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped validation_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No validation_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [OpeningJournalMap](OpeningJournalMap.md).`item_id` | OpeningItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
