# Correct a translated service notice between approval and handoff

A service moves rooms while a translated notice is scheduled. Exercise the handoff from the event steward to the translator, approver and delivery worker. A fluent reviewer, dispatch approver and event steward are different accounts in this run. All times are UTC on the same fixture day.

## Seed the organization

| Key | Start value |
| --- | --- |
| Service 17 | Approved event publication from occurrence revision 4. Start 16:30, room North. The steward approves venue and time changes. |
| Translation policy T3 | General events, approved public fields, drafting only. The service's restricted accessibility arrangements are outside the input boundary. |
| Assistant edition A2 | Cleared for this language and operation. A retranslation under a later approved model uses its own edition identity. |
| Recipients M and N | Both permit personal service notices in this language, each at a separate verified destination. Both are eligible in frozen audience S8. |
| Source edition P4 | Includes event title, time and authorized public room name. Excludes individual adjustment requests and staff-only directions. |
| Approval scope | The approval binds the source revision, signed proof, selected language/channel template edition and audience snapshot. |

## Establish the previous edition

1. At 09:00 the translator requests wording for P4. The run identifies T3, A2, the actor and this service. Evidence identifies the inspected source edition and permitted fields. Check the actual packaged inputs, including associated files and their descriptions. A restricted arrangement mentioning the same room contributes zero fields and zero file references.
2. The draft incorrectly gives 16:00. A fluent reviewer compares it with P4, requests a correction and records the affected time. The review of this version has no domain publication result. Counting deliveries, submissions and new publication approvals gives zero each.
3. A corrected version names North and 16:30. Preserve the superseded draft and review under its access limit. The reviewer accepts this precise wording. The communications editor produces approved template edition L4. The dispatch approver signs proof H4 against S8. The dispatch is scheduled for 09:30. Neither recipient has been contacted.
4. At 09:29 the steward approves P5 with room South and unchanged time. Member N withdraws this purpose before the first handoff. Retain the received and effective times of the withdrawal. Do not edit the older audience snapshot or destroy approval H4.

## Run the scheduled worker

| Observation | Expected result |
| --- | --- |
| The worker resolves L4 to its signed source at 09:30 | The source changed materially. Hold or cancel release of the obsolete rendering. There are zero handoffs for P4 and no provider charge. |
| The translator opens the old draft | The former proof may be inspected as history only by someone still permitted to read it. The work queue identifies the changed edition without exposing member N. |
| A fluent reviewer compares L5 with P5 | L5 contains South and 16:30 in both the standard and accessible text. An earlier approval for L4 cannot satisfy this review. |
| The approver signs H5 | Bind the specifically reviewed edition, source and audience. Retain the link to the cancelled or superseded instruction so the two proofs can be distinguished. |
| Worker executes the new release | M remains eligible. N is excluded after evaluating the live purpose decision. A missing eligible language rendition holds that recipient unless an explicitly permitted fallback was approved. |
| The scheduler replays twice | Exactly one intended handoff for M under the new dispatch; zero for N and zero under H4. No fallback is triggered for the withdrawal. |

Reconcile historical eligibility (2), current exclusions (1), eligible recipients released (1), handoffs to M (1) and provider-confirmed deliveries (0 until a verified observation arrives). One authorization to send and one external acceptance do not establish that M read the text.

## Branch at the handoff boundary

Reset to step 3. In this independent run, M's P4 handoff was accepted at 09:28 and N's is still queued when P5 arrives. Preserve the P4 attempt and its original proof. Suppress the unsubmitted obsolete copy. Under this fixture's correction policy send M one authorized correction for the new room and send N zero copies after withdrawal. Totals across the incident are two handoffs to M across two editions, zero to N, one corrected fact and one active event occurrence. A sender cannot recall M's already received copy by rolling back P4 locally.

If the model becomes unavailable after P5, the fluent editor can create L5 manually from the approved source. It still takes a fresh comparison and dispatch approval. Record no successful assistant run for this manual edit. Verify that a keyboard-only approver can inspect room, time, language and recipient policy on the same proof the signature binds.

Use the field contracts for [EventOccurrence](../../implementation/ministry/EventOccurrence.md), [AssistanceRun](../../implementation/platform/AssistanceRun.md), [EvidencePin](../../implementation/platform/EvidencePin.md), [AssistanceReview](../../implementation/platform/AssistanceReview.md), [TemplateEdition](../../implementation/communications/TemplateEdition.md), [PublicationApproval](../../implementation/communications/PublicationApproval.md) and [DispatchRecipient](../../implementation/communications/DispatchRecipient.md).
