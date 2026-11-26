# Missions and community service

A congregation can sponsor a long-term partner, run a food distribution, organize a mission trip or coordinate a response with several churches. Use projects to agree objectives, accountable owners, resources and evidence of delivery. Offering assistance must have a registration route for people who are outside the church and people who need limited identification.

## Records

| Logical record | Fields | Cardinality and rules |
| --- | --- | --- |
| MinistryPartner | `name text`, `kind code`, `contact_person_id → Person?`, `private_contact_ref id?`, `service_area text`, `review_state code`, `review_due_on date?`, `public_listing bool` | A project partner, community organization, missionary or sponsor. A partner relationship confers no access to church records. Finance owns the separate supplier, customer or payee identity. |
| MissionProject | `title text`, `owner_group_id → MinistryGroup`, `lead_person_id → Person`, `sponsoring_congregation_id → Congregation`, `start_on date`, `end_on date?`, `purpose text`, `location_scope text?`, `public_summary text?`, `finance_project_ref id?`, `state code` | Proposed, authorized, active, paused, completed, closed or cancelled. Projects can run multiple trips or distributions. Public summaries require publication approval. |
| ProjectPartnerRole | `project_id → MissionProject`, `partner_id → MinistryPartner`, `role code`, `from_date date`, `until_date date?`, `agreement_ref id?`, `share_scope code` | Many-to-many with effective scope e.g. sponsor, host, beneficiary organization or delivery partner. Ended agreements stop further sharing; history keeps its original scope. |
| ProjectMilestone | `project_id → MissionProject`, `title text`, `due_on date`, `owner_id → Person`, `target_quantity decimal?`, `unit code?`, `status code`, `evidence_ref id?` | Define what, by when and how measured. A percentage requires a defined denominator. Count visits and unique households as separate measures. |
| MissionTrip | `project_id → MissionProject`, `lead_person_id → Person`, `depart_at instant`, `return_at instant`, `origin_label text`, `destination_scope text`, `traveller_limit count?`, `finance_budget_ref id?`, `approval_state code` | Trip includes a sequence of dated itinerary events, travel legs, approved travellers, briefing and close-out. A detailed itinerary may be restricted. |
| TripParticipant | `trip_id → MissionTrip`, `person_id → Person`, `role code`, `stage code`, `emergency_contact_ref id?`, `consent_ref id?`, `readiness_result code`, `reviewed_by → UserAccount?` | Unique active place per person and trip. Use application, waitlist, accepted, cleared, departed, returned and withdrawn states as applicable. Evidence of travel readiness has scoped access and expiry. |
| TripLeg | `trip_id → MissionTrip`, `sequence count`, `occurrence_id → EventOccurrence?`, `from_label text`, `to_label text`, `depart_at instant`, `arrive_at instant`, `transport_ref id?`, `lead_person_id → Person` | Actual travel and expected return can be reconciled to the crew and passenger list. Each leg may have a different passenger manifest. |
| ProjectSupply | `project_id → MissionProject`, `item_label text`, `unit code`, `requested_qty decimal`, `approved_qty decimal?`, `stock_ref id?`, `fund_ref id?` | Planned quantities. Stock and finance own receipts, valuation and payments. Convert units only with an explicit valid conversion. |
| CommunityDistribution | `project_id → MissionProject`, `occurrence_id → EventOccurrence`, `steward_id → Person`, `site_label text`, `eligibility_policy code`, `identity_mode code`, `state code` | One operating session, with named, pseudonymous or anonymous recipients as policy allows. Capture eligibility privately and provide a manual review route. |
| AssistanceIssue | `distribution_id → CommunityDistribution`, `supply_id → ProjectSupply`, `recipient_person_id → Person?`, `recipient_household_id → Household?`, `anonymous_case_ref text?`, `issued_quantity decimal`, `unit code`, `issued_at instant`, `issued_by → UserAccount`, `stock_movement_ref id?`, `request_key text` | One recipient basis per issue, with policy permitting anonymous collection. Count and unit must be positive. Unique operation key prevents a repeated handover from decrementing stock twice. |
| ProjectOutcome | `milestone_id → ProjectMilestone`, `period_start date`, `period_end date`, `actual_quantity decimal`, `unit code`, `measure_method code`, `evidence_ref id?`, `reviewer_id → UserAccount?`, `publication_scope code` | Distinguish observed from estimated outcomes. Corrections supersede prior figures. Beneficiary testimony, name or photograph requires its own consent and publication decision. |

## From proposal to close

Approve scope, local host, objectives, eligible expenditure, safety arrangements and reporting dates before opening applications or soliciting restricted gifts. Finance links approved budgets, fund restrictions, gifts, expenses and unused balances to the project; a public progress view consumes approved totals. A pledge cannot count as money already received. Project closure records what happened to unspent balances, unfulfilled promises, undelivered supplies and pending reports. Finance authorizes any disposition.

For a distribution, the steward receives an approved quantity, records each handover, documents spoilage or returns through inventory, and compares opening stock, receipts, delivered units, returns and closing stock. When sensitive beneficiary details are necessary for casework the care team owns them. The outreach worker receives the practical authorization and next action. A shortage places the unresolved application in a fair waiting queue, preserving the original request time. A duplicate alert routes to review and cannot by itself deny assistance. External partners see only named fields authorized by the agreement and the person's sharing preferences.

For trips, collect readiness decisions and expiry dates, request guardian authority where relevant, arrange transport, roster qualified leads, capture called-for fees and publish a participant-only briefing. Before departure reconcile actual travellers with the approved manifest. On return record each passenger's arrival and exception owner. A restricted incident can reference the trip without exposing its private narrative in a donor update.

## Acceptance

| Scenario | Observable result |
| --- | --- |
| A pantry starts with 100 parcels, receives 30, issues 95 and returns five to central stores | Its closing local count is 30. Unexplained differences remain open for reconciliation. |
| A detached household requests food but declines church registration | Authorized assistance proceeds under the permitted identification mode. No formal membership or marketing subscription is created. |
| Two volunteers retry an issue captured at the same desk | One handover and one inventory movement remain; the receipt refers to the original issue. |
| A donor asks how many households received help | Show the approved, privacy-checked measure. If anonymous handovers prevent deduplication, publish distribution counts and the limitation separately. |
| A project spans two congregations and a partner | Staff see the scoped operational records. An aggregate project report can show combined results without revealing donor identities or private traveller documents. |
| A trip is cancelled after donations and participant fees were paid | Open a separate review for restricted gifts, commercial refunds and unused commitments. Communicate the applicable decision to each affected party. |

See [resources and fleet](resources.md), [registration](registration.md) and [operational readiness](readiness.md).
