# GiftAllocation

One portion of a gift directed to a church purpose.

Each line belongs to one gift. A combined pledge and appeal attribution still represents a single amount. Separate permission governs naming a donor. An unresolved purpose holds the gift for review.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `gift_id` | `ref Gift` | Owning monetary gift. [Gift](Gift.md). |
| `line_key` | `text` | Stable line identifier inside the gift. |
| `fund_id` | `ref Fund` | Accepted church designation. [Fund](Fund.md). |
| `amount` | `money` | Positive portion in original gift currency. |
| `restriction_id` | `ref FundRestriction?` | Applicable donor terms. [FundRestriction](FundRestriction.md). |
| `pledge_installment_id` | `ref PledgeInstallment?` | Progress credited against a specific promise. [PledgeInstallment](PledgeInstallment.md). |
| `instruction_ref` | `protected_ref?` | Donor direction and approved exception evidence. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AppealAllocationCredit](../development/AppealAllocationCredit.md).`gift_allocation_id` | GiftAllocation identity | Reconcile the reference in the source record and preserve its correction history. |
| [GiftAdjustment](GiftAdjustment.md).`allocation_id` | GiftAllocation identity | Reconcile the reference in the source record and preserve its correction history. |
| [GivingDocumentItem](GivingDocumentItem.md).`allocation_id` | GiftAllocation identity | Reconcile the reference in the source record and preserve its correction history. |
| [MatchQualification](../development/MatchQualification.md).`match_allocation_id` | GiftAllocation identity | Reconcile the reference in the source record and preserve its correction history. |
| [MatchQualification](../development/MatchQualification.md).`qualifying_allocation_id` | GiftAllocation identity | Reconcile the reference in the source record and preserve its correction history. |
| [PartnershipDelivery](../development/PartnershipDelivery.md).`gift_allocation_id` | GiftAllocation identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

On a gift of 100 the giver requests 70 for missions and 30 for the general fund. A campaign link on the missions portion credits at most 70. Reuse of the same line cannot add a second 70 to cash received.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
