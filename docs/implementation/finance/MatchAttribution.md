# MatchAttribution

[Campaigns and specialized gifts](../../finance/special-giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique agreement/allocation/portion. Sponsor pays a separate economic gift. A dashboard may present both once as separate donors.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `agreement_id` | → MatchAgreement | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `qualifying_allocation_id` | → GiftAllocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `eligible` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `matched` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `sponsor_gift_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `review_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### agreement_id

The target is [MatchAgreement](MatchAgreement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MatchAgreement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MatchAgreement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MatchAgreement·MISSING | Queue the missing MatchAgreement mapping or reject the command before linking. |
| Wrong scope | MatchAgreement·B01 | Do not attach another church’s MatchAgreement without a supported exchange and local authority. |
| Target rename | Rename MatchAgreement·A01 after linking | The existing agreement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No agreement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### qualifying_allocation_id

The target is [GiftAllocation](GiftAllocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftAllocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GiftAllocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GiftAllocation·MISSING | Queue the missing GiftAllocation mapping or reject the command before linking. |
| Wrong scope | GiftAllocation·B01 | Do not attach another church’s GiftAllocation without a supported exchange and local authority. |
| Target rename | Rename GiftAllocation·A01 after linking | The existing qualifying_allocation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No qualifying_allocation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligible

Use exact monetary amount with currency for `MatchAttribution.eligible`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No eligible at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### matched

Use exact monetary amount with currency for `MatchAttribution.matched`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No matched at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sponsor_gift_ref

Use scoped or external reference for `MatchAttribution.sponsor_gift_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified sponsor_gift_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped sponsor_gift_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No sponsor_gift_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### review_state

Use versioned classification or status code for `MatchAttribution.review_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active review_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped review_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No review_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
