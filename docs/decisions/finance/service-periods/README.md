# Reading a service-period decision

Use these cases for a price paid in advance for a contracted span of daily service. A church can be the purchaser holding a prepaid asset, or the supplier holding deferred income. The case assumes the full amount settled before the earliest snapshot. The dates determine how much can move from that balance into expense or earned income, how much remains deferred, and whether a refund has become payable or receivable.

| Column | What it proves |
| --- | --- |
| Days prior / Days now | Actual inclusive days of service supplied through each observation date, capped at the agreed last service day. Both are zero before service begins. |
| Prior cumulative / Cumulative now | Cumulative monetary recognition at the prior snapshot and the current cutoff. The posting for the interval is the difference between those rounded cumulative amounts. |
| Period charge | Newly recognized expense or income within the observed interval. It is zero when coverage has not begun or was fully recognized before the interval. |
| Refund balance | A confirmed unused amount payable or receivable after the terminating event has become effective. Opening/effective dates still govern when to post it. |
| Prepaid/deferred left | Contract balance after posted recognition and any already effective refund. At cutoff it is a real carrying balance. |
| Expected lifetime at contractual stop | Projection of total recognition if service is delivered through the stated last service day. This includes future days. Before coverage begins this amount can be positive while both actual recognition columns are zero. |

## Cutoff before coverage

A 120 contract covers 60 days starting 1 March. A mutually agreed stop after 30 supplied days makes the last service day 30 March. On 28 February cash has already settled. The book holds prepaid expense or deferred income 120, cumulative recognition zero, refund balance zero and expected lifetime recognition 60. The projected 60 is not a journal. On 15 March, 15 supplied days produce cumulative recognition 30, balance 90 and no refund yet. On 30 March, cumulative recognition reaches 60, unused 60 becomes the agreed refund receivable/payable, and prepaid/deferred balance is zero. Settlement of the refund later moves the receivable/payable into cash without recognizing another charge. A change in a still-uncertain termination forecast would remain a scenario until the church has the agreement used by these fixtures.

For cent rounding, compare cumulative recognized amounts at consecutive cutoffs. Rounding a daily rate and multiplying by days can leave an incorrect final residual. Each table fixes the observation date, prior snapshot and acting role in its opening paragraph. [Return to all finance decision profiles](../README.md).
