# One physical handover across two desks

A collection restriction reaches a campus after its ordinary check-in desk has printed a roster. During a continuity activation, the family liaison also receives a request to release the same child. Exercise the decisions through both desks. Use fictional identifiers and a single time zone. The activation in this fixture is a supervised test with no actual children.

## Starting ledger

| Clock | Record | Saved fact |
| --- | --- | --- |
| 09:00 | [ChildCheckIn](../../implementation/ministry/ChildCheckIn.md) CI4 | Subject P4 arrived for occurrence O7. The record is supervised, with no release time. |
| 09:02 | [HandoverCredential](../../implementation/ministry/HandoverCredential.md) HC8 | Version 2 is valid for CI4. Version 1 was replaced when the slip was lost. |
| 09:10 | [RepresentationAuthority](../../implementation/people/RepresentationAuthority.md) A2 | Representative R1 has verified collection permission for P4 at O7. R2 has a separate verified permission for the same subject and activity. |
| 09:20 | [AccountabilityEntry](../../implementation/assurance/AccountabilityEntry.md) E4 | The activation's authorized census includes P4 and nine other identified children. All ten are confirmed present at one location. |
| 09:25 | [ProtectiveMeasure](../../implementation/people/ProtectiveMeasure.md) M3 | The case lead activates a narrowly scoped denial for R1 collecting P4 at O7. The lead's purpose and case identity stay in the restricted area. The operational authority service records the corresponding verified restriction. |

The exercise policy requires a current collection decision and a witnessed physical handover. It permits the previously verified R2 to collect with ID and the current slip. The earlier roster, possession of a slip and the claimant's relationship are insufficient on their own. Authority and physical custody are separate questions.

## Execute in the specified order

| Time | Operator action | Required observable result |
| --- | --- | --- |
| 09:26 | The ordinary desk presents version 1 for R1. | The replacement makes the credential unusable. A failed attempt records the time and operator privately. CI4 is open and E4 is present. The screen has no case title or reason for the protection decision. |
| 09:27 | R1 presents version 2 and identity. The old roster still lists R1. | The current restriction defeats the earlier allow. The desk records an unsuccessful [CollectionAttempt](../../implementation/ministry/CollectionAttempt.md), gives the neutral instruction configured for this desk, and leaves CI4 open. |
| 09:28 | Repeat the second submission after its receipt was lost. | With the same operation identifier, the operator retrieves that attempt. There are two unsuccessful attempts in total. A genuine new attempt receives its own time and identifier. |
| 09:30 | The liaison inspects R2's identity and current authority and records an allowed [ReunificationDecision](../../implementation/assurance/ReunificationDecision.md). | The decision identifies R2, E4, the authority, the verifier and time. Its handover time and release receipt are empty. The census still has ten present. |
| 09:31 | The ordinary desk tries to complete R1's collection while the liaison is arranging R2's handover. | Recheck the claimant at completion. R2's authorization does not transfer to R1. The denial changes neither headcount nor custody. |
| 09:33 | The liaison confirms actual handover to R2 with operation H4. The same confirmed release is delivered twice to the ordinary desk. | Both desks refer to one release receipt. E4 is reunited, CI4 is released at 09:33 and exactly one successful handover exists. Nine remain present. Count the physical handover once in the activation report. |
| 09:34 | A second operator tries to complete another handover of P4 with a fresh identifier. | The current custody record is closed. No further successful receipt is created. The earlier recipient remains R2. |
| 10:00 | The lead reviews M3 and revokes it after the recorded decision. | Future actions use the revised authority. Replaying H4 still returns the 09:33 result. The 09:27 failed attempt retains the decision that actually applied. |

## Isolated failure branches

Reset to 09:30 for each branch. A branch never inherits a release from the main script.

1. The location loses contact with the authority owner before R2's handover. Under the example policy, refer to the designated lead. Leave CI4 open and E4 present. Do not treat the cached allow as current or pre-fill a handover time. Nine-present would be an incorrect count.
2. The lead places a fresh restriction on R2 at 09:32. The earlier allowed decision remains evidence of the check at 09:30. A fresh decision for the proposed handover records the restriction and no transfer. Ten participants remain present.
3. The release owner has saved H4 and the ordinary desk's acknowledgment fails. Recover using H4, the original recipient and release time. Show the delayed synchronization to authorized staff and prevent any second release while custody is unresolved at a desk. After reconciliation, both desks identify H4 and the same nine present.
4. The liaison for another campus enters the known P4 identifier. They receive the ordinary out-of-scope result. Neither M3 nor any claimant names, case number, location or participant count appear. The safeguarding lead can audit the attempted access through the protected review route.

A test operator can reconcile ten initially confirmed people to nine present plus one reunited. At 09:26, 09:27 and 09:31 there were three distinct unsuccessful attempts. The 09:28 replay added no fourth attempt. The distinct late attempt at 09:34 cannot alter that custody reconciliation.
