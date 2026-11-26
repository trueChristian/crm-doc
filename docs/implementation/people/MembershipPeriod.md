# MembershipPeriod

[Membership, transfers and certified rolls](../../people/membership-and-rolls.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Effective dated class and standing. Within one membership, periods cannot overlap. A gap requires a documented departure or correction. Cross-congregation overlap follows the applicable affiliation policy.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `membership_id` | → Membership | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `class_id` | → MembershipClass | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `standing` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `from_date` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `until_date` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `primary_affiliation` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `policy_id` | → MembershipPolicy | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `decision_id` | → MembershipDecision | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `MembershipPeriod.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MembershipPeriod·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### membership_id

The target is [Membership](Membership.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Membership·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Membership·MISSING | Queue the missing Membership mapping or reject the command before linking. |
| Wrong scope | Membership·B01 | Do not attach another church’s Membership without a supported exchange and local authority. |
| Target rename | Rename Membership·A01 after linking | The existing membership_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No membership_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### class_id

The target is [MembershipClass](MembershipClass.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MembershipClass·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MembershipClass·MISSING | Queue the missing MembershipClass mapping or reject the command before linking. |
| Wrong scope | MembershipClass·B01 | Do not attach another church’s MembershipClass without a supported exchange and local authority. |
| Target rename | Rename MembershipClass·A01 after linking | The existing class_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No class_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### standing

Use versioned classification or status code for `MembershipPeriod.standing`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active standing code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped standing code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No standing at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### from_date

Use civil calendar date for `MembershipPeriod.from_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No from_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### until_date

Use civil calendar date for `MembershipPeriod.until_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No until_date provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### primary_affiliation

Use explicit logical choice for `MembershipPeriod.primary_affiliation`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No primary_affiliation at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### policy_id

The target is [MembershipPolicy](MembershipPolicy.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MembershipPolicy·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MembershipPolicy·MISSING | Queue the missing MembershipPolicy mapping or reject the command before linking. |
| Wrong scope | MembershipPolicy·B01 | Do not attach another church’s MembershipPolicy without a supported exchange and local authority. |
| Target rename | Rename MembershipPolicy·A01 after linking | The existing policy_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No policy_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision_id

The target is [MembershipDecision](MembershipDecision.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MembershipDecision·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MembershipDecision·MISSING | Queue the missing MembershipDecision mapping or reject the command before linking. |
| Wrong scope | MembershipDecision·B01 | Do not attach another church’s MembershipDecision without a supported exchange and local authority. |
| Target rename | Rename MembershipDecision·A01 after linking | The existing decision_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No decision_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [RollEntry](RollEntry.md).`membership_period_id` | MembershipPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
