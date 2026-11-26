# Opening items with money or performance still in flight

Cut over at the end of day 30 using signed opening control balances and operational documents attached as subledger evidence. The legacy book already recognized the contribution behind a 70 deposit and the full supplier bill. A 90 sponsor placement remains unperformed. Use one book, one currency, no opening inventory and no intervening activity.

## Rehearsal pack

| Evidence | Signed amount | How the new book represents it |
| --- | ---: | --- |
| Bank ledger | 600 | Statement is 670 and an old payment of 70 is outstanding. The cashbook already includes that payment. |
| Undeposited giving | 70 | Original gift is in old-period giving and the cash is in transit to a separate future deposit. The old payment and the gift deposit happen to have equal amounts. They have different origins and directions. |
| Supplier liability | 110 | Original bill 180, payment recognized before cutover 70, balance due 110. |
| Unearned sponsor performance | 90 | Original receipt already recorded in bank. Signed sponsor still awaits one 90 placement. |
| Opening net assets | 470 | Signed net position. Bank 600 plus undeposited 70 less supplier 110 and deferred 90 equals 470. |

Record the [migration](../../implementation/finance/FinanceMigration.md) cutoff, strategy and evidence. Create [opening items](../../implementation/finance/OpeningItem.md) for outstanding bank timing, open bill and deferred performance. Preserve legacy_id, original_amount and outstanding_amount where appropriate. Bind financial control detail as subledger_evidence on the [opening map](../../implementation/finance/OpeningJournalMap.md). Each open item's control portion must match its signed opening amount without posting the original event twice.

## Journal

| Entry | Debit | Credit | Amount |
| --- | --- | --- | ---: |
| T0 | Bank | Opening net assets | 470.00 |
| T0 | Bank | Supplier payable | 110.00 |
| T0 | Bank | Deferred placement income | 20.00 |
| T0 | Undeposited giving | Deferred placement income | 70.00 |
| T1 | Bank | Undeposited giving | 70.00 |
| T2 | Supplier payable | Bank | 110.00 |
| T3 | Deferred placement income | Placement income | 90.00 |

T0 is a single compound entry for the signed balances. Its paired debit and credit amounts present the balance as elementary journal lines. No semantic connection between a specific paired opening debit and credit is implied. Match the old outstanding payment to its old bank line when its statement line of −70 arrives. This verification has no new journal. T1 is a confirmed deposit that clears the 70 in transit. T2 is a new bank-confirmed payment for the balance of the existing bill. T3 posts when the promised placement is accepted after cutover.

## Bank sequence and comparison

| Statement evidence | Statement balance | Corresponding book event |
| --- | ---: | --- |
| Signed prior close | 670 | Cashbook 600, old outstanding payment 70 |
| Old payment appears at bank | 600 | Match old −70 payment without a new journal |
| New deposit appears | 670 | Match +70 to T1 |
| Remaining supplier balance paid | 560 | Match −110 to T2 |

Final cashbook and statement are both 560. Undeposited giving, supplier payable and deferred placement income are zero. Current-period placement income is 90, new contribution income is zero, current supplier cost is zero and closing net assets are 470 + 90 = 560. The current-period donor statement does not include a second 70 gift on the day the deposit reached the bank. An authorized historical statement can still retrieve the original donation as of its legacy date.

## Failures and recovery

| Injected failure | Expected resolution |
| --- | --- |
| Import the 180 face value as the outstanding liability | [Migration control](../../implementation/finance/MigrationControl.md) shows 70 excess relative to the signed 110. Reject signoff before posting. |
| Both deposit and old payment have amount 70 and a similar memo | Require sign, source, account and date evidence. A deposit cannot clear an outstanding payment. Preserve two independent match records. |
| A worker stops after T0 but before attaching the old supplier bill | Keep production acceptance pending. Retry the same opening-map keys. Attach the open item once without another 110 control posting. |
| The original sponsor cash receipt arrives again in a delayed feed | Cutoff and source identify a pre-cutover capture. Link the old item or quarantine ambiguity. Bank and current-period income remain unchanged. |
| Sponsor sends two confirmations after the placement is accepted | Link both messages to the same recognized portion. One T3 extinguishes the opening obligation of 90. |
| A board member follows the opening pack's line to a donor or supplier bank detail | Expose only the approved comparison totals and permitted evidence. Re-enter the appropriate record's authority checks before opening sensitive source documents. |
