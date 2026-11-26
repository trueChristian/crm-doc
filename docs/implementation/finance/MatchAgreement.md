# MatchAgreement

[Campaigns and specialized gifts](../../finance/special-giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Track reserved, earned, received, expired and denied match. Concurrent qualifying gifts cannot exceed remaining sponsor cap.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `campaign_id` | → GivingCampaign | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sponsor_id` | → GivingParty | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `starts_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `ends_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `match_ratio` | decimal | Required when the record reaches its applicable state | [ratio](../value-conventions.md#ratio) |
| `cap` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `minimum` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `eligible_rule` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [rule](../value-conventions.md#rule) |
| `commitment_type` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `evidence` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `status` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### campaign_id

The target is [GivingCampaign](GivingCampaign.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingCampaign·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GivingCampaign·MISSING | Queue the missing GivingCampaign mapping or reject the command before linking. |
| Wrong scope | GivingCampaign·B01 | Do not attach another church’s GivingCampaign without a supported exchange and local authority. |
| Target rename | Rename GivingCampaign·A01 after linking | The existing campaign_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No campaign_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sponsor_id

The target is [GivingParty](GivingParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GivingParty·MISSING | Queue the missing GivingParty mapping or reject the command before linking. |
| Wrong scope | GivingParty·B01 | Do not attach another church’s GivingParty without a supported exchange and local authority. |
| Target rename | Rename GivingParty·A01 after linking | The existing sponsor_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No sponsor_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### starts_on

Use civil calendar date for `MatchAgreement.starts_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No starts_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ends_on

Use civil calendar date for `MatchAgreement.ends_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No ends_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### match_ratio

Use exact ratio, rate or weighting for `MatchAgreement.match_ratio`. Carry the declared unit, direction and calculation precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 1.125 under named rate basis | Carry the declared unit, direction and calculation precision. |
| Malformed or unmapped | rate with unknown direction | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | 0.125 fraction and 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | reciprocal quoted in opposite currency direction | Require explicit direction and an approved conversion. |
| Financial document already issued | historical line after a rate-table correction | Retain the original rate, effective date and rounding basis. |
| Incomplete record | No match_ratio at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cap

Use exact monetary amount with currency for `MatchAgreement.cap`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No cap at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### minimum

Use exact monetary amount with currency for `MatchAgreement.minimum`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No minimum provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### eligible_rule

Use versioned structured decision or expression for `MatchAgreement.eligible_rule`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for eligible_rule | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in eligible_rule | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No eligible_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### commitment_type

Use versioned classification or status code for `MatchAgreement.commitment_type`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active commitment_type code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped commitment_type code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No commitment_type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence

Use scoped or external reference for `MatchAgreement.evidence`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No evidence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Use versioned classification or status code for `MatchAgreement.status`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active status code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped status code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [MatchAttribution](MatchAttribution.md).`agreement_id` | MatchAgreement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
