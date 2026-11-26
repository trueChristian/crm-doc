# Reminders and orchestration

A reminder belongs to an event occurrence, duty, deadline or case task with a revision, an accountable owner and an end condition. The system should answer, for one member, why a reminder is due, what would stop it, which time zone controls it and whether a previous copy already went out.

| Entity | Fields after id | Integrity and relationships |
| --- | --- | --- |
| ReminderRule | organization_id Organization ref, owner_id UserAccount ref, name text, purpose_id CommunicationPurpose ref, trigger_event code, source_kind code, anchor_field field, direction before/after/at, offset_quantity nonnegative integer, offset_unit elapsed_minutes/calendar_days/business_days, anchor_zone_rule source/recipient/explicit, zone zone?, holiday_calendar_ref text?, recipient_rule typed expression, stop_condition typed expression, template_id MessageTemplate ref, max_sends integer, active_from instant, active_until instant?, revision integer, state draft/active/paused/retired | Validate anchor, conditions, eligibility fields and bounds against the source contract. Business days require a named versioned calendar. Each recurrence uses a stable occurrence id. |
| ReminderInstance | rule_id ReminderRule ref, rule_revision integer, source_kind code, source_id opaque, occurrence_key opaque, source_revision text, subject_person_id Person ref?, subject_unit_key opaque, sequence integer, anchor_at instant, intended_local_time local timestamp, zone zone, planned_at instant, latest_useful_at instant?, state pending/held/queued/sent/suppressed/cancelled/expired, reason code?, dispatch_id DispatchRequest ref? | Unique rule/occurrence/recipient unit/sequence. Changing the source revision reschedules or cancels the same semantic reminder. Reopening or reissuing requires an explicit new occurrence or sequence. |
| ReminderAcknowledgement | instance_id ReminderInstance ref, responding_person_id Person ref, representation_id RepresentationAuthority ref?, response accept/decline/acknowledge/request_help, received_at instant, source protected text, effect accepted/rejected/stale | A response handles the intended person and occurrence. Acknowledgement is independent of delivery status. Duplicate replies cannot reassign a duty twice. |
| EscalationStep | rule_id ReminderRule ref, sequence integer, wait_quantity duration, condition no_response/failed_delivery/overdue, recipient_selector permitted role/owner, action alert/assign_task/offer_alternate_channel, template_id MessageTemplate ref?, stop_when typed expression | Exhaustion opens one operational task. A chain has a maximum depth, per-person contact limit, permitted role and expiry. Repeating the same cycle requires explicit review. |
| SuppressionPeriod | organization_id Organization ref, scope campaign/purpose/group/sender, target_key opaque, from_at instant, until_at instant?, reason code, approved_by UserAccount ref, release_policy cancel/recompute/hold_for_review | Suspend optional sends during bereavement, service interruption or a crisis. Re-evaluate source relevance and recipient preference after release. |
| DigestEdition | person_id Person ref, purpose_id CommunicationPurpose ref, local_period text, zone zone, cutoff_at instant, planned_at instant, state open/sealed/sent/expired, dispatch_id DispatchRequest ref? | One edition per recipient/purpose/period. Each item keeps its source id, revision and own entitlement. Remove revoked or obsolete items before handoff; suppress empty digests. |

## Trigger contracts

| Origin and event | Target and timing | Stop, correction or escalation |
| --- | --- | --- |
| Volunteer duty accepted | Assigned volunteer, the previous local evening or an elapsed interval before service | A swap or cancellation suppresses the former volunteer. Missing confirmation creates a coordinator task. |
| Class enrolment, occurrence changed | Authorized guardian, on enrollment and shortly before the actual class | Re-evaluate current guardian authorization and attendance status. No personal group details on an unsafe route. |
| Meeting called or rescheduled | Eligible notice recipients, using the meeting's local notice and paper deadlines | Preserve delivered historical notice. Generate a distinct correction with revised details; cancel the obsolete future reminder. |
| Pledge installment coming due | Only the contact permitted for giving and the designated route | Payment, pause, write-off or disputed pledge stops the reminder. Avoid amounts on shared destinations. |
| Room booking and setup | Assigned custodian, before opening and after cleanup | Cancellation releases room and tasks. Approved substitute takes the next reminder only. |
| Follow-up task becomes overdue | Case assignee or restricted supervisor after the authorized response window | Closure, transfer or restricted access revocation suppresses future sends. Generic notification points to a protected record. |

## Timing and lifecycle

An elapsed offset is measured from the anchor instant. A calendar offset is measured on the named local calendar, at the chosen wall-clock time, even if the elapsed duration differs from 24 hours. An overnight quiet period crosses midnight. For a nonexistent local time use the policy's next valid time or hold for review; for an ambiguous time record the selected offset and use one occurrence. Freeze the chosen rule revision and original planned instant. Re-evaluate route and quiet hours at dispatch. Deferring past the latest useful time expires the reminder and creates an operator task only if configured.

A recurring meeting edited for one date affects the single occurrence. “This and following” carries a mapping from affected old occurrence keys to new ones, retires obsolete reminders, and preserves issued notices. When multiple source changes arrive, accept the authoritative latest revision and ignore or reconcile out-of-order revisions. On provider or scheduler outage do not flood members with expired reminders. Apply a bounded catch-up period, deduplicate by semantic key and release only current future-relevant content. Use an approval-gated emergency path with defined authorized users, purposes, affected audience and reason. A category marked emergency cannot bypass an unsafe destination.

## Acceptance cases

1. A rehearsal moves twice while a queue is down. On recovery one current reminder remains. If the first notice was already accepted, the new time goes out once as a correction. The change history shows both revisions.
2. A member confirms from one device while the reminder is due on another. The assignment changes once. Pending reminders recheck the source before handoff and record any unavoidable in-flight send.
3. A once-a-week digest includes five announcements; access to two is withdrawn before dispatch. The delivered edition includes three. Its audit identifies the count and the disposition of each source item for authorized staff.
4. A missed 10-minute alert is rediscovered two hours after the event. It expires. A recurring 30-day renewal notice can resume within its separate configured catch-up limit.
5. The office can reconcile every planned occurrence to pending, held, queued, issued or terminal disposition, report overdue acknowledgements without marking deliveries as read, and identify reminder loops before another send.
