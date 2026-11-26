# Partial award, paid draw and questioned cost

A church requests 12,000 to run a training project. A sponsor offers 9,000 as a reimbursement ceiling. Signed terms reimburse 75% of eligible costs and require the church to finance the remainder. Each submitted report must identify accepted costs, recognized reimbursement and cash collected as separate measures. All activity belongs to the same project. Opening bank is 2,000, financed by unrestricted opening net assets of 2,000.

## Arrange the records

| Owner and record | Input and constraint |
| --- | --- |
| [Application](../../implementation/development/GrantApplication.md) | Keep requested_amount at 12,000 and status at part_awarded after the decision. The finance award link is absent until authorization succeeds. |
| [Decision](../../implementation/development/AwardDecisionReview.md) | Record offer_amount 9,000, the revised scope, approver and acceptance. A declined version cannot create a ledger award. |
| [Award](../../implementation/finance/GrantAward.md) | One incoming award for 9,000, approved cost reimbursement basis, restricted to the named project and a defined service period. Terms permit repayment of a disallowed receipt. |
| [Eligible costs](../../implementation/finance/AwardCost.md) | Link services of 1,200 and materials of 400 to two posted expense journal lines. Both fall inside the eligibility window at initial review. |
| [Draw evidence](../../implementation/finance/AwardDrawItem.md) | Claim 900 against services and 300 against materials. Each item links one cost. Matching funds, proposal targets and unsigned forecasts cannot serve as an additional eligible cost. |
| [Submitted report](../../implementation/development/ReportSubmissionEdition.md) | Freeze the bundle, cost source fingerprints, approval and sponsor receipt for each revision. |

## Post the events

| Entry | Debit | Credit | Amount |
| --- | --- | --- | ---: |
| G0 | Bank | Opening net assets | 2000.00 |
| G1 | Project services | Supplier payable | 1200.00 |
| G1 | Project materials | Supplier payable | 400.00 |
| G2 | Grant receivable | Grant income | 1200.00 |
| G3 | Supplier payable | Bank | 1600.00 |
| G4 | Bank | Grant receivable | 1200.00 |
| G5 | Grant income | Refund due to sponsor | 150.00 |
| G6 | Refund due to sponsor | Bank | 150.00 |

G1 is the accepted supplier bill. At G2 the sponsor's substantive reimbursement conditions are met and the amount is collectible under the selected policy. Submission of the draw is evidence of collection activity and produces no further grant income. G4 settles the draw. Freeze sponsor report revision 1 here. At G5 the sponsor disallows 200 of services and directs immediate repayment of the already collected 75% share. The underlying services were received at the agreed price. Preserve both original expense lines. G6 is the bank-confirmed repayment.

## Checkpoints

| Measure | After paid draw G4 | Decision G5 | Repayment G6 |
| --- | ---: | ---: | ---: |
| Original requested amount | 12000 | 12000 | 12000 |
| Signed ceiling | 9000 | 9000 | 9000 |
| Recorded project expense | 1600 | 1600 | 1600 |
| Sponsor-eligible cost | 1600 | 1400 | 1400 |
| Cumulative income under the award | 1200 | 1050 | 1050 |
| Eligible church share | 400 | 350 | 350 |
| Additional cost borne solely by church | 0 | 200 | 200 |
| Grant receivable | 0 | 0 | 0 |
| Sponsor refund payable | 0 | 150 | 0 |
| Cash collected less repayments | 1200 | 1200 | 1050 |
| Book bank including opening | 1600 | 1600 | 1450 |

The service line's remaining eligibility is 1,000. Materials remain eligible for 400. Cumulative allowed portions are 750 and 300, respectively. Cost outside the award plus eligible church share equals 550, reconciling the 550 decline in bank. Income 1,050 less expense 1,600 gives the same change in net assets. Under terms that reopen disallowed capacity, unused ceiling equals 7,950. It remains contingent on future eligible costs.

## Verify exceptions and access

| Attempt | Observable result |
| --- | --- |
| Finance accepts a handoff, then development times out and retries it | Both sides resolve the original award ID. The requested 12,000 and offered 9,000 remain independently retrievable. Award count is one. |
| A second draw claims 100 against the fully claimed materials source | Payment preparation reports zero available sponsor share on that source. The new draw cannot advance with that item. |
| A coordinator edits the submitted report after G5 | Revision 1 still reports eligible expenses 1,600, recognized 1,200 and cash received 1,200. Revision 2 discloses the disallowed 200 and names the 150 repayment or liability as of its own cutoff. |
| Same sponsor decision arrives by correspondence and a later system acknowledgement | Resolve both against the decision evidence and existing revised claim. One G5 adjustment and one approved G6 repayment can settle the obligation. |
| A sponsor requests an identifiable participant roster using the financial evidence link | The sponsor edition exposes approved aggregate evidence only. Opening the internal expense or roster target requires independent permissions. |
| Someone closes the award after disallowance but before repayment | The unresolved sponsor liability and required report revision remain visible to the close reviewer. Record their settlement and submission evidence before close under these terms. |
