# FundRestriction

Evidence of terms governing what the church agreed to do with a designation or gift.

Keep donor conditions, internal board decisions and pass-through beneficiary instructions distinguishable. An authorized change preserves previous wording and applicability. Send a minimal purpose code externally and release supporting evidence only with specific authority.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `fund_id` | `ref Fund` | Church purpose. [Fund](Fund.md). |
| `giving_party_id` | `ref GivingParty?` | Party imposing terms where applicable. [GivingParty](GivingParty.md). |
| `kind` | `donor_purpose/time/agency/board_designation` | Source of the instruction. |
| `terms` | `protected_text` | Effective wording from the authorizing instrument. |
| `valid_from` | `date` | First effective date. |
| `valid_to` | `date?` | End under approved terms. |
| `reviewer_id` | `ref UserAccount` | Authorized reviewer. [UserAccount](../platform/UserAccount.md). |
| `evidence_ref` | `protected_ref` | Source of authority, beneficiaries and exception procedure. |
| `prior_restriction_id` | `ref FundRestriction?` | Previous edition on amendment or waiver. [FundRestriction](FundRestriction.md). |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AcceptedGiftLink](../development/AcceptedGiftLink.md).`fund_restriction_id` | FundRestriction identity | Reconcile the reference in the source record and preserve its correction history. |
| [FundRestriction](FundRestriction.md).`prior_restriction_id` | FundRestriction identity | Reconcile the reference in the source record and preserve its correction history. |
| [GiftAllocation](GiftAllocation.md).`restriction_id` | FundRestriction identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A board vote proposes a new use for a donor-restricted building gift. Offer to obtain authorized redirection or arrange a return. The vote alone cannot alter the donor instruction.

[Designations, restrictions and grant obligations](../../finance/stewardship.md) · [Giving record index](README.md)
