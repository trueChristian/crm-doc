# Endowment floor, treasury transfer and ministry disbursement

The instrument protects principal of 50,000. The church may authorize withdrawals from accumulated return up to 4% of a trailing measured base, capped by assets above the protected floor immediately before authorization. Prior draws in the same period count against the rate cap. A resolution limits this year's actual draw to 1,500 for ministry supplies. These are fixture terms rather than a generally applicable spending rule.

## Establish the position

The endowment opens with a 52,000 investment position funded by protected principal of 50,000 and accumulated return of 2,000. The operating bank has zero balance. Under this book's measurement policy the approved current position is marked to 51,800. The trailing measured base is 50,000. The rate cap is 2,000. Assets above the floor are 1,800. The applicable authorization limit is the lesser of these, 1,800. Approved_draw is 1,500, below that limit. For this fixture a sale of 1,500 at carrying value incurs no fees and realizes no additional gain or loss.

| Record | Decision |
| --- | --- |
| [Spending rule](../../implementation/finance/EndowmentSpendingRule.md) | Freeze version, effective date, authorized_rate, measurement dates, basis and reserve_floor 50,000. |
| [Draw](../../implementation/finance/EndowmentDraw.md) | Record measured_value 50,000, authorized_max 1,800, approved_draw 1,500, approval and destination. Link the actual settlement only after confirmation. |
| [Investment movement](../../implementation/finance/InvestmentMovement.md) | Retain valuation evidence for the 200 decrease and separate proceeds/cost evidence of the 1,500 sale. |
| [Treasury transfer](../../implementation/finance/TransferInstruction.md) | Keep source and destination legs. A transfer from the custody bank to operating bank is identifiable even if only one bank statement arrives on the first day. |
| [Stewardship review](../../implementation/finance/StewardshipReview.md) | Display opening principal, opening total assets, net return, authorized draw, actual draw, spending and closing endowment assets with their distinct meanings. |

## Journal

| Entry | Debit | Credit | Amount |
| --- | --- | --- | ---: |
| W0 | Investment | Opening protected principal | 50000.00 |
| W0 | Investment | Opening accumulated return | 2000.00 |
| W1 | Investment valuation loss | Investment | 200.00 |
| W2 | Custody bank | Investment | 1500.00 |
| W3 | Cash in transfer | Custody bank | 1500.00 |
| W4 | Operating bank | Cash in transfer | 1500.00 |
| W5 | Ministry supplies | Operating bank | 900.00 |

W2 settles the sale to the custody bank. W3 is the remitting bank's debit. W4 is the receiving bank's credit. On W4 move the fund attribution of 1,500 into the spendable ministry fund using the book's approved internal fund-transfer pair or reporting reclassification. If funds must balance separately, supply matching transfer-out and transfer-in dimensions without changing the entity's result. W5 is an authorized external expense. The exception check below assumes the unspent 600 stays restricted for the same ministry use.

## Checkpoints

| Measure | After W1 | After W2 | In transit W3 | After W4 | After W5 |
| --- | ---: | ---: | ---: | ---: | ---: |
| Investment asset | 51800 | 50300 | 50300 | 50300 | 50300 |
| Custody bank | 0 | 1500 | 0 | 0 | 0 |
| Cash in transfer | 0 | 0 | 1500 | 0 | 0 |
| Operating bank | 0 | 0 | 0 | 1500 | 600 |
| Entity assets | 51800 | 51800 | 51800 | 51800 | 50900 |
| Ministry supplies expense | 0 | 0 | 0 | 0 | 900 |

Endowment assets after W4 are 50,300. The instrument floor has headroom of 300 after distribution. Cumulative capital plus retained return plus the unspent ministry distribution equals closing entity assets of 50,900. The current entity result is a 200 valuation loss plus 900 ministry expense, a decline of 1,100 from the 52,000 opening. The sale at carrying value and internal transfer have zero effect on this result.

## Boundary probes

| Attempt | Outcome |
| --- | --- |
| Request a second 400 draw based only on the 500 unused theoretical rate cap | Current room above principal is 300 and the current resolution is fully used. Approve zero until additional valid authority and a current recomputation exist. |
| Submit W2 a second time when the custody advice appears on the statement | Match the one sale settlement. Endowment holdings after sale stay 50,300 and custody bank cannot increase twice. |
| A ministry volunteer buys 700 after an initial payment of 900 | Only 600 of the distributed 1,500 remains. The additional 100 requires another approved funding source. |
| Manual journal moves the 600 balance to general use at year-end | The signed purpose still applies. Keep the balance identifiable or obtain the applicable disposition authority before release. |
| Discover before posting W2 that current holdings are worth 49,700 | Revalue and recalculate under the instrument. Floor headroom is zero, release is blocked and the earlier draw decision is retained for review. |
| Reviewer attempts to count W3 as a 1,500 grant to the ministry and W5 as another 900 grant | The entity reconciliation identifies the internal transfer on both legs and recognizes one external expense of 900. |
