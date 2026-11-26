# Donated stock and consigned stock at the same counter

At a church conference a donor gives ten copies of a booklet. The independent valuation accepted by finance is 4 per book. A publisher delivers six other books on consignment. The church acts as agent for these and retains 20% of the publisher's 15 selling price. The church sells its own title at 9. Both groups occupy the same physical shelf. There are no fees, taxes or opening goods in this fixture.

## Configure ownership before counting

| Record | Decision |
| --- | --- |
| [Gift offer](../../implementation/development/GiftOfferAssessment.md) and [in-kind gift](../../implementation/finance/InKindGift.md) | Accept title to ten books, attach valuation evidence and record quantity 10, valuation 40 and recognized true. A permitted donor document describes the accepted goods; its wording follows document policy. |
| [Consignment](../../implementation/finance/ConsignmentAgreement.md) | Record the publisher as owner of six units, the agency basis, 20% commission, return provisions and settlement at the end of the conference. |
| [Stock layer](../../implementation/finance/StockCostLayer.md) | Create one owned layer for ten units and total_cost 40. Three of the publisher's six are sold initially. Their physical movements leave the church's owned inventory control unchanged. |
| [Stock application](../../implementation/finance/StockCostApplication.md) | Link each owned delivery or giveaway to this layer. An accepted resaleable return recovers the actual 4 issued against that returned unit. |
| [Publisher settlement](../../implementation/finance/ConsignmentSettlement.md) | For the closing settlement, retain sale and return identities, gross collections, commission, supplier due and remittance evidence. |

One customer buys four owned books and three publisher books. Payment is 4 × 9 + 3 × 15 = 81. The next day the same customer returns one resaleable copy of each and receives 24. A ministry later gives away two owned books under an approved reading programme. The publisher's unsold books remain in custody.

## Journal

| Entry | Debit | Credit | Amount |
| --- | --- | --- | ---: |
| B1 | Owned inventory | In-kind contributions | 40.00 |
| B2 | Bank | Owned book sales | 36.00 |
| B2 | Bank | Publisher payable | 36.00 |
| B2 | Bank | Commission income | 9.00 |
| B3 | Cost of owned sales | Owned inventory | 16.00 |
| B4 | Owned book sales | Bank | 9.00 |
| B4 | Publisher payable | Bank | 12.00 |
| B4 | Commission income | Bank | 3.00 |
| B5 | Owned inventory | Cost of owned sales | 4.00 |
| B6 | Reading ministry supplies | Owned inventory | 8.00 |
| B7 | Publisher payable | Bank | 24.00 |

B4 is one authorized customer refund against two order lines. B5 restores one saleable unit to the original owned layer. The consigned return restores the publisher's physical custody balance separately. B7 pays the publisher after both return lines have been confirmed.

| Control | Receipt | First delivery | After both returns | Close |
| --- | ---: | ---: | ---: | ---: |
| Owned units in custody | 10 | 6 | 7 | 5 |
| Publisher units in custody | 6 | 3 | 4 | 4 |
| Physical shelf count | 16 | 9 | 11 | 9 |
| Owned inventory asset | 40 | 24 | 28 | 20 |
| Publisher payable | 0 | 36 | 24 | 0 |
| Bank | 0 | 81 | 57 | 33 |

At close, owned net sales are 27 and cost of owned sales is 12. Publisher gross collections net of returns are 30, of which 24 were remitted and 6 retained as commission. In-kind income 40 plus net sales 27 plus commission 6 less cost 12 less giveaway 8 yields 53 net assets. Bank 33 plus owned stock 20 equals 53. The appeal's cash goal receives zero from the original in-kind gift. If its policy admits goods, its separately labelled goods measure can show ten donated units.

## Fault cases

| Change | Observable result |
| --- | --- |
| Receiving operator scans the same consignment slip a second time | Publisher units in custody stay six at intake. No contribution or cost layer is created for these units. |
| The cashier marks a refunded consigned book as owned | Reject the mismatch between order line, owner and receiving return. The owned 4 recovery applies only to the originally owned copy. |
| The owned return is unsaleable instead of resaleable | Isolate it from available units. If the approved valuation is zero, separately show the return cost recovery and write-down (or equivalent traceable net treatment). Closing saleable owned units four, owned stock 16, bank 33, net assets 49. |
| Two clerks attempt to settle publisher balance concurrently | A single approved 24 remittance consumes that settlement balance. Independent evidence can confirm execution without creating another B7. |
| A stockroom user opens the gift-origin link | The user can see source classification, owned quantity and lot. The gift's donor identity, valuation approval notes and donor document each require their own authority. |
