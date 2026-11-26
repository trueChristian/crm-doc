# GivingParty

[Offerings, gifts and donor service](../../finance/giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exactly one matching identity for identified parties. For anonymous, no personal target. A household giving party requires an explicit joint-giving instruction and authority for joint statements.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `kind` | {person,household,organization,anonymous} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `household_id` | → Household? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `party_organization_id` | → Organization? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `display_policy` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `statement_preference` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `correspondence_recipient_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### kind

Declared alternatives in owner order: `person`, `household`, `organization`, `anonymous`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | person | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### household_id

The target is [Household](../people/Household.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Household·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Household·MISSING | Queue the missing Household mapping or reject the command before linking. |
| Wrong scope | Household·B01 | Do not attach another church’s Household without a supported exchange and local authority. |
| Target rename | Rename Household·A01 after linking | The existing household_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No household_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### party_organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing party_organization_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No party_organization_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### display_policy

Use versioned classification or status code for `GivingParty.display_policy`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active display_policy code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped display_policy code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No display_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### statement_preference

Use versioned classification or status code for `GivingParty.statement_preference`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active statement_preference code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped statement_preference code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No statement_preference at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### correspondence_recipient_ref

Use scoped or external reference for `GivingParty.correspondence_recipient_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified correspondence_recipient_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped correspondence_recipient_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No correspondence_recipient_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AppealProspect](../development/AppealProspect.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealResponse](../development/AppealResponse.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DevelopmentCreditInstruction](../development/DevelopmentCreditInstruction.md).`credited_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DonationMandate](DonationMandate.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DonorServiceCase](../development/DonorServiceCase.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundRestriction](FundRestriction.md).`sponsor_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Gift](Gift.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftAttribution](GiftAttribution.md).`credited_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftOfferAssessment](../development/GiftOfferAssessment.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingClaim](GivingClaim.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingDocument](GivingDocument.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LegacyNotice](../development/LegacyNotice.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MatchAgreement](MatchAgreement.md).`sponsor_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MatchOffer](../development/MatchOffer.md).`matching_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PlannedGift](PlannedGift.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Pledge](Pledge.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StewardshipPlan](../development/StewardshipPlan.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupporterInstruction](../development/SupporterInstruction.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TributeInstruction](../development/TributeInstruction.md).`giving_party_id` | GivingParty identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Use the minimum evidence allowed by the selected anonymous, pseudonymous or identified mode. A permitted operator may be accountable for receiving or reviewing work without collecting the identity of a protected subject. Keep safe-channel, identity and case evidence apart from releasable totals and narratives; apply the original permissions to the verification evidence.
