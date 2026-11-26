# GivingClaimLine

[Offerings, gifts and donor service](../../finance/giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One live claim per scheme, allocation and claim portion; track partial acceptance, rejection and clawback without changing the donor's gift.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `claim_id` | → GivingClaim | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `allocation_id` | → GiftAllocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `eligible_base` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `requested_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `received_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `adjustment_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### claim_id

The target is [GivingClaim](GivingClaim.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingClaim·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GivingClaim·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GivingClaim·MISSING | Queue the missing GivingClaim mapping or reject the command before linking. |
| Wrong scope | GivingClaim·B01 | Do not attach another church’s GivingClaim without a supported exchange and local authority. |
| Target rename | Rename GivingClaim·A01 after linking | The existing claim_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No claim_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allocation_id

The target is [GiftAllocation](GiftAllocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftAllocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GiftAllocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GiftAllocation·MISSING | Queue the missing GiftAllocation mapping or reject the command before linking. |
| Wrong scope | GiftAllocation·B01 | Do not attach another church’s GiftAllocation without a supported exchange and local authority. |
| Target rename | Rename GiftAllocation·A01 after linking | The existing allocation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No allocation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligible_base

Use exact monetary amount with currency for `GivingClaimLine.eligible_base`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No eligible_base at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_amount

Use exact monetary amount with currency for `GivingClaimLine.requested_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No requested_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### received_amount

Use exact monetary amount with currency for `GivingClaimLine.received_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No received_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### adjustment_ref

Use scoped or external reference for `GivingClaimLine.adjustment_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified adjustment_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped adjustment_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No adjustment_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
