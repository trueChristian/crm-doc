# Gift

One monetary contribution received, with a persistent source key and a separate verification decision.

Enforce uniqueness by church, source account, source key and part. To verify, allocations in the same currency must sum to the gift. An unnamed giver can be truly anonymous or awaiting identification. Keep those cases distinguishable in intake evidence. Assigning an identity later requires a reviewed amendment.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `organization_id` | `ref Organization` | Receiving church. [Organization](../foundation/Organization.md). |
| `giving_party_id` | `ref GivingParty?` | Verified giver, absent for an unnamed contribution. [GivingParty](GivingParty.md). |
| `batch_id` | `ref CollectionBatch?` | Physical collection, if applicable. [CollectionBatch](CollectionBatch.md). |
| `source_account_ref` | `opaque_ref` | Namespace of the physical or digital intake. |
| `source_key` | `text` | Durable office receipt or provider transaction identity. |
| `source_part` | `text` | Stable gift portion of a mixed transaction. |
| `received_on` | `date` | Church-local date with available original capture time retained as evidence. |
| `currency` | `code` | Currency of the contribution. |
| `gross_amount` | `money` | Positive contributed portion before fees or adjustments. |
| `tender` | `code` | Locally recognized payment method category. |
| `state` | `recorded/held/verified/declined` | Verification status. Later corrections have separate records. |
| `publicity` | `code` | Most restrictive applicable public naming instruction. |
| `evidence_ref` | `protected_ref?` | Relevant proof of receipt or review. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AcceptedGiftLink](../development/AcceptedGiftLink.md).`gift_id` | Gift identity | Reconcile the reference in the source record and preserve its correction history. |
| [DevelopmentCreditInstruction](../development/DevelopmentCreditInstruction.md).`source_gift_id` | Gift identity | Reconcile the reference in the source record and preserve its correction history. |
| [GiftAllocation](GiftAllocation.md).`gift_id` | Gift identity | Reconcile the reference in the source record and preserve its correction history. |
| [GiftAttribution](GiftAttribution.md).`gift_id` | Gift identity | Reconcile the reference in the source record and preserve its correction history. |
| [LegacyNotice](../development/LegacyNotice.md).`received_gift_id` | Gift identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A capture of 100 contains a ticket portion of 65 and a contribution of 35. One gift for 35 and its source part is verified. A replay with a different contribution amount is held as a conflict.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
