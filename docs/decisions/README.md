# Worked decisions by department

These tables give concrete inputs and expected outcomes under named, fictional church policies. Use a table to answer a specific implementation or acceptance question. Each family describes the scope, units, evaluation sequence and boundary conditions of its fixtures. A church adopting a different charter, calendar, currency policy, safeguarding protocol or other local choice must compare results against its own approved version.

| Question | Decision desk |
| --- | --- |
| Who was a formal member on this date? Which household authority applies? What can be disclosed? How much assistance remains after reversal? | [People and care](people/README.md) |
| Can the last seats be allocated, can this child be handed over, and does a moved room, clock change or rota conflict change the result? | [Ministry operations](ministry/README.md) |
| Did the meeting have quorum, did the motion carry, and may a reminder or channel post go out at this time? | [Governance and communications](governance/README.md) |
| What is the journal, fund, payroll, settlement or service-period amount, including rounding and later corrections? | [Accounting](finance/README.md) |
| How are order discounts, tax credits, stock, paid access, royalties, grants and sponsorship commitments allocated? | [Commerce and development](commerce/README.md) |
| What changes after delegation expiry, duplicate delivery, conflicting offline work, migration, restore or review of an AI draft? | [Platform](platform/README.md) |

## How to use a case

1. Identify the case family and its profile. Copy the actual input row and expected outputs, including units, scope, time basis, previous state and observation point where present.
2. Build just the fixture records it requires. A reviewer with privileged access and a publicly visible report are different execution contexts; retain that distinction.
3. Run the action under the stated policy. Compare each effect, including any expected absence of a second charge, handover, publication, vote or acknowledgement.
4. Compare a neighboring row whose input crosses the threshold. An implementation that happens to produce the right amount or decision for one profile can still fail on a boundary or under another charter.
5. Where the case describes input to an integration, inspect both record owners and the handoff receipt. A correct source record and a stale or duplicated downstream effect is a failed case.
6. Record the case identifier, policy edition, observed outcome and reason for any difference. A configurable choice is a legitimate difference only if the selected profile actually differs and the church has approved that choice.

The [desk manuals](../handbook/README.md) explain why the business rules exist and how a person resolves exceptions. The [record contracts](../implementation/README.md) define the fields and links used to implement them. Cross-department acceptance work begins with the [integrated journeys](../verification/journeys.md).
