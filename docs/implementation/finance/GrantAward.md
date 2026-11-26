# GrantAward

Administrative record of signed incoming or outgoing mission support or grant terms.

An award ceiling describes the agreement. Keep actual transfers, requested draws, recognized income and sponsor acceptance separate. Changes to amount or scope require a new approved edition with its effective date.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `organization_id` | `ref Organization` | Church administering the relationship. [Organization](../foundation/Organization.md). |
| `direction` | `incoming/outgoing` | Church as grantee or sponsor. |
| `sponsor_ref` | `protected_ref` | Verified sponsor. |
| `recipient_ref` | `protected_ref` | Grantee or authorized partner. |
| `external_award_key` | `text` | Identifier within the issuing sponsor. |
| `fund_id` | `ref Fund?` | Designated purpose, if applicable. [Fund](Fund.md). |
| `currency` | `code` | Award currency. |
| `approved_ceiling` | `money` | Maximum in accepted agreement. |
| `start_on` | `date` | Earliest authorized activity. |
| `end_on` | `date` | End of current terms. |
| `terms_ref` | `protected_ref` | Signed edition and evidence of authority. |
| `state` | `proposed/accepted/active/suspended/closed/terminated` | State of the relationship. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AwardDecisionReview](../development/AwardDecisionReview.md).`finance_award_id` | GrantAward identity | Reconcile the reference in the source record and preserve its correction history. |
| [AwardMilestone](AwardMilestone.md).`award_id` | GrantAward identity | Reconcile the reference in the source record and preserve its correction history. |
| [GrantApplication](../development/GrantApplication.md).`award_id` | GrantAward identity | Reconcile the reference in the source record and preserve its correction history. |
| [PartnerPromise](../development/PartnerPromise.md).`finance_award_id` | GrantAward identity | Reconcile the reference in the source record and preserve its correction history. |
| [SponsorReport](../development/SponsorReport.md).`award_id` | GrantAward identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A sponsor offers 8,000 on an application for 12,000. Publish the signed revised ceiling of 8,000 once approved. Cash remains zero until actual receipt is reported.

[Designations, restrictions and grant obligations](../../finance/stewardship.md) · [Giving record index](README.md)
