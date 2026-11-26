# GiftAdjustment

A confirmed correction to one original allocation, preserving its initial value and subsequent effects.

Returns and chargebacks consume remaining allocation value. A reinstatement is capped by the linked loss. A redesignation moves equal units out and in within the gift’s currency. An attribution correction changes no money and records the verified scope of the correction. Apply multi-line decisions atomically.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `allocation_id` | `ref GiftAllocation` | Original allocation. [GiftAllocation](GiftAllocation.md). |
| `source_namespace` | `opaque_ref` | Authority supplying the amendment. |
| `source_key` | `text` | Unique amendment identity within its authority. |
| `kind` | `return/chargeback/reinstatement/redesignation/attribution` | Kind of evidenced change. |
| `amount` | `money?` | Positive magnitude for a monetary change. |
| `destination_fund_id` | `ref Fund?` | Destination for an approved redesignation. [Fund](Fund.md). |
| `prior_adjustment_id` | `ref GiftAdjustment?` | Disputed, restored or corrected adjustment. [GiftAdjustment](GiftAdjustment.md). |
| `replacement_party_id` | `ref GivingParty?` | Effective corrected giver for an attribution correction. [GivingParty](GivingParty.md). |
| `effective_on` | `date` | Date applicable to the correction. |
| `approved_by` | `ref UserAccount` | Scoped reviewer. [UserAccount](../platform/UserAccount.md). |
| `evidence_ref` | `protected_ref` | Reason, decision and donor authorization as applicable. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [GiftAdjustment](GiftAdjustment.md).`prior_adjustment_id` | GiftAdjustment identity | Reconcile the reference in the source record and preserve its correction history. |
| [GivingDocumentItem](GivingDocumentItem.md).`adjustment_id` | GiftAdjustment identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A verified gift of 70 has a confirmed return of 20. An unrelated second return of 60 is held. Replaying the first leaves the net at 50. Reinstating the disputed 20 returns the net to 70.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
