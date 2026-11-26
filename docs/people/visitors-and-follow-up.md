# Visitors, outreach and follow-up

Welcome workers need to distinguish an unnamed headcount from an individual who asked to be contacted. A returning visitor can participate in pastoral care, a meal or a class with no membership application. A named prospect can decline every subsequent invitation and remain welcome at services.

## Logical records

| Record | Fields | Integrity and use |
|---|---|---|
| VisitorEncounter | id ID, congregation_id → Congregation, campus_id → Campus?, person_id → Person?, occurrence_ref ID?, attendance_ref ID?, encounter_at instant, source enum(service_card, online_form, referral, outreach, walk_in, other), interaction_code code, captured_by → UserAccount?, self_reported_first_visit boolean?, intake_reference text?, safe_contact_requested boolean | A named encounter may reference one attendance entry. An anonymous numeric count stays with attendance; a temporary unlinked inquiry has its own expiry and cannot initiate contact without authority. Unique intake reference per source where supplied. |
| OutreachInterest | id ID, encounter_id → VisitorEncounter?, person_id → Person, interest_code code, congregation_id → Congregation, expressed_at instant, source code, contact_decision_ref ID?, status enum(open, referred, fulfilled, withdrawn, expired) | One person can request several things, such as a home visit or class information. Confirm that each contact purpose is allowed, especially with a third-party referral. |
| FollowUpPath | id ID, organization_id → Organization, name text, version integer, eligible_trigger code, owner_role code, effective_from date, until_date date?, inactivity_rule code, stop_rules code set | Versioned pathway for welcome, newcomers' class, transfer inquiry, bereavement check-in or return after absence. Use care workflows for private case details. |
| FollowUpStep | id ID, path_id → FollowUpPath, sequence integer, title text, responsible_role code, due_offset integer, due_unit enum(hours, calendar_days, working_days), trigger enum(on_start, after_prior, manually), completion_rule code, allowed_channels code set | Ordered, uniquely identified steps per path. Owner and fallback rules must resolve. Deadlines use the congregation's time zone, working days and quiet hours. |
| FollowUpEnrollment | id ID, path_id → FollowUpPath, person_id → Person, interest_id → OutreachInterest?, congregation_id → Congregation, source_reference text, owner_id → UserAccount?, started_at instant, paused_until instant?, state enum(active, paused, complete, declined, cancelled, expired), closed_at instant?, close_reason code? | Unique person, path version and triggering source. Re-entering later is a new episode with an independently valid purpose. Membership and regular attendance are independent. |
| FollowUpAction | id ID, enrollment_id → FollowUpEnrollment, step_id → FollowUpStep, assigned_to → UserAccount?, due_at instant, status enum(queued, assigned, scheduled, done, unsuccessful, skipped, cancelled), attempted_at instant?, attempt_number integer, outcome code?, next_try_at instant?, message_or_task_ref ID?, handoff_recipient_id → UserAccount? | Multiple explicit attempts per step. An automated retry of the same transmission does not create a new personal contact attempt. Limit attempts and stop on refusal or unsafe contact. |
| OutreachReferral | id ID, person_id → Person?, source_label restricted text?, referring_organization_id → Organization?, receiving_scope_ref ID?, authority_ref ID?, safe_summary restricted text, initiated_at instant, accepted_at instant?, state enum(received, verifying_authority, offered, accepted, declined, expired) | External referrers may provide minimal information. Block outreach until permission or another documented, approved contact authority exists. Internal handoffs transfer only the needed purpose and owner. |

## Daily operation

1. Record the service headcount or a voluntary visitor card. Search before creating a person. A group visiting together can be counted without creating named children or linking everyone to the person who filled out one card. If an existing guest returns, add the encounter to the existing person.
2. Record the requested help and preferred contact channel, safe hours, contact endpoint and permission. A paper “please call about the youth program” request authorizes that specific follow-up per local policy, without enrolling the person in newsletters. Provide an accessible alternative to online forms.
3. Assign the next task to an eligible welcome worker. If a volunteer is unavailable, reassign with a reason and visibility limited to the welcome task. A worker can mark no answer, wrong number, completed conversation, declined or escalated. Sensitive disclosures are entered in the appropriate restricted service.
4. Pause on request or while awaiting another team's response. Stop pending contact after withdrawal, verified death, disallowed endpoint, applicable protection, expiry or completion. A channel failure is not permission to try every other channel. Promote to a different pathway only after its own entry condition is satisfied.
5. Report unique first recorded encounters separately from self-reported first visits; historic data may be incomplete. For a return-rate cohort, specify first encounter period, eligible named contacts, return window and observation cutoff. Display anonymous attendance separately and suppress potentially identifying small breakdowns.

## Verification

| Case | Expected result |
|---|---|
| A worker submits a paper card twice and a second ministry imports it | A stable source reference makes the repeated import idempotent. A potential cross-source match enters review, with one active enrollment for the confirmed request. |
| One guest supplies a household phone and another declines follow-up | Only the consenting guest receives purpose-appropriate contact through a safe route. The entire household stays unsubscribed unless each applicable party agrees. |
| A volunteer starts a visit and receives a confidential request | The private care owner receives a minimal handoff. General welcome notes do not contain the disclosure. |
| Two workers claim the same available visit | One assignment succeeds and the other sees the updated owner. A shared task counts once in completion statistics. |
| A person withdraws while a reminder is queued | Before delivery, recheck permission, cancel the queued notice and show a neutral stop reason to the worker. Attendance history remains intact. |
| A guest has attended weekly for a year | Clerks can find the person on participation reports and start a membership inquiry on request. The formal roll has no automatic admission. |
