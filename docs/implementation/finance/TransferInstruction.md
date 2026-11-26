# TransferInstruction

[Banking, cash and currencies](../../finance/treasury.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Link both legs, including partial settlement, timing differences and bank fees. Do not double-count internal cash movements in consolidated cash flows.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `source_account_id` | → TreasuryAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `destination_account_id` | → TreasuryAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `instructed_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `sent_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `received_amount` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `rate_id` | → CurrencyRate? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `fee` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `source_settlement_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `destination_settlement_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `status` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### source_account_id

The target is [TreasuryAccount](TreasuryAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TreasuryAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | TreasuryAccount·MISSING | Queue the missing TreasuryAccount mapping or reject the command before linking. |
| Wrong scope | TreasuryAccount·B01 | Do not attach another church’s TreasuryAccount without a supported exchange and local authority. |
| Target rename | Rename TreasuryAccount·A01 after linking | The existing source_account_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No source_account_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### destination_account_id

The target is [TreasuryAccount](TreasuryAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TreasuryAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | TreasuryAccount·MISSING | Queue the missing TreasuryAccount mapping or reject the command before linking. |
| Wrong scope | TreasuryAccount·B01 | Do not attach another church’s TreasuryAccount without a supported exchange and local authority. |
| Target rename | Rename TreasuryAccount·A01 after linking | The existing destination_account_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No destination_account_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### instructed_on

Use civil calendar date for `TransferInstruction.instructed_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No instructed_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sent_amount

Use exact monetary amount with currency for `TransferInstruction.sent_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No sent_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### received_amount

Use exact monetary amount with currency for `TransferInstruction.received_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No received_amount provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### rate_id

The target is [CurrencyRate](CurrencyRate.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CurrencyRate·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | CurrencyRate·MISSING | Queue the missing CurrencyRate mapping or reject the command before linking. |
| Wrong scope | CurrencyRate·B01 | Do not attach another church’s CurrencyRate without a supported exchange and local authority. |
| Target rename | Rename CurrencyRate·A01 after linking | The existing rate_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No rate_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### fee

Use exact monetary amount with currency for `TransferInstruction.fee`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No fee provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_settlement_ref

Use scoped or external reference for `TransferInstruction.source_settlement_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified source_settlement_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped source_settlement_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No source_settlement_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### destination_settlement_ref

Use scoped or external reference for `TransferInstruction.destination_settlement_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified destination_settlement_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped destination_settlement_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No destination_settlement_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### status

Use versioned classification or status code for `TransferInstruction.status`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active status code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped status code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
