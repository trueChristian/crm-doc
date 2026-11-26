# FinanceCodeMapping

A scoped interpretation of a church designation or activity at an external accounting destination.

For one connection, source and effective event date, one published mapping applies. A bridge may map many local purposes to one destination where source line identities survive. Ambiguity or missing maps block only affected event groups.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `organization_id` | `ref Organization` | Sending church. [Organization](../foundation/Organization.md). |
| `connection_ref` | `opaque_ref` | Authorized account or file destination. |
| `source_kind` | `code` | Gift purpose, receipt type, outreach project or approved support category. |
| `source_key` | `text` | Stable local code. |
| `destination_code` | `text` | Agreed external code. |
| `edition` | `integer` | Approved, immutable mapping edition. |
| `effective_from` | `date` | First effective date. |
| `effective_to` | `date?` | End of applicability. |
| `approved_by` | `ref UserAccount` | Church reviewer of destination and meaning. [UserAccount](../platform/UserAccount.md). |

## Acceptance decision

A destination retires a missions code after a gift has been sent. Replaying the original event preserves its effective mapping. An explicitly approved mapping correction creates a new business revision with history.

[Accounting exchange and source ownership](../../finance/accounting-exchange.md) · [Giving record index](README.md)
