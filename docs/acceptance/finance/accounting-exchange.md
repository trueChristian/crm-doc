# Accounting exchange acceptance

Use separate configurations for independent operation, file exchange and API exchange. Church A's example currency is NAD. Giving staff have no accounting credentials. The accountant receives only the data agreed for this connector. The receiving system in these fixtures exposes accepted source keys and destination references so the tester can inspect the effect of a lost acknowledgement.

## 1. Church with no accounting connection

Verify a NAD 100 gift, with 75 General and 25 Youth, for an identified donor. Close local custody, issue a permitted acknowledgement and retrieve the donor's history. The two designations total 100. The history, authorized donor correspondence and count evidence remain available with the accounting integration disabled. There are zero external deliveries and zero external acceptance references. Enabling a connection later requires selecting an effective starting point and approving any historical export. No historical gift is sent twice because a connection was added or changed.

## 2. API accepted the gift but the reply was lost

Choose a receiving system that accepts a whole gift with all its allocations as one logical item. Approve gift A-101, NAD 100, with two allocation lines of 75 and 25. Set the fixture's recipient scope to exclude personal identity. Include the church, source identity, revision, received date, currency and mapped purpose codes in the outgoing item. Assert that no donor name, address, member reference, care note or payment credentials appear in its payload or delivery log.

1. The receiver accepts A-101, assigns destination reference D-701 and commits. Drop the acknowledgement before the sender can save it. The giving report already shows one gift of 100. The sender shows unconfirmed delivery with the original source key.
2. Retry unchanged content under the same key. The receiver returns D-701 or its documented equivalent duplicate acknowledgement. Verify that exactly one item was accepted, its two purposes are intact and the sender stores D-701. Concurrent processing of two retries produces the same result.
3. Submit a different amount using the same revision and key. The receiver reports a conflict and the sender routes the item for review. A legitimate later correction must refer to A-101 and carry its own source identity or version according to the exchange contract.
4. Repeat with the receiving system offline before the first commit. Service and donor work can continue. A permitted retry after recovery yields one accepted gift, one D-701-equivalent reference and a trace of both attempts.

## 3. File delivery with a rejected item

Approve two gifts. F-01 is NAD 40 General and F-02 is NAD 60 Missions. Export the files under a manifest identifying the authorized church, currency, version, control count 2 and gross 100. Have the receiving desk accept F-01 as R-11 and reject F-02 for an unknown Missions mapping. Import a trustworthy result identifying each original row.

| Checkpoint | Expected reconciliation |
| --- | --- |
| File available for download | Two eligible source items, zero confirmed acceptances. |
| Result imported | One accepted item totaling 40 and one rejected item totaling 60. The local giving record still totals 100. |
| Repeated original result | Same totals and rows. The reviewer can inspect the original failure and its reason. |
| Missions mapping corrected and rejected item retried | Source identity for F-02 remains traceable through the approved mapping correction and retry. After confirmation, accepted total 100, unresolved total zero and F-01 has one external effect. |
| Delayed copy of the rejection arrives | R-11 and the later accepted F-02 stay accepted. The receiver can trace the stale response against its earlier delivery attempt. |

A church whose recipient cannot return line-level results uses its agreed manual confirmation or whole-file acknowledgement. An ambiguous result requires an operator to establish what the recipient accepted before resending any part. Unknown outcomes stay visible. If two providers exchange the same cutoff after a migration, compare exporting authority, last acknowledged items and overlap by church and economic source before authorizing a backfill.

## 4. External gift, corrected amount and inbound loop

Configure a giving platform as source for gifts in its own account. Allow confirmed captures and linked corrections into Church A. Configure a distinct accounting destination for approved facts and suppress echo to the originating connection.

1. Receive an authenticated external capture X-7 for NAD 90, allocated 60 General and 30 Missions. Receive its exact duplicate. One gift appears in the local register and one logical delivery to the configured accounting destination becomes eligible. Push nothing back to the source as a new gift.
2. Receive a linked partial return XR-7 for NAD 20 from the original Missions allocation. Expect gross original 90, recorded return 20, current total 70 with 60 General and 10 Missions. Replaying the notice leaves both the donor history and downstream correction count unchanged.
3. In a fresh run, deliver XR-7 before X-7. Hold it under its source and original-gift reference until the original arrives or a reviewer resolves it. Apply it once when X-7 becomes available. A return beyond the remaining applicable allocation stays under review.
4. Send the same provider-local X-7 identifier from a separately authorized Church B connection. It can identify a distinct Church B gift. A Church B token attempting to update Church A's gift is denied without disclosing Church A's donor or creating a correction.
5. Send an aggregate bank receipt of NAD 90 without individual donor identity or qualifying gift references. Route it for reconciliation according to the connector agreement. It cannot silently create a second donor gift or identify a person from the amount alone.

Inspect failed payloads, application logs, file downloads, replays and operator diagnostics under a user without donor access. A correlation reference and permitted error reason support follow-up without revealing protected fields. The [accounting exchange contract](../../finance/accounting-exchange.md) defines the ownership boundary. The [giving records](../../finance/giving.md) define the donor history inspected in these cases.
