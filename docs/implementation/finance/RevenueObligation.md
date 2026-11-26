# RevenueObligation

[Receivables, sales and payment clearing](../../finance/receivables.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Cumulative recognized amount cannot exceed contracted amount, as adjusted. Store one sourced posting per recognized portion.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `invoice_line_id` | → SalesInvoiceLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `recognition_trigger` | {delivery,access_grant,service_period,milestone} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `deferral_account_id` | → LedgerAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `income_account_id` | → LedgerAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `total` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `start_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `end_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `fulfillment_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `schedule_version` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### invoice_line_id

The target is [SalesInvoiceLine](SalesInvoiceLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SalesInvoiceLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SalesInvoiceLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SalesInvoiceLine·MISSING | Queue the missing SalesInvoiceLine mapping or reject the command before linking. |
| Wrong scope | SalesInvoiceLine·B01 | Do not attach another church’s SalesInvoiceLine without a supported exchange and local authority. |
| Target rename | Rename SalesInvoiceLine·A01 after linking | The existing invoice_line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No invoice_line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recognition_trigger

Declared alternatives in owner order: `delivery`, `access_grant`, `service_period`, `milestone`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | delivery | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_recognition_trigger | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No recognition_trigger at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### deferral_account_id

The target is [LedgerAccount](LedgerAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LedgerAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | LedgerAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | LedgerAccount·MISSING | Queue the missing LedgerAccount mapping or reject the command before linking. |
| Wrong scope | LedgerAccount·B01 | Do not attach another church’s LedgerAccount without a supported exchange and local authority. |
| Target rename | Rename LedgerAccount·A01 after linking | The existing deferral_account_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No deferral_account_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### income_account_id

The target is [LedgerAccount](LedgerAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LedgerAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | LedgerAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | LedgerAccount·MISSING | Queue the missing LedgerAccount mapping or reject the command before linking. |
| Wrong scope | LedgerAccount·B01 | Do not attach another church’s LedgerAccount without a supported exchange and local authority. |
| Target rename | Rename LedgerAccount·A01 after linking | The existing income_account_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No income_account_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### total

Use exact monetary amount with currency for `RevenueObligation.total`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No total at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### start_on

Use civil calendar date for `RevenueObligation.start_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No start_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### end_on

Use civil calendar date for `RevenueObligation.end_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No end_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### fulfillment_ref

Use scoped or external reference for `RevenueObligation.fulfillment_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fulfillment_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped fulfillment_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No fulfillment_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### schedule_version

Use whole-number measure for `RevenueObligation.schedule_version`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No schedule_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
