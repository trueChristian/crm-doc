# Match weekend registrations and gifts to the external acknowledgment

Use church A and the people in the [register exercise](register.md). The event office has accepted two fee-bearing retreat places for P2’s family with a fee of 10 per place. Two separately approved gifts are also received. At the point of interruption, retain these source references and the observation for each. For this exercise, the church accepts independently confirmed capture to fund a held place and gift confirmation to acknowledge a gift. Use a single two-decimal currency.

| Source | Church observation | External gross |
| --- | --- | ---: |
| S1 | P2 books two distinct places S1a and S1b, 10 per place | 20.00 |
| G1 | P1 gives to general ministry and elects a private acknowledgement | 30.00 |
| G2 | An anonymous giver designates relief | 50.00 |

P1 and P2 share endpoint E1. No booker, donor or receipt identity is inferred from that shared endpoint. The provider reports one combined transfer, with gross 100, fee 3 and net 97. The transfer has references for all three source transactions, one per place allocation on S1. A finance reviewer matches sources by identifier, currency, purpose and amount. The reviewer records the batch reference and acceptance or discrepancy for each source. The external books retain the bank reconciliation and fee accounting.

| Desk | Expected state after verified capture and acknowledgment | Expected state after P2 cancels S1b and the provider confirms a 10 refund |
| --- | --- | --- |
| Registration | Two funded places with distinct active tickets | S1a remains active. One S1b cancellation, one retired ticket, one released place. Its refund moves from requested to externally confirmed. |
| Giving | Exactly two gifts, 80 in total, one named general gift of 30 and one anonymous relief gift of 50 | Same two gifts and designations. Neither donor receives a refund notice. |
| Finance liaison | Three external source references acknowledged with 100 gross. Only the liaison requires the fee/net details. | One refund reference mapped to S1b. The provider reports 87 net transferred over the complete sequence (97 less 10). |
| Register and communications | Six people and their separately permitted destinations | Same six people. No membership or contact preference change on cancellation. |

Reimport the batch and refund twice. Counts, references and amounts remain unchanged. Try an external summary containing only net 97 and no source detail: it cannot substantiate how much went to relief or either event place. Retain the existing church observations, flag the external correlation as incomplete and have the reviewer obtain the source detail. The test passes only when both operational results and the handoff status can be distinguished.

P2 sees the two place outcomes and the authorized adjustment without P1’s gift. P1 obtains only the private general gift acknowledgment. Neither adult gains access to the other's documents because they share an endpoint. A church choosing anonymous giving can report aggregate relief without creating an identifiable donor.

[Church resource desks](../../commerce/desk-handoffs.md) · [Giving and handoff](../../finance/README.md) · [Event registration](../../ministry/registration.md)
