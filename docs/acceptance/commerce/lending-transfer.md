# Move a retail book into circulation and recover it after a loss charge

The bookstore and the lending desk share a counter. Five church-owned copies of a study book are held in retail inventory at 12.00 each. The approved fixture expenses books placed in lending service at transfer and tracks individual copies by accession. On permanent loss the library may assess a 20.00 charge after review. A recovered usable copy returned within the agreed 30-day remedy window qualifies for full credit. There is no administrative fee or tax.

Use four accounts with distinct roles: retail stock steward, circulation desk, finance reviewer and authorized refund worker. Use one borrower with a private contact destination and one different borrower waiting on the title.

## Retail custody to library accession

| Step | Command and evidence | Expected result |
| --- | --- | --- |
| Sale | One visitor buys one copy for 20.00 and takes it. | Debit cash 20.00, credit sales 20.00. Debit cost of sales 12.00, credit inventory 12.00. Four retail copies remain, value 48.00. |
| Transfer proposal | The librarian selects one available, unreserved retail unit. Include organization, variant, original lot, retail bin, purpose, receiving desk, transfer authority and stable action identity LIB-1. | Hold that physical unit for the approved handoff under the local process. Three remain freely promiseable. It has no circulation availability yet. |
| Custody handoff | The stock steward and librarian acknowledge the same physical copy and accession L-7. | Issue one unit from retail on LIB-1. Debit library materials expense 12.00, credit inventory 12.00. Create or activate one LoanCopy with accession L-7 linked to the title. Three retail units remain, value 36.00. |
| Public catalogue | Search for the title and select the lending desk. | One copy is available for loan. Its title, approved circulation status and campus may appear. There is no retail share of this copy and no public borrower identity. |

A barcode common to the edition identifies the retail variant or title. The accession identifies the individual lending copy. Scanning the cover code at the two desks must ask for the appropriate operation or copy evidence. If a buyer already holds the final eligible retail unit, the transfer must re-evaluate its selection under the hold policy before the librarian acknowledges custody.

## Issue, waiting list and loss assessment

1. Check out L-7 to borrower A with the due date and condition at handover. The status becomes on loan and there is exactly one open CirculationLoan. A subsequent reservation by borrower B joins the title queue without disclosing A's identity.
2. At the first overdue cutoff send the authorized reminder to A. The reminder records a contact attempt. The borrower still owes the physical copy under the existing loan. Record the due time, delivery decision and current loan status.
3. After the agreed waiting period an independent reviewer accepts evidence that L-7 is missing. Mark the copy missing and record disposition against the existing loan. The approved charge produces an issued invoice for 20.00, debit borrower receivable and credit loss recovery 20.00.
4. A pays the outstanding 20.00. Debit cash and credit receivable 20.00. The receivable is settled. The copy remains missing and B stays waiting. The retail register still has three units.
5. Two weeks after paying, A returns L-7 in usable condition. The receiver identifies the individual accession, records the recovery and inspects the book. The approved remedy reverses the original 20.00 assessment through a credit document to A. An inspection awaiting approval does not itself execute a payment.
6. Post debit loss recovery 20.00 and credit refundable customer balance 20.00 on the settled charge. On verified repayment debit that balance and credit cash 20.00. Present the assessment, receipt, credit and repayment as separate dated references. Draw no additional receipt clearing or merchandise return entry.
7. The recovered copy returns to eligible circulation and is held once for B under the queue policy. A private pickup notification goes to B. If B's hold expires, advance the queue from that offer's identity exactly once. Initial expense of 12.00 is unchanged under this consumption-at-transfer policy.

| Fixture balance | Before retail sale | After transfer | After loss payment | After recovery and refund |
| --- | ---: | ---: | ---: | ---: |
| Retail inventory units | 5 | 3 | 3 | 3 |
| Retail inventory value | 60.00 | 36.00 | 36.00 | 36.00 |
| Net new cash | 0.00 | 20.00 | 40.00 | 20.00 |
| Net loss recovery income | 0.00 | 0.00 | 20.00 | 0.00 |
| Lending materials expense | 0.00 | 12.00 | 12.00 | 12.00 |
| Unique lending copies | 0 | 1 | 1 | 1 |

## Replay, data access and alternative outcomes

- **Lost accession acknowledgement.** After the library accepts LIB-1 but before the counter receives its response, resubmit the same handoff. The library resolves L-7 and finance resolves the existing 12.00 posting. Until acknowledgement, keep the physical copy under pending custody and suppress additional issue or sale. If inspected lists disagree, compare one retail issue to one accession.
- **Another copy with the same title turns up.** Record the found item for identification. Do not satisfy A's loan or issue a refund by title alone. If policy accepts a replacement rather than recovery of L-7, record a separately authorized replacement accession and the disposition of L-7.
- **Recovery arrives before A paid.** Restart from step 3. Credit the original 20.00 receivable and use the credit against its open balance. Cash refund is zero. If A already paid 8.00, apply 12.00 to the unpaid balance and leave 8.00 refundable. The original paid/unpaid split must survive replay.
- **A second return follows the first.** A duplicate scan resolves to the original return and does not cancel B's hold. A distinct physical copy presents an unresolved identity. Neither path should produce a second 20.00 credit.
- **Desk privacy.** The bookkeeper sees the charge, payer reference and adjustment, with purpose-limited evidence for approval. The circulation worker sees the copy, loan and outcome of the fee decision. The shop cashier cannot open circulation history from a retail transaction. B has no access to A's identity or charges.
- **Close review.** Trace one 12.00 retail sale issue and a separate 12.00 reclassification to library materials. Retail margin on the sale is 8.00. Show the separate materials expense without combining it into sales returns or the 20.00 borrower credit.

See [inventory and custody](../../commerce/inventory.md), [LoanCopy](../../implementation/administration/LoanCopy.md), [CirculationLoan](../../implementation/administration/CirculationLoan.md), [LoanReservation](../../implementation/administration/LoanReservation.md) and [CustomerCredit](../../implementation/finance/CustomerCredit.md).
