# Implementing ministry operations

Choose the manual by the decision the operator needs to make. The [ministry record dictionaries](../../ministry/README.md) give the fields and ownership. These manuals specify how to decide between competing claims, what becomes visible, when to reconcile and what the operator can do when a promise cannot be kept.

| Operational decision | Manual | Acceptance evidence |
| --- | --- | --- |
| Which dated meetings exist, including moves and exceptions? | [Recurrence and calendar changes](recurrence.md) | Re-expand the same calendar across excluded dates and an offset change without losing registrations. |
| Which seats belong to whom and how much remains refundable? | [Capacity, admission and priced units](admission.md) | Reconcile scarce seats, partial captures, bundle allocations and a family cancellation under replay. |
| Who is responsible for this child at this moment? | [Child custody and room handover](supervision.md) | Recover interrupted transfers, evaluate current collection authority and reconcile an open session. |
| How many people actually took part in a service or season? | [Counting participation through time](attendance.md) | Reproduce distinct-person counts, visit counts, anonymous observations and certified history. |
| Who can serve without a conflict, fatigue or expired qualification? | [Rota construction and fair assignment](rota.md) | Reproduce candidate eligibility, a tie break, a standby substitution and coverage after a withdrawal. |
| Can the church promise these rooms, stock and equipment? | [Reservations across rooms and equipment](facilities.md) | Resolve a partition, a pooled item, setup buffers and an interruption using one consistent plan. |
| Which service order, music edition and media segment may each audience receive? | [Worship execution and media handoff](worship.md) | Follow one revision from planning to two differently cleared recordings. |
| How does a learner move between classes and complete a pathway? | [Groups, education and progression](formation.md) | Close a term, transfer equivalent evidence, review a missing requirement and certify an outcome. |
| Who and what actually travelled, and which assistance was delivered? | [Missions, transport and distribution](missions.md) | Reconcile passengers by segment and supplies by location without double counting a household. |

## Use during implementation review

Run each fixture from a known state and capture the saved records, balances, decisions and visibility for at least two roles. Repeat the same command, then repeat with a stale revision and with another operator acting on the last available unit. The expected result covers both the change and the evidence left when a change cannot proceed. Where the church must choose a policy, the fixture gives one explicit choice. Its numbers and local procedures are test data.

The manuals use half-open time intervals: a resource is occupied at its start, and available again at its end. An observed time and the time somebody entered the observation remain separate. Every command that can change multiple records has one operation identity, a scope, an actor, the expected source revision and a recorded outcome. A retry with the same identity and conflicting parameters requires review. A repeated request with matching parameters returns its prior outcome. Changes crossing into another department preserve each owner's decision and delivery acknowledgement.

[Department dictionary](../../reference/records-ministry.md) · [Worked Sunday across departments](../../ministry/service-rehearsal.md)
