# Fulfil, return and exchange

## One purchaser, several beneficiaries

A parent buys one adult place at 30.00 and one child place at 18.00, a merchandise kit at 24.00 plus 2.40 tax, delivery at 5.00 and a voluntary gift at 10.00. The fixture charges no separate tax on tickets, delivery or gift. The amount due is 89.40. A 30.00 admission voucher covers 20.00 on the adult place and 10.00 on the child place. Card collection of 59.40 covers the adult balance 10.00, child balance 8.00, kit 26.40, delivery 5.00 and gift 10.00. The parent is the buyer. The attendees, receiver of the parcel, authorized collector and actual giving party are independently identified.

| Service boundary | Send | Do not infer |
| --- | --- | --- |
| Cart → admission hold | EventOccurrence, selected AdmissionOption, unit quantity, participant or authorized provisional claim, price class, eligible concessions, hold expiry | A captured adult price does not establish a child's age, supervision permission or attendance. Eligibility is evaluated by admissions. |
| Orders → admissions | OrderHandoff, OrderLine, unit ordinal, AdmissionSaleUnit referring to RegistrationPlace, due amount/currency, verified TenderAllocations, commercial and occurrence times | Finance confirmation is separate from admission capacity. One child place cannot settle a second registration or count attendance before arrival. |
| Orders → fulfilment | Eligible physical units, assigned FulfilmentGroup, StockReservation, required shipping/collection details from authoritative OrderContact version | A packer cannot see donor designation or the child's health instructions. |
| Orders → giving | Confirmed 10.00 gift line and source key, approved fund, consented donor identification if any, restrictive or acknowledgement preferences | The 79.40 admission/kit/delivery balance is not donation income. The payer's household does not automatically receive its own statement. |
| Cancellation → admissions and finance | OrderAmendment, specific AdmissionSaleUnit, AdmissionSaleAdjustment, eligible RefundAllocations by tender, reservation disposition, reason and contact decision | Another child's or adult's place remains intact. A refund request is not evidence that money was returned. |

## Seat release and late capture

Reserve both places until the stated expiry. If the verified capture arrives while holds are active, produce two independently traceable admission settlements. Releasing the child place before the deadline when a full cancellation is allowed reverses exactly 18.00. Restore 10.00 to the voucher and 8.00 to the original card, and send one released-seat decision. The adult 30.00, kit 26.40, delivery 5.00 and gift 10.00 remain paid. Remaining net order value is 71.40. Where a cancellation fee applies, specify who owes it, tax class and whether each original tender may fund it. Record the fee separately before approval.

If the buyer leaves checkout, the hold expires and the waitlist assigns the last child place to another family. A verified late capture cannot reacquire that place automatically. Mark the child unit as collected and unresolved. Offer an authorized equivalent or refund in accordance with the accepted terms. Preserve the adult place if still available and the buyer agreed to partial fulfilment. If all-or-nothing family admission was a condition, hold linked fulfilments and seek a combined remedy. Finance preserves the actual capture whichever remedy the family accepts.

## Physical claims

| Problem | Operator handling | Quantities, money and privacy |
| --- | --- | --- |
| Wrong kit packed before dispatch | Reverse pick/packing allocation, verify correct variant/lot and reconfirm parcel. | One dispatch and one cost issue for the item actually leaving. Preserve erroneous pick with its correcting action. |
| Carrier reports lost after dispatch | Open FulfilmentException. Verify parcel and delivery contacts, obtain authorized remedy and link replacement shipment or refund. | Do not duplicate the original sale. A replacement consumes its actual stock and cost under approved claims policy. Track any carrier compensation outside customer revenue. |
| Package delivered to former address | Inspect approved OrderContact versions and carrier handover time. Keep the used address fixed on that shipment. | A later correction may govern a reshipment. Never reveal recipient address details to a third party who only knows the tracking number. |
| Unopened kit returned | Link ReturnLine to delivered unit, inspect and re-enter the observed lot/location at authorized carrying value. | Example refund 26.40 only if delivery 5.00 is contractually retained. Credit original 24.00 and 2.40 tax components. Never route money to the child's ticket voucher. |
| Defective kit exchanged for higher-priced kit | Under this case, approve full 26.40 return credit and create a replacement order for 30.00 plus 3.00 tax. | Difference is 6.60. Collect buyer consent and payment or offer another remedy. Record an inspected return disposition plus a new issue for the replacement. |
| Verified damaged arrival without physical return | Supervisor authorizes no-return disposal remedy with evidence and delivery state. | One monetary credit, zero false stock receipt. Separate carrier/supplier claim and any cost adjustment for the defective goods. |
| Order redirected from shipment to collection | Obtain buyer authority, recheck tax/delivery eligibility and withdraw obsolete shipping instructions. | Deal explicitly with the 5.00 delivery price and associated refund if due. Pickup verifies named collector and one-time credential at handover. |

## Permission and failure rehearsal

A support agent can locate the order using verified contact proof and masked identifiers. A seating steward sees the named attendees, ticket status and current safety checklist. An authorized guardian check-in flow separately decides custody and pickup. The merchandise desk receives only its parcel instructions. Giving records remain restricted to donor services. Sending one household order summary to the purchaser never authorizes publishing the identity of the receiving child to sponsors.

Run the same cancellation at two service counters. Both can view the pending status; only one financial execution per refund part and one seat release per unit may become effective. When a callback confirms the card refund first, show restored card 8.00 and voucher remedy pending 10.00. A second attempt can restore the voucher exactly once. If a replacement ticket has already been assigned, issue the corrected confirmation for that holder without exposing who previously held it.

Compare operational completion with reporting. The event report shows issued places, cancelled places, admissions actually scanned and no-shows by event. The shop report shows kit fulfilment and physical returns. Giving reports show 10.00. Treasury reports show payment and refund amounts by tender. Each sequence is reproducible at its own as-of instant. A cancelled seat cannot persist in the service leader's active attendance list simply because the original OrderLine remains in a permanent invoice.
