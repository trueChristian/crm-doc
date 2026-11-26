# PledgeInstallment

One due amount and date in an accepted giving schedule.

Derive progress from linked verified allocations and effective adjustments, separately displaying waivers. An excess gift requires instructions before assignment elsewhere. A returned payment can reopen an installment.

Organization scope, revision and audit information follow the [shared record conventions](../../foundation/record-conventions.md).

## Fields

| Field | Declaration | Use |
| --- | --- | --- |
| `pledge_id` | `ref Pledge` | Parent promise. [Pledge](Pledge.md). |
| `sequence` | `integer` | Unique installment in the pledge. |
| `due_on` | `date` | Effective local due date. |
| `target_amount` | `money` | Due portion, in the pledge currency. |
| `waived_amount` | `money` | Portion formally released, zero at creation. |
| `waiver_ref` | `protected_ref?` | Authorized evidence for changed obligation. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [GiftAllocation](GiftAllocation.md).`pledge_installment_id` | PledgeInstallment identity | Reconcile the reference in the source record and preserve its correction history. |

## Acceptance decision

A 50 installment has a 30 allocation and then a return of 10. It displays 20 received and 30 outstanding. An automatic reminder still respects contact permissions.

[Offerings, gifts and donor correspondence](../../finance/giving.md) · [Giving record index](README.md)
