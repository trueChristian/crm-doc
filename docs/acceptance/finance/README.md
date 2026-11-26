# Reconciling development activity to the finance book

Run each case in a fresh accrual book. Case identifiers refer to independent sets of records. The currency is the book currency and amounts have two decimal places. Amounts are illustrative policy choices. Each case specifies the recognition point, document authority and any restrictions needed to reproduce the result.

| Office handoff | Decision the implementation must reproduce |
| --- | --- |
| [Partial award and questioned cost](partial-award.md) | Restate an earned reimbursement after the sponsor disallows part of a paid cost. Preserve the expense and two distinct financial report editions. |
| [Returned gift after a paid sponsor match](paid-match.md) | Apply the offer's waiting-list and refund terms, update giving evidence and reconcile a sponsor repayment without counting the same gift twice. |
| [Estate distribution and restricted equipment](estate-equipment.md) | Follow a private estate estimate into a confirmed distribution, asset purchase and authorized disposition of unspent terms. |
| [Sponsorship with a missed placement](sponsor-delivery.md) | Separate a gift from two exchange obligations and resolve an undelivered benefit without modifying the gift statement. |
| [Endowment draw and unspent distribution](endowment.md) | Apply a principal floor, protect the unused spending authority and reconcile an internal transfer separately from a ministry payment. |
| [Owned and consigned books at one counter](book-counter.md) | Reconcile one tender and two ownership classes across donor service, the stockroom, sales, returns and publisher settlement. |
| [Outstanding items crossing a migration](cutover.md) | Settle an old gift deposit, part-paid bill and unearned sponsorship in the new book while maintaining a signed historical comparison. |
| [Aid, agency collections and privacy](aid-agency.md) | Pay the same external partner in two capacities and reconcile church expenses separately from custodial funds. |

## How to read a fixture

A row in a posting table represents a debit line and an equal credit line. Rows sharing an entry ID belong to one atomic, balanced source event. An implementation may aggregate identical lines on the same side if the approved dimensions and source allocations still reconcile. A journal account name denotes a local mapping of the stated accounting purpose. The event identifiers are fixture keys and the record links identify the owning definitions.

1. Seed the stated opening balances, roles, terms, and dates. Read individual checkpoints at the end of their listed events. Derive control totals from posted records in the same book, fund scope and cutoff.
2. Save the dated report or statement at the specified checkpoint. Introduce the adverse event and read the new report with a separate as-of value. Reproduce the first report from its saved edition.
3. Retry each nominated event under its original economic key. Simulate failure before commit and after commit with a lost response. Compare the balances, posted purpose count, active links, issued numbers and external payments against the stated results.
4. Use the specified restricted role to follow the same identifiers through list, detail, search and export entry points. A summary may legitimately disclose an aggregate while its underlying records require separate authority.

The [finance department guide](../../finance/README.md) defines posting and reporting policies. The [development department guide](../../development/README.md) defines contact, proposal and agreement responsibilities. The [finance decision fixtures](../../decisions/finance/README.md) exercise component calculations for claims, settlements, matching and period allocation.
