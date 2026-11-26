# Convert supplier cartons into outreach packs and reconcile a distribution

A church buys 24 sealed cartons at 9.00 per carton. The effective packaging agreement defines six identical outreach packs per carton. The stock-keeping unit is one pack. A separate outreach project has approval for 108 packs at the distribution site. Store purchase quantity in original cartons alongside the conversion evidence, then use whole packs as the base unit for reservation, movement, count and beneficiary handover. All packs have the same lot and carrying cost for this exercise. No tax, price markup or cash exchange applies.

## Warehouse to project

| Checkpoint | Evidence and custody | Finance |
| --- | --- | --- |
| Receive the 24 cartons | Count 24 intact cartons and confirm the six-pack edition on the purchase. One posted receipt puts 144 packs at Central. No individual has been served. | 216.00 owned inventory. Effective unit cost is 1.50 per pack. |
| Approve the distribution quantity | Authorize 18 cartons equivalent or 108 base packs. Reserve the project allocation and retain conversion version. Central physically holds 144. | An approval or reservation alone creates no cost of distribution. |
| Dispatch the 108 | Central 36, transit 108, site zero. Release or consume the physical holds once as dispatch is recorded. | Carrying values by custody are 54.00, 162.00, 0.00. Entity inventory still 216.00. |
| Site signs for physical delivery | Central 36, transit zero, site 108. Allow assistance only against signed site stock. | Values are 54.00 at Central and 162.00 at site. There is no sale, gift receipt or additional purchase. |
| Open the distribution | Bind one CommunityDistribution to the occurrence, steward, eligibility policy and an authorized mixed-identification intake. | Expenses attach to the approved fund/project only when packs are consumed under the example policy. |

Before authorizing a second shipment verify both the base quantity and the unit code. An incoming line labelled “18” with no unit has no determinable custody effect. The receiving steward returns it for clarification while retaining the original evidence.

## Handovers, spoilage and return

For the named/identified route create 24 distinct household issues of two packs and 14 distinct household issues of one pack. For the anonymous route create 25 issues of one pack under distinct operation keys with a permitted session-scoped reference. These counts describe handovers. An anonymous reference cannot establish a unique person or household across visits.

| Site activity | Base units out | Site quantity after activity | Carrying value issued |
| --- | ---: | ---: | ---: |
| Opening | 0 | 108 | 0.00 |
| 24 two-pack handovers | 48 | 60 | 72.00 |
| 14 one-pack handovers | 14 | 46 | 21.00 |
| 25 anonymous one-pack handovers | 25 | 21 | 37.50 |
| Three damaged packs inspected and authorized for disposal | 3 | 18 | 4.50 |
| Return eighteen intact packs to Central with both custody acknowledgements | 18 | 0 | 27.00 transferred |

Record 63 AssistanceIssue records linked to their distribution and stock issue action: 38 identified issues totaling 62 packs and 25 anonymous issues totaling 25 packs. Debit outreach expense 130.50 and credit inventory 130.50 for all 87 delivered packs. Before write-off, segregation of the three damaged packs changes eligibility but preserves their physical count. On approved disposal debit spoilage expense 4.50 and credit inventory 4.50. Returning eighteen moves value 27.00 back to Central with no expense or operating income.

The closing warehouse report shows Central 54, transit zero and site zero. Carrying value is 81.00. Prove 144 = 87 delivered + 3 spoiled + 54 remaining and 216.00 = 130.50 outreach + 4.50 spoilage + 81.00 inventory. The project requested and received 108 packs, distributed 87, spoiled three and returned eighteen. The donor-facing report can publish the approved number of packs delivered when its audience rules permit. The 38 identified households are distinct in this fixture; the 25 anonymous handovers cannot be added to claim 63 unique households.

## Interruptions and expected decisions

| Injection | What the operator observes | Evidence required to clear |
| --- | --- | --- |
| The current catalogue changes to eight packs per carton after delivery. | Historical input remains 24 cartons × six = 144 packs. No retrospective increase of 48 packs. | Preserve dated conversion, lot identification and original supplier document. Apply a changed pack size only to appropriately identified subsequent supplies. |
| Warehouse confirms dispatch while site receives a delayed duplicate of the same transfer message. | One 108-pack receipt and no remaining transit after confirmation. Site capacity and carrying values stay consistent. | Match transfer, source line, lot and receiving action. A second driver report is a separate observation until traced. |
| A terminal resends an identified two-pack issue after losing acknowledgement. | One handover and one two-pack issue remain. If a different quantity is submitted on the old key, return a conflict and route the amended fact for review. | Show the original acceptance and the discrepant message without revealing other recipients. |
| Two volunteers see similar anonymous descriptions. | Keep distinct genuine handovers separately and apply purpose-limited review to suspected duplicates under the policy. | Only evidence of the same physical action justifies correction. Shared presentation or family resemblance is insufficient. |
| A handover was recorded for two packs but only one was given; the pack remains at site. | Before closing, append the authorized correction with witnessed custody. From that branch, deliver 86, spoil three, return 19 and close Central at 55. | Outreach expense becomes 129.00 and ending inventory 82.50. Do not reuse the original request key as a positive second issue. |
| The returned cartons are damaged in transit. | Keep the dispatched eighteen in transit until actual arrival, segregate observed damage and obtain separate disposition. | Record actual count, location, custodian and evidence. A carrier claim or compensation does not prove that goods can be sold or distributed. |
| An external sponsor requests named recipient and eligibility lists. | Return approved aggregates at the permitted audience level. Suppress small or identifying subsets when policy requires. | Route any separately authorized case-sharing request to the case owner. Stock and expense traces can use opaque issue references. |

Use [ProjectSupply](../../implementation/ministry/ProjectSupply.md), [CommunityDistribution](../../implementation/ministry/CommunityDistribution.md), [AssistanceIssue](../../implementation/ministry/AssistanceIssue.md), [StockTransferLine](../../implementation/commerce/StockTransferLine.md) and [InventoryValuationEvent](../../implementation/finance/InventoryValuationEvent.md) to follow the handoffs.
