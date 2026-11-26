# After-sale service and accounting

A return records custody, a refund records money going back, and a credit note corrects the financial document. Any one of these can precede another. Finance chooses posting dates, recognition rules, fund dimensions, rounding, exchange rates and approved accounts. Every posting request carries its source identity and approval. Corrections append linked events so that the numbers at an earlier close remain reproducible.

## Logical records

| Table | Fields | Relationships and rules |
| --- | --- | --- |
| ReturnRequest | order_id ref Order, requester_account_id ref UserAccount?, request_proof_ref opaque_ref?, opened_at instant, return_number text, reason code, state requested/approved/in_transit/inspected/resolved/declined, decision_by ref UserAccount?, due_at instant? | Unique return number. Guest requests require proof of order control. Record policy version, exception evidence and notice outcome. |
| ReturnLine | request_id ref ReturnRequest, order_line_id ref OrderLine, requested_units quantity, authorized_units quantity, received_units quantity, condition code?, outcome restock/quarantine/write_off/no_physical_return, eligible_net money, eligible_tax money, movement_id ref StockMovement?, replacement_order_line_id ref OrderLine? | Sum of authorized returns respects delivered units less earlier remedies, with approved exceptions. Returns use original discount allocations and tax basis. |
| Refund | order_id ref Order, return_request_id ref ReturnRequest?, reason code, currency code, requested_amount money, approved_by ref UserAccount?, requested_at instant, completed_at instant?, state requested/approved/submitted/part_paid/paid/failed/review | A refund may cover delivery, a digital cancellation or a goodwill payment. Determine gift treatment separately. Restrict discretionary cash refunds and approver thresholds. |
| RefundAllocation | refund_id ref Refund, order_line_id ref OrderLine, tender_allocation_id ref TenderAllocation?, original_capture_ref text?, allocated_net money, allocated_tax money, allocated_gift money, method code, execution_key text, provider_ref text?, state planned/submitted/confirmed/failed | Unique execution key. Refund through the original method up to amount captured less prior refunds and disputed sums under review. Explicit exceptions require authorization and evidence. |
| PaymentDispute | payment_attempt_id ref PaymentAttempt, processor_account_ref opaque_ref, case_number text, currency code, disputed_amount money, fee money, opened_at instant, response_due_at instant?, reason code, withdrawn_at instant?, result won/lost/withdrawn?, state opened/evidence_due/submitted/provisional/closed | Unique case per processor account. Keep financial withdrawal separate from initial notification. Freeze the overlapping remedy amount while reviewing any refund already in flight. |
| DisputeEvidence | dispute_id ref PaymentDispute, kind order/terms/dispatch/access/customer_contact, evidence_ref opaque_ref, captured_at instant, reviewed_by ref UserAccount?, submitted_at instant?, retention_until date? | Minimize disclosed material. Viewing history, pastoral or member details require specific authority and purpose. |
| ProcessorPayout | organization_id ref Organization, processor_account_ref opaque_ref, payout_ref text, payout_currency code, period_start instant, period_end instant, expected_arrival date?, gross_captures money, refunds money, fees money, dispute_debits money, other_net money, expected_net money, bank_line_ref opaque_ref?, state announced/received/part_matched/reconciled/exception | One payout per issuer/reference. One deposit may aggregate multiple payouts. Partial reconciliation uses allocations and recorded differences. |
| PayoutItem | payout_id ref ProcessorPayout, issuer_item_ref text, kind capture/refund/fee/dispute_hold/dispute_release/reserve/fx/adjustment, source_ref opaque_ref?, source_currency code, source_amount money, payout_amount_signed money, exchange_rate rate?, occurred_at instant | Unique statement item per issuer account, even when reports overlap. Signed payout amount sums to payout net. Unidentified items enter suspense for review. |
| BankPayoutMatch | payout_id ref ProcessorPayout, bank_line_ref opaque_ref, currency code, matched_amount money, matched_by ref UserAccount, matched_at instant | Prevent over-application at either endpoint. Identify separate bank fees, reserves and exchange differences. |
| CommercePosting | source_type code, source_id opaque_ref, source_action code, revision integer, currency code, accounting_date date, finance_mapping_version text, journal_entry_id ref JournalEntry?, reversal_of_id ref CommercePosting?, state waiting/posted/review/reversed | Unique organization, source, action and revision. Acknowledged entries are immutable. Finance rejects unbalanced or unmapped requests and returns the exception to its owner. |

## Worked example

Illustrative amounts are in one currency. The approved policy recognizes a 100 book sale on delivery, tax of 10 at collection, a separate unconditional 20 gift on receipt, and inventory cost 40 on delivery. The processor deducts a fee of 3. A different policy can recognize tax or gifts at another event. The input records retain distinct facts so finance can apply its own approved schedule.

| Event | Debits | Credits |
| --- | --- | --- |
| Collect 130 | Processor clearing 130 | Customer advances 100, tax payable 10, contribution income 20 |
| Dispatch and transfer control | Customer advances 100, cost of goods sold 40 | Book sales 100, inventory 40 |
| Receive net payout of 127 | Bank 127, processing expense 3 | Processor clearing 130 |
| Approve a full merchandise return after dispatch, with recoverable sales tax | Sales returns 100, tax payable 10 | Refund payable 110 |
| Inspect and restore a resaleable unit at original cost | Inventory 40 | Cost of goods sold 40 |
| Processor confirms 110 refund | Refund payable 110 | Processor clearing 110 |
| Processor draws 110 from bank as its own debit | Processor clearing 110 | Bank 110 |

The gift remains 20 and the original fee remains 3 in this example. A damaged item follows its inspection valuation instead. Where refund and processor fee net against the next payout, reconcile its items and actual bank deposit. Never book both a separate bank draw and a net deduction for the same item. An exchange is a return and a distinct replacement order linked together. Collect or refund the price difference transparently.

For an unrelated 50 dispute, a processor temporarily withholds 50 and charges a nonrefundable fee of 2. Under an approved policy tracking recoverable holds, debit disputed funds receivable 50 and dispute fee expense 2, credit processor clearing 52. On winning and receiving the 50 release, debit clearing 50 and credit disputed funds receivable 50. On losing instead, debit the approved loss or adjustment account 50 and credit disputed funds receivable 50. Finance decides whether an associated credit note, sale, tax or gift needs correction from the facts. A disputed payment is never also counted automatically as a customer refund.

## Reconciliation and acceptance

- The treasury reviewer reconciles gross sales, gifts, tax, returns, fees and timing items before comparing payout net with bank deposits. Date filters distinguish sale, collection, recognition, payout and bank dates. Closing clearing equals opening clearing plus recognized inflows less outflows and settlements, with documented reasons for unsettled items.
- Partial refunds across three equal items never return more tax or discount than was originally charged. Give the final eligible refund any residual minor unit assigned by the original policy. Preserve the allocation to gift, merchandise and each tender. A store-credit tender reinstatement increases the liability exactly once.
- Two refund workers submit the same approved allocation. One execution key yields one outgoing payment, one associated posting and one notice. An unknown response holds the case for confirmation. Chargeback arriving during that hold routes to joint review.
- A return arrives after hard close. Finance records the effective transaction date, reason, original period and authorized posting period on the credit/reversal. The previous period's published statements remain reproducible.
- A payout covers two campuses, three funds and mixed currencies. Reconcile provider item amounts in payout currency first, then trace each source-currency amount and fund/campus mapping to the journal. Unknown differences remain visible and block completion.
