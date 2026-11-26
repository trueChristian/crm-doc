# One partner, two capacities and one restricted payment file

A church receives 600 for its own relief programme and a separate 400 it must forward to a housing partner. Signed terms give the church discretion over its own programme. The partner alone decides use of the 400 held in custody and the church charges no fee. The same partner later provides an emergency housing service to an approved aid applicant. Keep the agency payable separate from the church's cost of the housing service.

## Set the authority boundary

| Record | Fixture decision |
| --- | --- |
| [Fund](../../implementation/finance/Fund.md) and [restriction](../../implementation/finance/FundRestriction.md) | Create a restricted church programme fund and a separately identified agency balance. Store signed purpose and custody evidence. Only the 600 belongs in the church's contribution income. |
| [Aid award](../../implementation/people/AidAward.md) | Independent approver authorizes up to 260 of vendor support for one private applicant. Payment goes to the verified housing partner. The award authorizes a future cost. |
| [Aid fulfillment](../../implementation/people/AidFulfillment.md) | Queue installments for verified services. Keep distinct idempotency keys, the finance reference and delivery evidence for each installment. |
| [Disbursement](../../implementation/finance/Disbursement.md) | Separate purposes for custody transfer and service invoice. Both use a verified destination and each carries its own instructions and finance authority. |
| [Adjustment](../../implementation/people/AidAdjustment.md) | Link a later authorized service credit to the specific original fulfillment and returned amount. The amended award determines whether unused authority may be reused. |

The partner invoices 220 for supported lodging. The church verifies delivery, posts the bill and pays it. It separately remits the 400 of custodial funds to the same account. On a later review the partner credits 40 for an unused night and returns it to the church. The case owner closes the unneeded support; remaining award authority expires. The original terms let the programme reuse the returned 40 for its relief purpose. The approved credit creates a partner refund receivable between approval and bank settlement.

## Journal

| Entry | Debit | Credit | Amount |
| --- | --- | --- | ---: |
| A1 | Bank | Programme contribution income | 600.00 |
| A2 | Bank | Agency payable | 400.00 |
| A3 | Housing assistance expense | Supplier payable | 220.00 |
| A4 | Supplier payable | Bank | 220.00 |
| A5 | Agency payable | Bank | 400.00 |
| A6 | Partner refund receivable | Housing assistance expense | 40.00 |
| A7 | Bank | Partner refund receivable | 40.00 |

The ministry award, supplier bill and bank release have different owners. A3 books supported cost once and A4 settles it. The fund's restriction presentation follows eligible expenditure, with a linked reversal or current reclassification of 40 as the approved policy requires. A5 settles the custodial liability and carries zero relief expense. If the bank combines A4 and A5 into one 620 debit, allocate it to both separately approved purposes under one reconciled total.

| Control | A1–A2 | After A4 | After A5 | A6 | A7 |
| --- | ---: | ---: | ---: | ---: | ---: |
| Bank | 1000 | 780 | 380 | 380 | 420 |
| Custodial amount due | 400 | 400 | 0 | 0 | 0 |
| Net church assistance expense | 0 | 220 | 220 | 180 | 180 |
| Approved refund awaiting bank | 0 | 0 | 0 | 40 | 0 |
| Church assets net of liabilities | 600 | 380 | 380 | 420 | 420 |

Verify that the board programme statement shows contributions 600, aid net 180 and available church resources 420. The custodial report shows 400 entrusted and 400 remitted. The vendor settlement shows 220 paid for services and 40 refunded. The partner received cash of 620 and returned 40, giving combined net transfers of 580. Of this, 400 was agency money and 180 was ultimately paid for services. The case's unused 80 of authorization is closed, leaving zero available for another claim under that award.

## Confidentiality and exceptions

| Actor or change | Acceptance probe |
| --- | --- |
| Care assessor | Can reconcile the 220 vendor fulfillment and 40 return to the opaque award and private case with the assessor's own grant of access. Cannot release the payment solely on the assessment. |
| Finance operator | Receives the fund, amount, approved payee, opaque award key and payment evidence. A private housing narrative or unsafe-contact note never appears in the disbursement file. |
| Development volunteer | Neither assistance nor custody creates a prospect, a testimonial, a contact permission or an individual aid-recipient giving statement. |
| Treasurer imports combined −620 bank line twice | First match allocates −220 and −400. Duplicate import leaves the match, agency liability, expense and bank balances unchanged. |
| Later remittance advice quotes only the partner's name and 400 | Require custody transfer evidence. Identical partner identities do not authorize settlement of an unrelated vendor obligation. |
| Partner's refund arrives before the approved credit is available | Hold and reconcile the bank receipt to its source, then apply the approved adjustment once. The final eligible expense and treasury cash still reconcile to 180 and 420. |
| Public publication can identify a household from location and aid amount | Withhold or combine the cells according to the approved reporting rule. Preserve the controlled internal totals for independent reconciliation. |
