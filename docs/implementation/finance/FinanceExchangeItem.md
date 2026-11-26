# FinanceExchangeItem

A source event with durable business identity and its latest destination disposition.

The business key is unique per church, direction, connection, namespace and revision across manifests. Retries carry the same event, mapping and digest. Identical deliveries reference the existing business outcome. Conflicting bodies enter review. A transport receipt never certifies financial application.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `batch_id` | `ref FinanceExchangeBatch` | Manifest including this transfer. [FinanceExchangeBatch](FinanceExchangeBatch.md). |
| `source_namespace` | `opaque_ref` | Producer and account in the receiving church. |
| `event_key` | `text` | Stable key per business fact. |
| `source_revision` | `integer` | Ordered version of the source decision. |
| `group_key` | `text` | Atomic set of dependent lines. |
| `operation` | `code` | Gift verification, correction, support request or other advertised capability. |
| `source_ref` | `opaque_ref` | Immutable church fact or authenticated external identifier. |
| `predecessor_key` | `text?` | Earlier operation required to apply the item. |
| `payload_digest` | `text` | Canonical business content excluding transport metadata. |
| `mapping_edition` | `integer?` | Released mapping edition, where required. |
| `external_ref` | `opaque_ref?` | Scoped destination reference. |
| `outcome` | `code` | Pending, transport received, applied, rejected, uncertain or explicitly superseded. |
| `evidence_ref` | `protected_ref?` | Minimized decision, time, reason and operator where needed. |

## Acceptance decision

An external service accepts an item and its response is lost. Lookup or replay using the same key obtains the original result. On an interface without deduplication or status lookup the operator confirms the external outcome before resending.

[Accounting exchange and source ownership](../../finance/accounting-exchange.md) · [Giving record index](README.md)
