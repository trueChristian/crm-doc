# Hire a hall, inspect it and release a refundable deposit

An outside group hires a hall for 240.00 and pays a separate 150.00 security deposit. The agreement permits an evidenced damage assessment and repayment of the balance. The example recognizes hire revenue when the agreed service completes. Tax and processing fees are zero. A steward controls the booking, a separate inspector signs the condition report, finance assesses amounts and treasury executes the return.

## Reserve and collect

The hall has a confirmed layout capacity of 60. The booking covers 14:00 through 16:00 with 30 minutes of setup and 20 minutes of reset. Record 55 expected people. The occupied interval is [13:30, 16:20). An unrelated group requests a partition that excludes the hall.

| Competing proposal | Expected decision |
| --- | --- |
| Partition requested from 13:00 to 13:30 without setup/reset | The intervals touch but do not overlap. Proceed if all other checks pass. |
| Partition requested from 16:15 to 17:00 without buffers | Five minutes overlap the hall reset. Return the conflict and first possible boundary of 16:20, subject to other bookings. |
| Partition requested from 16:25 with ten minutes of setup | Effective start 16:15 conflicts. The earliest activity start with that setup is 16:30. |
| The same group raises expected attendees to 61 | Hold the proposed change for a new layout or allocation. The accepted 55-person version and existing calendar occupation remain identifiable. |

Confirm the 390.00 bank receipt with a finance reference and identify both portions on the rental agreement. Record debit bank 390.00, credit deferred hire 240.00 and credit refundable deposit liability 150.00. Prevent advance hire and deposit from inflating income. The renter's confirmation shows 240.00 as the hire price and shows how the separate 150.00 can be applied or returned. A tentative booking, proof-of-payment image or unpaid agreement on its own creates no confirmed bank receipt.

## Inspect, assess and pay

| Time | Desk action | Observable evidence |
| --- | --- | --- |
| 13:30 | Steward grants access at setup and records key handover. | Custody reference, recipient and due time appear on the restricted issue. Public calendar shows the agreed availability only. |
| 16:00 | Lead verifies that agreed hire concluded. | Release 240.00 deferred hire to income once. A missing key is a separate follow-up. |
| 16:20 | Inspector sees a damaged chair. A competing staff note estimates 60.00. | Keep both observations with their authors and time. Release the occupied interval upon completed reset. Freeze the unresolved deposit portion under the agreement. A private photo stays outside public calendar and ordinary invoice attachments. |
| Next day | A reviewer accepts 25.00 for the documented damage, issues the assessment and obtains approval to apply the deposit. | Debit renter receivable 25.00, credit damage recovery 25.00. Apply only 25.00 by debiting the deposit liability and crediting that receivable. Show remaining refundable 125.00. |
| Next day | Override the proposed return destination without the required payer verification. | Hold execution while retaining the approved 125.00 liability. A payment request to an unrelated organizer supplies no authority. |
| After verification | Treasury repays 125.00 to the approved payer and receives confirmation. | Debit refundable deposit liability 125.00, credit bank 125.00. Renter statement shows 150.00 deposit received, 25.00 applied, 125.00 repaid and zero deposit outstanding. |
| After repair | Accept and pay the repair bill for 31.00 under operating-expense policy. | Debit repair expense 31.00 and credit payables 31.00 on approval. Debit payables 31.00 and credit bank 31.00 on payment. |

Close only when custody items and work orders have their own disposition and each finance handoff is acknowledged or assigned to an accountable exception owner. The deposit liability and renter receivable both end at zero. The net bank movement is 234.00 (390.00 less 125.00 and 31.00). Income of 240.00 plus damage recovery of 25.00 less repair expense of 31.00 also equals 234.00. The difference of 6.00 between assessed and actual damage costs remains visible.

## Independent recovery branches

1. **Inspector withdraws before finance approves.** From the inspection checkpoint, append a correction with evidence that the chair was already damaged at check-in. Authorize return of the full 150.00. No damage assessment or application belongs to this branch. Hire income remains 240.00. Charge repairs to the appropriate owner under a separate decision.
2. **Duplicate release after a lost acknowledgement.** From the verified 125.00 repayment checkpoint, simulate a missing return status. Look up the original transfer and confirm it before permitting another instruction. Record one 125.00 bank debit even when both rental and treasury workers retry.
3. **Damage decision arrives after full refund.** From branch 1, approve a new evidence review. The available deposit is zero. A separately authorized claim, if the agreed policy permits one, creates a receivable and notification. It cannot re-open an applied deposit or withdraw money from the payer.
4. **Repairs make the room unsafe.** Add a dated closure with a public label such as “maintenance.” Reassess each affected future booking. An alternative hall with capacity 48 cannot automatically replace a 55-person commitment. Give the renter an authorized alternative, amendment or cancellation with its own financial disposition.
5. **Material must be disclosed selectively.** The key steward sees the issued item and return status. The next renter sees confirmed availability. The payer sees the approved assessment, necessary evidence through the authorized sharing route and repayment status. An unassigned volunteer cannot see entry instructions, private incident correspondence, inspection photos or payout destination.

The [RoomBooking](../../implementation/ministry/RoomBooking.md) and [FacilityRental](../../implementation/ministry/FacilityRental.md) describe the commitment and finance references. [ResourceWorkOrder](../../implementation/ministry/ResourceWorkOrder.md) describes the repair, [AccessItemIssue](../../implementation/ministry/AccessItemIssue.md) the key and [receivables](../../finance/receivables.md) the separate financial events.
