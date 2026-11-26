# InKindGift

The church’s receipt of property, goods, services or use of space under agreed terms.

Track written terms, condition, quantity and custody. Match valuation only when external reviewers supply it. A security sale, appraisal or disposal receipt never creates a second donation. Keep cash reporting separate.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `organization_id` | `ref Organization` | Accepting church. [Organization](../foundation/Organization.md). |
| `giving_party_id` | `ref GivingParty?` | Verified donor if available. [GivingParty](GivingParty.md). |
| `assessment_id` | `ref GiftOfferAssessment?` | Terms and acceptance decision. [GiftOfferAssessment](../development/GiftOfferAssessment.md). |
| `description` | `text` | What was offered or received. |
| `quantity` | `decimal` | Quantity, expressed in the accompanying unit. |
| `unit` | `code` | Units, hours, use-period or item count. |
| `received_on` | `date?` | Actual custody or completion date. |
| `custody_ref` | `protected_ref?` | Custodian or recorded confirmation of service. |
| `disposition_ref` | `protected_ref?` | Return, transfer to ministry, authorized disposal or external outcome. |
| `valuation_ref` | `opaque_ref?` | Optional authorized accounting evidence with source and currency. |
| `state` | `offered/accepted/received/declined/returned` | Operational status. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AcceptedGiftLink](../development/AcceptedGiftLink.md).`in_kind_gift_id` | InKindGift identity | Reconcile the reference in the source record and preserve its correction history. |
| [GivingDocumentItem](GivingDocumentItem.md).`in_kind_gift_id` | InKindGift identity | Reconcile the reference in the source record and preserve its correction history. |
| [PartnershipDelivery](../development/PartnershipDelivery.md).`in_kind_gift_id` | InKindGift identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A donor offers ten chairs and eight pass inspection. Record acceptance and handover of eight, decline or return two with evidence, and acknowledge the received chairs without assigning an unsupported cash value.

[Noncash, memorial, matching and planned gifts](../../finance/special-giving.md) · [Giving record index](README.md)
