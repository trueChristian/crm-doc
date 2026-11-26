# CollectionBatch

A collection of physical tenders received into the church’s custody.

Verification reconciles envelope allocations and anonymous loose amounts with exactly one approved count round per tender. A receiving signature closes physical handover. Track accounting delivery separately.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `organization_id` | `ref Organization` | Receiving church. [Organization](../foundation/Organization.md). |
| `campus_id` | `ref Campus?` | Campus where collected. [Campus](../foundation/Campus.md). |
| `occurrence_id` | `ref EventOccurrence?` | Service or event, when applicable. [EventOccurrence](../ministry/EventOccurrence.md). |
| `collected_on` | `date` | Local date of collection. |
| `currency` | `code` | One currency per batch. |
| `seal_ref` | `text?` | Physical bag or container identifier. |
| `custodian_ref` | `protected_ref` | Current custodian established by confirmed movements. |
| `selected_round` | `integer?` | Approved count of that batch. |
| `state` | `open/under_review/verified/handed_over` | Custody and verification state. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CollectionCount](CollectionCount.md).`batch_id` | CollectionBatch identity | Reconcile the reference in the source record and preserve its correction history. |
| [CustodyTransfer](CustodyTransfer.md).`batch_id` | CollectionBatch identity | Reconcile the reference in the source record and preserve its correction history. |
| [Gift](Gift.md).`batch_id` | CollectionBatch identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

Two independent teams each count 247. Assigned counters confirm 247 in one selected round. The church giving total stays 247 after handover.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
