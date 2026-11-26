# Petition endorsement after a membership correction

A church clerk, membership registrar and presiding officer examine a petition for an agenda item. A correction changes one historical membership fact after the petition's filing deadline. This exercise tests which facts were known to each decision and which actor can reopen it.

## Fixture charter and electorate

The example charter admits the petition with three distinct eligible signers. A signer must belong to the voting class at the filing cutoff. All times are local to one congregation. Signatures must arrive before 17:00 on 30 September. A verified paper submission and an authenticated online submission have equal effect. Independent review can accept later evidence of an already-effective membership change. It cannot extend the cutoff for an otherwise late signature. Acceptance creates a proposed agenda item. Only the presiding body can admit that item or decide its substance.

The certified [RollSnapshot](../../implementation/people/RollSnapshot.md) R1 is as of 30 September with a 17:00 knowledge cutoff. It initially identifies A, B and D as eligible. C's record shows the nonvoting class. A and B live at the same address. E has another congregation's membership. A membership correction for C will be recorded on 2 October with an effective date of 28 September. The two resulting editions of membership evidence are distinct from the [MeetingRoll](../../implementation/governance/MeetingRoll.md) for a meeting.

## Ingest and reconcile

| ID | Received | Signer and source | Registrar/clerk result at initial determination |
| --- | --- | --- | --- |
| SG1 | 15:02 | A, witnessed paper endorsement | Accepted once with dated evidence. |
| SG2 | 15:05 | A, new online endorsement | Duplicate of A's already counted right. Preserve evidence of this submission. |
| SG3 | 15:10 | B, same postal address as A | Accepted independently. A household key cannot collapse B into A. |
| SG4 | 15:15 | C, timely paper endorsement | Rejected for eligibility under the evidence available for R1. Retain signature time and restricted evidence to permit review. |
| SG5 | 15:19 | E, external congregation | Rejected under this body's rule. The office cannot browse E's home congregation to construct an entitlement. |
| SG6 | 17:00 | D, otherwise eligible | Rejected at the exclusive deadline. D's membership remains valid. |

1. Submit SG3's exact transport receipt twice. There remain six underlying submissions. SG2 was a distinct human submission and still shows a duplicate determination. The first determination has two accepted, one duplicate and three rejected. The configured threshold of three is unmet. Record a reasoned decline on the [GovernancePetition](../../implementation/governance/GovernancePetition.md). No agenda item exists.
2. On 2 October the registrar records C's [MembershipDecision](../../implementation/people/MembershipDecision.md) with the original effective date, actual recording time, prior decision and supporting scope. Issue certified edition R2 referencing R1. The original R1 was actually used on 30 September. R2 describes restated facts at the same business date with a later knowledge cutoff.
3. A clerk reopens yesterday's petition screen after R2 exists. They can distinguish original and restated evidence. Its declined decision remains in force pending review. The new roll alone cannot change the petition result, enter a vote or create an agenda item.
4. A conflicted original decision maker tries to decide the appeal. Preserve its lodged time and allocate to an independent eligible reviewer. The [GovernanceReview](../../implementation/governance/GovernanceReview.md) records the petition reference under its decision-review category, recusal check, governing rule and independent term.
5. The reviewer varies only C's eligibility determination using R2. Capture the reviewed [PetitionEndorsement](../../implementation/governance/PetitionEndorsement.md), original decision evidence and the later review time. The final partition is three accepted, one duplicate and two rejected. SG6 remains late even under R2.
6. The clerk executes the acceptance and creation of one [AgendaItem](../../implementation/governance/AgendaItem.md), storing its reference on the petition. Simulate loss of the result after commit and replay the same acceptance. Return the existing proposed item, preserve its original sequence and show one agenda item in the meeting. A simultaneous attempt to act from the declined version must re-read the current disposition.
7. A person who only hosts the meeting reads the public agenda. The host can see the authorized title after publication. The signers' identity evidence, contact endpoints and C's membership history stay restricted. A public total can be reported only if the body's disclosure policy permits that aggregate.

## Change one rule at a time

| Independent variation | Exact effect |
| --- | --- |
| C signs at 17:01 instead of 15:15 | Correcting class eligibility cannot make C timely. The restated count remains two, and no item is created. |
| B's endorsement is validly withdrawn at 16:55 and the withdrawal is recorded before the initial ruling | Initial accepted count is one. After C succeeds on review there are two. Keep B's withdrawal and do not create an item. |
| The corrected class starts 1 October | C is ineligible for this petition's September cutoff, even when the current profile displays full membership. Two accepted, no new item. |
| The same three accepted members file a separate petition for different business | Give it its own identity and endorsement evidence. No submission from the original petition counts automatically. |
| The agenda item is later deferred by the body | Keep all three accepted signatures and the original petition's accepted outcome. Only the agenda item's disposition changes. |

A passing run reconciles six timely-or-late submissions, six individual determinations and three counted rights after review. The meeting's eligible vote weight, presence and any eventual ballots are independently established. Admission of a petition creates none of them.
