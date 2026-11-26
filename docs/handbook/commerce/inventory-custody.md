# Track custody and offline stock

A central store supplies a second campus and a bookstall that may lose connectivity. A customer-facing stock figure must distinguish physically present, currently eligible to sell, already reserved, in transit, consigned and quarantined. A local seller can promise offline stock only from a bounded allocation already removed from the online pool.

## Rehearsal with quantities and costs

Begin with 10 copies in lot A at 4.00 and 8 copies in lot B at 5.00, all owned and sellable at the central store. The example uses individually traceable acquisition lots, with the selected lot driving the illustrated issue cost. Policy reserves a two-unit safety buffer at central. Other locations have no buffer. The trackable value starts at 80.00. StockMovement owns quantity. InventoryValuationEvent and StockCostApplication in finance own carrying value.

| Event | Central lot A/B | Mobile bookstall A | Transfer A | Campus East A | Consequence |
| --- | --- | ---: | ---: | ---: | --- |
| Receive both lots | 10 / 8 | 0 | 0 | 0 | Eligible central balance 18. Available to promise 16 before holds. |
| Move four A to the mobile bookstall | 6 / 8 | 4 | 0 | 0 | Central open balance drops immediately. Disconnected mobile quota is four across its authorized register(s). |
| Dispatch five A to Campus East | 1 / 8 | 4 | 5 | 0 | Transit excluded from both storefronts. Packing a box without confirming dispatch is a different state. |
| Central accepts six online holds, one A and five B | 1 / 8 | 4 | 5 | 0 | Nine physically present at central. Nine less six reserved less two buffered leaves one newly promiseable. No valuation entry for the hold. |
| Mobile sells three A while offline | 1 / 8 | 1 | 5 | 0 | Three unique issue identities travel with three sale units. Isolated mobile register can promise one more. |
| East acknowledges four good units | 1 / 8 | 1 | 1 | 4 | One unit remains in transit with named custodian and tracing deadline. |
| Authorized investigation resolves shortage as loss | 1 / 8 | 1 | 0 | 4 | Fourteen units physically held across owned locations. Three sold plus one lost plus fourteen ending equals eighteen beginning. |

Physical closing value is central 44.00, mobile 4.00 and East 16.00, totalling 64.00. The three mobile cost issues equal 12.00 and the transport loss equals 4.00. Ending value plus issues and loss equals the opening 80.00. The six reservations do not reduce total carrying value. A transfer between these locations changes custody, and finance may move location dimensions under its policy, but it cannot create a sale. A later confirmed online shipment consumes its reserved units once.

## Event contract

| Sender → owner | Required fields | Guard and recorded response |
| --- | --- | --- |
| Purchase receiving → stock | Authorized delivery reference, expected/arrived/accepted/quarantined/refused quantities, units, actual lot or serial, location, receive time, counter and inspection evidence | Reject any sums that do not reconcile. Link purchase-line receipt and each distinct movement. Unknown lot or unauthorized substitution goes to quarantine. |
| Central → offline custody | Organization, dedicated mobile location, device/register scope, allocation revision, allowed variants and physical lots, quantities, time window, custodian, starting sequence and approved tender modes | Allocate once and deduct central availability before issuing authority. If multiple devices operate disconnected, partition quota per device or use one physical/operating custodian. |
| Mobile → reconciliation | Shift identity, issue identity, source quota/revision, monotonic local sequence, physical unit, capture time, actual tender evidence, sales/returns, cash count and custody sign-off | Replay safely. Missing sequence creates an exception, never a synthetic sale. If authority expired, record actual observed custody and route unauthorized sales to review. |
| Sender → receiver | Transfer and line, origin/destination/transit, lot, unit, authorized/dispatched amount, seal where used, dispatch instant, receiving reference | Early receipt is unconfirmed evidence until matched to authorized dispatch. A receipt of six against five triggers review without fabricating a fifth or sixth origin issue. |
| Stock → finance | Immutable movement reference, source and destination, owners/fund/campus dimensions, lot, original cost revision, movement reason, actual quantity and effective date | Finance acknowledges unique event and resulting valuation/posting. Corrections link to original. Valuation outage keeps quantity visible with an unposted-value flag. |

## Count and reverse

The East steward physically counts their four units and seals the count at a declared cutoff. One unit sells locally ten minutes later. A count of four compares to the cutoff balance of four. The one subsequent sale reduces current stock to three without creating a discrepancy. If only three were found at cutoff, request recount and independent variance approval. A zero is a genuine count. A blank is uncounted. Permitting close with uncounted scoped lines requires a recorded policy exception with a recovery owner.

Two lots can have the same book ISBN and different valuation and recall exposure. Preserve the scanned lot as issued even when the catalogue SKU later changes. A reversal for an incorrectly posted issue restores the original lot where custody evidence supports it. A customer return from an unknown lot enters segregated inspection. A retailer cannot make that copy sellable merely by sending a refund.

## Failures and acceptance

| Fault injected | Expected action | Evidence of recovery |
| --- | --- | --- |
| Same mobile shift uploads twice, in different event order | Retain original business-action keys. Match each accepted unit; keep late siblings awaiting their prerequisite when needed. | Three sale movements, 12.00 cost and one remaining copy at the stall. |
| A device claims to have sold five against four authorized copies | Preserve five reported transactions as observations. Accept only economically supported operations automatically and open discrepancy for the excess. | Investigation can locate a missing transfer or oversale. No silent negative stock or deleted cash evidence. |
| East reports four receipts before sender's dispatch arrives centrally | Hold the receipt claim. Once dispatch arrives, match four of five. | One pending unit in transit. No transient listing of both central and East's copy for sale. |
| A lost transfer item later appears | Approve recovery with reference to the earlier loss, inspection and actual destination. | Ending physical value increases once at the authorized basis, with a linked finance recovery. |
| A consigned copy with the same SKU is sold | Select its ownership-specific lot and route terms to ConsignmentSettlement. | Custody changes. Owned inventory and supplier/payee obligation reconcile separately. |
| A recall arrives while one bookstall is disconnected | Block central reservations, dispatch and online selling for affected lots. Queue stop-sale, require acknowledgement/reconciliation on reconnect and produce a list of unresolved offline holders. | Live displays distinguish confirmed stop-sale coverage from pending contact. A post-notice sale receives an incident and purchaser remedy. |

The inventory desk sees current lot and case data. Only an assigned recall officer can access purchaser contact information needed to notify affected recipients. A report for the board can show units and value at risk without exposing buyer names. For a disputed transfer, custody and finance each publish their own as-of date so a timing lag is observable instead of being mistaken for missing stock.
