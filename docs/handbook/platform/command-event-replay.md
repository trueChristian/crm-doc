# Keep a business action correct through retries and reordering

Use the [exchange dictionary](../../platform/exchange-events.md) for contracts, requests, receipts, subscriptions and deliveries. A command requests a business decision such as confirming a registration. An event reports an accepted fact such as a registration being confirmed. A receipt can confirm delivery of either message while the business work is still pending. A business decision and a transport acknowledgement must have separate states.

## Contract choices before a producer goes live

| Decision | Required declaration |
|---|---|
| Identities | Organization, producer namespace, stable operation key, subject/aggregate ID, event ID, contract edition, aggregate revision, causation and end-to-end correlation keys. State how long copies and retired keys remain detectable. |
| Input equivalence | Define material identity, money, currency, quantity, deadlines and normalized field values. Whitespace in a free-text address and a changed amount have different meanings; document which fields enter the equality test. |
| Atomic unit | Name the business change, local outcome and durable event intent that succeed together. Name the external effects that happen later. A business commit never claims the recipient already acted. |
| Ordering | State whether events replace complete state or describe individual transitions. Specify contiguous revisions only within the appropriate producer stream; do not assume consecutive sequence numbers on a filtered subscription. |
| Recovery | Specify retryable outcomes, maximum delay, deadline, discrepancy owner, reconciliation query and how to resume from a durable checkpoint. Decide whether aggregate projections, notices and financial effects can be replayed independently. |
| Compatibility | Define nullable fields, stable units, recognized enumeration behavior, precision, default, deletion type, support period, test fixtures and retirement route. A changed meaning requires a new edition even if the field still has the same name. |

## Worked stream from a paid event

A member requests one retreat place under operation R-41 at 09:00. The amount is 120 in the confirmed order currency and the price edition is E3. The registration owner commits a hold and its durable change. A payment service may confirm capture later. All identifiers in this fixture are fictional.

| Step | Observation | Owner's durable result |
|---|---|---|
| 1 | R-41 arrives twice with the identical payload before the first response returns | One provisional hold. Either respondent receives the original deterministic result, or pending with a way to obtain that same result. |
| 2 | R-41 is reused with amount 125 | Conflict. No additional hold, price revision, charge or confirmation. The caller must submit a genuinely new reviewed operation. |
| 3 | The return screen reports success, but an authenticated capture has not yet arrived | Leave payment pending. A browser message cannot issue a ticket, grant media access or create a posted receipt. |
| 4 | Verified capture C9 arrives twice under two transport attempts | The designated fee steward verifies recipient, registration reference, currency and amount against the payment provider and records one confirmed capture reference. Count two transport attempts separately. |
| 5 | A cancellation revision 5 reaches a roster projection before revision 4, the confirmation | Record revision 5 as waiting if this is a delta stream. Obtain the missing authorized state or revision, apply 4 then 5 once and leave the place cancelled. A full authoritative snapshot at revision 5 may replace both for that projection. |
| 6 | An email worker receives revision 4 after revision 5 is already authoritative | Check current state, audience and useful deadline. Suppress the now-obsolete confirmation rather than recreating it while replaying history. Keep the suppression reason. |
| 7 | The capture occurred but its order hold expired and a different family owns the only seat | Route to the agreed replacement or refund process. The payment stays traceable. Reconciliation cannot take another qualified family's place. |

## Failure and repair decisions

An unknown provider outcome receives a stable pending state and a reconciliation reference. Check for the original external effect by reference before retrying a charge, payout or notice. A provider without a reliable idempotency or inquiry mechanism may require human review before a resend. Do not label an uncertain dispatch a failure merely to trigger retry.

A consumer receiving an older revision than its applied state may still need an immutable financial or audit fact. Classify consumers. A roster displaying current state can ignore proven obsolete state messages. A church gift history reconciles source events and corrections. A separate accounting consumer reconciles its own posting keys and reversals. A snapshot cannot prove that a notification was sent or that each money movement was posted. When requesting a current snapshot, include the source coverage and replay floor.

On repeated failure capture a protected quarantine record with safe business reason, observed contract edition and owner. Halt automatic retry for that delivery after the allowed attempts. Other organizations or subscribers continue. After repair, replay an operator-specified range using the original event identities and current downstream permissions. Record replay counts, skipped duplicate outcomes, missing editions and any external effects requiring independent confirmation. A rollback may rebuild read models; it must never repeat actual disbursement.

## Evolving a contract

An existing event named “receipt recorded” includes amount and currency. Adding an optional human reference with no effect on posting is compatible when old consumers can ignore it. Splitting the same amount into a gift and an exchange portion changes its economic meaning. Publish a new edition with explicit line allocations and the authority of each recipient. Declare whether historical mixed transactions can be converted and how unknown splits are handled. During a parallel transition the same economic action uses one stable source handoff key across both editions. Acknowledging both editions cannot double the donation.

Retirement requires a list of actual subscribers, last successful use, agreed cutoff and archived replay instructions. Test a previous edition, unrecognized enumeration, optional value absent, invalid mandatory field, stale grant, out-of-order event, duplicate with changed content and unavailable authoritative source. Keep a human-readable explanation of which compatibility decisions are safe and which require manual reconciliation.

## Pass criteria

The sample produces one place hold, one payment capture, no active ticket after final cancellation and no late confirmation notice. Financial effects and customer remedies are reconciled separately. Killing a worker between receipt and acknowledgement changes the attempt count only. Replaying both editions leaves the external posting acknowledgement, roster and donor history unchanged, while the replay log explicitly identifies duplicates and current-state suppressions.
