# CollectionCount

A tender line in a separately attributable count or recount.

For denomination lines require positive denomination, nonnegative quantity and an exact product. Amend by recording a new count round. Preserve officer, reason and selection when a variance is resolved.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `batch_id` | `ref CollectionBatch` | Parent physical batch. [CollectionBatch](CollectionBatch.md). |
| `round` | `integer` | Independent count group. |
| `line_no` | `integer` | Unique inside round. |
| `tender` | `code` | Cash, cheque or other locally accepted instrument. |
| `denomination` | `money?` | Face value in batch currency when counted by units. |
| `quantity` | `integer?` | Number of units at that face value. |
| `amount` | `money` | Verified count for the line. |
| `counter_id` | `ref UserAccount` | Individual making the count. [UserAccount](../platform/UserAccount.md). |
| `witness_id` | `ref UserAccount?` | Independent observer where required. [UserAccount](../platform/UserAccount.md). |
| `counted_at` | `instant` | Actual observation time. |
| `discrepancy_note` | `protected_ref?` | Restricted account of an exception. |

## Acceptance decision

A sealed bag has 99 in the first round and 100 in the second. Opening review leaves both observations intact. Selecting the verified round requires a resolution.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
