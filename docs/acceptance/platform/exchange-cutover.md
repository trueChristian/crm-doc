# Change an exchange contract while two subscribers are at different checkpoints

A church exposes an approved service-calendar feed to a public directory and a private facilities desk. A directory receives published title, start instant, public location, state and stable event key. Facilities additionally receives its approved space key. The facilities agreement does not include member identities, adjustment requests or private notes. Both subscriptions use distinct principals and connections. An operations observer can see delivery classes and checkpoint positions, without payload text.

## Freeze the source and define the compatibility rule

| Event | Service | Business change under its own revision | Feed position |
| --- | --- | --- | ---: |
| U41 | A, revision 5 | Start becomes 16:30. | 41 |
| U42 | B, revision 2 | Public notice is withdrawn. | 42 |
| U43 | A, revision 6 | Public venue becomes South. | 43 |
| U44 | C, revision 1 | Newly published service. | 44 |

All four events were committed exactly once. The first two have the same occurrence instant. A snapshot at position 40 contains A and B. The stable order for this feed uses the opaque feed continuation, not event time. Counting current publicly listed services after all changes yields A and C only. A department with independent internal booking evidence may continue to see B under its internal permissions.

Contract C1 carries public start instant and optional display zone; C2 requires a venue zone in addition to the instant. In this exercise an explicitly configured venue zone supplies the value. An unknown venue zone cannot be invented. A candidate C2 delivery that lacks its required zone remains pending resolution; the source retains the committed change. Withdrawal instructions in both editions are keyed tombstones and do not require the withheld fields of a withdrawn service.

## Execute the cutover

1. Both subscribers start at 40. Directory accepts U41 and U42 under C1, then is paused for cutover. Its durable checkpoint is 42, A shows 16:30, and B is absent. Facilities accepts U41 only. Its independent checkpoint is 41.
2. At a recorded contract boundary, enable the directory's C2 subscription with explicit predecessor checkpoint 42. If the transport supplies edition-specific opaque tokens, resolve the predecessor to a verified source boundary or take a fresh authorized snapshot. Copying an opaque cursor verbatim is legitimate only when the contract guarantees continuation compatibility.
3. U43 initially lacks the required C2 zone. U44 is valid. The directory cannot declare complete coverage through 44 until it accounts for 43. Under this fixture's in-order consumer, hold both beyond 42, report one blocked position and one waiting position; A still displays its last accepted revision. The operations desk can identify which contract field is absent without receiving the venue's private notes.
4. Resolve A's zone from confirmed authoritative venue data. Preserve original event identity and source revision. Record the approved representation/mapping correction and the evidence against the failed attempt. Deliver the corrected C2 representation of U43, then U44. If a receiving service already locked a key to different bytes, reconcile that receipt under its supported correction procedure instead of reusing the key with a different digest.
5. Facilities resumes under C1 before its supported retirement boundary and consumes U42–U44. Its receipt and missing public entry for B do not erase a separately authorized internal reservation. Stop C1 after the agreed date; replay requiring a retired edition must use an explicitly supported archived reader or a reconciled fresh snapshot.
6. Final consumer checks: directory 44, facilities 44, visible public services A and C, A start 16:30 and venue South, one withdrawn key B. Each consumer applied four distinct source changes since 40. A failed serialization may have transport attempts but cannot itself advance either source watermark or trigger a public send.

## Interruptions to run independently

| Intervention | Expected receiving and producing state |
| --- | --- |
| Directory receives its old C1 U42 after onboarding C2 | The same business withdrawal remains applied once. Transport proof may include an additional recognized delivery. No new source revision, second public withdrawal notice or second cancellation is produced. |
| Two workers open page 2 at the same verified continuation | A replay of that page is harmless under stable event identities. The pair with the same timestamp is completely accounted for. |
| A cursor for the facilities principal is used by the public directory | Reject or restart in the directory's own scope. Return no facilities record, field name, hidden count or working cursor that exposes a protected partition. |
| The destination acknowledges receipt, then its local update fails | Record transport acceptance separately from the business discrepancy. Reconcile with the receiver's processing evidence and resume the missing application once. |
| A callback uses an existing sender key with a changed body | Retain the original trusted receipt and business result. Quarantine the changed body and do not advance using it. An authorized correction has a new operation identity or a documented supersession relation. |
| A snapshot required after replay-floor expiry begins while C is edited | Bind its pages to the same authorized snapshot, apply the later delta exactly once, and reconcile the final service revisions. A changed permission can invalidate the snapshot; obtaining a new one must recheck the new scope. |
| Facilities principal is revoked before retry | The facilities backlog cannot move under the revoked principal. The directory remains current. Restoration of access requires explicit authorization and scope verification for the unapplied interval. |

Check [InterfaceEdition](../../implementation/platform/InterfaceEdition.md), [DomainEvent](../../implementation/platform/DomainEvent.md), [IntegrationSubscription](../../implementation/platform/IntegrationSubscription.md), [InboundReceipt](../../implementation/platform/InboundReceipt.md), [IntegrationDeliveryAttempt](../../implementation/platform/IntegrationDeliveryAttempt.md) and [ExchangeRequest](../../implementation/platform/ExchangeRequest.md).
