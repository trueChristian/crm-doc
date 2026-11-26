# RestrictionRelease

[Funds, awards and stewardship](../../finance/stewardship.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Cumulative releases cannot exceed eligible restricted resources. Same event cannot release twice. Transfers of cash and satisfaction of a restriction are separate events.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `restriction_id` | → FundRestriction | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `released_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `qualifying_event` | source | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |
| `release_evidence` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |
| `authorized_by_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `posting_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `reversal_of` | → RestrictionRelease? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### restriction_id

The target is [FundRestriction](FundRestriction.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FundRestriction·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FundRestriction·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FundRestriction·MISSING | Queue the missing FundRestriction mapping or reject the command before linking. |
| Wrong scope | FundRestriction·B01 | Do not attach another church’s FundRestriction without a supported exchange and local authority. |
| Target rename | Rename FundRestriction·A01 after linking | The existing restriction_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No restriction_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### released_on

Use civil calendar date for `RestrictionRelease.released_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No released_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount

Use exact monetary amount with currency for `RestrictionRelease.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### qualifying_event

Use typed value or bounded compound record for `RestrictionRelease.qualifying_event`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of qualifying_event matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for qualifying_event | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No qualifying_event at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### release_evidence

Use typed value or bounded compound record for `RestrictionRelease.release_evidence`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of release_evidence matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for release_evidence | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No release_evidence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authorized_by_ref

Use scoped or external reference for `RestrictionRelease.authorized_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified authorized_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped authorized_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No authorized_by_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### posting_ref

Use scoped or external reference for `RestrictionRelease.posting_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified posting_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped posting_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No posting_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reversal_of

The target is [RestrictionRelease](RestrictionRelease.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RestrictionRelease·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RestrictionRelease·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RestrictionRelease·MISSING | Queue the missing RestrictionRelease mapping or reject the command before linking. |
| Wrong scope | RestrictionRelease·B01 | Do not attach another church’s RestrictionRelease without a supported exchange and local authority. |
| Target rename | Rename RestrictionRelease·A01 after linking | The existing reversal_of keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reversal_of provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [RestrictionRelease](RestrictionRelease.md).`reversal_of` | RestrictionRelease identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
