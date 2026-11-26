# Resolving uncertain sends, replies and delivery costs

The operator's task is to determine which recipient, destination, edition and provider operation are in doubt and how to resolve it without duplicate messages or misleading evidence. The [delivery register](../../communications/delivery-and-responses.md) owns attempts and observations. Never use this procedure to override an unsafe route or send across organizations.

## Handoff with recovery boundaries

| Boundary | Information committed | Recovery decision |
| --- | --- | --- |
| Before submission | One intended delivery, immutable content digest, authorized endpoint revision, sender identity, deadline and unique request key | A recovered worker rechecks current restrictions and expiry before taking a valid time-limited claim. |
| Ready to contact provider | Durable attempt intent and provider-scoped handoff key | Retry against the same handoff key if the provider guarantees idempotent handling; otherwise reconcile before repeating an ambiguous submission. |
| Definitive acceptance | Provider account and message identifier, acceptance time, cost estimate and raw response reference scoped to the operator | Wait for channel-appropriate receipt or expiry. An accepted email is not proof that a member read it. |
| Timeout or crash after external request | Prior attempt marked unknown until reconciled against source/provider facts | Query permitted provider evidence; if inconclusive and retries cannot be deduplicated, open an exception. An operator considering resend sees possible duplicate, deadline and sensitivity. |
| New feedback | Verified event identity, sender/tenant scope, source occurrence time, receipt time, protected evidence and semantics | Apply each verified event once in context. Unsupported or conflicting observations remain visible to authorized staff. |

The atomic unit is the local intent and evidence of what happened. An external channel can accept a request when local acknowledgment is lost. Lease expiry by itself cannot prove an unsent message, and a provider that lacks a duplicate-prevention guarantee cannot promise one physical delivery. A callback about an unknown yet validly authenticated message is quarantined by provider account and message id. A later returned submission identifier may link it after verification. Invalid evidence does not change status, disclosure or contact preferences.

**Fixture D1, SMS with a lost response.** At 09:00:00 create D1 with digest H, issue identity S and scoped handoff K. At 09:00:02 the provider accepts K and assigns P8; the worker times out. At 09:00:05 a delivery callback for P8 arrives before the response and is held unmatched. At 09:00:10 a supported lookup returns P8 for K. Link the original attempt, apply its delivery evidence and mark confirmed delivery once. At 09:00:15 a duplicate callback with the same event identity adds no delivery or cost. At 09:00:18 a late acceptance event with an earlier observation time cannot downgrade a confirmed delivery. If P8 belongs to another church sender, keep it quarantined and escalate without exposing details.

**Fixture D2, definitive failure and fallback.** An email attempt is accepted then returns a hard bounce. Retain both events and mark the address unavailable under policy. If the notice permits SMS and the member has verified, permitted SMS, create a related SMS delivery with a distinct key. The one intended person now has two routes: failed email and successful SMS. Staff can see each provider attempt while an audience report counts one reached individual under its declared evidence rule. If the email outcome remained ambiguous and the fallback could expose sensitive material, seek the specified override or leave an exception rather than racing both providers.

## Status interpretation and charges

Define status semantics per channel and provider version. Platform handoff, provider acceptance, delivery to a device, opening estimation, verified member acknowledgment, inbound reply and action completion are separate. A complaint after delivery establishes a later contact event; it does not negate physical delivery. An apparently simultaneous redelivery and hard bounce may refer to separate destinations or provider stages. Compare provider account, message identity, observation times and documented semantics. If contradictory under those semantics, mark the effective result as under review while retaining raw events.

On a statement with three charge lines of 0.10, 0.10 and 0.20, verify provider account, currency and unique charge references. Reimporting the same statement retains 0.40 total, including any charge for a failed transmission. Apply a later supported 0.10 supplier credit as a separate signed billing event for a revised 0.30, preserving original charges. Finance determines posting. A one-message SMS may be billed in multiple segments after personalization or translation. Report billed segments independently from people reached.

## Reply, cancellation and retry cases

1. An inbound “stop” arrives from a shared number. Authenticate its source channel and scope. Block applicable future traffic to that destination promptly, retain minimal evidence and avoid changing unrelated identities by guessing which adult replied. Re-enrollment requires a validated applicable mechanism.
2. A reminder is cancelled while one operation is in flight. Queued sends stop; the in-flight member can still receive it. Record a subsequent acknowledgment if received and send an independently approved correction when appropriate. Previously delivered copies cannot be recalled by changing local status.
3. A member receives a “confirm” link twice. The permitted business action validates intended account, source revision, eligibility and known action key. Two clicks result in a single business acknowledgment. A reply from an unknown party starts restricted triage.
4. An operator restarts after a prolonged outage. Reconcile in-flight attempts first, refresh permissions and suppressions, expire stale messages, check budget and only then resume eligible work. Produce counts by outcome with one disposition per recipient and publish provider backlog and human follow-up separately.
