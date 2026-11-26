# Participation categories and personal milestones

A church often needs to distinguish a first-time guest, returning guest, regular attender, community partner, member of another church and person seeking membership. These descriptions support welcome and planning. A person can be a regular attender at one congregation and an official member of another. Participation history helps answer who was connected to each congregation during a period independently of its formal register.

## Logical records

| Record | Fields | Integrity and use |
|---|---|---|
| ParticipationCategory | id ID, organization_id → Organization, code code, label text, description text, category_family code, exclusivity enum(single_at_a_time, multiple), eligible_evidence code set, active_from date, until_date date? | Define behavioral descriptions and local reporting labels. Never use a category as a credential or a substitute for a formal membership decision. |
| CongregationParticipation | id ID, person_id → Person, congregation_id → Congregation, campus_id → Campus?, category_id → ParticipationCategory, effective_from date, effective_until date?, recorded_at instant, recorded_by → UserAccount?, source_kind enum(self_declared, staff_confirmed, imported), evidence_ref ID?, ending_reason code?, revision integer | Separate many-to-many person/congregation episodes. Prevent overlaps in the same exclusive family and scope. Different participation families may coexist, and the person may retain memberships or roles elsewhere. |
| MilestoneDefinition | id ID, organization_id → Organization, code code, version integer, label text, category enum(formation, service, welcome, anniversary, locally_defined), prerequisite_rule_ref ID?, confirmation_role code?, repeat_rule code, evidence_policy code, visibility code, validity_months integer?, effective_from date, until_date date? | A configurable non-sacramental milestone such as completing orientation, finishing a course or starting a year of service. Activities, rites and membership decisions keep their own authoritative records. |
| PersonMilestone | id ID, person_id → Person, definition_id → MilestoneDefinition, congregation_id → Congregation, status enum(planned, proposed, verified, expired, superseded, withdrawn), achieved_on date?, achieved_year year?, date_precision enum(day, year, unknown), verified_at instant?, verified_by → UserAccount?, source_kind code, source_ref ID?, evidence_ref ID?, supersedes_id → PersonMilestone?, next_review_on date? | One person can have multiple milestones. Historical knowledge can be year-only. A repeatable milestone has a distinct occurrence or eligible interval; repeated imports of the same source occurrence create one record. |
| PersonalGoal | id ID, person_id → Person, title private text, description private text?, target_on date?, visibility enum(private, named_mentor), mentor_person_id → Person?, linked_definition_id → MilestoneDefinition?, state enum(active, paused, achieved, withdrawn), created_at instant, closed_at instant? | Optional member-controlled record. A mentor sees only explicitly shared goals within consent and current assignment; completion may suggest verification of a milestone where requested. |

## Operating rules

* A voluntary self-description or clerk-confirmed change opens a participation period. Attendance trends may flag an invitation to review where the organization has a purpose; never silently assign a religious standing or infer formal admission. Declining follow-up, stopping attendance or living in a member's home does not imply a change in standing.
* Support household and congregation counts with explicit measures. “People in households with a formal member” counts distinct linked people, including nonmembers, under the chosen residence convention. “Regular attenders who are not formal members here” selects participation episodes and excludes qualifying MembershipPeriods in the same congregation on the same date. Report guests who never joined a household separately.
* A member can choose a plan such as completing orientation, joining a service team and scheduling a welcome meeting. Show prerequisites, which evidence is needed, who can confirm completion, available accommodations and who may view it. Participation in a plan and accomplishment of a rite remain individually disclosable.
* Capture education, safeguarding training and role credential evidence in the owning training/service domain. A profile milestone may link to a verified result but never independently authorize a child-facing or finance role. Historic role snapshots remain attributable after a new version of a milestone definition takes effect.
* Offer shareable achievements and anniversary reminders as optional features. Staff suggest a celebration and the person selects the wording and audience; a default dashboard should not display a private conversion date, age or religious history. Reevaluate active preferences and eligibility at dispatch.
* Clerks can prepare a church census at a reference date by campus, category, household composition and age band. Use an explicit unknown-age bucket and a policy for partial dates. Counts from separate campuses may overlap; group totals deduplicate people or identify that they count affiliations.

## Acceptance

| Case | Expected result |
|---|---|
| A visiting adult is staying temporarily with a family of formal members | The person can appear on household and guest reports. They are absent from the formal roll unless they have their own qualifying membership. |
| An adult is a regular attender at congregation A and a member at congregation B | Both facts are retrievable independently; a scoped user at A cannot infer B's restricted information. |
| A family wants to celebrate a child's milestone, but only one parent has consented | Publication checks the child's representation and disclosure policy. Completing the activity alone never publishes a photo or name. |
| A member withdraws access from a mentor | Mentor loses the goal from search and tasks, and queued reminders containing private information are suppressed. |
| A milestone is retracted by the reviewing leader after an entered mistake | The original and its correction remain reconstructable, with notifications to authorized dependent services. Formal and financial records do not change implicitly. |
