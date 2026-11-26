# Secretary workspaces and report contracts

An application team needs to know what populates a screen, how an operator resolves ambiguity and what changes when someone presses the final button. These contracts cover the front desk, registrar and annual meeting pack. Read them together with the record owners for exact permissions and state transitions.

## Person search and registration

A name query returns only matched people the operator may discover. Display enough approved disambiguation to prevent a mis-link: official versus preferred name, locally permitted congregation, and a masked or purpose-approved contact hint. A common surname, repeated street address or shared phone is a matching clue. A registrar must confirm the identity before carrying forward financial, membership or authority records. Offer “create separate person” with an auditable distinct decision and a safe review route if the evidence is inconclusive.

| Input group | Minimum behavior | Confirmed write |
| --- | --- | --- |
| Name and origin of entry | Support single names, multiple scripts, unknown parts and a record made on behalf of another person. Make the register purpose clear. | Person and permitted PersonName facts with their source. |
| Age or birth details | Allow exact date, year, month/year, recurring birthday without year, estimated or unknown where declared. State what information will appear in the directory. | Precisely the supplied components and precision marker. |
| Family or household | Search authorized households, identify role, current/effective dates, multiple residences and any safe correspondence rule. | HouseholdPerson and independently supported PersonRelationship records. |
| Formal register | Ask separately about existing status and evidence for admission. Show the effective date, decision authority and affected roll when there is a proposed change. | Application, decision and period only after the appropriate approval. |
| Self-service access | Identify the person invited and verified channel; preview the audience of each contact field. | AccountInvitation followed by a verified UserAccount link, independent of membership. |
| Communications | Identify purpose, exact channel, applicable language, safety restriction, and whether the person wants optional notifications. | Versioned contact decision and delivery endpoint with separate verification state. |

When identity remains uncertain, allow ordinary attendance recording if authorized without forcing a duplicate formal member entry. On save, return the created or linked record identifiers, any pending steps and the actor. Returning to the form after a delayed response cannot create another person if the operation already succeeded. Reject a second request using the same operation key for a different person.

## The registrar’s change inbox

Use separate queues for suggested matches, member-submitted corrections, pending membership decisions, and conflicting representation claims. A single “approve all” action cannot cross categories with different authority. Show submitted value, current authorized value, effective date, source and requested result. Hide safe addresses and restricted case notes from the reviewer unless needed and permitted. A material change to the submitted request invalidates a prior approval.

Accepting an address correction for one adult does not replace the mailing address for everyone listed at the household. A requested guardianship change requires its own evidence and review. A member's opt-out from an optional newsletter takes effect on eligible pending sends even if an unrelated profile correction is still awaiting review.

## Report specifications

| Report | Grain and cutoff | Essential output | Reconciliation or privacy control |
| --- | --- | --- | --- |
| Dated membership roll | One qualifying membership/person/congregation at the chosen civil date; specify source cutoff for a signed output | Local register number, permitted name, class, congregation, effective status and filter description | Historical period count equals signed total; excluded statuses and unresolved movements have separate counts. |
| Household mailing run | One permitted route per configured purpose and addressing policy | Addressee, salutation, delivery address version, do-not-mail status and print batch | Household coalescing is optional and cannot override safe route or an adult's independent privacy choice. |
| Volunteer vacancies | One occurrence/role/shift and count of eligible confirmed assignees | Needed, confirmed, tentative, exceptional and still vacant | A person assigned two incompatible duties is investigated and never silently counted twice. |
| Attendance and participation | Visits and distinct people per occurrence or interval, with anonymity and missing reports identified | Known attendance, guest headcount where supported, coverage, group/campus, prior comparable period | Do not report exact unique individuals across anonymous counts or prohibited organization boundaries. |
| Treasurer’s congregational pack | Posted book and fund dimensions as of an approved closing cutoff | Opening, receipts, spend, transfers, period change, closing and comparison to budget | Cross-foot to the ledger; retain evidence without exposing individual donors or salaries in small cells. |
| Action register from minutes | One accepted action including any reissued or superseded due date | Decision, accountable officer, mandate, due date, accepted closure evidence and next review | Closing an assigned task by itself cannot authorize expenditure or issue amended minutes. |

Every report identifies its title, organization, included units, producing actor, applied policy/definition, date interval and zone, generation time, data cutoff, units/currency, whether figures are complete or restated, and the permitted audience. If a user cannot drill through to a protected source, still make the aggregate's definition and quality visible where authorized.

[Workspace definitions](../../foundation/workspaces.md) · [Administration manuals](README.md)
