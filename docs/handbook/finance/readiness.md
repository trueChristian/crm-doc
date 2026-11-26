# Financial onboarding and acceptance by church profile

## Choose the point of accountability

Define which legal entity issues receipts, owes suppliers, employs workers, owns inventory and reports to a governing body. A campus is a ministry location even when its local leader has spending authority. An independent local church may be a different legal entity even when it shares a denominational name. Finance onboarding asks how bank signatories, accounting basis, reporting calendar and accepted fund restrictions map to each book before choosing the matrix of roles. A member login or household relationship is insufficient authority to access a financial record.

Select between an opening-balance migration, full transaction history or a combination by period/document type. Obtain a signed prior close, latest statement, open AP/AR items, forward pledges or grant obligations, held deposits, stock costing, fixed assets, payroll/tax balances, fund restrictions and official document numbering. Validate legal identities and effective dates. Historical publication of aggregate annual totals alone cannot rebuild donor receipts or open liabilities. If supporting history is intentionally retained in a read-only legacy archive, document which historical questions can be answered in which place, who controls access and what evidence future reviewers can obtain.

## Profile A: a small congregation on receipts and payments

The church owns one bank account and locks Sunday collections in a counted safe before depositing. Its congregation receives a monthly receipts-and-payments summary. There are two rotating volunteer counters, a treasurer, an independent reviewer and no employees. The church has adopted a cash-basis policy for this example. A supplier invoice is tracked even when it does not qualify as cash expenditure. A grant-restricted balance is separately identified to protect its permitted use.

| Opening or first-week event | Expected result |
| --- | --- |
| Signed opening at start of month | Bank 420 and counted cash 80. Total money 500, of which youth 100 and general 400. A youth pledge of 70 is memorandum only. A documented unpaid hall invoice 90 is operationally due. |
| Deposit the opening counted cash | Bank 500, safe zero. No new offering: the 80 was already in opening money. |
| Sunday counted gifts | Receive 60 general and 40 youth cash. Cash in safe 100, bank 500, total 600. Giving received in current period totals 100. |
| Pay 70 against the 90 hall invoice from general bank | Bank 430, safe 100 and operational unpaid amount 20. March/this-period cash expenditure 70. |
| Deposit the Sunday cash | Bank 530, safe zero. Total cash unchanged. Youth resources 140, general 390. |
| Release report | Opening 500 + cash receipts 100 − cash expenditure 70 = closing 530, agreeing to bank and safe. Pledges outstanding 70 and unpaid bills 20 are supplemental schedules. |

A failed mobile signal at the service must still allow a numbered offline count and custody acknowledgement. Importing it on Monday uses the service's actual receipt date and unique source key. Re-entering the same count through the mobile interface or bank screen cannot recognize another 100. The independent reviewer verifies count sheet, deposit slip, fund split and matching statement. The sample assumes the amounts clear; an outstanding bank timing difference must instead be visible on a signed reconciliation. A volunteer leaving office loses financial access while their original signoffs remain readable.

## Profile B: a multi-campus accrual organization

Two campuses share one legal entity, bank and chart of accounts. Track campus dimensions without inventing inter-entity donations for internal budget assignments. A separate ministry body may be consolidated only if included under the approved reporting boundary. This profile has a restricted grant, two payroll cost centers, a stockroom and online sermon sales. The treasurer needs statements by campus and fund, but an employee and donor's private details are restricted to separate authorized officers.

Opening bank is 2,000, AR 300, stock 200 and equipment cost 800 with accumulated depreciation 200. AP is 350, unearned funding 150 and payroll-related liability 100. Net assets must be 2,500, comprising restricted 600 and general 1,900. Assets = 2,000 + 300 + 200 + 800 − 200 = 3,100; external liabilities = 600. Opening customer invoices of 180 and 120 support AR 300. Supplier bills of 200 and 150 support AP 350. The equipment register shows gross and accumulated values separately. Any payroll liability must reconcile to authority and due date. The 150 unearned advance is not additive to the 600 recognized restricted net assets.

| First operating event | Posting and control |
| --- | --- |
| Collect the 180 open invoice | Debit bank 180 and credit AR 180. Customer aging 120, bank 2,180. Do not report current-period sales income for this collection. |
| Settle the 200 opening supplier bill | Debit AP 200 and credit bank 200. Remaining AP 150, bank 1,980. No new expense. |
| Accept documented 50 of the unearned grant under its agreement | Debit advance 50 and credit grant income 50. Liability 100, cash unchanged. Assume the income is restricted and no release occurs. |
| Run one month of approved depreciation 20 | Debit depreciation 20 and credit accumulated depreciation 20. Equipment net 580, no bank movement. Assume depreciation enters general expense. |
| Final balances | Bank 1,980, AR 120, stock 200, equipment net 580. Assets 2,880. Liabilities AP 150, grant advance 100, payroll 100 = 350. Net assets 2,530 = general 1,880 and restricted 650. Change 30 = grant income 50 less depreciation 20. |

Test importing both open documents and signed opening balances without duplicating AR/AP; the opening-account bridge must zero. A migrated historical gift cannot trigger new receipt delivery to every donor. A department member may approve time or retrieve approved cost totals without seeing personal payroll information. A campus manager can see their ministry budget and outstanding invoices but cannot settle the other campus's bank obligations through a mistyped filter.

## Go-live decision and recovery

Define explicit control tolerances before rehearsing. Financial balance equations, document duplicates, double-applied payments, unexplained fund opening differences and unresolved privileged access are exact or policy-blocking controls. Display foreign-currency rounding only within documented thresholds to an authorized account. Allow expected timing items on bank or clearing with source, age and signoff. Summary counts alone cannot substitute for a reconciled value at each cutoff.

A dry run should compare signed totals to calculated controls, sample one donor receipt, one invoice, one return, one payroll sequence, one restricted allocation and one closed report with the actors actually expected to use them. Generate a test backup/export, restore into an isolated organization and reproduce the original balances and the exact report publication. During final cutover freeze/mark the last accepted legacy sequence, collect new activity separately, replay once and keep unaccepted items discoverable. Communicate which register is authoritative for each dated transaction. After the first live month, resolve clearing exceptions and confirm that report readers can explain prior-to-current movements without administrative access.

For the data dictionary and further acceptance examples use [cutover and handover](../../finance/cutover.md), [worked month](../../finance/worked-month.md), and [period close](closing-desk.md).
