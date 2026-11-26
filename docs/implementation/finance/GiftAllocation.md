# GiftAllocation

[Offerings, gifts and donor service](../../finance/giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

At least one allocation. Allocations equal gross. Benefit and eligible amounts follow local rules. Fees are an expense or contract adjustment under policy and never silently reduce allocation totals.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `gift_id` | → Gift | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `fund_id` | → Fund | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `campaign_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `grant_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `pledge_installment_id` | → PledgeInstallment? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `benefit_value` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `eligibility_class` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `restriction_evidence` | ? | Optional under owner conditions | [structured](../value-conventions.md#structured) |
| `anonymity_scope` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### gift_id

The target is [Gift](Gift.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Gift·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Gift·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Gift·MISSING | Queue the missing Gift mapping or reject the command before linking. |
| Wrong scope | Gift·B01 | Do not attach another church’s Gift without a supported exchange and local authority. |
| Target rename | Rename Gift·A01 after linking | The existing gift_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No gift_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fund_id

The target is [Fund](Fund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Fund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Fund·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Fund·MISSING | Queue the missing Fund mapping or reject the command before linking. |
| Wrong scope | Fund·B01 | Do not attach another church’s Fund without a supported exchange and local authority. |
| Target rename | Rename Fund·A01 after linking | The existing fund_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No fund_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### campaign_ref

Use scoped or external reference for `GiftAllocation.campaign_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified campaign_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped campaign_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No campaign_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### grant_ref

Use scoped or external reference for `GiftAllocation.grant_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified grant_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped grant_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No grant_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### pledge_installment_id

The target is [PledgeInstallment](PledgeInstallment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PledgeInstallment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PledgeInstallment·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PledgeInstallment·MISSING | Queue the missing PledgeInstallment mapping or reject the command before linking. |
| Wrong scope | PledgeInstallment·B01 | Do not attach another church’s PledgeInstallment without a supported exchange and local authority. |
| Target rename | Rename PledgeInstallment·A01 after linking | The existing pledge_installment_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No pledge_installment_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### amount

Use exact monetary amount with currency for `GiftAllocation.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### benefit_value

Use exact monetary amount with currency for `GiftAllocation.benefit_value`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No benefit_value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligibility_class

Use versioned classification or status code for `GiftAllocation.eligibility_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active eligibility_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped eligibility_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No eligibility_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### restriction_evidence

Use typed value or bounded compound record for `GiftAllocation.restriction_evidence`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of restriction_evidence matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for restriction_evidence | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Absent in intake | No restriction_evidence provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### anonymity_scope

Use versioned classification or status code for `GiftAllocation.anonymity_scope`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active anonymity_scope code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped anonymity_scope code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No anonymity_scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AppealAllocationCredit](../development/AppealAllocationCredit.md).`gift_allocation_id` | GiftAllocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingClaimLine](GivingClaimLine.md).`allocation_id` | GiftAllocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingDocumentItem](GivingDocumentItem.md).`allocation_id` | GiftAllocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MatchAttribution](MatchAttribution.md).`qualifying_allocation_id` | GiftAllocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MatchQualification](../development/MatchQualification.md).`match_allocation_id` | GiftAllocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MatchQualification](../development/MatchQualification.md).`qualifying_allocation_id` | GiftAllocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PartnershipDelivery](../development/PartnershipDelivery.md).`gift_allocation_id` | GiftAllocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
