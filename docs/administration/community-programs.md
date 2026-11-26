# Agreements, service rounds and relief distribution

A food pantry, scholarship, mission support or disaster appeal may serve people who never join the church. Permit a confidential service identifier and a safe contact method. A ministry coordinator organizes the distribution. A care worker determines entitlement to individual assistance. A stock keeper or treasurer records the actual goods or money delivered. A sponsor sees agreed results only.

## Ownership from agreement to delivery

| Question | Authoritative record | Link used by the coordinator |
| --- | --- | --- |
| Which organization or missionary is working with us? | MinistryPartner and ProjectPartnerRole | Use that partner's identifier in PartnershipAgreement and preserve the role held on the service date. |
| What did both parties undertake to deliver? | PartnershipAgreement and PartnerPromise | Attach service terms below. A sponsor benefit is a contractual deliverable; aid handed to a guest is a service fulfilment. |
| Who may receive assistance, and how much? | AidProgram, AidApplication, AidAssessment and AidAward | Invite participation in a specific round. Only authorized caseworkers see the evidence supporting a decision. |
| Where and when was stock actually handed over? | CommunityDistribution and AssistanceIssue | One dated operating session and a single source key per physical handover. Where an inventory partner is connected, link its acknowledged dispatch reference. One AidFulfillment can point to that issue as its execution evidence. |
| Who was paid? | AidFulfillment and an external payment acknowledgement | The payee can be a vendor while the applicant remains the beneficiary. An approved award can await execution. Record an external reference or restricted confirmation of payment before counting money delivered. |
| Which results may a partner publish? | ProjectOutcome and ImpactPublication | Approve the aggregate scope and language separately from case records and personal testimonies. |

## Additional records for running a service round

| Table | Fields | Integrity and handoff |
| --- | --- | --- |
| ProgramServiceTerms | id; agreement_id → PartnershipAgreement; project_id → MissionProject; aid_program_id → AidProgram; service_area: text; valid_from, valid_until: dates; eligibility_policy_ref; approved_budget_ref; report_due_rule; disclosure_limits; signatories; evidence_ref | Add operational terms to a specific agreement. A budget is a ceiling. It never authorizes an individual payment. |
| AssistanceRound | id; terms_id → ProgramServiceTerms; intake_opens_at, intake_closes_at: instants; service_date: date; distribution_id → CommunityDistribution optional; unit_kind: parcel, voucher, visit, scholarship or service; capacity: count; coordinator; state: draft, open, paused, closed, reconciled | One round can accept many applications. Opening, closing intake and completing reconciliation are independent transitions. |
| RoundPlacement | id; round_id → AssistanceRound; application_id → AidApplication; award_id → AidAward optional; requested_units: quantity; offered_units: quantity; state: waiting, offered, confirmed, withdrawn or expired; offer_expires_at: optional instant; source_key | Unique active placement for the application and round. Waiting for a session does not alter the caseworker's eligibility decision. |
| CollectionAcknowledgement | id; fulfillment_id → AidFulfillment; issue_id → AssistanceIssue optional; occurred_at; receiver_or_delegate_key: optional private reference; acknowledgement_method: code; evidence_ref; recording_actor; operation_key | Binds receipt evidence to the original fulfilment. A recipient may decline a photograph or signature and use approved private alternatives. Re-recording evidence cannot consume stock or funds again. |
| ProgramIndicator | id; terms_id; milestone_id → ProjectMilestone; label: text; unit: code; numerator_rule, denominator_rule: versioned criteria; permitted_breakdown: list; minimum_report_size: count | Specify distinct people versus service encounters. A ProjectOutcome holds the actual observation. Suppress identifying small cells and complementary subtotals. |
| ProgramFeedback | id; terms_id; anonymous_ref: optional; submitted_at; safe_response_ref: optional; kind: suggestion, appeal or complaint; handler; due_at; outcome; closed_at; audience; referred_case_ref: optional | Refer eligibility appeals to AidReview and a protected complaint to the independent docket. An ordinary coordinator sees only permitted status. |

**Example.** A pantry authorizes two parcels for a guest household. One is collected on Tuesday, another by a verified delegate on Friday. Store two fulfilments linked to two issues. If a warehouse participates, correlate each handover with its external stock reference. Repeating Friday's offline upload leaves both the parcel count and downstream instructions unchanged. A public dashboard may count one household, two parcels and two service visits. Sponsors receive aggregate results and approved expenses. The household may later choose to apply for church membership independently.

**Acceptance.** A stock shortage after the first parcel leaves the award partially fulfilled and offers an agreed appointment or approved substitute. A lost voucher can be cancelled and reissued without doubling the award. An appeal has an independent safe response route. A change of congregation does not change an approved grant. Compare units awarded, distributed, returned or spoiled with custody sheets or an authorized warehouse extract. Record an open difference and an owner when warehouse evidence is still outstanding.

See [missions and community service](../ministry/missions.md), [benevolence](../people/benevolence-and-community-aid.md), [development](../development/README.md) and [protected complaints](../assurance/complaints-and-grievances.md).
