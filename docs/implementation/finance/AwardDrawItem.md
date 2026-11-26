# AwardDrawItem

[Funds, awards and stewardship](../../finance/stewardship.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exactly one supporting source. Prevent overlapping claims or re-use above unreimbursed amount.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `draw_id` | → AwardDraw | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `award_cost_id` | → AwardCost? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `milestone_id` | → AwardMilestone? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### draw_id

The target is [AwardDraw](AwardDraw.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AwardDraw·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AwardDraw·MISSING | Queue the missing AwardDraw mapping or reject the command before linking. |
| Wrong scope | AwardDraw·B01 | Do not attach another church’s AwardDraw without a supported exchange and local authority. |
| Target rename | Rename AwardDraw·A01 after linking | The existing draw_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No draw_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### award_cost_id

The target is [AwardCost](AwardCost.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AwardCost·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AwardCost·MISSING | Queue the missing AwardCost mapping or reject the command before linking. |
| Wrong scope | AwardCost·B01 | Do not attach another church’s AwardCost without a supported exchange and local authority. |
| Target rename | Rename AwardCost·A01 after linking | The existing award_cost_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No award_cost_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### milestone_id

The target is [AwardMilestone](AwardMilestone.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AwardMilestone·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AwardMilestone·MISSING | Queue the missing AwardMilestone mapping or reject the command before linking. |
| Wrong scope | AwardMilestone·B01 | Do not attach another church’s AwardMilestone without a supported exchange and local authority. |
| Target rename | Rename AwardMilestone·A01 after linking | The existing milestone_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No milestone_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### amount

Use exact monetary amount with currency for `AwardDrawItem.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
