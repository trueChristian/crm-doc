# Collect, dispute and reconcile

Use the [67.51 basket](quote-calculation.md). The buyer pays 20.00 using previously issued store credit and 47.51 by card. Store credit is an existing church liability. In this fixture it can purchase merchandise, but cannot fund the gift or be cashed out. Assume all merchandise and delivery obligations complete on the day used in the recognition example. Finance would defer the corresponding revenue for any undelivered obligation. Keep the tender allocation pattern displayed to the operator reproducible.

| Order purpose | Gross | Credit consumed | Card captured |
| --- | ---: | ---: | ---: |
| Workbook | 29.08 | 20.00 | 9.08 |
| Audio | 15.75 | 0.00 | 15.75 |
| Journal | 11.68 | 0.00 | 11.68 |
| Delivery | 3.00 | 0.00 | 3.00 |
| Voluntary gift | 8.00 | 0.00 | 8.00 |
| Total | 67.51 | 20.00 | 47.51 |

## Collection and allocation protocol

1. Checkout supplies the accepted quote, order, organization, buyer proof, terms, tender restriction and due balances. Open two distinct PaymentAttempts. The held 20 credit can be reserved for this order before collecting the remaining amount. Expose reserved and spendable balances on the wallet. A guest who knows a receipt number alone cannot see either.
2. Authenticate the processor's capture notice and reconcile its account, reference, currency, amount and order before applying it. Store occurrence time and observation time separately. Authorization alone does not fulfill a capture requirement. A duplicate event ID is a replay. A new event ID describing the already-known capture also cannot duplicate settlement.
3. Convert the 20 credit reservation exactly once to a CreditMovement and apply 47.51 through the frozen TenderAllocations. Recheck that the total is 67.51 and that no gift amount is funded from a prohibited method. If the card fails, leave the order explicitly partially funded or restore the hold under the accepted timeout policy. A later verified success follows the late-payment exception policy.
4. Emit independent handoffs for digital access, physical fulfilment, the 8 gift and finance. A paid indicator is insufficient evidence for any specific child record. Downstream consumers accept line/unit amounts once per source action and return their authoritative identifiers. Print one customer confirmation. Donor service independently controls any authorized gifting document.
5. When the processor fee is 1.73 and no other rows affect the payout, expect 47.51 − 1.73 = 45.78 to bank. Match the fee and capture rows separately. A payout of 45.78 alone does not prove that the capture belongs to this church or this particular order.

## Balance proof

| Event | Debit | Credit |
| --- | --- | --- |
| Complete collection and obligations under this fixture | Processor clearing 47.51, store-credit liability 20.00 | Trading revenue 52.05, delivery revenue 3.00, tax payable 4.46, contribution income 8.00 |
| Settle to bank | Bank 45.78, processing fees 1.73 | Processor clearing 47.51 |
| Approve full return of the workbook only | Sales returns 26.43, tax payable 2.65 | Refund payable 29.08 |
| Confirm both tender remedies | Refund payable 29.08 | Store-credit liability 20.00, processor clearing 9.08 |
| Processor debits bank separately for the refund | Processor clearing 9.08 | Bank 9.08 |

Inventory cost for the returned physical unit follows inspection disposition in [inventory custody](inventory-custody.md). The gift remains 8.00. Net bank movement from these events is 36.70. Processor clearing ends at zero. If the processor nets the 9.08 from a later deposit, match it to that payout item instead of recording another bank withdrawal. Restoring store credit creates one available balance for the authorized holder; restoration is not another cash deposit.

## Partial chargeback and subsequent outcome

After the workbook refund, the cardholder disputes the separately supplied journal at 11.68. The provider withholds that amount and charges a 2.50 case fee. Under the example's approved recoverable-hold policy, debit disputed funds receivable 11.68 and dispute fee expense 2.50, credit processor clearing 14.18. The reviewer associates the case with the specific card allocation. An unrelated refund of the book or a distinct giving line does not resolve the dispute. If the claim refers ambiguously to the already-refunded workbook, send settlement evidence and prohibit a second outbound remedy on the overlapping portion while under review.

| Observed result | Financial consequence | Operational consequence |
| --- | --- | --- |
| Funds restored after winning | Debit clearing 11.68, credit disputed funds receivable 11.68. If the fee is separately returned, reverse only the fee actually restored. | Close case and reconsider any suspended privileges against current rights. |
| Processor rejects evidence and retains principal | Debit the approved loss/contra-revenue account 11.68, credit disputed funds receivable 11.68. Finance separately decides any tax or credit-note correction. | Close loss, preserve evidence and communicate the approved resolution. |
| Temporary debit appears before case notification | Match issuer account and provider reference. Hold in a reviewed reconciling item until identified, then link the existing movement. | Opening the later case does not withdraw money again. |
| Case is withdrawn before financial debit | Record notice and closure. | No journal until financial movement or other recognized obligation is independently evidenced. |

## Handoff evidence and acceptance

The cashier sees tender labels, totals, status and approved next action. The treasury reviewer sees processor account, payout/item reference, settlement and source currency, amount, fee types, rate, bank line and clearing posting. The dispute worker receives order confirmation, agreed terms, fulfilment proof and necessary correspondence. A commerce case links its authoritative finance PaymentDispute. A product entitlement or private viewing history is disclosed only within separately authorized evidence scope. A sponsor, pastor or unrelated household adult gets none of these data by default.

Exercise the following in both event orders: capture before browser return and browser return before capture. Both yield one captured 47.51. Retry the handoff after finance posts but before the sender receives acknowledgement. One journal remains. Capture 47.51 in an unexpected currency and observe a review exception with no automatic fulfilment. Enter a one-cent provider adjustment without provenance and observe a visible unreconciled item with an owner. Closed status requires explained differences and matching evidence, never a forced zero.
