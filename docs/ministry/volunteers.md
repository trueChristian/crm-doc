# Volunteers and rotas

A coordinator fills actual positions at a particular time and place. A volunteer expresses interest and availability, accepts or declines a request and can arrange cover. A team leader sees vacancies and attendance. A designated reviewer assesses sensitive evidence and gives the coordinator a scoped eligibility decision.

## Records

| Logical record | Fields | Cardinality and rules |
| --- | --- | --- |
| VolunteerProfile | `person_id → Person`, `started_on date`, `state code`, `preferred_campus_id → Campus?`, `max_assignments_per_week count?`, `preferred_contact_window text?` | One current profile per person. An interest enquiry can be recorded before activation. Suspension prevents future assignment. Record changes and restrict the explanation. |
| VolunteerSkill | `person_id → Person`, `skill_code code`, `level code`, `basis code`, `assessed_by → UserAccount?`, `assessed_on date?` | One entry per assessed skill and period. Mark self-assessment, demonstrated ability or reviewed qualification. |
| ServicePosition | `group_id → MinistryGroup`, `title text`, `responsibilities text`, `skill_code code?`, `minimum_age count?`, `training_required bool`, `conflict_group code?`, `active bool` | One ministry has many positions, such as driver, door steward or interpreter. Restrict changes to requirements after appointment and flag affected future assignments for review. |
| PositionRequirement | `position_id → ServicePosition`, `credential_code code`, `scope code`, `minimum_level code?`, `mandatory bool`, `effective_from date`, `effective_until date?` | All mandatory requirements must be valid for the assignment interval, including the end of a late shift. |
| VolunteerApplication | `person_id → Person`, `position_id → ServicePosition`, `submitted_at instant`, `stage code`, `reviewer_id → UserAccount?`, `decision_at instant?`, `reason_code code?` | Enquiry, applied, screening, training, approved, declined, withdrawn. Preserve decisions when a person reapplies. Application answers and references belong in restricted evidence records. |
| VolunteerCredential | `person_id → Person`, `credential_code code`, `jurisdiction code?`, `verified_by → UserAccount?`, `verified_at instant?`, `valid_from date`, `valid_until date?`, `status code`, `restricted_evidence_ref id?` | Rota users receive valid, expired, suspended or needs review. Store reference checks, evidence and reasons under separate access and retention rules. |
| AvailabilityWindow | `person_id → Person`, `kind code`, `starts_on date`, `ends_on date?`, `weekdays code_set?`, `local_start time?`, `local_end time?`, `zone zone`, `priority count` | Available, preferred or unavailable. A dated unavailability overrides a recurring preference. Split overnight ranges at the local boundary when checking conflicts. |
| DutyShift | `occurrence_id → EventOccurrence`, `position_id → ServicePosition`, `room_booking_id → RoomBooking?`, `starts_at instant`, `ends_at instant`, `required_count count`, `standby_count count`, `lead_person_id → Person?` | One occurrence can have many shifts, including setup and teardown outside its public hours. The shift belongs to one organization and its campus location is explicit. |
| VolunteerAssignment | `shift_id → DutyShift`, `person_id → Person`, `state code`, `offered_at instant?`, `respond_by instant?`, `responded_at instant?`, `assigned_by → UserAccount`, `slot_kind code`, `override_reason text?` | One active assignment per person and shift. Invited, accepted, declined, expired, withdrawn, removed, served and absent. An accepted standby is tracked separately from required coverage. |
| ShiftExchange | `original_id → VolunteerAssignment`, `candidate_person_id → Person?`, `requester_id → Person`, `requested_at instant`, `state code`, `reviewed_by → UserAccount?`, `replacement_id → VolunteerAssignment?` | Many proposals may exist, only one can replace the same active assignment. Keep original and replacement linked. |
| ServiceTimeEntry | `assignment_id → VolunteerAssignment`, `arrived_at instant?`, `departed_at instant?`, `break_minutes count`, `approved_minutes count?`, `reviewed_by → UserAccount?`, `correction_of_id → ServiceTimeEntry?` | Measured minutes exclude breaks. Prevent negative durations and overlapping approved time for the same person. Estimate and approved hours are distinguishable. |

## Scheduling and exceptions

Build shifts from a ministry pattern or copy a prior service. The draft carries role requirements and times. Every invite checks availability, credential validity, age policy, workload, double bookings, travel allowance between campuses and permitted supervision ratios. Differentiate hard constraints such as a suspended clearance from preferences such as serving twice a month. Record the coordinator's rationale and authorization for a permitted soft exception. Eligibility is checked again when a person accepts, when a replacement is chosen and before check-in.

A volunteer may offer their place to a qualified colleague without sharing the whole roster. The colleague sees the role, times and relevant location. A transfer completes once the colleague accepts and approval requirements are satisfied. Until then the existing allocation stays effective unless its holder explicitly withdraws, which creates a visible vacancy. Expiry of a credential after publication removes the person from eligible coverage, privately instructs the reviewer to resolve the problem and alerts the leader to an unfilled position. Keep sensitive causes off group messages.

A reminder follows the person's channel and quiet-time preferences. A schedule change invalidates outdated accept links. Moving a shift beyond the originally accepted time triggers a new confirmation under the ministry's change policy. After service, the leader checks actual attendance and approves claimed hours. Volunteer participation does not create a payroll obligation or a payment instruction. Approved expense claims move to finance separately.

## Coordinator screens and verification

Show open positions, upcoming renewals, people awaiting orientation, consecutive weeks of service, declined assignments, standby capacity and unexplained gaps. Give volunteers a calendar of their own commitments, a simple unavailable-date control and a private response link. A matching assistant can suggest available volunteers and explain skill, availability and workload matches. The coordinator owns invitations. Hidden health, pastoral, household and giving records cannot be matching inputs.

| Acceptance case | Observable result |
| --- | --- |
| A door steward declines and an eligible reserve accepts | Vacancy clears after acceptance, reminder recipients change, the declined offer remains in history. |
| Two leaders schedule a person for overlapping shifts | The second assignment is blocked or referred under a documented compatible-role policy. Separate campuses include travel time. |
| A volunteer's credential is suspended after the rota is printed | The live coverage view marks a vacancy and the duty lead receives a private action. The paper copy carries its issue time and replacement instructions. |
| Two coordinators approve different substitutes for the same seat | One exchange takes effect. The second reviewer sees the current assignment and can choose a different vacancy. |
| An assistant leader exports the roster | Their file includes shift, volunteer display name and permitted contact route. It excludes evidence, screening reasons and unrestricted member contact details. |
| A volunteer serves 09:00–12:00 with a 15-minute break | Approved service time can be 165 minutes. A correction preserves the original entry, actor and reason. |
