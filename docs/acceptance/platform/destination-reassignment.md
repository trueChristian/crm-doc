# Reconcile a printed and digital notice after an endpoint changes owner

This fixture exercises a personal pastoral appointment reminder carrying the appointment time. No message contains case notes or the reason for the appointment. The local release rule permits private verified destinations and a separately confirmed, private postal fallback. A contact preference and proof that a person controls a particular destination are independent.

## Prepare the routing evidence

| Recipient | At snapshot creation | Change before dispatch |
| --- | --- | --- |
| A | Granted optional reminders to private verified endpoint EA. No postal route. | A reports EA was reassigned; the steward applies an endpoint restriction and retires the binding. |
| B | Granted this purpose to private EB and separately to postal address PB. | EB becomes household-shared. PB remains individually verified and safe for sealed mail under this appointment policy. |
| C | Granted this purpose to private EC. | No change. The provider initially returns an ambiguous outcome. |
| D | Granted this purpose to private ED. | Withdraws all appointment reminders before dispatch. Other people still use the same service. |

Freeze a four-person audience at 08:00. The steward records the changes at 08:10 with immediate effectiveness. The dispatch executes at 08:15. The print slot is 09:00. Use different per-recipient keys and a separate handoff key for each intended delivery. Trigger each scheduler twice.

| Routing proof at 08:15 | Digital handoffs | Print envelopes prepared | Required disposition |
| --- | ---: | ---: | --- |
| A | 0 | 0 | Restrict the reassigned endpoint; no remaining permitted appointment route. Staff may review a separately authorized contact path without sending any private detail to EA. |
| B | 0 | 1 | EB cannot receive this sensitive notice. Under the approved fallback, reserve exactly one sealed envelope for PB and record which permission made postal handling possible. |
| C | 1 | 0 | Preserve the first intent and ambiguous response. Do not send through another route while acceptance remains unresolved under this fixture's policy. |
| D | 0 | 0 | Live purpose withdrawal excludes D without creating a temporary retry or a print job. |

Prepared envelopes = 1; external digital intentions actually submitted = 1; confirmed digital acceptance at this checkpoint = 0. Four frozen entries remain available under the original authorization to audit them. The coordinator's ordinary summary exposes outcomes and counts, not private endpoint histories or appointment details.

## Test three independent continuations

**Run P, withdrawal before mail leaves.** At 08:59 B withdraws postal permission. The batch is still inside church custody. Invalidate the envelope, record its contained disposition, adjust or replace the protected manifest and authorize zero envelopes at handover. Previously staged counts remain interpretable: one prepared, one withheld/destroyed, zero handed over. A duplicate print request must not put the excluded envelope into a new batch.

**Run Q, withdrawal after handover.** Reset to the original prepared state. Hand one envelope over at 09:00 with the verified manifest. B withdraws at 09:01. Record one physical handover at its real time. The new decision prevents future sends. An attempt to recall or correct this already-issued copy gets its own custody outcome and evidence; no one records destruction or attempted recall as proven delivery.

**Run R, delayed receipts and new destination owner.** The provider later confirms C's original external reference as accepted. The next duplicate observation carries the same event key. Finish with one attempt, one distinct verified acceptance and no fallback for C. A new person E acquires EA and completes their own verification challenge. The old A-purpose permission cannot send A's reminder to E or establish consent for E. Process E's new relationship and preferences independently. A verified inbound stop to the shared address must be protected at the applicable destination scope even if the individual author cannot be resolved.

Send an unverified event claiming C unsubscribed. Keep it quarantined with a redacted reason; zero effective preference changes can rely on that event. A verified withdrawal received later has its own evidence and effective time. Repeat using a different organization whose external provider happens to reuse the same message identifier. Match connection and delivery before granting any observation an effect.

Use [DeliveryEndpoint](../../implementation/communications/DeliveryEndpoint.md), [ChannelBindingChallenge](../../implementation/communications/ChannelBindingChallenge.md), [ContactDecision](../../implementation/communications/ContactDecision.md), [DeliveryException](../../implementation/communications/DeliveryException.md), [DeliveryObservation](../../implementation/communications/DeliveryObservation.md) and [PrintBatch](../../implementation/communications/PrintBatch.md).
