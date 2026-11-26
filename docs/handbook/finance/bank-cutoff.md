# Bank cutoff and foreign exchange desk

## Build the reconciliation at a fixed boundary

Choose one treasury instrument, statement currency, statement ending date/time, book accounting cutoff and posted revision. Capture the opening statement balance, ending statement balance, total credits, total debits and line count before matching. A file downloaded on the first day of a new month may contain both months. Use the bank's booked line date and verified cutoff convention, preserve transaction and value dates and visibly exclude the other period. If two statement pages overlap, deduplicate using the bank's genuine unique identifier where available and classify plausible matches for review otherwise. Two identical amounts to the same supplier may be separate valid payments.

Identify the financial owner of a statement line. A bank statement may report 200 for a deposited bag already posted, 200 of new unsolicited giving, 200 from a provider netting fees and refunds, or a transfer from the church's other account. The amount alone does not distinguish these. Expected signals include account and currency, instrument reference, deposit/transfer number, merchant settlement ID, traceable payer, date range, amount sign and remaining unmatched allocation. A match closes evidence; a new economic bank event may require posting. The interface must show which will happen before the reviewer accepts.

| Type of difference at cutoff | Ledger effect | Reconciliation effect |
| --- | --- | --- |
| Verified late deposit in books, absent from statement | No extra bank entry | Add outstanding deposit to statement balance. Confirm subsequent clearing. |
| Issued payment in books, outstanding at bank | No extra expense or bank entry | Deduct amount from statement balance. Track aging and stop/reissue if required. |
| Bank fee or interest shown only on statement | Independently authorized actual charge or interest posting | Match resulting journal to bank statement and remove book-side discrepancy. |
| Actual bank mistake supported by evidence | Record bank error as a reconciling explanation per approved policy; any recognized claim has its own journal | Track case, owner and expected correction. Never mark an unsupported matching line cleared on convenience. |
| Unidentified credit already in bank | Use verified bank amount and approved unapplied cash or suspense with review | Tie statement to recognized cash and leave attribution unresolved until evidence supports it. |
| Wrong church ledger account or fund | Post controlled correction preserving both sides and relation to source | Match only the correct account. The unrelated account's reconciliation must not be “fixed” by cross-matching. |

## Worked month and subsequent clearance

A book has recorded bank 2,000 before imports. The bank closes at 1,840. Two deposits of 200 and 60 were recorded on the last day but have not appeared. Two issued cheques of 75 and 45 are also outstanding. The bank has charged a 25 service fee and paid 5 interest. Those two transactions appear only in the statement and were absent from the 2,000 books. This fixture assumes all other items are matched.

- Adjust bank statement 1,840 + 200 + 60 − 75 − 45 = 1,980.
- Correct the books by debiting bank fees 25 and crediting bank 25, then debiting bank 5 and crediting interest 5. Corrected book bank = 2,000 − 25 + 5 = 1,980.
- Record the fee and interest match references, four outstanding items, their dates, owner and expected clearance. Closing difference is zero. A statement matching exactly to a fabricated plug of 140 would fail this test.
- In the next period both deposits clear as one bank credit 260 and both cheques clear as separate debits. With no other movements, next statement reaches 1,980. A single deposit match uses two source allocations; neither matching nor clearance creates new income or expense. Carry-forward outstanding list then empties.
- If the prior 45 cheque instead becomes stale, the original issue remains in the prior reconciliation. A stop/cancellation after bank confirmation reopens the underlying supplier liability if still owed. Reissue refers to the original and creates one new bank instrument. Outstanding money owed to a third party cannot become unrestricted church income merely because the cheque aged.

A reviewer signs the reconciliation with the exact statement and journal cutoff, unresolved but permitted timing items and any exceptions. Reopening a signed reconciliation with new bank data preserves the original and prompts review of downstream monthly cash reports. A second bank account using the same cheque sequence remains out of scope.

## Realized and unrealized FX fixture

Take a church whose base currency is B and supplier invoice is 180 units of F. Rates mean B per F. The invoice date rate is 11.25. The book uses a nonreversing closing valuation and separates realized settlement differences from period-end remeasurement. Local statutory presentation may require a reclassification of previously recognized unrealized amounts; the lifetime net result must reconcile.

| Event | Journal in B | Foreign and base open position |
| --- | --- | --- |
| Receive goods/services and recognize bill | Debit expense 2,025; credit supplier AP 2,025 | 180 F at carrying amount 2,025 B. |
| Settle 60 F at 11.50 before closing | Debit AP 675 and realized exchange loss 15; credit bank 690 | 120 F remain at historical carrying amount 1,350 B. |
| Period-end closing rate 11.75 | Debit unrealized exchange loss 60; credit AP 60 | 120 F remain, carrying amount 1,410 B. No foreign units moved. |
| Pay remaining 120 F at 11.40 | Debit AP 1,410; credit bank 1,368 and FX gain 42 | Open foreign and base liabilities both zero. |
| Entire invoice | Cash paid 690 + 1,368 = 2,058, recognized historic expense 2,025 | Lifetime net exchange loss = 15 + 60 − 42 = 33. |

Under a reversing valuation policy, the next period first reverses the 60 B revaluation exactly once. Settlement then clears 1,350 B and pays 1,368 B, recognizing a new loss of 18 B. Across both periods the two valuation movements cancel, and lifetime loss remains 15 + 18 = 33 B. Do not remeasure inventory originally acquired at historical cost merely because the unpaid foreign-currency invoice is monetary. Bank charges assessed separately in B require their own expense and never become additional foreign invoice units.

## Transfer in transit and failure

Transfer 300 between two bank accounts before a weekend, payer bank debits on Friday and recipient bank confirms Monday. A two-step policy debits transfer clearing 300 and credits sending bank, then debits receiving bank and credits clearing. A fee of 4 separately deducted from the sender debits bank charges and credits bank 4. On Friday the totals show one outstanding receivable/transit of 300 and total external fee 4; on Monday transit clears. A returned transfer credits the original sending bank and clears transit when confirmed. Do not recognize receiver cash prematurely or classify the internal movement as income. A cutoff pack identifies which balances meet the policy's cash/cash-equivalent criteria and reconciles any scope differences.

In foreign transfers retain amount and currency sent, amount and currency received, agreed/actual rate and separately charged fees. An unexpected short receipt can be an intermediary fee, rate change, unauthorized deduction or incomplete transfer. Hold unexplained amount for review rather than silently writing it to currency gain/loss. Test that matching in foreign units, cash in domestic equivalent, fees and rounding all reconcile separately. See [treasury](../../finance/treasury.md) and [closing desk](closing-desk.md).
