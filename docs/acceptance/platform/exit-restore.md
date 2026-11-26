# Prove that a church can leave and a neighboring church can still be restored

Church A is moving to another operating system. Church B shares a building and has an agreement with A for two joint-event registrations. Both organizations happen to use local person key 17. A manages a volunteer rota, three contact points, two consent decisions and a published resolution. A third-party restricted attachment has a continuing preservation duty but cannot transfer to the successor under this fixture's recorded disposition.

## Authorized inventory at the final cutoff

| Class | Source count for A | Expected transferred count | Reconstruction or disposition check |
| --- | ---: | ---: | --- |
| Person | 2 | 2 | A:17 and A:23 remain distinct; neither is B:17. The successor can resolve the two stable source keys. |
| PersonContactPoint | 3 | 3 | A:17 has two, A:23 has one. Links and confidentiality flags resolve to the correct person. |
| ConsentDecision | 2 | 2 | A:17's older permit and subsequent withdrawal both transfer with effective times and the supersession relationship. The current outcome for the covered purpose is withdrawn. |
| VolunteerAssignment | 2 | 2 | Both belong to A's rota. Include or map the referenced shifts, people and assigning account explicitly in the full export manifest. |
| Resolution | 1 | 1 | Preserve the approved wording, governing body and minute item leading to its meeting. Supporting minutes and their parts keep their original access ceilings. |
| Designated restricted attachment | 1 | 0 | A recorded continuing custodian keeps the original and the review date. The successor receives only the permitted disposition entry. |
| B-owned records | 0 owned by A | 0 | The joint-event agreement does not give A exit authority over B. |

The ten transferred business records listed above are a reconciliation subtotal: 2 + 3 + 2 + 2 + 1 = 10. Dependency records, dictionary editions, joins, redactions and the manifest itself get separate class counts. Do not certify the entire package merely because ten rows can be opened. Inspect cross-references without disclosing protected third-party names or document titles.

## Normal handoff

1. Two authorized accounts request and approve A's exit scope and stop time 18:00. Have them exercise account sign-in separately; one user changing organization context is not two independent approvals under this profile.
2. At 17:30 take a provisional export. A:17 withdraws optional newsletter permission at 17:45. At 17:50 A:23 moves assignment time. The final sweep covers the provisional watermark through 18:00 and accounts for both changes once. Select the existing assignment identity for the changed time, never a duplicate shift or volunteered person.
3. Rehearse import in the recipient's isolated workspace. Verify stable joins, record counts, checksums, time precision, representation of missing values, access ceilings, document lineage and the effective withdrawal. A successful download or matching byte count is insufficient to prove this reconstruction.
4. Deliberately remove one referenced contact row and regenerate the transport checksum for this negative run. A byte-integrity check alone passes. Independent per-class count and relation checking fail; hold acceptance, restore the authorized record and revalidate. Retain the failed result and its correction.
5. At the stop time revoke A's ordinary interactive access, terminate future queued dispatch and prevent generation of further routine exports. Preserve the documented custody route for held material and scoped remediation of prior sharing. B's ordinary operations and giving connections stay available.
6. The successor acknowledges the verified final edition. Recipient acceptance covers that edition, item count and exception list. It does not establish erasure of A's remaining authorized holdings or destruction by a third party.

## Prove post-exit remediation survives restore

At 18:10 A's departing custodian sends a narrowly authorized correction for one of the two joint-event registrations, as permitted by the remediation clause. B acknowledges transport. Its duty desk applies the correction at 18:20. Record both instants. At 19:00 restore B alone from a backup taken at 17:00 with A still active. The separate current obligations evidence includes the exit cutoff, terminated ordinary sharing, A's protected withdrawal and the B correction as applicable to each scope.

| Probe after recovery in isolation | Expected result before reopening |
| --- | --- |
| B retrieves B:17 | B sees its own latest permitted record. No A contact or merged profile based on the identical local key. |
| A's old integration submits an ordinary new registration | Reject new business under the expired agreement. Its old credential or an old pending event cannot reactivate sharing. |
| B reprocesses the correction twice | One corrected local registration, one application of the operational change. Retain evidence of any duplicate transport without creating a new registration or changing the other transferred entry. |
| Operator requests A's held attachment through B's restore | No record, preview, manifest name or non-neutral diagnostic is exposed. The nominated continuing custodian has the separate preservation evidence. |
| B dispatch scheduler sees A's old audience entries | Nothing sends on behalf of A. Independently permitted local B dispatch can proceed only after reconciliation and owner release. |
| A's obligations watermark is unavailable | Suppress impacted A-derived records and processing. An independent proof can release an unaffected B-only scope; record the owner for the missing segment. |
| Successor cannot resolve a referenced shift | Verification of that manifest item fails. Preserve the original cutoff and reconcile the missing dependency through an authorized correction package. |

Use [ExitPlan](../../implementation/platform/ExitPlan.md), [ExitManifestItem](../../implementation/platform/ExitManifestItem.md), [SharingAgreement](../../implementation/platform/SharingAgreement.md), [SharedDelivery](../../implementation/platform/SharedDelivery.md), [RestoreExercise](../../implementation/platform/RestoreExercise.md), [RecoveryCheck](../../implementation/platform/RecoveryCheck.md) and [ConsentDecision](../../implementation/platform/ConsentDecision.md).
