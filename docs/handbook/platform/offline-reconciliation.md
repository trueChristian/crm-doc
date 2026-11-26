# Reconcile disconnected service-day work

The organizer chooses what can be done without a live connection, how long the information is useful and what to do when the time or evidence runs out. [Offline records](../../platform/offline-continuity.md) define the pack, changes, attempts and conflicts. The relevant ministry remains responsible for attendance, capacity and custody decisions. “Saved on this device,” “received centrally” and “accepted by the owner” are distinct user-visible results.

## Before leaving the network

Select one occurrence, assigned users, the minimum permitted fields and scoped write operations. Choose a fixed expiry under the venue's actual risk assessment. Estimate how long devices will be away, whether observers have independent contact with a supervisor and whether the event can continue after a pack expires. Configure protection on the device and a physical fallback route. Prepare different views for ushers, room supervisors and staff handling special instructions.

Complete two checks. The pack manifest must match the authorized source edition, records and field classes. The assigned operator must be able to open it and complete a sample change without connectivity. Display a preparation time and explicit future expiry with time zone. A missed download or partially written pack must appear incomplete. An expired, reassigned or compromised device cannot obtain a replacement without reauthorization.

## Worked conflict set

In a fictitious Sunday service at 09:00, two devices receive roster revision 33 for occurrence O7. Each pack allows provisional attendance and visitor capture through 11:00. Both contain household H12 and person P91. Device A creates temporary guest T1 and records a new number for P91. A centrally authorized secretary independently updates P91's contact before reconnection.

| Local observation | Server state at synchronisation | Expected result and evidence |
|---|---|---|
| A1 marks P91 present; B1 also marks P91 present | No named attendance initially | Two observations support exactly one named attendance fact for O7/P91. Preserve observer and actual local capture time separately. |
| A2 creates T1; A3 records attendance for T1 | No imported person independently verified as T1 | Accept A2 with canonical P120; map A3 to P120. A similar surname on the roster creates a candidate for later review, not an automatic match. |
| A4 proposes a changed number against contact revision 8 | The secretary already committed revision 9 | Return a field conflict with a restricted review task. Preserve both authoritative and proposed values under their respective visibility. No reminder routes to the proposed number until resolved and verified. |
| B2 submits a previously acknowledged attendance after a response was lost | Same scoped operation key and identical contents | Return its original outcome without incrementing headcount. A changed target under that key is an explicit conflict. |
| B3 observes attendance captured at 10:45 but received at 11:15 | B's pack expired at 11:00 | Keep the capture as evidence eligible for supervised late review. Expiry does not confer permission for a new 11:15 action or erase a real observation. |
| A5 proposes a child collection based on a printed roster | Current authority cannot be verified | No automatic release or authority change. Keep custody with the responsible staff and use the verified supervised handover procedure. |

Reconciliation can now report named unique attendance for P91 and P120, totaling two, and count the supporting observations separately. If an usher counted 45 people including both, report 45 total and two identified; do not add 45 to two. Where count methods differ, show the overlap as unknown. If T1's creation is rejected, the dependent attendance stays pending or is accepted as an anonymous count only by a duly authorized reconciliation that prevents double counting.

## Decision procedure

1. Confirm organization, user, device, pack and current operating rights. Check expiry and whether the proposed action has a permitted offline path. Read authoritative time separately from operator-supplied and device time.
2. Detect duplicate operation keys before applying a change. Compare normalized material inputs, not transient client fields. Resolve any temporary keys using durable mappings. If a dependency cannot resolve, report its key and leave dependants pending.
3. Check the relevant base revision. Independent observations may coexist, and a domain uniqueness key can coalesce the resulting fact. Independent edits to different fields may merge only under a documented field rule, with both inputs recorded. A disputed safety restriction, custody state, pledge, private address or approval requires an accountable custodian.
4. Validate capacity and dated permissions against the current owner. A reservation may be held offline only when a nonoverlapping allocation was explicitly delegated to that device. A scope of ten local places can never admit the eleventh automatically. After reconnecting, reconcile unused delegated inventory before returning it to the general pool.
5. Record outcome, canonical target, persisted checkpoint and actions requiring a supervisor. Unknown outcomes are retried with the same keys. The local screen may discard acknowledged details under its cleanup policy, while preserving the minimum read-only receipt for authorized reconciliation.
6. Independently count accepted facts, duplicate observations, rejected operations, conflicts, gap and pending dependencies. A checkpoint cannot move past an unknown operation without an explicit durable per-operation ledger that still tracks the gap.

## Exception handling and acceptance

If a field becomes protected while a device is offline, stop further server disclosure immediately. A returning device receives a redacted conflict or neutral disposition; it cannot retrieve the newly protected value as a convenient comparison. If a clock is wrong, preserve the observation and recorded offset, alert on improbable times and seek eyewitness confirmation when chronological order affects an official decision.

A lost device stops receiving new data at revocation. Local access is bounded by its protection and expiry; the church records whether destruction can actually be confirmed. A reassigned device undergoes verified local cleanup and a fresh pack for the new operator. A printed alternate roll has an issue identity, limited fields, named custodian, receipt and return/disposal process.

The rehearsal passes when both devices reach a final status for every observation, two named people are counted in the fixture, one contact conflict stays unresolved until review, the questionable handover never authorizes release and every person completing the exercise can explain which actions remain pending.
