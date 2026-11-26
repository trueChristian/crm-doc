# Incidents, near misses and independent review

A hall steward may report a trip without injury, damage to a borrowed vehicle or a service interruption. The organization needs to account for what happened, route it to the appropriate people and verify preventive action. General incident intake can receive a report with a sensitive element. Transfer that element privately to the designated owner, then keep the general record to the operational facts and actions that staff need.

## Logical records

| Record | Fields | Rules |
|---|---|---|
| IncidentReport | id ID, organization_id → Organization, campus_id → Campus?, event_ref ID?, resource_ref ID?, category code, is_near_miss boolean, observed_from instant?, observed_until instant?, received_at instant, source_kind code, safe_summary text, detailed_account_ref restricted ID?, reporter_person_id → Person?, reporter_contact_ref restricted ID?, anonymity enum(named, confidential, anonymous), privacy_class code, status enum(received, triaged, assigned, action_pending, verified, closed, reopened) | An incident may be reported before its scope is established. Record observations, discovery time, location precision and uncertainty. Distinguish original report from verified findings; keep links to related reports and mark duplicates without discarding witnesses. |
| IncidentTriage | id ID, report_id → IncidentReport, classification code, actual_impact code, potential_impact code, assigned_owner_id → UserAccount, reviewer_id → UserAccount, assessed_at instant, rationale restricted text, urgency code, escalation_due_at instant?, policy_revision text, supersedes_id → IncidentTriage? | Potential impact can be significant even when actual injury or loss is zero. A material reclassification creates a new signed decision and prompts a deadline review. |
| IncidentParty | id ID, report_id → IncidentReport, role code, person_id → Person?, supplied_identity restricted text?, safe_contact_ref ID?, contact_authority_ref ID? | Permit external or unidentified people, including witnesses, contractors and guests. A party role does not admit liability or become a general profile tag. |
| IncidentHandoff | id ID, report_id → IncidentReport, owning_area code, reason code, outgoing_fields code set, recipient_role code, dispatched_at instant?, due_at instant?, acknowledged_at instant?, destination_ref opaque ID?, status enum(requested, sent, acknowledged, declined, escalation_due) | One report may require facilities, insurance, personnel, safeguarding or statutory review. The receiving domain owns substantive details and current decisions. Dedupe on report, destination and purpose. |
| IncidentEvidence | id ID, report_id → IncidentReport, artifact_ref protected ID, describes text, submitted_by → UserAccount?, obtained_at instant?, submitted_at instant, origin code, access_class code, custody_ref ID?, retention_hold_ref ID? | Preserve originals, corrections and redacted extracts separately. Restrict material that identifies witnesses or affected children. |
| IncidentReview | id ID, report_id → IncidentReport, lead_id → UserAccount, review_method code, enabling_conditions text, evidence_refs ID set, conclusion text, uncertainty text?, independence_review_ref ID?, approved_at instant?, actions_required boolean | A review can identify missing control evidence without attributing blame. Document dissent, alternative explanations, related findings and information still outstanding. |
| IncidentResolution | id ID, report_id → IncidentReport, closing_reviewer_id → UserAccount, rationale text, finding_refs → AssuranceFinding set, open_handoff_summary code, closed_at instant, residual_risk_ref → RiskEntry?, supersedes_id → IncidentResolution? | Resolve open handoffs, or explicitly assign outstanding work with due dates and owner before closure. Keep names and primary evidence out of aggregated oversight packs. |

## Staff workflow

A public or volunteer intake allows minimal information, safe contact preference and an anonymous report. Explain that this is a reporting channel and show the church's approved route for immediate help. Give a neutral receipt without sending sensitive words to an unsafe endpoint. Avoid forcing a worker to select a legal or clinical conclusion to submit a report.

The intake coordinator compares actual and potential consequences, records immediate operational actions already taken, and routes the evidence to the competent owner. For an injury, incident staff see only information needed for their responsibility. Clinical care and emergency response remain with qualified services. A concern involving a child or vulnerable adult triggers referral to the applicable safeguarding lead; do not duplicate statements in the general incident timeline.

Assign a reviewer with suitable authority and no material conflict. Link conditions and failed controls to the risk register, specify who owns each corrective action, when verification is due and what counts as proof. The reviewer may reopen an event when new evidence arrives. Local reporting and insurer deadlines remain versioned policy settings rather than uniform defaults.

## Acceptance and oversight

| Case | Expected result |
|---|---|
| Three witnesses independently report the same wet entrance | Keep the three original reports and evidence, group them as one occurrence, and report one incident with three submissions. Correct a mistaken linkage without altering original statements. |
| An incident contains a name that must be protected | The facilities steward receives the condition and work request. General search returns no protected name, allegation or case reference. |
| Insurance acknowledges a claim and facilities repairs the floor | Both handoffs show separate owners and outcomes. The review still requires independent confirmation of corrective action where policy requires it. |
| A near miss reveals that no one owned a recurring inspection | Create a control finding and review obligation. A report can show actual injury count zero and a high potential impact simultaneously. |
| A leader requests monthly numbers | Show incident/near-miss counts, distinct occurrences, acknowledgment time, overdue actions and recurrence by permitted category; suppress sensitive or small cells. Personal reports stay restricted. |
