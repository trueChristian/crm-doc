# Fund

A church giving designation or collection purpose available to a donor or clerk.

The CRM designation identifies donor intent. External accounting maps it to the appropriate destination. Retiring a designation blocks new intake and preserves historical use, corrections and printed wording.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `organization_id` | `ref Organization` | Entity authorized to accept the purpose. [Organization](../foundation/Organization.md). |
| `code` | `text` | Stable church designation code. |
| `name` | `text` | Display name, including permitted language variants. |
| `purpose` | `text` | Approved use and what happens if it cannot be fulfilled. |
| `owner_id` | `ref UserAccount` | Officer responsible for the purpose. [UserAccount](../platform/UserAccount.md). |
| `active_from` | `date` | First day on which new allocations may be accepted. |
| `active_to` | `date?` | End of availability for new designations. |
| `instruction_ref` | `protected_ref?` | Donor-facing wording or authorizing decision. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [FundraisingAppeal](../development/FundraisingAppeal.md).`finance_fund_id` | Fund identity | Reconcile the reference in the source record and preserve its correction history. |
| [FundRestriction](FundRestriction.md).`fund_id` | Fund identity | Reconcile the reference in the source record and preserve its correction history. |
| [GiftAdjustment](GiftAdjustment.md).`destination_fund_id` | Fund identity | Reconcile the reference in the source record and preserve its correction history. |
| [GiftAllocation](GiftAllocation.md).`fund_id` | Fund identity | Reconcile the reference in the source record and preserve its correction history. |
| [GiftOfferAssessment](../development/GiftOfferAssessment.md).`intended_fund_id` | Fund identity | Reconcile the reference in the source record and preserve its correction history. |
| [GrantAward](GrantAward.md).`fund_id` | Fund identity | Reconcile the reference in the source record and preserve its correction history. |
| [Pledge](Pledge.md).`fund_id` | Fund identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

Two campuses call a designation “Missions”. Mapping by scoped code assigns the correct one. An archived code remains visible on a previously issued private statement.

[Designations, restrictions and grant obligations](../../finance/stewardship.md) · [Giving record index](README.md)
