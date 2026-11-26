# AwardMilestone

A delivery, report, approval or activity that the church agreed to evidence to a sponsor.

Require authorization to disclose names, images and individual stories. A missed date escalates to a responsible officer. An accepted narrative report alone conveys no disbursement authority.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `award_id` | `ref GrantAward` | Parent agreement and scope. [GrantAward](GrantAward.md). |
| `title` | `text` | Concrete reporting or delivery obligation. |
| `kind` | `deliverable/report/condition/follow_up` | Effect specified by agreement. |
| `due_on` | `date` | Local date or deadline in the sponsor’s stated zone. |
| `owner_id` | `ref UserAccount` | Responsible person. [UserAccount](../platform/UserAccount.md). |
| `evidence_required` | `text` | What the sponsor expects to see. |
| `submission_ref` | `protected_ref?` | Actual edition or evidence sent within disclosure authority. |
| `decision_ref` | `protected_ref?` | Sponsor acceptance, refusal or amendment. |
| `state` | `scheduled/submitted/accepted/returned/waived` | Administrative status. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [SponsorReport](../development/SponsorReport.md).`milestone_id` | AwardMilestone identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A sponsor accepts a quarterly report and requests more evidence on equipment expenditure. Close the narrative milestone. Open a separate evidence follow-up for the cost and retain the accepted edition.

[Designations, restrictions and grant obligations](../../finance/stewardship.md) · [Giving record index](README.md)
