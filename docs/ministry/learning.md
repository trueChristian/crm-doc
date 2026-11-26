# Learning and formation

Education covers Sunday school, adult classes, newcomer orientation, mentoring, premarital preparation and leadership development. A church determines its own curriculum and completion criteria. Finishing a course can open a review for a formal milestone. The authorized register keeper decides whether to record it.

## Records and keys

| Logical record | Fields | Meaning and constraints |
| --- | --- | --- |
| Curriculum | `owner_group_id → MinistryGroup?`, `title text`, `summary text`, `audience code`, `language code`, `version count`, `state code`, `review_on date?` | A published curriculum version is immutable. Aliases, translations and successors reference an explicit version. |
| LearningUnit | `curriculum_id → Curriculum`, `parent_id → LearningUnit?`, `sequence count`, `title text`, `objective text`, `duration_minutes count?`, `resource_ref id?`, `delivery_mode code`, `required bool` | Nested topics, lessons and activities with ordered children. Parent must belong to same curriculum, and cycles are invalid. Store teacher and learner materials under distinct visibility. |
| FormationPath | `title text`, `owner_group_id → MinistryGroup`, `version count`, `entry_policy code`, `completion_policy code`, `state code` | Paths combine courses, meetings, mentoring or staff review. Churches can use one stage or several parallel branches. A path owner reviews adverse decisions. |
| PathStep | `path_id → FormationPath`, `label text`, `kind code`, `curriculum_id → Curriculum?`, `required bool`, `approval_role code?`, `completion_evidence code` | One path has many steps. Dependencies use PathDependency. An optional activity cannot silently become mandatory after enrolment. |
| PathDependency | `step_id → PathStep`, `requires_step_id → PathStep`, `logic_group code` | An actual predecessor in the same path. Each logic group accepts any satisfied option; all required groups must be met. Disallow cycles. |
| CourseOffering | `curriculum_id → Curriculum`, `term_id → GroupTerm?`, `instructor_id → Person`, `campus_id → Campus?`, `start_on date`, `end_on date?`, `language code`, `capacity count?`, `enrol_policy code`, `state code` | Many offerings of one version. Named approval required to substitute materials or an instructor. Use the event waitlist when places are limited. |
| CourseSession | `offering_id → CourseOffering`, `occurrence_id → EventOccurrence`, `unit_id → LearningUnit?`, `session_number count`, `teacher_person_id → Person` | Connect lesson, teacher and attendance. A replacement session explicitly references the affected occurrence through its revision. |
| LearningEnrolment | `offering_id → CourseOffering`, `person_id → Person`, `submitted_by → UserAccount?`, `started_on date?`, `ended_on date?`, `status code`, `accommodation_ref id?`, `completion_basis code?` | One active enrolment per person and offering. Applied, waitlisted, enrolled, paused, withdrawn, completed. Confirm appropriate authority for a dependent. |
| LearningEvidence | `enrolment_id → LearningEnrolment`, `unit_id → LearningUnit`, `kind code`, `attempt count`, `outcome code`, `attested_by → UserAccount`, `earned_on date`, `evidence_ref id?`, `supersedes_id → LearningEvidence?` | Attendance, demonstrated outcome, assessment, prior-learning credit or instructor attestation. Keep retake and correction history. Sensitive details require a restricted evidence scope. |
| PathParticipation | `person_id → Person`, `path_id → FormationPath`, `adviser_id → Person?`, `started_on date`, `state code`, `finished_on date?` | A person can undertake many paths. Repeating a path preserves earlier progress and anchors the participant to a defined version. |
| PathStepResult | `participation_id → PathParticipation`, `step_id → PathStep`, `evidence_id → LearningEvidence?`, `state code`, `approved_by → UserAccount?`, `decided_on date?`, `reason text?` | Satisfied, exempted, deferred, in review or incomplete. A waiver has an authorizer and scope. |
| LearningAward | `person_id → Person`, `enrolment_id → LearningEnrolment?`, `participation_id → PathParticipation?`, `title text`, `serial text`, `issued_on date`, `expires_on date?`, `withdrawn_on date?`, `issuer_id → UserAccount` | Exactly one completion source. Unique serial within the organization. Reprinting preserves serial and any withdrawal. Public verification, if offered, discloses the minimum approved information. |

## Workflows and inclusion

A coordinator opens a term, assigns instructors and publishes ages, prerequisites, capacity, accessible formats and available languages. Calculate age on the configured assessment date and route incomplete birth evidence for review. Children in two households can attend without duplicating a person. A church can allow an unregistered guest to try a class while preserving supervision or consent requirements.

A teacher marks the actual session, records attendance in the common attendance record and assesses only the stated learning outcomes. Registering someone for an alternate Sunday or changing their caregiver leaves their completion record intact. When an instructor is screening their own achievement, a distinct authorized reviewer must decide under the course's separation policy.

A learner may pause for a season, challenge an error, transfer to another offering or receive recognition for prior learning. Transfer evidence by unit equivalence and curriculum version with a recorded decision. Preserve unfinished or disputed items in context. A missed session can be made up if the course policy permits. Program staff see matters requiring action. Leaders see aggregated enrolment, capacity, completions, withdrawals and outcomes. Personal learning plans or faith disclosures stay inside the learning consent and role boundaries.

## Acceptance

| Scenario | Observable result |
| --- | --- |
| A teacher is reassigned to another class midterm | Their former class access ends on the effective date. Historic attendance remains attributable to them. |
| A learner completes four of five units and the fifth is formally waived | Their record shows four earned units and one approved waiver with the reason visible only within the review scope. |
| A new curriculum version changes the prerequisite | Enrolled learners continue under their original version unless an authorized migration presents its impact and records explicit decisions. |
| A family requests an accessible take-home lesson | The teacher sees the approved adjustment and permitted material, with private supporting details available only to the designated reviewer. |
| A confirmation course is complete and requires pastoral review | A single review task is created. Rerunning completion leaves one task. Formal membership and rite records change only through authorization in the register. |
| An award was issued against a mistaken identity | Withdraw the mistaken award with audit history, correct the evidence and issue the correct recipient a separate award. |

See [groups](groups.md), [child check-in](child-check-in.md) and [attendance](registration.md).
