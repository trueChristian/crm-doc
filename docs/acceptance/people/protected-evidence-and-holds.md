# Independent intake, evidence custody and overlapping holds

An anonymous submitter uses the independent route because the ordinary lead is implicated. The church's exercise policy permits an appointed alternate to receive the concern and authorizes a limited referral after human review. No real testimony, identities or attachments are required. Use short synthetic labels solely to determine whether unintended surfaces reveal them.

## Arrange the exercise

| Object | Test fact |
| --- | --- |
| Case PC8 | Received on 6 February. The named alternate A is eligible. Ordinary lead L and the general office administrator have no case-read grant. There is no verified reporter identity or safe response endpoint. |
| Entry E1 | A third-party account includes the synthetic phrase “cedar-window-seven”. Protect both the case and the phrase. |
| Evidence X | One original attachment is received with an integrity fingerprint. A separately identifiable working copy W has one redacted passage. |
| Grant G | Reviewer V can read the authorized case material from 08:00 through 09:00 on 7 February, end exclusive. V is not the evidence custodian. |
| Holds H1 and H2 | Two authorized [PreservationHold](../../implementation/platform/PreservationHold.md) records independently cover X and its case-linked working copies. |

## Receipt, original and correction

1. Accept PC8 without creating a member, person profile or endpoint. A repeated transmission bearing the same intake receipt returns the same restricted case through its authorized route. Two anonymous reports with the same wording and different submissions remain separate unless an authorized reviewer establishes a relation. Equal text cannot establish common authorship.
2. Route PC8 only to A. A general delivery confirmation is insufficient to fill the case acknowledgment time. Record the actual human acknowledgment. At the general office, searching for the case number and searching for a nonexistent case produce the same visible empty result. L receives no task that identifies the subject or reporter.
3. A takes receipt of X and records the evidence identifier, fingerprint, time and current custodian in [EvidenceCustody](../../implementation/people/EvidenceCustody.md). A second custodian B receives an approved transfer. Verify X against its saved fingerprint, append the transfer from A to B, and keep the original receipt. Replaying the same transfer returns the recorded movement. A stale request for a concurrent transfer from A to a third custodian must stop for review.
4. Compare W with the redaction authorization. Give X and W separate references and retain their relationship within the protected evidence area. W must not inherit a claim to be the unchanged original. An unauthorized request for X using a link obtained for W reveals neither X nor its title.
5. The reporter's account is subsequently corrected by an authorized person. Append [ProtectionEntry](../../implementation/people/ProtectionEntry.md) E2 with kind correction and reference E1. E1 remains a third-party account as received. An authorized timeline can show the event time, recording time and later correction without displaying the correction as evidence known at intake.

## Reader and referral observations

| ID | Operation | Required observation |
| --- | --- | --- |
| P01 | V opens the permitted material at 08:59. | Check case, actor, purpose and current grant, record access and return only the allowed original or working material. Read permission does not grant custody transfer. |
| P02 | V reopens at 09:00 through a previously seen reference. | The [ProtectionAccess](../../implementation/people/ProtectionAccess.md) window has ended. Deny renewed retrieval. The earlier authorized access event stays in the protected audit history. |
| P03 | The office administrator searches by phrase or requests autocomplete, a print preview and a bulk export. | No result, matching count, name, snippet or artifact attributable to PC8 appears. Public and general staff assisted search during this exercise cannot index or quote E1, E2, X or W. |
| P04 | A authorizes a [ProtectionReferral](../../implementation/people/ProtectionReferral.md) of W only, to named recipient S for the approved purpose. The send is completed with no response from S. | Record minimum fields, authority, actual sent time and one sent referral. Store no acknowledgment. The working copy, source and recipient must match the authorization before dispatch. |
| P05 | Recipient S later acknowledges by the original reference; the notification is processed twice. | One real acknowledgment with its observed time. One referral. The authorized reviewer can trace the exact redacted version. There is no record stating that X was released. |
| P06 | The same recipient requests the removed passage. | Open a fresh human authority decision if the request is pursued. The limited approval for W supplies no automatic release of X or a complete case history. |
| P07 | An automated operational reminder becomes due. | Use an authenticated destination and neutral wording. No case narrative or phrase appears in ordinary subject lines, calendars, team dashboards, general alerts or metrics broken down to one identifiable person. |

## Disposition ledger

- With H1 and H2 active, reaching a scheduled review date initiates review only. X, W, custody entries and covered evidence remain held according to the configured scope.
- Release H1 with its authorizing actor and actual time. Re-evaluate the selected material. H2 still blocks disposition of X and W. A delayed copy of H1's release must have no effect on H2.
- Release H2 under separate authority. A hold count of zero makes the material eligible for the ordinary retention decision. It does not certify that the retention period has elapsed, disposition was approved or copies were destroyed.
- If the specified rule permits destruction after both holds, review the originals, renditions, indexes and controlled exports in scope. Record actual performance or unresolved custody separately for each location. Do not certify deletion at the external recipient from an instruction alone.
- Reopen the concern after authorized closure. Re-evaluate access and any operative measures separately. No old reader grant revives automatically, no retired hold is silently reinstated, and the release record continues to describe the version actually disclosed.
