# Pastoral cover, referral delivery and staff return

One office request produces a private pastoral case and a practical visit. An absent employee has a named deputy for scheduling. The church uses an independently assigned clinician or external service only when it has approved a specific referral. The fixture names a generic receiving service and tests the exchange evidence.

## Set up Monday's caseload

| Identifier | State at 08:00 |
| --- | --- |
| OR5 | One [OfficeRequest](../../implementation/administration/OfficeRequest.md) records a safe callback and a neutral request to be contacted. |
| CR5 / CC5 | One accepted [CareRequest](../../implementation/people/CareRequest.md) and one open [CareCase](../../implementation/people/CareCase.md) with coordinator K, a restricted note, and a review due Thursday. |
| V5 | A [CareContact](../../implementation/people/CareContact.md) for a meal delivery is planned at 12:00. Volunteer V may see the delivery time and agreed instructions. |
| CA5 | A [CareAssignment](../../implementation/people/CareAssignment.md) grants K case coordination. A separate approved visitor assignment grants V access for the meal only. |
| AC5 | [ResponsibilityCover](../../implementation/platform/ResponsibilityCover.md) allows deputy D to claim scheduling tasks during K's absence from Monday 09:00 through Wednesday 09:00, end exclusive. |
| DC5 | [CareDisclosure](../../implementation/people/CareDisclosure.md) authorizes one named receiving service to receive wording “Please arrange an introductory appointment” for the agreed referral purpose by the named channel. There is no permission for bulletin publication. |

Every successful change has an owner, time and purpose. Use OR5 as the office's neutral tracking reference. A description of the pastoral conversation belongs only to the care owner.

## Exercise the handover

| ID | Action | Expected record and operator view |
| --- | --- | --- |
| C01 | At 09:01 D claims an available scheduling task and attempts to open the signed case note. | D acquires one task. The task has a neutral label. Scheduling cover alone cannot open CC5's restricted note, even through direct lookup or a saved search. |
| C02 | At 09:03 the supervisor assigns D a case-specific visitor duty limited to recording the meal attempt. | D can now record the agreed action within its dates. D cannot change DC5, approve a referral, print the case or browse prior notes. The supervisor can see the particular assignment that enabled the new action. |
| C03 | At 12:00 V finds no answer and reports an attempted delivery. D's older screen proposes to mark the same visit completed. | V5 is attempted with its observed outcome and empty completion time. D's stale write returns a conflict. Re-reading permits a new evidenced action. The attempted visit contributes zero completed visits. |
| C04 | At 12:05 V arranges a separately agreed visit for 14:00, and at 14:10 records actual delivery on that contact. | Show one attempted and one completed contact. The second has the actual completion time. The case stays open for Thursday's review. Family and public calendars show only the authorized representation. |
| C05 | An authorized coordinator creates [CareReferral](../../implementation/people/CareReferral.md) RF5 and approves only the DC5 wording. A sender submits it at 15:00 and loses the response. | A repeated attempt reconciles with the original dispatch. Accepted dispatch records one sent referral and no recipient acknowledgment. Keep an unresolved delivery visible if the recipient cannot identify the original dispatch. Do not announce receipt from a send success. |
| C06 | At 15:30 the approved service acknowledges the original reference twice. | RF5 has one effective acknowledgment at 15:30. It contains the approved scope and no pastoral note. The Thursday review stays scheduled. A search by the public bulletin editor finds no publishable item. |
| C07 | At 16:00 the subject withdraws DC5. The recipient asks for supplementary details under the original referral. | Timestamp the withdrawal. Deny further disclosure under DC5. The earlier sent wording, recipient and acknowledgment remain visible only for authorized review. Never certify removal of a copy beyond the church's control without evidence. |
| C08 | At the Wednesday 09:00 boundary D tries to re-claim an unassigned scheduling task. | AC5 no longer confers cover. End D's temporary visitor assignment at its agreed boundary as a distinct action. The coordinator returning to work reviews unresolved tasks; the completed visit does not reopen. |

## Counterfactual checks

- **Withdrawal before dispatch.** Reset to C05 with RF5 authorized and no send. Revoke DC5 at 14:59 and attempt the 15:00 dispatch. Refuse the handoff, withdraw the referral under the case owner's process, retain a blank sent time and no acknowledgments. The main-script C07 history cannot be substituted for this case.
- **External delivery accepted, acknowledgment missing.** Set RF5 to sent at 15:00 and remove all acknowledgment evidence. The reviewer sees one outstanding acceptance at the next review. Reconcile using the reference and an approved contact route. A second receiver is a different audience and requires its own decision.
- **Coordinator returns early.** End cover at Tuesday 10:00, then let D attempt a claim at 10:01. The claim is unavailable under AC5. Keep K's original work, the history of D's completed actions and the authorized substitute for any independently assigned case. Ending cover and ending care access have separate accountable owners.
- **Correction after signature.** A reviewer identifies an erroneous date in the original signed [CareNote](../../implementation/people/CareNote.md). The author records a linked correction and effective date. Previously released referral wording and original visit times remain as issued. The office clerk receives no new narrative or notification.
