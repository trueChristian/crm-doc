# CashCount

[Counter sales and fulfilment](../../commerce/fulfilment.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique denomination and round. Blind count before showing expected close. Preserve first and recount evidence.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `shift_id` | ref CashShift | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `denomination` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `count` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `denomination_type` | note/coin | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `counted_by` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `counted_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `count_round` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### shift_id

The target is [CashShift](CashShift.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CashShift·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CashShift·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CashShift·MISSING | Queue the missing CashShift mapping or reject the command before linking. |
| Wrong scope | CashShift·B01 | Do not attach another church’s CashShift without a supported exchange and local authority. |
| Target rename | Rename CashShift·A01 after linking | The existing shift_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No shift_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### denomination

Use exact monetary amount with currency for `CashCount.denomination`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No denomination at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### count

Use whole-number measure for `CashCount.count`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No count at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### denomination_type

Declared alternatives in owner order: `note`, `coin`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | note | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_denomination_type | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No denomination_type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### counted_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing counted_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No counted_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### counted_at

Use unambiguous point in time for `CashCount.counted_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No counted_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### count_round

Use whole-number measure for `CashCount.count_round`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No count_round at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
