# Exchange admission and recovery

Use the church’s configured source, destination, operation and effective mapping. One source gift and its allocations form an atomic business group. Track independent groups separately when they appear in the same administrative batch.

| Current observation | Next evidence | Decision, owner and expected effect |
| --- | --- | --- |
| Church has collected 80 with the connection disabled | Giving clerk verifies the purpose and count | Local giving status can complete. No delivery is created. A later activation requires approved cutoff or backfill. |
| New authenticated provider capture | Correct destination church, known purpose, 80 in one currency with matching lines | Admit once within the provider account. Apply minimum donor disclosure and source lineage. |
| Two captures of 80 on the same date | Different stable capture IDs, same household/email | Treat them as separate where provider evidence confirms both. Content resemblance alone cannot discard a gift or merge donors. |
| Previously accepted source event | Same canonical body, same key and revision, new HTTP request ID | Return the stored disposition. Count one source gift and one applied destination event. |
| Previously accepted source event | Same key and revision, changed beneficiary, currency or amount | Quarantine conflict. Keep both payload fingerprints and restrict evidence. No mutation to the committed gift. |
| A valid external return arrives first | Missing original gift or allocation | Hold the dependency and signal a safe operational reason. Once the original is accepted, re-evaluate the return once with its own key. |
| File accepted for upload | No item decisions available | Show delivered, application unknown. The accountant must confirm per agreed reconciliation process before declaring applied. |
| Two independent items transmitted | Receiver confirms one and rejects an unknown purpose on the other | Preserve acknowledged first item. Have the designated liaison approve the mapping and select the second for corrected release with lineage. |
| One group partially applied by a limited receiver | Receiver already has the 80 gross but lacks allocation B | Hold group status, reconcile using destination references and repair the outstanding part under the agreed protocol. Never send a second 80 as a new gift. |
| Retry window expired | Recipient lookup finds original reference A07 | Record authenticated disposition with A07. If no reliable lookup/deduplication exists, leave uncertain pending independent evidence. |
| Old response arrives after a correction | Source revision is earlier than current approved revision | Preserve response against historical event. Current disposition stays tied to the authorized revision. No reversion to a prior designation. |
| Daily report expected 80, reply reports 78 | Source controls separately show a 2 fee | Confirm comparable amount basis and date. Preserve 80 gift, 2 fee and 78 settlement separately. An unexplained difference remains under review. |

[Accounting exchange contract](../../finance/accounting-exchange.md) · [Exchange exercises](../../acceptance/finance/accounting-exchange.md)
