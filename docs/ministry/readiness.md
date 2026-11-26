# Operational readiness, interruptions and review

A duty lead needs a clear decision before doors open, a way to locate responsible people during an interruption and an evidence trail afterward. A church configures its own authorized procedures, roles, emergency contacts, locally approved instructions, training and thresholds. The system supports recording, coordination and handover. During an urgent incident the interface must make approved offline instructions and immediate contacts available without waiting to create a record.

## Records

| Logical record | Fields | Cardinality and validation |
| --- | --- | --- |
| ReadinessPlan | `title text`, `campus_id → Campus?`, `owner_id → Person`, `kind code`, `version count`, `effective_on date`, `review_on date`, `state code`, `approved_by → UserAccount?`, `restricted_procedure_ref id?` | Each approved edition is preserved. Scope may be an activity type, campus or trip. Separate public directions, duty instructions and confidential incident procedures. |
| ReadinessCriterion | `plan_id → ReadinessPlan`, `sequence count`, `label text`, `capability_code code`, `mandatory bool`, `evidence_kind code`, `failure_action code` | Examples include confirming responsible staff, accessible routes, headcount owner, room readiness, communications contact and alternate venue. |
| OperationalBriefing | `occurrence_id → EventOccurrence`, `plan_id → ReadinessPlan`, `duty_lead_id → Person`, `opened_at instant`, `decision code`, `decided_at instant?`, `decided_by → UserAccount?`, `reason text?` | Maps a dated activity to an approved plan. Pending, ready, ready with authorized conditions, delayed or cancelled. Preserve superseded decisions if circumstances change. |
| ReadinessCheck | `briefing_id → OperationalBriefing`, `criterion_id → ReadinessCriterion`, `owner_id → Person`, `due_at instant`, `result code`, `observed_at instant?`, `reviewed_by → UserAccount?`, `exception_ref id?` | One outcome per applicable criterion and briefing revision. Pending, passed, failed or inapplicable with approved reason. A mandatory unmet item with no authorized alternative prevents a ready decision. |
| DutyAcknowledgement | `briefing_id → OperationalBriefing`, `assignment_id → VolunteerAssignment`, `plan_version count`, `acknowledged_at instant`, `method code` | A changed instruction can require a new acknowledgement. Silence does not constitute receipt. |
| OperationsIncident | `occurrence_id → EventOccurrence?`, `campus_id → Campus?`, `reported_at instant`, `observed_at instant?`, `reported_by → UserAccount?`, `category code`, `urgency code`, `restricted_summary text`, `controller_id → Person?`, `state code`, `closed_at instant?` | Log a facilities issue, interruption, welfare concern, near miss or drill. Separate factual observation, staff actions and later conclusions. Protect reporter identity and location according to role. |
| IncidentUpdate | `incident_id → OperationsIncident`, `recorded_at instant`, `effective_at instant`, `actor_id → UserAccount`, `kind code`, `audience code`, `text text`, `supersedes_id → IncidentUpdate?` | Chronological, append-only timeline. A correction identifies the superseded entry. Public announcement text must be a separately approved communication. |
| AccountabilityCheck | `incident_id → OperationsIncident`, `session_id → SupervisedSession?`, `group_id → MinistryGroup?`, `responsible_id → Person`, `checked_at instant`, `expected count?`, `accounted count`, `unknown count?`, `basis code`, `restricted_exception_ref id?` | Multiple reports per area with timestamp and scope. Distinguish actual roll-call, anonymous headcount and estimate. Unknown attendance requires an explicit uncertainty indicator. |
| OperationalAction | `incident_id → OperationsIncident?`, `briefing_id → OperationalBriefing?`, `owner_id → Person`, `assigned_at instant`, `due_at instant?`, `action_text text`, `completion_evidence_ref id?`, `status code`, `verified_by → UserAccount?` | At least one source. An action can require an independent checker where policy calls for it. Retain transfers of responsibility. |
| OperationalReview | `incident_id → OperationsIncident`, `reviewer_id → Person`, `reviewed_on date`, `summary text`, `lessons text`, `approved_by → UserAccount?`, `share_scope code`, `next_review_on date?` | Link approved corrective actions, procedure updates and follow-up exercises. Publish a redacted learning note independently of the confidential record. |

## Use at an event

Before a large service, the duty lead selects the applicable plan and assigns checks. Each owner confirms the actual state and records a failure or an exception. The checklist distinguishes a planned staffing number from qualified people present. The lead can delay opening, reduce room capacity under approved policy or cancel. A public notice contains the practical change. Private personnel, safeguarding and medical information stays with its decision owners.

During disruption staff capture an incident when practical, identify a controller, make an appropriate internal report and record the decision affecting each activity. A missing child or safeguarding disclosure is referred to the designated protection workflow; the general incident retains only a restricted reference, referral time and contact owner. Care information and detailed allegations stay within the protection case. A facility failure can trigger a closure and fresh availability checks. Posting public messages, notifying families or sharing a photo each requires its own audience, authority and delivery confirmation.

For a drill, label every view and message as an exercise, select a limited test audience, and confirm before releasing any real alert. For an actual interruption, the duty roster displays alternate contacts when acknowledgements are overdue. Staff reconcile printed or offline rosters when service returns, preserving document issue time, observer, actual event time, entry time and unresolved differences. A registration count provides an expected population and cannot certify physical presence.

After the event, a reviewer compares the timeline, decisions, response acknowledgements and outcomes. Assign each corrective action an owner and a date, then track completion independently of incident closure. Reports show time to acknowledgement, outstanding mandatory checks, unresolved discrepancies and repeated types of interruption within authorized scopes. Repeated small groups are suppressed in broad reports if they could identify a protected person.

## Acceptance

| Scenario | Observable result |
| --- | --- |
| A service is marked ready but the only qualified room supervisor departs | The briefing becomes subject to recheck, occupancy and admissions reflect the authorized response, and the new decision is recorded. |
| A drill coordinator selects a real congregation-wide audience | The system distinguishes exercise from live mode and requires explicit authorization before issuing any live announcement. |
| An unauthorized leader searches a safeguarding concern | They cannot discover protected case details from incident lists, notification previews, ordinary search or exports. |
| Two rooms report headcounts at different times after a transfer | The duty lead sees separate timestamps, scopes and the transfer. The system flags an unresolved overlap instead of declaring a definitive total. |
| An operator corrects the time of a recorded observation | The original entry, corrected time, actor, reason and sequence remain available for authorized review. |
| A review has an overdue facilities repair | The duty lead can trace the outstanding action to its work order and responsible steward after the incident itself is closed. |

See [child check-in](child-check-in.md), [facilities](resources.md) and [volunteers](volunteers.md).
