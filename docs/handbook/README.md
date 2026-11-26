# Implementation handbook

Start with a church task, then use the record and conformance material to design the screen, import, report or integration for that task. An accepted command, an approved change, a published fact, a cash movement and a notification are separate events. A single form submission may produce some of these and leave others awaiting review.

| Work to implement | Manual |
| --- | --- |
| Identity, households, formal membership, casework and independent assurance | [People, care and protection](people/README.md) |
| Worship, rooms, serving, admissions, teaching and supervised collection | [Ministry operations](ministry/README.md) |
| Boards, ballots, minutes, official registers, notices and delivery | [Governance and communications](governance/README.md) |
| Gifts, accruals, payroll, treasury, reconciliations and close | [Finance](finance/README.md) |
| Inventory, pricing, settlement, paid media, fundraising and sponsorship | [Commerce and development](commerce/README.md) |
| Accounts, integration, privacy, accessibility, recovery and assisted work | [Platform](platform/README.md) |

## How to decide whether a feature is specified

For the business action, identify the actor, the person or organization affected, the authority, the effective and recorded times, the exact input, the owner's decision and the evidence returned. For each rejected, repeated or corrected action identify which facts must remain unchanged. For work handed to another department identify the source record, the operation key, who can see it, the expected acknowledgement and how to reconcile a late result.

For instance, agreeing to refund a ticket, receiving the processor's confirmation, returning money to the bank, freeing an admission place, and retaining a separate household donation each have different owners. A passing screen demonstration includes the duplicate confirmation and partial cancellation routes as well as the first successful sale.

The [domain index](../../README.md) establishes the record owner. The [record and field specifications](../implementation/README.md) describe the logical contracts. The [decision tables](../decisions/README.md) provide worked inputs and expected outcomes for selected policy profiles. The church decides which profile and effective edition governs its actual work.
