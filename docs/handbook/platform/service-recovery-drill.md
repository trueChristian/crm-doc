# Recover a service without duplicating real-world effects

Use the [operations specification](../../platform/operations-recovery.md) to select objectives with each department. The duty officer owns communications and service status. The recovery operator restores a consistent point. The registrar, finance reviewer, privacy officer and check-in lead each decide whether their evidence supports reopening the functions entrusted to them. A health check alone cannot answer whether children are accounted for, a payout occurred or a private address was removed.

## Choose measures with explicit clocks

A sample church commits to a four-hour recovery target measured from service disruption to verified usability for its named transaction, and an allowed data loss of fifteen minutes measured from disruption to the latest verified recoverable point. An earlier start of investigation or a later opening of public search cannot be substituted for these timestamps. Different services can have different objectives and release criteria; the overall score shows the slowest critical path as well as individual results.

For a 28-day reporting window with 40,320 covered minutes, an example 99.9-percent availability target allows 40.32 minutes unavailable. A 35-minute outage alone yields about 99.913 percent availability. Adding a separate 12-minute outage yields about 99.883 percent and breaches that target. Avoid double-counting overlapping downtime. Publish whether planned maintenance, unknown telemetry and degraded service are included. Availability of the public home page is insufficient evidence about member sign-in or finance settlement.

## Exercise the timeline

| Local time | Observation and required action |
|---|---|
| 09:38 | The last verified base backup is complete. Its manifest includes the register, attachments, audit obligations and defined integration positions. Independent recovery logs still have to be checked. |
| 09:50 | The last verified recoverable register change is recorded independently. A later broker acceptance or backup job success cannot move the confirmed point forward by itself. |
| 10:00 | A disruption begins. Registrations and payment acknowledgements become unavailable. Local custody staff retain responsibility and invoke the named supervised fallback. |
| 10:07 | Monitoring detects the incident. Record seven minutes to detection and the actual disruption start of 10:00. Notify the duty lead through an unaffected channel. |
| 10:18 | Recovery starts in isolation. Turn off external dispatch, charges, live publishing and scheduled exports, including restored workers. Keep cross-organization scopes separate. |
| 11:10 | The restored register can answer local queries, but privacy changes, ledger positions, issued receipts and custody evidence need reconciliation. State remains restricted. |
| 11:42 | Register, privacy and custody owners sign their tests, giving verified usable register service after 102 minutes with ten minutes of possible lost changes. The register meets both example objectives. |
| 12:03 | Finance reconciles the uncertain payout and opens posting after 123 minutes. State its own residual loss and reconciliation result; the register's ten-minute loss calculation is not a finance guarantee. |

If only the 09:38 backup could be verified, the potential loss interval would be 22 minutes. Report a loss-objective failure even if staff finish restoration in under four hours. A verified external record can reconstruct specific transactions but cannot establish that all other facts in that interval survived.

## Reconcile four independent effects

1. **Payments.** A checkout receipt appears as pending in the restore but the processor confirms one captured payment by its stable transaction key. Validate payee, amount and currency, reconcile the missing local outcome, then run finance posting once. There is no reason to charge the person again.
2. **Mail and receipts.** An SMS reminder is queued in the backup, and independent provider evidence shows it was accepted before the outage. Mark the intended delivery's actual known state; do not resend automatically. If the useful deadline has passed, suppress a still-unsent message. Where acceptance is unknown, route to reconciliation with an accountable operator.
3. **Personal data.** Replay withdrawals, disposals, holds, current staff revocations and acquired authority changes from independently controlled evidence. The privacy officer tests a revoked grant and a removed photograph through detail, search, file delivery and offline issue before opening those routes.
4. **Supervision and attendance.** A supervisor recorded two children physically present during the outage. Verify their safe current custody against local evidence, reconstruct handovers with original event times, and resolve ambiguities under the designated procedure. Reconstructed named attendance and physical headcounts retain different counting rules.

## Operational instrumentation

Track the time and scope of the oldest unprocessed event, failed auth or privacy refresh, unsettled payment, stale search edition, unreconciled offline pack, consent replay gap and unsatisfied custody charge. Measure latency by transaction and censor private identifiers in traces. For 100 representative sorted roster requests with the 95th value 1.9 seconds, an objective at or below 2.0 seconds passes under the declared nearest-rank method. A mean below two seconds alone cannot establish that. Include timeouts in the denominator under the declared rule.

Alerts name the impacted service, severity, human owner, fallback route, next update, affected time window and evidence reference. Deduplicate repeated alerts without hiding independent organizations or changed severity. Keep status language factual, for example “registrations saved on desk devices await confirmation” or “some financial receipts are awaiting matching.” Never publish member names, care cases, donor amounts or provider secrets in status notices.

## Sign back in

Custodians compare trial balances and control accounts, count active restrictions and held evidence, sample protected attachments, test search permissions, confirm all supervised handovers and reconcile external deliveries. The incident owner records scope reopened, remaining restrictions, recovery point, actual measured loss, service restoration time and each exception's owner and due date. The communications owner issues a clear end-of-incident notice. Rehearse again after a material change to permissions, backup scope, financial connectors or offline operating policies.
