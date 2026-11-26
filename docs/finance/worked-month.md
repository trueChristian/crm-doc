# Worked month from offering to published accounts

Use this deterministic acceptance fixture to test a single-entity accrual book. All amounts use one currency with two decimal places. The general fund opens with bank 1,000 and inventory 40, funded by opening net assets 1,040. A donor-restricted outreach fund opens at zero. The church controls both funds. Both shop lines in this fixture are taxed at an illustrative 10%, performance occurs at delivery and restricted resources stay unspent. The named accounts can map to local account codes.

## Source documents and journals

| ID | Event | Debit | Credit |
| --- | --- | --- | --- |
| M00 | Signed opening balances | Bank 1,000 and inventory 40 | Opening general net assets 1,040 |
| M01 | Recorded offering with two verified allocations | Cash in transit 400 | General contributions 300 and restricted outreach contributions 100 |
| M02 | Deposit the full collection under one slip | Bank 400 | Cash in transit 400 |
| M03 | Deliver book priced 30 and sermon access priced 20; capture total 55 | Provider clearing 55 | Book revenue 30, media revenue 20 and sales tax payable 5 |
| M04 | Deliver physical book from stock | Cost of goods sold 20 | Inventory 20 |
| M05 | Matched provider payout, fee 2 | Bank 53 and payment fees 2 | Provider clearing 55 |
| M06 | Approve full refund on digital line, tax included | Sales returns 20 and sales tax payable 2 | Provider clearing 22 |
| M07 | Provider recovers approved refund from bank | Provider clearing 22 | Bank 22 |
| M08 | Recognize approved utilities invoice | Utilities expense 90 | Accounts payable 90 |
| M09 | Pay part of utilities bill | Accounts payable 70 | Bank 70 |
| M10 | Approved payroll gross 100 and withholding 20 | Wages expense 100 | Net wages payable 80 and withholding payable 20 |
| M11 | Pay employees net amount | Net wages payable 80 | Bank 80 |
| M12 | Buy and commission qualifying equipment | Equipment cost 120 | Bank 120 |
| M13 | Record monthly depreciation, full month, 12-month life, zero residual | Depreciation expense 10 | Accumulated depreciation 10 |

Split both sides of M01 and M02 by fund for a separately balanced fund book. All other movements belong to General. The two offering allocations may represent identified and anonymous gifts respectively. Test donor statement visibility by using one identified donor for 300 and an anonymous loose offering for 100. Record the signed offering sheet, deposit slip, order lines, shipment, access grant, provider settlement, refund/revocation, supplier bill, payment instruction, pay run and asset commissioning approvals as separate sources.

## Expected closing trial balance before annual close

| Account or group | Debit | Credit |
| --- | ---: | ---: |
| Bank | 1,161 | 0 |
| Goods inventory | 20 | 0 |
| Equipment at cost | 120 | 0 |
| Accumulated depreciation | 0 | 10 |
| Accounts payable | 0 | 20 |
| Sales tax payable | 0 | 3 |
| Payroll withholding payable | 0 | 20 |
| Opening general net assets | 0 | 1,040 |
| General contributions | 0 | 300 |
| Restricted contributions | 0 | 100 |
| Book and media revenue before returns | 0 | 50 |
| Sales returns | 20 | 0 |
| Cost of goods sold | 20 | 0 |
| Utilities expense | 90 | 0 |
| Payment fees | 2 | 0 |
| Wages expense | 100 | 0 |
| Depreciation expense | 10 | 0 |
| **Total** | **1,543** | **1,543** |

Cash in transit, provider clearing and net wages payable close at zero. Verify the supplier aging lists one open balance of 20. The tax balance is 5 less the credit note of 2. The payroll liability remains 20 until separately remitted. The member giving statement is 300, the restricted fund statement includes the anonymous 100, and the public finance pack identifies no donor.

## Cross-statement tests

- Change in net assets is contributions 400 + gross sales 50 − returns 20 − cost of goods 20 − utilities 90 − fees 2 − wages 100 − depreciation 10 = **208**. Closing net assets are **1,248**, comprising unrestricted/general 1,148 and restricted 100.
- Closing assets are bank 1,161 + goods 20 + net equipment 110 = **1,291**. Closing liabilities are supplier 20 + tax 3 + withholding 20 = **43**. Assets less liabilities equal closing net assets 1,248.
- Operating cash flow is offerings 400 + net shop cash 31 − supplier payment 70 − payroll cash 80 = **281**. Net shop cash is capture 55 less fee 2 less refund 22. Investing cash flow is **−120**, financing zero. Opening bank 1,000 plus 161 equals **1,161**. Indirect check: 208 result + 10 depreciation + 20 inventory decrease + 20 AP increase + 3 tax increase + 20 payroll liability increase = **281**.
- Published balances tie to posted subledgers at the same cutoff. A reviewer can drill to two different operational actions for M06 and M07. Replaying either event does not alter the result. A reversed media entitlement is inaccessible according to the original sale terms, and M04 has no inventory reversal because the physical item was retained.
- After close, reverse a duplicate operational notice before any posting. Figures stay unchanged. If a real new adjusting entry subsequently posts into a reopened period, issue a revised pack with a distinct snapshot and preserve these original expected balances.
