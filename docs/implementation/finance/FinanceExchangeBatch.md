# FinanceExchangeBatch

A sealed manifest of financial handoff items, transport-neutral and scoped to one connection.

Bulk release includes stable row identities and atomic event groups. Support a one-item manifest and a reviewed file handoff through the same rules. Never collapse different currencies or book an acknowledgment into gift totals.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `organization_id` | `ref Organization` | Church responsible for release. [Organization](../foundation/Organization.md). |
| `connection_ref` | `opaque_ref` | Named, authenticated destination or source. |
| `direction` | `inbound/outbound` | Direction relative to the CRM. |
| `manifest_key` | `text` | Durable batch identifier scoped to the connection. |
| `contract_edition` | `text` | Contract used to interpret the payload. |
| `cutoff_at` | `instant` | Inclusion cutoff. |
| `count` | `integer` | Number of distinct business items. |
| `controls` | `structured` | Count and signed totals by event type and currency, with separate measures for contributions, fees and benefits. |
| `fingerprint` | `text` | Digest of the sealed normalized contents. |
| `state` | `prepared/released/part_resolved/resolved` | Manifest progression, separate from item outcome. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [FinanceExchangeItem](FinanceExchangeItem.md).`batch_id` | FinanceExchangeBatch identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A file has ten items of which nine are accepted. Seal the original totals, show nine accepted and one outstanding, and reconcile each line to its outcome. Retrying the one item cannot release nine new gifts.

[Accounting exchange and source ownership](../../finance/accounting-exchange.md) · [Giving record index](README.md)
