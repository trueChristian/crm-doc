# GivingParty

The giving identity that a donor-services officer may use for gifts and correspondence.

Exactly one typed donor identity agrees with the selected kind. A person can act for an organization, give individually and participate in a joint gift under different instructions. Do not infer an identity from household contact access, a login or a common email. Unknown donors have no party on their gifts.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `organization_id` | `ref Organization` | Receiving church. [Organization](../foundation/Organization.md). |
| `kind` | `person/household/organization` | Select the identity on whose behalf the gift was given. |
| `person_id` | `ref Person?` | Identified individual, including a visitor. [Person](../people/Person.md). |
| `household_id` | `ref Household?` | Joint giving unit, with documentary authority. [Household](../people/Household.md). |
| `party_organization_id` | `ref Organization?` | A verified organization known to the receiving church. [Organization](../foundation/Organization.md). |
| `authority_evidence` | `protected_ref?` | Covers attribution, joint giving or designation of a representative. |
| `recipient_ref` | `protected_ref?` | Authorized correspondence recipient and basis. |
| `effective_from` | `date` | Start of the giving instruction. |
| `effective_to` | `date?` | End of use for new gifts. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AppealProspect](../development/AppealProspect.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [AppealResponse](../development/AppealResponse.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [DevelopmentCreditInstruction](../development/DevelopmentCreditInstruction.md).`credited_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [DonationMandate](DonationMandate.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [DonorServiceCase](../development/DonorServiceCase.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [FundRestriction](FundRestriction.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [Gift](Gift.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [GiftAdjustment](GiftAdjustment.md).`replacement_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [GiftOfferAssessment](../development/GiftOfferAssessment.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [GivingDocument](GivingDocument.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [InKindGift](InKindGift.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [LegacyNotice](../development/LegacyNotice.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [MatchOffer](../development/MatchOffer.md).`matching_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [Pledge](Pledge.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [StewardshipPlan](../development/StewardshipPlan.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [SupporterInstruction](../development/SupporterInstruction.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |
| [TributeInstruction](../development/TributeInstruction.md).`giving_party_id` | GivingParty identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A spouse with portal access to family events requests the personal gift history of their partner. Only explicit giving authority for the requested scope allows disclosure.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
