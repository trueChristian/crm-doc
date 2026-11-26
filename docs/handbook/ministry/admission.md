# Allocate places and reconcile their price

A booking can use an overall event place, a workshop place, an accessible seat and part of a bundled pass. Identify each independently limited pool and record which promised units consume it. Keep actual admission, ticket redemption and money received separately inspectable. The [registration dictionary](../../ministry/registration.md) names the authoritative ministry records.

## Allocate once against all relevant limits

1. Normalize the request into attendee, option, date, required quantity, seat preference, group-together rule and any pass prerequisite. Reject a nonpositive quantity, an expired sale or a place for the same person already present in the same mutually exclusive choice. A guest place may remain unnamed if the activity allows it.
2. Look up the operation identity and submitted revision. Return the original result for an identical repeat. A reused identity with changed quantities is an operator-visible conflict. Evaluate any person-specific eligibility privately and return only the permitted next action to the booker.
3. Determine demand per pool. For each pool compute limit less confirmed units, live holds and blocked inventory. Never count a hold twice when it becomes confirmed. A reservation of 2 that touches event and workshop capacity subtracts 2 from each pool, yielding 2 people rather than 4. For a partly expired hold, evaluate its expiry against the same decision instant used for all pools.
4. Claim every required pool, allocated seat and unit identity as one all-or-nothing decision. Serialize competing decisions on the same finite inventory. A limit shown on a preview is advisory until this commit. If a required pool fails, keep all untouched and create at most one wait request for the agreed grouping. A response names the obstructing pool without exposing other bookers.
5. A hold expires at its deadline. A payment accepted just as the hold expires uses the confirmed ordering of decisions. If allocation still exists, confirm it. Otherwise attempt a fresh claim or refer the payment for a documented remedy. Record the result once. A failed email delivery never releases confirmed capacity.
6. When a cancellation opens space, evaluate waiting entries by published priority band, submission time and stable sequence. Make a time-limited offer against actual free units. Specify whether a too-large first group blocks all later requests, may be skipped for a smaller group, or can opt for a split. Persist the reason for skipping an entry and expose the position and policy among eligible staff.

**Capacity fixture.** An event has 20 places, 15 confirmed and 3 active holds. A children's room attached to the event has 8 places and 7 confirmed. A family asks for one adult and two children. Event demand is 3 and the children's pool demand is 2. It cannot proceed now. When the three-place hold expires, event capacity becomes 5, but the children's pool still has 1. Allocate nothing and retain the family request. Releasing one children's place plus its underlying event claim changes free capacity to 6 and 2. The family can now be offered all three units. While it holds the offer, available balances are 3 and 0. When payment confirms, available balances remain 3 and 0. A duplicate confirmation cannot reduce either again.

## Reconcile a family booking against provider decisions

**Desk fixture.** One family books an adult place A and a child place C. The event permits independent confirmation and requires full funding per unit. Its payment provider has quoted A at 55.00 and C at 27.50 in the same currency. A separate designated gift of 12.50 goes to the church giving workflow. Hand the provider stable scoped unit references for A and C, accepted terms and the local booking reference. The door steward sees the confirmed place and issuer status. The finance reviewer can retrieve permitted provider evidence separately.

| Action | Organizer's expected observation |
| --- | --- |
| The family returns from the payment screen. The provider has supplied no authenticated notice. | Both places remain held subject to their expiry. A browser success screen cannot issue a ticket. |
| The provider reports A fully funded, C partly funded at 10.00, and a separate gift. | Confirm A once if its claim is still valid. C stays held with its expiry. The admission desk receives no gift data. |
| The provider later confirms C fully funded at 27.50. Staff retry that notice following a timeout. | One current ticket per place. The second notice returns C's prior result. A later delivery of the earlier partial state cannot reverse it. |
| Repeat the same case under a published family-together policy. | Keep A and C held together until the verified booking is fully funded. Expired holds require a fresh all-or-nothing capacity decision. |
| The family cancels C. The provider acknowledges 10.00 refunded and the rest pending. | C releases once and its ticket is retired. The operator sees the partial refund and provider reference. A remains valid and the separate gift is unchanged. |
| The provider later confirms the full 27.50 refunded. Another child has taken the place. | Record the linked refund outcome once. The new holder's place is independent. A correction to the refund state opens financial review with the provider. |
| A delayed funded notice arrives for an expired place which another child already holds. | Leave the new booking intact. Route the funded unit to an authorized operator for an alternate place or refund request. Provide the affected family's permitted status while the provider is unavailable. |

## Doors, disputes and closure

A checker scans the ticket under its current version, occurrence and admissible time. A valid unit already redeemed elsewhere returns that observation to an authorized steward and routes it to review. For a permitted transfer, atomically retire the old credential and issue one for the eligible new attendee. During an outage, an admission device can spend only explicitly reserved local capacity. Without exclusive credentials across devices, duplicate scans can still occur: preserve both observations and reconcile the persons actually present. An emergency decision to admit someone records the authorized actor, inventory exception and evidence separately.

At closure compare each pool's limits, active claims and blocked inventory; named sales versus expected and observed attendance; provider-confirmed units versus local funded places; released seats versus open refund requests; and upcoming retries versus completed handoffs. Reject negative free capacity unless a newly reduced limit created an explicitly owned over-capacity exception. Never remove an existing churchgoer automatically to balance that number.

[Manual index](README.md) · [Registration and payment notices](../../ministry/registration.md) · [Accounting exchange](../../finance/accounting-exchange.md)
