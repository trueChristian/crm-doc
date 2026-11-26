# Close the first settlement

Use three transactions from church A in the opening weekend. Its fixture book uses one two-decimal currency, an unrestricted operating fund and a restricted relief fund. Numbers are in that currency. Assume no sales tax for these fixture items, an earned-on-sale recognition policy for goods delivered at the desk, and fee expense charged to the operating fund. The payment service settles these three transactions in one transfer. Opening balances are outside this workpaper. The bookstall holds at least two books at unit cost 6 before the exercise.

| Source | Owner and observed business event | Gross | Fund |
| --- | --- | ---: | --- |
| S1 | P2 buys and takes two books at 10 each | 20.00 | Operating |
| G1 | P1 gives 30 to general ministry | 30.00 | Operating |
| G2 | A giver chooses anonymous treatment for a 50 relief gift | 50.00 | Relief |

P1 and P2 share an address. The application records the 20 sale to P2 and the 30 gift to P1. The 50 has no named donor. No adjustment to the membership register is needed. The provider withholds 3.00 in fees from the batch, then deposits 97.00. After the deposit, P2 returns one unused book at the original price and the provider debits 10.00 from the bank for the refund. There is no further fee in this fixture.

## Expected posting bridge

Take debit and credit as separate positive columns. Treat provider clearing as an asset account which can carry a temporary credit amount pending the refund debit. For a church producing separate fund balance sheets, use the fund detail in the next paragraph when posting the deposit.

| Event | Debit | Credit |
| --- | --- | --- |
| S1 fulfilled and captured | Provider clearing 20.00 | Book sales 20.00 |
| Two books issued | Cost of goods sold 12.00 | Inventory 12.00 |
| G1 accepted | Provider clearing 30.00 | Unrestricted giving 30.00 |
| G2 accepted | Provider clearing 50.00 | Restricted relief giving 50.00 |
| Deposit confirmed | Bank 97.00 and fee expense 3.00 | Provider clearing 100.00 |
| One refund confirmed | Sales returns 10.00 | Provider clearing 10.00 |
| Returned copy inspected and restocked | Inventory 6.00 | Cost of goods sold 6.00 |
| Bank debit matched | Provider clearing 10.00 | Bank 10.00 |

For the deposit, the operating fund debits bank 47 and fee expense 3 against its clearing credit of 50. Relief debits bank 50 against its clearing credit of 50. Assign both movements of the book, the return and the later refund debit to operating. Each fund balances at every posting event. Exactly one owner posts each cash movement even if several departments receive the same observation.

## Reconcile independently

| Evidence | Expected change from opening position |
| --- | --- |
| Bank | Operating +37.00, relief +50.00, combined +87.00 |
| Provider clearing | Zero in each fund after the refund debit |
| Inventory | One fewer saleable copy overall, carrying value down 6.00 |
| Store results | Gross book sales 20.00, returns 10.00, net sales 10.00, net cost 6.00 |
| Giving register | Two gifts totalling 80.00; one named gift 30.00, one anonymous restricted gift 50.00 |
| Operating net activity | Giving 30.00 + net sales 10.00 − net cost 6.00 − fees 3.00 = 31.00 |
| Relief net activity | 50.00 still restricted and unspent |
| Control across funds | Net assets rise 81.00, equal to bank increase 87.00 less inventory decrease 6.00 |

A donation statement available to P1 shows 30.00. A customer receipt available to P2 shows the original sale and subsequent refund. A supervisor discloses neither to the other adult merely because both use E1. A public fundraiser can use an authorized aggregate without identifying the anonymous donor. The refund has no effect on gift totals.

[Order lifecycle](../../commerce/orders.md) · [Stock movements](../../commerce/inventory.md) · [Settlement and disputes](../../commerce/settlement.md) · [Giving](../../finance/giving.md) · [Book controls](../../finance/controls.md)
