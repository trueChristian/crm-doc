# Groups and participation

A church may run a national youth ministry, campus chapters, classes within each chapter and time-limited volunteer teams. A person may lead one group, visit a second, attend a third regularly and retain membership of another congregation. Preserve each connection and its dates separately.

## Records and relationships

| Logical record | Fields | Interpretation and constraints |
| --- | --- | --- |
| GroupKind | `code code`, `label text`, `purpose text`, `default_visibility code`, `default_join_policy code`, `allows_children bool` | Unique code per organization. Examples include ministry, fellowship, committee, home group, course cohort and duty team. Retiring a kind preserves its old groups. |
| MinistryGroup | `kind_id → GroupKind`, `congregation_id → Congregation?`, `campus_id → Campus?`, `name text`, `short_code code`, `purpose text`, `language code?`, `visibility code`, `join_policy code`, `status code`, `opened_on date`, `closed_on date?`, `capacity count?`, `public_contact_person_id → Person?` | Unique short code per organization. Public, members-only, listed-by-invitation and confidential visibility govern discovery. A confidential group's existence and member counts are protected. A household's private address requires explicit release before appearing as a meeting place. |
| GroupLink | `parent_id → MinistryGroup`, `child_id → MinistryGroup`, `kind code`, `from_date date`, `until_date date?` | Reporting parent, affiliate or successor. One active primary reporting parent per child on any date. Reject self-link or a cycle in the reporting hierarchy. Affiliates can span campuses without inheriting control of each other's rosters. |
| GroupTerm | `group_id → MinistryGroup`, `title text`, `starts_on date`, `ends_on date?`, `enrolment_opens instant?`, `enrolment_closes instant?`, `seat_limit count?`, `state code` | Group has many terms. A term may represent an open-ended year-round roster. Freeze dates when the term closes. |
| GroupRole | `group_id → MinistryGroup`, `code code`, `title text`, `seat_limit count?`, `eligibility_policy_key code?` | Define coordinator, assistant, ordinary participant, visitor or observer per group. Screen who may hold a role separately from who may see a roster. |
| GroupParticipation | `term_id → GroupTerm`, `person_id → Person`, `entry_route code`, `state code`, `requested_at instant?`, `joined_on date?`, `left_on date?`, `departure_reason code?`, `approved_by → UserAccount?`, `priority count?` | At most one open spell per person and term. Completed spells support leave and later readmission. Contacts and contact preferences stay on person records. |
| GroupRolePeriod | `participation_id → GroupParticipation`, `role_id → GroupRole`, `from_date date`, `until_date date?`, `appointed_by → UserAccount`, `basis text?` | Roles can overlap when different. Same person's periods for the same role cannot overlap. Role and participation must belong to same group. |
| GroupJoinRule | `term_id → GroupTerm`, `criterion code`, `value text`, `decision code`, `effective_from date`, `effective_until date?` | Criteria include age on term start, qualification, expressed interest or sponsor review. Decisions include permit, require review and disallow. Define precedence and display the actionable reason to an authorized reviewer. |
| GroupInvitation | `term_id → GroupTerm`, `person_id → Person?`, `private_contact_ref id?`, `invited_by → UserAccount`, `expires_at instant`, `accepted_at instant?`, `status code` | Exactly one intended person or restricted contact reference. One invitation produces at most one request. Revocation makes unused invitations ineligible. |
| GroupRosterSnapshot | `term_id → GroupTerm`, `as_of date`, `produced_by → UserAccount`, `purpose text`, `field_set code`, `expires_at instant`, `row_count count` | Freeze a permission-filtered list when required for an event. Check current restrictions again on any later access or regeneration. |

## Running a group

1. A coordinator proposes name, purpose, sponsoring congregation, role owner and policy. An administrator approves it for listing. Choose whether interested people can join immediately, request approval, accept a private invitation or be assigned by staff.
2. At application, confirm the person's identity using the register. If the person is a guest without an account, record the request on their behalf and retain who submitted it. Unknown date of birth produces a manual eligibility review when an age limit matters.
3. Accept eligible requests up to the term's limit. Requested, invited and waitlisted people have no access to member-only group details. When two applications take the last place simultaneously, commit one acceptance and retain the other waiting position.
4. Appoint leaders for a term and define the scope they can actually operate. An acting leader has an end date. On turnover remove privileged access at the effective time and reassign upcoming actions and communications to the successor. A departed leader's previous actions remain attributable.
5. End a term by offering explicit renewal, transfer or closure. A new group for the same age band next year can inherit a proposed roster. The coordinator resolves current permissions, preferences and age eligibility before activation.

A transfer ends the origin participation only once the destination accepts when a continuous place was promised. On a split, keep original group history and record successor links. On closure, retain attendance and decisions, withdraw the listing, stop future invitations and present pending duties to the owner.

## Decisions, reports and controls

A secretary can search by language, accessible venue, meeting day, caregiver arrangements, available places and invitation route. Confidential groups may appear only to a person with explicit permission. Leaders can see contactable participants in their assigned groups and an outreach queue for their own requests. Group attendance trends count distinct people for an organization total, so a person in two chapters counts once. A list of people attending a group regularly who have never joined may support a welcome invitation where contact consent allows it.

| Acceptance case | Observable result |
| --- | --- |
| A household of five attends a welcome event and one adult joins the choir | One choir participation is created. The remaining four people and formal membership records retain their previous state. |
| A temporary assistant's authority ends Friday | Saturday's roster export excludes that assistant as an eligible operator even if they retained a saved link. |
| Two siblings share an address and one requests a confidential support group | Public search, profiles visible to relatives, aggregate reports with small counts and household activity do not disclose the request. |
| Moving a chapter beneath one of its own descendants | Save is refused with the conflicting path and the prior hierarchy stays in effect. |
| A former participant returns after a year | Historic attendance remains under the earlier dates and a new spell records the return. |
