# MatchQualification

[Appeals and attribution](../../development/appeals.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique offer/allocation/revision. Link the verified gift allocation of actual sponsor payment, with capped amount. Never match the sponsor's own matching receipt unless the published rules expressly establish another independent offer.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `offer_id` | ref MatchOffer | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `qualifying_allocation_id` | ref GiftAllocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `eligible_base` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `earned_match` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `evaluated_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `decision_reason` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `match_allocation_id` | ref GiftAllocation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `state` | provisional/verified/paid/reversed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### offer_id

The target is [MatchOffer](MatchOffer.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MatchOffer·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MatchOffer·MISSING | Queue the missing MatchOffer mapping or reject the command before linking. |
| Wrong scope | MatchOffer·B01 | Do not attach another church’s MatchOffer without a supported exchange and local authority. |
| Target rename | Rename MatchOffer·A01 after linking | The existing offer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No offer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### qualifying_allocation_id

The target is [GiftAllocation](../finance/GiftAllocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftAllocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GiftAllocation·MISSING | Queue the missing GiftAllocation mapping or reject the command before linking. |
| Wrong scope | GiftAllocation·B01 | Do not attach another church’s GiftAllocation without a supported exchange and local authority. |
| Target rename | Rename GiftAllocation·A01 after linking | The existing qualifying_allocation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No qualifying_allocation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligible_base

Use exact monetary amount with currency for `MatchQualification.eligible_base`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No eligible_base at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### earned_match

Use exact monetary amount with currency for `MatchQualification.earned_match`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No earned_match at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `MatchQualification.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Hold the row for currency mapping before an amount-dependent approval or exchange. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evaluated_at

Use unambiguous point in time for `MatchQualification.evaluated_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No evaluated_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision_reason

Use versioned classification or status code for `MatchQualification.decision_reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active decision_reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped decision_reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No decision_reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### match_allocation_id

The target is [GiftAllocation](../finance/GiftAllocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftAllocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GiftAllocation·MISSING | Queue the missing GiftAllocation mapping or reject the command before linking. |
| Wrong scope | GiftAllocation·B01 | Do not attach another church’s GiftAllocation without a supported exchange and local authority. |
| Target rename | Rename GiftAllocation·A01 after linking | The existing match_allocation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No match_allocation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `provisional`, `verified`, `paid`, `reversed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | provisional | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
