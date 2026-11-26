# Commerce and fundraising decision tables

These nine suites contain independent input-and-expected-output cases. Choose the policy matching the operation, open a range, enter the inputs in a fresh organization fixture, then compare the resulting outputs with that row. Monetary values are **integer minor units**, including amounts in the examples. Each table states its own order of operations, license window, recognition policy or cost method. The church must configure its actual policies separately.

A case ID identifies exactly one row. The ordering groups related input changes so a reviewer can follow boundary transitions. A replay uses the same source identity and must leave the first successful result unchanged. Do not treat a neighbouring case as the next transaction. For multi-event traces and reversal context use the [operations handbook](../../handbook/commerce/README.md).

| Operation | Cases | Pages |
| --- | ---: | ---: |
| [Allocate a promotion and compute the quoted tax](01-quote/README.md) | 2,880 | 12 |
| [Refund specific units to their original tenders](02-refund/README.md) | 4,800 | 20 |
| [Issue, return and revalue original FIFO cost layers](03-fifo/README.md) | 4,158 | 18 |
| [Prorate earned service against a paid plan change](04-proration/README.md) | 1,416 | 6 |
| [Evaluate rental and rights boundaries for a named viewer](05-access/README.md) | 4,416 | 19 |
| [Apply a licensed sale royalty and recoverable advance](06-royalties/README.md) | 2,480 | 11 |
| [Recalculate qualifying gifts sponsor capacity and cash shortfall](07-match/README.md) | 1,920 | 8 |
| [Measure sponsor entitlement after a cost disallowance](08-award/README.md) | 2,000 | 9 |
| [Credit multi-component tax by returned unit](09-tax-credit/README.md) | 1,496 | 7 |

**Total coverage: 25,566 decisions.** Additional filters such as membership, organization, permissions and staff role belong in the access and workflow tests. They are not multiplied into the numerical suites when they would produce identical arithmetic.
