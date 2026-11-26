# Finance decision fixtures

These are finite numerical acceptance cases for finance workflows. Each case fixes one transaction or one cutoff and states the expected journal components, open obligation, balance or control decision. Select a family, then the specific policy profile. Each profile is independently readable and states its own assumptions. Values are examples, never statutory tax or payroll rates. The [finance handbook](../../handbook/finance/README.md) explains the actors, evidence and notifications surrounding these decisions.

| Decision family | Inputs that vary | Cases |
| --- | --- | ---: |
| Fund Claims | Eligible cost, exclusions, claims already credited and real award ceilings | 3,072 |
| Exchange Settlement | Transaction magnitude, partial foreign units, first settlement rate and valuation rate | 3,072 |
| Processor Settlements | Gross, refund, remaining principal disputed, reserve, fees, releases and dispute disposition | 3,072 |
| Payroll Portions | Ordinary and premium hours, remaining contribution caps and taxable noncash inputs | 3,072 |
| Service Periods | Service start relative to cutoff, term, contract amount and actual inclusive stop date | 3,072 |
| Tax Reversals | Sub-cent tax bases, quantities, independent second line and fraction of original line credited | 3,072 |
| Bank Matching | Instrument amounts, independent source/statement cutoff states, posting errors and bank adjustments | 3,072 |

## Select a policy profile

### Fund Claims

- [Unrestricted cost share permitted by a purpose-limited gift](fund-claims/purpose-gift.md)
- [Sponsor reimburses one half of qualifying net costs](fund-claims/sponsor-match.md)
- [Grant reimburses four fifths of qualifying net costs](fund-claims/cost-sharing.md)
- [Repair initiative covers eligible costs above an agreed deductible](fund-claims/excess-insurance.md)
- [Partner pays three quarters after a 12.50 first-loss share](fund-claims/partner-share.md)
- [Emergency award has a separate per-invoice reimbursement limit](fund-claims/capped-relief.md)
- [Training award covers two thirds to a 150 item limit](fund-claims/training-waiver.md)
- [Shared outreach award contributes 90% after a 10 deductible, limited to 240](fund-claims/matched-overhead.md)

### Exchange Settlement

- [Supplier payable, carry valuation forward](exchange-settlement/payable-held.md)
- [Customer receivable, carry valuation forward](exchange-settlement/receivable-held.md)
- [Supplier payable, reverse valuation once](exchange-settlement/payable-reverse.md)
- [Customer receivable, reverse valuation once](exchange-settlement/receivable-reverse.md)
- [Low quote foreign payable and functional-cent rounding](exchange-settlement/small-unit-payable.md)
- [Low quote foreign receivable with auto reversal](exchange-settlement/small-unit-receivable.md)
- [High quote foreign payable and reversal threshold](exchange-settlement/large-unit-payable.md)
- [High quote foreign receivable across both cutoffs](exchange-settlement/large-unit-receivable.md)

### Processor Settlements

- [Gross capture, retained fees and open dispute](processor-settlements/standard.md)
- [Confirmed refund earns a proportional processor fee credit](processor-settlements/fees-returned.md)
- [Settlement includes a release from an earlier reserve](processor-settlements/reserve-release.md)
- [Provider later returns the principal of a won dispute](processor-settlements/recovered-dispute.md)
- [Provider confirms a previously provisionally withdrawn dispute lost](processor-settlements/lost-dispute.md)
- [Won dispute and pre-existing reserve release](processor-settlements/won-plus-release.md)
- [Donor platform with zero fixed capture fee and retained dispute cost](processor-settlements/gift-platform.md)
- [Ticket platform with returned proportional fee and timed reserve release](processor-settlements/ticket-platform.md)

### Payroll Portions

- [Hourly work and ordinary taxable benefits](payroll-portions/ordinary.md)
- [Employee pension reduces withholding base](payroll-portions/pretax-pension.md)
- [Fixed taxable cash allowance and unit supplements](payroll-portions/cash-allowance.md)
- [Double-time supplement and pension relief](payroll-portions/holiday-pay.md)
- [Sessional church worker with a transport allowance](payroll-portions/stipend-hours.md)
- [Higher band flat-rate acceptance fixture with deductible pension](payroll-portions/upper-rate.md)
- [Part-time cover with low noncash benefit threshold effects](payroll-portions/part-time.md)
- [Event worker with separate cash preparation allowance](payroll-portions/event-worker.md)

### Service Periods

[How to read recognition cutoffs and lifetime projections](service-periods/README.md)

- [Insurance coverage and nonleap February](service-periods/insurance-february.md)
- [Purchased licence on a leap-year close](service-periods/licence-leap.md)
- [Facility service contract at year end](service-periods/maintenance-year-end.md)
- [Advance mission housing at a 30-day quarter end](service-periods/missions-housing.md)
- [Stand-ready digital access at a 31-day month end](service-periods/sermon-subscription.md)
- [Training coverage at a nonleap February close](service-periods/retreat-service.md)
- [Continuing venue access at fiscal year end](service-periods/venue-subscription.md)
- [Learning membership across a leap February close](service-periods/learning-leap.md)

### Tax Reversals

- [Single sales tax rounded on each unit](tax-reversals/single-unit.md)
- [Single sales tax rounded by invoice line](tax-reversals/single-line.md)
- [Single tax on document with largest-remainder allocation](tax-reversals/single-document.md)
- [Two independent taxes on net, line-rounded](tax-reversals/parallel-line.md)
- [Independent document taxes and original-line credits](tax-reversals/parallel-document.md)
- [Second tax on net plus rounded first tax, by unit](tax-reversals/compound-unit.md)
- [Second tax on net plus first tax, by line](tax-reversals/compound-line.md)
- [Compound document taxes with component allocation](tax-reversals/compound-document.md)

### Bank Matching

- [Operating bank monthly cutoff](bank-matching/monthly-checking.md)
- [Year-end bank service fee and dated outstanding cheques](bank-matching/year-end-fee.md)
- [Reserve savings with interest earned at cutoff](bank-matching/savings-interest.md)
- [Mobile wallet payout and monthly wallet fee](bank-matching/wallet-charges.md)
- [Confirmed duplicate bank debit subject to external correction](bank-matching/duplicate-debit.md)
- [Confirmed bank credit belonging to another party](bank-matching/excess-credit.md)
- [Investment cash account with fee and interest posted together](bank-matching/interest-fee.md)
- [Bank short-credits a verified deposit at period cutoff](bank-matching/transfer-error.md)

## Coverage and verification

Each profile crosses six representative underlying amounts or service starts with four settings for each of three independent operational inputs. Values are selected to exercise real boundaries such as fractions of a foreign unit, cost exceeding an award, a zero cap, one cent of bank variance, a leap-day cutoff or a partial credit on a document-rounded component. The decision tables contain 21,504 independent cases across 56 policy profiles. Each profile contains 384 cases. The same underlying transaction may produce different results under different documented policies. IDs are stable within their profile.

Acceptance requires both matching individual outputs and reconciling invariants: fund entitlement less prior claims and award ceiling, lifetime foreign exchange result versus total cash and original carrying value, processor gross to payout and later recovery, gross payroll to bank and liabilities, consumed service plus refund plus carrying amount, original tax components minus credit, and two-sided bank reconciliation. Every fixture was independently recomputed from its published input columns and verified against its balancing equation. These finite cases complement the narrative failure, permission, replay and jurisdiction scenarios; they do not certify a specific church policy or prescribe a legal treatment.
