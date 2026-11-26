# Match two deliveries, one counter sale and a late freight bill

The bookstall orders 24 copies of one workbook at 8.00 per copy. The supplier sends two deliveries, invoices the original order in full and separately charges freight after an event sale. Use a perpetual, single-currency book with receipt accrual, exact matching, unit-based freight allocation, zero tax and two open periods. Ownership passes only on acceptance. The buyer may cancel open units with supplier confirmation. Receipt clerks, buyer, bill reviewer, cashier and payment releaser are separate operators.

## Receive and match

| Action | Stock and purchasing observation | Finance observation |
| --- | --- | --- |
| Approve order B24 and send it to the supplier | One issued purchase order for 24. The warehouse has zero saleable units. | Open encumbrance is 192.00 under the fixture's order-stage policy. No inventory or bill posting. |
| Delivery A arrives with fourteen copies. Twelve pass. Two are refused at the door and leave with the driver. | Receipt A records arrived 14, accepted 12, quarantined 0 and refused 2. Movement A puts 12 units in the shop. Purchase B24 has 12 accepted, 12 outstanding. | Goods receipt A records 12 accepted and two rejected. Debit inventory 96.00 and credit receipt clearing 96.00. Remaining encumbrance is 96.00. |
| Delivery B contains ten acceptable copies. | Receipt B records ten accepted, no refusal. Both receipts point to the same purchase line and retain separate delivery identities. Total accepted 22. | Debit inventory 80.00 and credit receipt clearing 80.00. Remaining commitment 16.00 covers two units. |
| Supplier invoices 24 at 8.00 with the original packing slip attached. | Retain the refused evidence. Both refused copies remain outside custody. | Record the supplier's claim for 192.00 on hold. At zero tolerance only 176.00 is matched. The fixture requires a corrected invoice before posting any portion. |
| Buyer documents supplier agreement to cancel the final two units. Supplier replaces its claim with a bill for 176.00 and withdraws the earlier claim. | Close the two-unit remainder with its reason and version. Orders retain original ordered quantity 24 and final accepted 22. | Release remaining commitment 16.00. Retain both documents with the resolution and mutual reference. Post debit receipt clearing 176.00, credit payables 176.00 once. |

A discrepancy clerk must be able to show how 14 arrived at the door and 12 reached the bin. Entering the refused two as both opening inventory and a subsequent write-off would misstate throughput and loss. The receiving handoff contains purchase line, delivery line, accepted/rejected quantities, stock movement and inspection evidence. A changed carrier receipt number alone cannot change the accepted quantity.

## Sell, allocate freight and close

At the event counter, sell seven units from the first received lot for 14.00 each. Under this fixture the cashier records net tender and the customer takes the books immediately. Debit cash 98.00 and credit sales 98.00. Issue seven at their recorded cost of 8.00, debiting cost of sales 56.00 and crediting inventory 56.00. Available quantities after handover are five from A and ten from B. There are no open holds or safety stock.

In the next period the carrier bills 22.00 for carriage of all 22 accepted copies. Finance verifies the charge, assigns it on units across the two cost layers and has authority to adjust prior sales cost in the current open period. A prepaid customer order, identical barcode or current list price does not establish that a unit was shipped. Use the actual seven posted issues and their original stock cost applications.

| Cost layer | Received | Carriage assigned | Delivery expense adjustment | Increase to inventory |
| --- | ---: | ---: | ---: | ---: |
| A | 12 | 12.00 | 7.00 | 5.00 |
| B | 10 | 10.00 | 0.00 | 10.00 |
| Total | 22 | 22.00 | 7.00 | 15.00 |

Post debit cost of sales 7.00 and inventory 15.00, credit carrier payable 22.00. The freight creates no physical movement. Settle the 176.00 merchandise bill and the 22.00 carriage bill once to their respective payees. Treasury records 198.00 outbound, the payables for these two items return to zero and receipt clearing stays zero.

| Observation | Before carrier bill | After carrier bill and settlement |
| --- | ---: | ---: |
| Owned units at counter | 15 | 15 |
| Inventory control | 120.00 | 135.00 |
| Cumulative cost of the seven sale units | 56.00 | 63.00 |
| Sales revenue | 98.00 | 98.00 |
| Margin before other expenses | 42.00 | 35.00 |
| Capitalized receipts plus carriage assigned | 176.00 | 198.00 |

## Perturb the handoffs

- Interrupt immediately after finance accepts delivery B and before stock receives acknowledgement. Replay B. Follow its original receipt and journal link. The two physical receipts still total 22 and merchandise accrual is 176.00. A receipt marked as B that now asserts eleven accepted units enters conflict review.
- Put an unsupported extra unit on the freight allocation and try to apply 23.00 against the 22.00 charge. Reject approval with the 1.00 difference. Both layer balances and the carrier payable retain their previous values.
- Send the cashier the supplier bill as an attachment to an event sale. The cashier view can trace seven sold and the selling price. The payee destination, freight invoice and independent payment approval are restricted to the authorized finance roles.
- Run the sale-day report again after carrier settlement. Reproduce its 120.00 stock value and 56.00 cost as recorded at that cutoff. The next period displays the dated 7.00 catch-up and 15.00 stock increase.
- Reuse the corrected supplier invoice number for a second delivery claim. Duplicate screening presents the supplier-specific match to the reviewer. A genuine delivery needs its own authorized receipt and uncovered purchase quantity.

Trace the handoffs through [StockReceiptLine](../../implementation/commerce/StockReceiptLine.md), [GoodsReceiptLine](../../implementation/finance/GoodsReceiptLine.md), [SupplierBillLine](../../implementation/finance/SupplierBillLine.md), [StockCostApplication](../../implementation/finance/StockCostApplication.md) and [LandedCostAllocation](../../implementation/finance/LandedCostAllocation.md).
