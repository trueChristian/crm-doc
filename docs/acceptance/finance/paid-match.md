# Return after a fully paid sponsor match

A sponsor offers one unit per eligible unit, capped at 150 across the offer and 100 per giving party. Apply the cap in accepted receipt order. On a qualifying return within the review period, recompute the queue using the original order and remaining eligible amounts. Signed terms require repayment of excess sponsor cash after the queue clears. This book recognizes gifts on receipt. There is no receivable for a verified but unpaid match.

## Configure and capture

| Record | Fixture identity and field decisions |
| --- | --- |
| [Offer](../../implementation/development/MatchOffer.md) | M concerns one appeal, one currency and a closed eligibility window. Store match_rate 1, cap 150, per_donor_cap 100, the queue/reversal rule and signed evidence. Sponsor receipts cannot qualify. |
| [Qualification](../../implementation/development/MatchQualification.md) | Link each source allocation to its own giving party, retain eligible_base, earned_match and decision_reason for each evaluation. The original three donor receipts belong to three different parties. |
| [Attribution](../../implementation/finance/MatchAttribution.md) | Finance and development refer to the same offer and qualifying portion. Link each actually paid portion to the one sponsor gift. The two projections may never post independently. |
| [Appeal credit](../../implementation/development/AppealAllocationCredit.md) | All four actual gifts are fully allocated to this appeal. One party withholds permission for recognition. The public snapshot shows an aggregate. |
| [Giving statement](../../implementation/finance/GivingDocument.md) | Each identified remitter has their own giving party. A replacement references its own earlier document through replaces_id. Sponsor and ordinary donor are independent recipients. |

A gives 95, then B gives 75 and C gives 20. M admits 95, 55 and zero against its cap. The sponsor pays 150. Freeze the first received-cash snapshot at 340. A subsequently receives an authorized full return of 95. All three transactions still fall in the policy's review period. The new queue awards zero, 75 and 20. B absorbs 20 and C absorbs 20 of the 95 released by A. No further qualified donors remain. Record 55 excess sponsor cash and return it after approval.

## Post the events

| Entry | Debit | Credit | Amount |
| --- | --- | --- | ---: |
| M1 | Bank | Ordinary gifts | 95.00 |
| M2 | Bank | Ordinary gifts | 75.00 |
| M3 | Bank | Ordinary gifts | 20.00 |
| M4 | Bank | Sponsor gifts | 150.00 |
| M5 | Ordinary gifts | Bank | 95.00 |
| M6 | Sponsor gifts | Sponsor refund payable | 55.00 |
| M7 | Sponsor refund payable | Bank | 55.00 |

M5 includes confirmed repayment to A. M6 is the accepted sponsor adjustment before payment, while M7 is its bank settlement. Preserve a positive record of each original receipt plus a linked adjustment. The match recalculation itself produces no bank movement.

| Measure | M4 | M5–M6 | M7 |
| --- | ---: | ---: | ---: |
| Ordinary cash retained | 190 | 95 | 95 |
| Qualifying sponsor support earned and retained as income | 150 | 95 | 95 |
| Sponsor cash held, including excess awaiting repayment | 150 | 150 | 95 |
| Liability to sponsor | 0 | 55 | 0 |
| Actual bank balance | 340 | 245 | 190 |
| Net eligible contributions | 340 | 190 | 190 |

The corrected giving statements show A zero net, B 75, C 20 and sponsor 95. For an as-of report that separates cash movement from net cleared support, show 245 bank at M6 and explain the 55 refundable balance. Recompute any goal using its published measure and cutoff. Rendering the 340 historical snapshot uses its original edition.

## Verify adverse paths

| Attempt | Required evidence and result |
| --- | --- |
| Replay M4 after the three qualification links are written | One sponsor gift at 150, one bank receipt, original cap consumption 150. Summing the linked gift header once per attribution would incorrectly report multiple receipts. |
| Process two requests for A's return concurrently | Only one confirmed economic return of 95 and one revised evaluation set. A second return request sees zero refundable balance. |
| Retry the recalculation after B's new share is proposed but before C's portion is applied | The operator sees a pending computation or one completed revision. The published result can never show a mixed 95 removed from A with the other two proportions only partly applied. |
| An operator tries to pay the sponsor before the waiting donors are evaluated | The provisional 95 released capacity cannot authorize the outgoing payment. The final verified payable is 55. |
| A donor opens another household's match receipt through a common appeal | Return only the caller's authorized donor statement. The sponsor can receive the aggregate match reconciliation under the instrument without individual donor identities. |
| Duplicate bank advice arrives for M7 | Attach it to the existing repayment evidence or flag ambiguous matching. Bank remains 190 and sponsor payable zero. |
