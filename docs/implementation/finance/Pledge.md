# Pledge

A donor’s accepted promise to support a purpose on an agreed schedule.

An active schedule totals the agreed promise. A revised edition distinguishes amounts already received from remaining commitments. Fulfillment follows eligible net allocations. A pledge creates no collection, payment mandate or receipt.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `giving_party_id` | `ref GivingParty` | Party making the promise. [GivingParty](GivingParty.md). |
| `fund_id` | `ref Fund` | Intended use. [Fund](Fund.md). |
| `agreed_on` | `date` | Date of consent to the terms. |
| `currency` | `code` | Currency of the schedule. |
| `promised_amount` | `money` | Total commitment. |
| `conditions` | `protected_text?` | Matching, timing or other written terms. |
| `prior_pledge_id` | `ref Pledge?` | Prior edition when amended. [Pledge](Pledge.md). |
| `state` | `proposed/active/fulfilled/withdrawn/superseded` | Status of terms and progress. |
| `evidence_ref` | `protected_ref` | Signed or confirmed instruction. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AcceptedGiftLink](../development/AcceptedGiftLink.md).`pledge_id` | Pledge identity | Reconcile the reference in the source record and preserve its correction history. |
| [AppealAsk](../development/AppealAsk.md).`pledge_id` | Pledge identity | Reconcile the reference in the source record and preserve its correction history. |
| [MatchOffer](../development/MatchOffer.md).`pledge_id` | Pledge identity | Reconcile the reference in the source record and preserve its correction history. |
| [PartnerPromise](../development/PartnerPromise.md).`finance_pledge_id` | Pledge identity | Reconcile the reference in the source record and preserve its correction history. |
| [Pledge](Pledge.md).`prior_pledge_id` | Pledge identity | Reconcile the reference in the source record and preserve its correction history. |
| [PledgeInstallment](PledgeInstallment.md).`pledge_id` | Pledge identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A pledge to give 600 over twelve installments receives 50. The donor later cancels future installments. Confirmed money remains 50 and the eleven cancelled installments stop generating reminders.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
