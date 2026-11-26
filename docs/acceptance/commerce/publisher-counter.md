# Sell church and publisher copies at the same event counter

A publisher leaves ten copies of a booklet. The church already owns three copies with the same retail identifier, each carried at 9.00. Under the fixture's approved agency agreement the publisher retains title to its copies until sale. A publisher copy sells for 20.00, of which the church earns 6.00 and owes the publisher 14.00. The church also charges 20.00 for each owned copy. Inventory and settlement use distinct lots even though visitors see the same description. Sales are cash, tax is zero and the church may accept an eligible intact return after the original period closes.

The publisher statement covers confirmed handovers by source sale, original lot and the approved return terms. Use separate permissions for counter custody, settlement review and authorization of cash movements. Start operating cash movements at zero for ease of reconciliation. Any float is recorded and tracked separately.

## First event and publisher remittance

1. Check in ten units into the supplier-owned lot P, and identify the three existing units as church-owned lot C. The event shelf holds 13. The church inventory control holds 27.00 for three C units. Receipt of ten P units creates no church purchase, supplier payable or donated stock.
2. At the counter sell five from P and one from C with handover at payment. Tender totals 120.00. The source data must identify which five units were sold under the publisher contract even if their order lines share the same product variant.
3. Debit cash 100.00, credit publisher payable 70.00 and commission income 30.00 for the P units. Debit cash 20.00 and credit book sales 20.00 for the C unit. Debit cost of sales 9.00 and credit owned inventory 9.00. The counter now holds five P units and two C units.
4. Close statement S1 for the five publisher sales. It shows gross collections 100.00, commission 30.00, tax 0.00 and publisher due 70.00. Remit the 70.00 and identify the completed disbursement on S1. Keep the church-owned sale out of S1.
5. Obtain the remaining custody sign-off at cutoff. Seven units are on the shelf, comprising five held for the publisher and two owned by the church. Carrying value is 18.00. Retain S1 as issued.

## A return after the publisher was paid

The next event begins with S1 closed. One purchaser returns a documented publisher copy in saleable condition and receives the agreed 20.00 cash refund. Two different buyers then purchase two P copies at the same price. The contract permits a credit on the next settlement and the fixture uses a publisher receivable while no new payable is available.

| Action | Custody | Monetary effect |
| --- | --- | --- |
| Approve and inspect the identifiable returned P copy | P increases from five to six after inspection releases it. C stays at two. | Debit commission returns 6.00 and amount recoverable from publisher 14.00, credit cash 20.00 upon repayment. The owner sales report references the original sale on S1. |
| Hand over two additional P copies | P decreases to four. Church-owned inventory remains two copies. | Debit cash 40.00, credit publisher payable 28.00 and commission income 12.00. |
| Prepare S2 and prove entitlement to offset | One returned P unit and two new P sale units are individually traceable. | Gross new collections 40.00 less 20.00 return is 20.00 net. Church share 12.00 less 6.00 is 6.00. Publisher portion 28.00 less recoverable 14.00 is 14.00. |
| Apply the credit and remit S2 | No stock change. | Debit publisher payable 14.00 and credit publisher recoverable 14.00 for authorized offset. Debit publisher payable 14.00 and credit cash 14.00 for remittance. |

The physical roll-forward for P is 10 received less five sold plus one returned less two sold, closing at four. C closes at two and 18.00. Lifetime publisher net sales are six copies and 120.00. S1 plus S2 remit 84.00 and earn 36.00 commission. Including the owned sale, net customer collections are 140.00, net cash retained after remittances is 56.00, and gross margin before other expenses is 47.00 (36.00 commission plus 20.00 owned revenue less 9.00 owned cost).

## Control failures

| Injected problem | Required outcome |
| --- | --- |
| Return desk scans the shared cover identifier but has no original receipt or lot evidence. | Place the observed copy in segregated inspection under the return policy. Escalate proof and owner determination. A scan cannot credit S1 or increase owned inventory value. |
| An operator edits S1 to remove the returned sale. | Preserve S1 as issued. Link the current-period return and credit through S2. The prior event report must still show its five original P sales. |
| Two desks create S2 from overlapping exports of the same sale units. | Mark those settlement items as allocated once per agreement and source action. Retrying the export resolves to the existing allocation. The second desk cannot remit a second 14.00. |
| The publisher disputes the offset before settlement. | Retain the refund and physical return, flag the 14.00 recoverable and withhold automatic netting. Pay undisputed amounts only under an approved, separately documented instruction. The subledgers show each open leg. |
| A bulk report groups C and P as church-owned. | Reconcile the physical six to recognized two units and 18.00. Flag any 4-unit overstatement for owner correction before publication. |
| Publisher asks for the entire event sales and buyer file to verify commission. | Supply only contract-scoped sale/return references, dates, units, amounts and settlement evidence. Exclude unrelated church sales, buyer details and cash-drawer identities unless separately authorized. |

Follow [StockLot](../../implementation/commerce/StockLot.md), [ReturnLine](../../implementation/commerce/ReturnLine.md), [ConsignmentAgreement](../../implementation/finance/ConsignmentAgreement.md) and [ConsignmentSettlement](../../implementation/finance/ConsignmentSettlement.md).
