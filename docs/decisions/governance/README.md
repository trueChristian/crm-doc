# Governance and communications decision cases

Use these 21,737 finite examples with the [clerk's procedural manuals](../../handbook/governance/README.md). Choose the family first and then a charter, calendar or channel profile. Pages contain up to 325 cases each. Each row is an independent acceptance test unless the row itself specifies an ordered history. These are explicit example policy choices. Each church still adopts its own charter, privacy restrictions, authorities and operational settings.

| Decision family | Cases | What varies |
| --- | ---: | --- |
| [Motion majorities and denominator choices](motion-thresholds/README.md) | 3,360 | Votes, abstentions, absences and four denominator/threshold combinations. |
| [Quorum under vacancies, recusals and representation minima](quorum-checkpoints/README.md) | 3,058 | Vacancies, proxy inclusion, recusals, district minima and quorum boundaries. |
| [Formal notice windows and deemed service](notice-deadlines/README.md) | 3,040 | Meeting dates, notice periods, weekends, holidays and postal deemed service. |
| [Proxy conflicts, personal arrival and consumed rights](proxy-entitlements/README.md) | 1,680 | Holder caps, timing of direct attendance, revocation, conflicts and preceding ballot use. |
| [Auditable preferential ballot transfers and unresolved final seats](election-transfers/README.md) | 1,630 | First-preference counts, second choices, exhausted papers, ties and fixed or continuing denominators. |
| [Minutes corrections, stays and authority already consumed](minute-authority/README.md) | 1,695 | Issued transcript, proven original decision, correction stage, prior commitments and a live execution stay. |
| [Quiet windows, elapsed reminders and discontinuous local clocks](reminder-windows/README.md) | 3,500 | UTC instants, intended local time, overnight or daytime windows, clock gaps and repeated wall times. |
| [Channel preference, opt-out and last-minute authority changes](recipient-routing/README.md) | 1,944 | Recipient capacity, verification, shared endpoints, allowed channel order and post-freeze changes. |
| [Reconciling out-of-order callbacks, duplicate events and publication counts](delivery-event-order/README.md) | 1,830 | Acceptance, final delivery, rejection, withdrawal, mismatched and duplicate callbacks in different arrival orders. |

## How to use and audit

- Load a row's facts independently from other cases and use the policy exactly as printed on its page. Apply an as-of time before each step. Compare all expected fields, including denied or deferred outcomes and the reason.
- In voting tests recompute the denominator and threshold before deciding the winner. A simple yes/no majority, an inclusive fractional threshold and a predetermined count of confidential ballot papers answer different questions. In notice tests count clear dates from service as a separate check on the reverse deadline calculation.
- In reminder tests compare the first eligible actual minute and the final useful instant. In callback tests reconstruct the effective state after each observation. Neither elapsed clock time nor a late notification should manufacture an observed delivery or grant access.
- In correction tests compare the original authority, separately issued document, execution stay, cash/reservations already recognized and capacity that remains. A clerk's corrected extract cannot erase a historical commitment.
- Every case was independently recalculated from the published rows. The checks used rational arithmetic for vote thresholds, forward calendar enumeration against computed notice deadlines, a timezone database for skipped and repeated local minutes, and replay of observed events under each channel's evidence rules. The tested transitions and limits are the ones named in the profile. They make no claim about every charter, election system or provider.
