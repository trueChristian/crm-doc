# GroupMeeting

The coordinator connects an occurrence with the term whose roster is invited. A person's presence, a seat claim, a role on the rota and a child handover each have their own records. Several classes may use one shared occurrence. A recurring series may span terms with different rosters.

## Field inventory

| Field | Logical declaration | Owner rule |
| --- | --- | --- |
| `term_id` | → GroupTerm | Resolve the particular group term in this church. Link the term explicitly even if the series usually serves the same group. |
| `occurrence_id` | → EventOccurrence | Resolve a dated occurrence in the authorized church scope. A move preserves this identity. A cancelled meeting keeps its decision history. |
| `roster_purpose` | code | Record whether the term supplies an expected attendance roll or only an invitation audience. An invitation-only roster does not contribute to the expected-person denominator. |
| `state` | code | Proposed, confirmed or withdrawn. Only confirmed links contribute to the authorized roster. Record the operator, review and revision through the shared envelope. |

Enforce uniqueness of term and occurrence within an organization. Reconfirming a withdrawn link requires the responsible coordinator's explicit decision. The same occurrence may link to several terms, with no cross-roster permission implied. If a meeting is moved outside term bounds, flag the affected links, obtain a local decision about the invited cohort, and withdraw or confirm before distributing the revised roll. Preserve previous dates and decisions.

| Fixture | Required outcome |
| --- | --- |
| Term A has 12 expected participants, term B has 8, and 2 people belong to both. All are active and shareable for this gathering. | The permitted combined roster has 18 distinct people. A shared person occupies one place and can contribute one named attendance observation for the occurrence. |
| A 19th person is invited as a visitor and has no term participation. | Record the visitor registration or actual visit under the event's policy. The two term rolls remain accurate. |
| Two confidential groups share a room and one group leader asks for the whole attendance export. | Scope the export to what this leader is authorized to see. The designated steward sees only the safety information needed for the shared session. |
| A volunteer adds a second meeting link for term A after losing the response. | Return the existing link for an identical repeat. A changed purpose needs an authorized revision and keeps the original roster issue traceable. |

[Group terms](GroupTerm.md) · [Occurrences](EventOccurrence.md) · [Group operations](../../ministry/groups.md) · [Named attendance](AttendanceRecord.md)
