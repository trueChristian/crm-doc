# Payroll calendar, liabilities and correction

## Define three calendars

Work dates describe when effort was supplied. A payroll cycle groups earnings into a run. A payment calendar determines when each worker, tax authority or benefit fund should receive money. Those dates can span fiscal periods and local holidays. Define the church's pay groups, pay frequency, period boundary, cutoff for time approval, pay date adjustment for nonbusiness days, bank submission deadline, settlement country/time zone and separate remittance dates. Store the resolved pay day and payment batch date so changing a future holiday list cannot retroactively move an issued payslip.

A timesheet must identify the engagement and role, work date or interval, authorized rate class, paid units, work location, grant/cost allocation and approving supervisor. For a night shift spanning midnight, record start/end instants and local zone; apply the organization's rule for splitting work, overtime, payroll periods and public holidays. A time change that repeats or skips a wall-clock hour should yield unambiguous elapsed time. A pre-approved fixed salary can use contractual calendar or working-day proration. A term change in the middle of a cycle splits units by effective date. A worker with two compensated roles may have different rates and cost allocations and one approved payment if the employing entity/pay group permits.

## Gross-to-net input and rule sequence

1. Validate employment, termination, legal entity, currency, authority, bank destination, worker identifiers and active payroll policy at relevant dates. The salary administrator can resolve compensation issues without granting ministry leaders access to tax/bank data.
2. Load signed time, leave, contractual pay, allowances, benefit elections, deductions, overtime, garnishments under approved local rules, advances and retroactive items. Enforce annual caps and correct prior-year-to-date amounts before recomputation.
3. Compute cash earnings, noncash benefits, taxable bases per authority, employee deductions, employer charges and net payable. Each rule declares its base, order, thresholds, rounding level and whether it affects cash. A reimbursement or noncash taxable benefit can be reportable without increasing payroll cash wages. Reports expose the rule edition that produced each result.
4. Compare expected payroll to prior runs, head count, changed destinations and unusually large or negative amounts. Require approval for exceptions. Authorized signoff freezes run inputs, slips, component totals, cost allocations, liability totals and employee payout instructions.
5. Post and then settle. A pay run can be posted while a bank rejection leaves one worker's wages payable open. A new instruction requires verified destination and idempotent reissue. Remit deductions and employer amounts at their own due dates; a printed payroll register is not evidence of remittance.

## Worked cycle across a fiscal month

In this fixture ordinary time pays 12 per hour; four approved premium hours pay 18 each. All allowance is cash and taxable. Withholding is 10%, employee pension 5% and employer pension 6% of stated gross. Local legislation and rates belong to the employer's selected policy. Use one worker, one currency and standard two-place rounding without annual limits in this fixture.

| Earnings source | Work period | Computation | Amount |
| --- | --- | ---: | ---: |
| Five ordinary 8-hour shifts | March | 40 × 12 | 480 |
| Four ordinary 8-hour shifts | April | 32 × 12 | 384 |
| Four premium hours | April | 4 × 18 | 72 |
| Contractual allowance | April | Fixed | 24 |
| **Gross** | Cycle paid in April | 480 + 384 + 72 + 24 | **960** |

March ends before payroll release. To accrue incurred expense debit March wages 480 and employer benefits 28.80; credit accrued payroll 508.80. No employee bank transfer has been issued, and no individual withholding remittance has been declared in this fixture. On 1 April reverse the accrual exactly once: debit accrued payroll 508.80, credit wages 480 and benefits 28.80. If local policy instead retains an account-specific accrued breakdown, match the actual payroll to that breakdown and clear it without auto-reversal.

On the approved April run debit wages 960 and employer benefits 57.60; credit net wages payable 816, withholding payable 96 and pension payable 105.60 (48 employee + 57.60 employer). Total expense 1,017.60 across March/April; March holds 508.80 and April net expense is 508.80 after reversal. If costs are authorized 60% general and 40% outreach, gross wages are 576 and 384, employer expense 34.56 and 23.04. Total allocated cost is 610.56 and 407.04. The two shares do not create two payslips or two remittances. Grant eligibility and funding evidence must separately justify the split, including the allowance.

Debit net wages payable 816 and credit bank 816 on successful employee settlement or use payments clearing until confirmation. Withholding 96 and pension 105.60 remain outstanding until the two authorities/funds confirm payment. On eventual remittance the complete run consumes 1,017.60 of cash, assuming all obligations are settled. Before settling, the accountant can reconcile gross expense, worker bank list and liability schedule at different cutoffs. A ministry manager receives grant cost totals without payroll identifier, tax base or bank details.

## Corrections and exceptional runs

After release an independently approved time correction adds two April premium hours. Supplemental gross is 36, withholding 3.60, employee pension 1.80, employer pension 2.16 and net wages 30.60. Debit wages 36 and employer benefits 2.16; credit net payable 30.60, withholding payable 3.60 and pension payable 3.96. Cumulative totals now gross 996, employer costs 59.76, net 846.60, withholding 99.60 and pension liability created 109.56. Original and supplemental slips remain linked with attributed work periods and actual pay dates. A rerun of the corrected timesheet cannot add those hours again. Where local rules require tax recomputation on cumulative earnings, calculate the new cumulative liability less already recognized amounts, and preserve both calculations.

If an overpayment is discovered, determine the lawful recoverable amount and any amendment to withholding or benefit submissions. Record the approved recovery plan, each permitted deduction and outstanding receivable. A negative computed net never becomes a bank debit from an employee by default. A deceased or terminated worker may require a verified representative, final pay, unused leave treatment and stop of recurring deductions with restricted visibility. A beneficiary or ministry affiliation does not authorize redirection of unpaid wages.

A worker receives a taxable noncash benefit of 50 under a local policy. The software can increase that authority's taxable basis by 50 while keeping cash earnings paid unchanged; the actual withholding change depends on the effective rule. An advance repayment reduces take-home cash and clears its receivable rather than becoming church income. A late benefit remittance that incurs an external fee records the fee to its own account, leaving the employees' previously settled net and statements intact.

## Payroll desk checks

Reconcile approved timesheet hours to earnings, earnings plus employer charge to total expense, gross less cash-affecting deductions to net, net register to bank instructions, withholding and benefits to filings and bank confirmations. Check active employees with no pay, terminated engagements paid, unexpected duplicate bank destination, overlapping time, unapproved fund allocation, outlier year-to-date totals and expired rules. A rejected employee payout does not undo a settled remittance. When reporting previous tax years, present as-issued and amended values with their correct worker access. See [payroll dictionary](../../finance/payroll.md) and [recognition schedules](../../finance/recognition.md).
