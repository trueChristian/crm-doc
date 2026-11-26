# Estate distribution, fixed asset and return of unused funds

An estate tells the church it may receive 10,000 for replacement sound equipment. No right is enforceable at notification in this fixture. The verified estate later distributes 8,200 subject to a signed condition. Recognize only actual qualifying purchases. Unused cash must be returned. The church can acquire and control the equipment indefinitely once the acquisition condition has been satisfied. The fund has zero opening balance.

## Handoffs

| Owner | Source or evidence |
| --- | --- |
| [Estate contact](../../implementation/development/LegacyNotice.md) | Record the confidential estimate, disclosure scope and review date. A second notification quoting the earlier estate reference updates the case history. |
| [Offer acceptance](../../implementation/development/GiftOfferAssessment.md) | Verify the representative's authority and the restricted purchase terms. Preserve currency, stated_terms, intended_fund_id and decision evidence. |
| [Accepted link](../../implementation/development/AcceptedGiftLink.md) | The accepted_version and handoff_key identify the finance record for the 8,200 actual distribution. An already acknowledged handoff is retrievable after retry. |
| [Restriction](../../implementation/finance/FundRestriction.md) | Keep purchase eligibility, return duty and the authority to determine eligible installation costs. Public finance reports need no executor identity. |
| [Asset funding](../../implementation/finance/AssetFundingPart.md) | One funding part of 7,800 links the equipment asset with the estate source and restriction. Hardware and necessary installation appear as two source costs. |
| [Depreciation](../../implementation/finance/DepreciationCharge.md) | Start on commissioning under a full-month rule. Zero residual, 60 months, straight line. The contract sets no continuing use restriction after qualifying acquisition. |

The vendor invoices hardware 7,500 and required installation 300. The church pays both directly. A separately quoted optional maintenance contract of 450 is declined and never ordered. On commissioning the officer verifies the capitalizable purchase and original donor condition. Keep receipt of 8,200, qualifying expenditure of 7,800, and refund of 400 distinct in giving and finance reports.

## Post the events

| Entry | Debit | Credit | Amount |
| --- | --- | --- | ---: |
| E1 | Bank | Conditional estate advance | 8200.00 |
| E2 | Equipment awaiting commissioning | Bank | 7500.00 |
| E2 | Equipment awaiting commissioning | Bank | 300.00 |
| E3 | Equipment in service | Equipment awaiting commissioning | 7800.00 |
| E4 | Conditional estate advance | Estate contribution income | 7800.00 |
| E5 | Conditional estate advance | Bank | 400.00 |
| E6 | Depreciation expense | Accumulated depreciation | 130.00 |

The terms require commissioning evidence for E4. E1 through E2 leave 8,200 of conditional advance and 400 bank pending that evidence. E3 and E4 may share an atomic completion event if the book can still trace both purposes. E5 is the actual return transfer. E6 is the first full-month charge.

## Reconcile the estate file and asset

| Measure | After E1 | After E4 | After E6 |
| --- | ---: | ---: | ---: |
| Historical estimate | 10000 | 10000 | 10000 |
| Cumulative estate cash received before returns | 8200 | 8200 | 8200 |
| Estate cash returned | 0 | 0 | 400 |
| Estate advance liability | 8200 | 400 | 0 |
| Capitalized and commissioned cost | 0 | 7800 | 7800 |
| Accumulated depreciation | 0 | 0 | 130 |
| Bank | 8200 | 400 | 0 |
| Net assets from this activity | 0 | 7800 | 7670 |

Book value at E6 is 7,670 and the next 59 scheduled charges total 7,670. An accepted estate acknowledgement can distinguish the 8,200 entrusted, 7,800 used and 400 returned, according to document policy. The difference of 1,800 between the estimate and the actual distribution generates an estate-history explanation and zero accounting loss.

## Failure, replay and disclosure

| Attempt | Expected observable outcome |
| --- | --- |
| Import the notice as a pledge and then as a receipt | The estimate's nonbinding terms keep it out of both collectible receivables and cash. E1 is tied to actual remittance. |
| Approve E4 from a draft installation quote | No qualifying release. The reviewer sees incomplete proof of commissioning and the full conditional balance. |
| Add 450 for the declined optional contract to the asset | Acquisition and funding evidence support only 7,800. The unsupported item cannot pass asset reconciliation. |
| Reprocess the equipment import after facilities already created a physical item | Finance attaches the existing physical reference, retains one funded asset and produces no new acquisition or E4. |
| Run depreciation twice or in parallel for the first full period | One effective charge of 130 on the schedule and one net 130 on the ledger. |
| Close the estate case with the 400 still in the bank | Flag the unreturned funds and assign the return. Record actual transfer evidence before final settlement. |
| A technician opens the equipment origin from the physical register | Authorized access can show serial, location and in-service date. The estate's documents and private representative contacts stay behind their own authority checks. |
