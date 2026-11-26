# Carry a learning decision to a registrar

Two congregations share a curriculum. Congregation A uses course completion to invite a person to a separate local rite review. Congregation B issues a learning award only. The labels, requirements and authorities are fixture choices. A successful run preserves the difference between evidence of learning, proof that a ceremony occurred, a register entry, an issued extract and a membership decision.

## Pin the versions and people

| Fixture record | Applicable rule |
| --- | --- |
| A.Path version 3, final step F | Require both dependency groups. Group 1 accepts either attendance at orientation O or a reviewed equivalence E. Group 2 accepts assessed practice P only. The final reviewer must approve completion. |
| A.Course teaching version 5 | Two units, orientation and practice. An informal visit is permitted as observation only. The practice demonstration is independently assessed. On a repeat attempt, preserve the earlier genuine attempt. |
| A.Registrar policy version 2 | For the example local commissioning rite require one principal, one authorized officiant and one attesting witness. Require verified evidence that it occurred. One book is open with prior entries through 140. Certificates require separately authorized disclosure. |
| B.Policy | The same curriculum may be taught. No local rite or register workflow is enabled from completion. Course completion has the same meaning even though its follow-up differs. |
| People and authority | Ari is the learner. Em teaches, Pat reviews, Sol is the registrar, and Ren is a named witness without a local account. Only Sol is authorized to confirm the entry. Pat may approve training and has no register authority. |
| Stable provenance | Map each academic decision to person, offering, curriculum version, unit, attempt and evidence. Map each rite to its own definition, congregation, kind, date precision, participants and provenance. A matching name is insufficient to merge any two histories. |

The dependency calculation is (O or E) and P followed by an authorized final decision. The table below tests prior satisfactory results. A formally deferred result is unsatisfied until a decision changes it.

| O | E | P | Which requirement remains before final review |
| --- | --- | --- | --- |
| No | No | No | One orientation option and assessed practice. |
| Yes | No | No | Assessed practice. |
| No | Yes | No | Assessed practice. |
| Yes | Yes | No | Assessed practice. The two alternative results satisfy one requirement group. |
| No | No | Yes | One orientation option. |
| Yes | No | Yes | Prerequisites satisfied. Await the final authorized reviewer. |
| No | Yes | Yes | Prerequisites satisfied by equivalence and assessed practice. Await the final authorized reviewer. |
| Yes | Yes | Yes | Prerequisites satisfied. Both alternatives do not count as two completed final steps. |

## Run the learner's case

1. Enrol Ari once in the version 5 offering. Record one observation visit. Reception can show that attendance under the occurrence's rules. It cannot satisfy P, publish a testimony or update the person's congregational standing.
2. Pat accepts Ari's external orientation evidence as E. Preserve the external origin and the specific version it satisfies. The curriculum owner publishes version 6 the next day. Continue evaluating the active enrolment against version 5.
3. Em records attempt 1 at P as incomplete, and attempt 2 as satisfactory following a second actual demonstration. Preserve two real attempts. A retry of the attempt 2 submission creates no third attempt. Correct a mistaken factual observation via LearningEvidence.supersedes_id and its audit trail. A correction to attempt 2 and a newly taken attempt 3 have different business meanings.
4. The final reviewer sees E and P under their approved scope. Em may teach and attest, but cannot use another person's reviewer identity. Pat accepts F, links the source evidence and approves the completion. A repeat event for F returns the same effect.
5. The award issuer creates one LearningAward tied to exactly one source, either this enrolment or this path participation according to the selected award rule. Record issuer, serial and issue date. Reprinting an unchanged award uses the same serial. A revocation sets its withdrawal date and does not erase the course attempts.
6. In A, completion opens one private preparation or registration review. In B, run the equivalent approved learning sequence with B's own learner and scope. B gets zero new rite reviews. Neither church records a rite, certificate or membership admission from this completion alone.
7. If A's ceremony is postponed after a fee or waiver is recorded, keep the receipt or waiver in its owning domain, move the event and recheck participants and room bookings. Keep the local register unchanged. If a later request is declined, record the case outcome without revising the fact that Ari completed the course.

## Ceremony, entry and issue

The ceremony eventually takes place. Ari is the principal, an approved guest officiates, and Ren witnesses. The officiant's confirmation is available to Sol. All dates are precise on this path. The same book will also receive another independent local entry.

| Record or command | Check before committing | Result to inspect |
| --- | --- | --- |
| Prepare Ari's RiteRecord | Definition version 2 allows performed_here. The registrar has actual occurrence evidence, its place, date precision and the allowed participant roles. | One pending review referencing the local occurrence evidence. The named guest and witness can remain unlinked to a directory account. |
| Validate participant values | Only fields belonging to that definition version can be accepted. Required roles are present and the allowed value type and visibility of each configured field apply. | Ren appears as witness under the authorized register entry. Being a witness gives no access to a learning file, church directory or extract. |
| Confirm Ari and independently confirm the other local entry | Two clerks concurrently request entry into the same open book. Their request identities are distinct. | Current numbers are 141 and 142 in whichever allocation order wins. A clerk's retry returns its own original outcome. The two principals never share a number. |
| Issue Ari's authorized extract | Check disclosure authority for the requested recipient, current register status and approved template revision. | One CertificateIssue records the original name snapshot, issue number, recipient, authority and issued artifact. The learning award keeps its separate serial. |
| Correct Ren's name | Sol reviews documentary evidence, links corrected record and amendment, retains original wording and verifies book scope. | The original book number remains reserved and traceable. Issue a replacement extract only under disclosure authority and link its replaces_id to the prior issue. Narrow recipients see only the permitted wording. |
| Request an extract as the course teacher | Teaching role alone supplies no disclosure authority for the register. | No new issue, artifact, witness information or revealing search result is produced. Record the access decision under the applicable policy. |
| Enter a year-only attestation from another church | The local definition permits attested_elsewhere. Confirm external source, year precision and evidence. | Historic record preserves its entered provenance. The local-performed count remains two. No synthetic ceremony day, service occurrence or local officiant is invented. |
| Record a second event with similar participant names | Evaluate definition repeat_rule and assigned reviewer. The local fixture requires review of a possible repeat. | Pending review may link a verified duplicate, accept a distinct occurrence or reject it with reason. A name match alone cannot invalidate either original. |

## Wrong person discovered after both awards

Test the scopes of correction independently. If the assessment belonged to another learner, withdraw the mistaken award, correct the learning evidence with a reviewed identity decision, and evaluate the other learner's own enrolment and permissions before issuing a new serial. A training correction reaches a pending rite review as a re-evaluation signal.

If the registrar has independent evidence that Ari actually took part in the ceremony, retain that historical fact. The registrar decides any consequence under the rule in force and records it; a teacher cannot revoke a ceremony by correcting a class entry. Conversely, if the incorrect identity was copied into the register, the registrar issues an authorized amendment, evaluates existing extracts and records the disposition of each. Check the locally chosen membership workflow independently. This fixture has authorized zero membership admissions.

| Reconciliation question | Expected evidence |
| --- | --- |
| What did the learner actually do? | Two original practice attempts with their individual outcomes, one recognized orientation equivalent and a dated reviewer decision. Any correction preserves its predecessor. |
| What was issued? | The learning award and register certificate each have their own authority, serial or issue number, historical wording and current validation status. An unchanged reprint does not increase the count of distinct issues. |
| What did each church perform? | A's two locally confirmed entries, its distinct external attestation and any reviewed correction are separable. B has no local register action from its teaching path. |
| Who can inspect supporting evidence? | Registrar sees the authorized preparation outcome. Teacher sees learning evidence under current teaching scope. Neither inherits the other's private evidence or the rights of the subject. |

[Learning and formation](../../ministry/learning.md) · [Local register and certificate rules](../../people/rites-and-milestones.md) · [Ceremony administration](../../administration/life-events.md) · [Membership decision fields](../../implementation/people/MembershipDecision.md)
