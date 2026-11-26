# Sponsor benefit shortfall and mixed-purpose payment

A sponsor pays 1,200 under signed terms. The parties explicitly identify an unconditional 720 gift and 480 consideration for two equal advertising placements. The church has approved the split and recognizes each 240 exchange obligation on accepted delivery. This fixture has no taxes, transaction fees or inventory. The agreement requires a cash refund for each missed placement unless the sponsor accepts a replacement.

## Assign the sources

| Document | Inputs and ownership |
| --- | --- |
| [Sponsorship benefit](../../implementation/development/SponsorshipBenefit.md) | Two placements, 240 per placement, one audience, approved artwork and a named acceptance condition. Retain both amounts and valuation evidence separately from any public sponsor label. |
| [Delivery](../../implementation/development/BenefitDelivery.md) | One row for the accepted placement. Record a shortfall on the second and attach the sponsor's signed refund decision to make_good_ref. |
| [Gift](../../implementation/finance/Gift.md) | The capture references the transfer of 1,200. The actual gift portion is 720. Store one allocation for 720, zero benefit against that independently designated gift, under the approved purpose. |
| [Obligation](../../implementation/finance/RevenueObligation.md) | Track the 480 exchange portion on the source document, its two separately verifiable units, delivery evidence, recognized total and remaining balance. |
| [Partnership cash delivery](../../implementation/development/PartnershipDelivery.md) | Tie the gift and exchange portions to their owning allocation and invoice line with distinguishable source delivery keys. Both resolve the same remittance without attributing 1,200 to each. |
| [Impact evidence](../../implementation/development/ImpactEvidenceLine.md) | Report one accepted placement out of two. Do not infer visitor counts, gift consent or participant releases from the remittance. |

The institution issues a single mixed payment request with two lines. Under this fixture posting occurs on receipt and delivery. An operational invoice used to split the remittance cannot separately debit bank or record the contribution.

## Journal and settlement

| Entry | Debit | Credit | Amount |
| --- | --- | --- | ---: |
| S1 | Bank | Sponsor contribution income | 720.00 |
| S1 | Bank | Deferred placement income | 480.00 |
| S2 | Deferred placement income | Placement income | 240.00 |
| S3 | Deferred placement income | Refund payable | 240.00 |
| S4 | Refund payable | Bank | 240.00 |

Record S2 only after the accepted first placement. A reminder about the due second placement leaves balances unchanged. S3 falls in the next reporting period when the sponsor selects cash and the authorizer approves it. S4 requires payment confirmation. Preserve the original invoice and issue the applicable credit only against the exchange portion. Where a payment system needs an execution key, use the original refund obligation and its one approved outgoing payment.

| Control | After S1 | After S2 | After S3 | After S4 |
| --- | ---: | ---: | ---: | ---: |
| Book bank | 1200 | 1200 | 1200 | 960 |
| Contribution income | 720 | 720 | 720 | 720 |
| Earned placement income | 0 | 240 | 240 | 240 |
| Unperformed obligation | 480 | 240 | 0 | 0 |
| Refund payable | 0 | 0 | 240 | 0 |
| Appeal gift cash | 720 | 720 | 720 | 720 |

The sponsor reconciliation reads money paid 1,200, money refunded 240, retained 960. The two retained purposes are gift 720 and performed service 240. The published period-one statement retains its 240 unperformed amount even after the next-period refund. A restricted donor statement includes only the 720 permitted gift.

## Alternative resolution and failures

| Trigger | Expected decision |
| --- | --- |
| Sponsor chooses an equal replacement instead of cash while S3 is still unapproved | Save evidence of the replacement and retain the 240 contract liability. On accepted replacement, debit deferred placement income 240, credit placement income 240. Closing bank 1,200, gift 720, placement income 480. |
| Refund and accepted replacement arrive together | Resolve the sponsor's authorized remedy once. A conflict enters review. The same 240 cannot produce both earned income and a refund payment. |
| Sponsorship coordinator chooses a replacement after S4 | The original exchange obligation is settled. Require an independently authorized new service arrangement or recovery before promising another chargeable placement. |
| A recipient returns the original remittance identifier while capturing the gift record | Resolve the original split and the balance of the exchange obligation. Bank at S1 remains 1,200, contribution 720, deferred balance 480. |
| Edition 1 used a public sponsor logo and the agreement then terminates | Stop future unauthorized logo placements, keep the restricted evidence of the delivered first placement, and preserve the historical count and finance entries. |
| Sponsor asks for donor or attendee details to make up the missed placement | The deliverable and refund authorities confer no access to participant records or individual donation amounts. The shortfall remains on the contract until a permitted remedy settles it. |
