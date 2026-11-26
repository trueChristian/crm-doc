# Recover and sign off the opening weekend

Before the interruption keep four independently reviewable receipts: the registrar’s certified roll and correction, the external bulletin receiver's delivery register, the provider's transfer and refund observations, and the event desk's per-place cancellation receipt. Use the [three original transactions](settlement.md) and the same church and person identities throughout.

Take the recovery point after the original June roll, bulletin preview and three captures but before the June amendment, actual dispatch, provider batch, place cancellation or refund. Let the original system complete those events against isolated test receivers and keep their observations available. Restore the earlier copy separately with outbound actions disabled. A database restore cannot undo delivery of a bulletin or return a paid fee to the provider.

| Sequence | Recovery action | Inspect before releasing normal writes |
| --- | --- | --- |
| 1 | Apply the accepted register corrections, access revocations and P5’s dated withdrawal from controlled evidence. | The original and amended June roll editions are distinguishable. Current June members are P1 and P4. A stale audience cannot release a notice. |
| 2 | Find D1 and D2 by existing references in the external bulletin receiver. Include a repeated D2 observation. | Exactly one accepted dispatch to each of E1 and E2. Zero to E3 or E4. Keep a missing receiver response unresolved until independently reconciled. |
| 3 | Match the three source references and both relief/general designations to the external batch. Import its receipt twice. | Two gifts total 80; two fee-bearing places originally total 20. Gross 100, fee 3 and net 97 agree with the provider's report. No new charge is requested. |
| 4 | Match S1b’s cancellation evidence to the one external 10 refund. | S1a still has one live ticket. S1b has one retired ticket, one released place and one confirmed refund status. No extra payment or cancellation request. |
| 5 | Recheck each measure against its owner. | Six church A people; two current June members; two accepted bulletin destinations; one live retreat ticket; two gifts; one external refund. The provider’s net transfer over the fixture is 87. |
| 6 | Try P2's ordinary account, then a church B operator account. | P2 sees the permitted registration and refund status only. Church B cannot discover North people, gifts or destinations through lookup, notifications, exports or report details. |

## Missing cancellation evidence

Repeat the restore with the externally confirmed refund reference intact but with no church cancellation or release observation for S1b. A refund can arise for reasons besides a cancelled place. Keep the money observation attached to the original place and show an unresolved admission decision; do not advertise that place as available or send an automatic cancellation notice. The registrar obtains the original authorized cancellation evidence, reconciles the ticket and releases one place exactly once. Replay it to show the release cannot recur. If a steward already recorded actual attendance, keep that separate observation for review.

The clerk signs the membership cutoff and included identities. Communications signs purpose, edition, suppressions and receiver acknowledgments. The event coordinator signs ticket states and remaining capacity. The giving steward signs the gift designations and totals; the finance liaison signs the provider match and its exceptions. The recovery lead records which external actions are certain, who owns each outstanding discrepancy and when each writer was reopened.

[Service recovery](../../platform/operations-recovery.md) · [Migration and data quality](../../platform/migration-data-quality.md) · [Opening-weekend sequence](README.md)
