# CustodyTransfer

A witnessed release and receipt of a collection or sealed bag.

One open transfer at a time per bag. Validate current custodian, monotonic times and recipient confirmation. An outstanding or refused transfer retains the sending/receiving evidence and triggers escalation.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `batch_id` | `ref CollectionBatch` | Collection being moved. [CollectionBatch](CollectionBatch.md). |
| `sequence` | `integer` | Position in custody chain. |
| `from_ref` | `protected_ref` | Responsible holder releasing the batch. |
| `to_ref` | `protected_ref` | Intended recipient. |
| `sent_at` | `instant` | Release time. |
| `received_at` | `instant?` | Actual acceptance by recipient. |
| `seal_before` | `text?` | Seal identifier or recorded condition on release. |
| `seal_after` | `text?` | Seal identifier or recorded condition at receipt. |
| `amount` | `money?` | Amount known when custody changes. |
| `exception_ref` | `protected_ref?` | Broken seal, refusal, missing bag or custody investigation. |

## Acceptance decision

An uncounted sealed bag is accepted during transport. An absent amount stays unknown. Arrival confirmation supplies custody evidence and does not verify the later count.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
