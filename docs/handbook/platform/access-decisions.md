# Decide exactly who may see or change a record

Use this manual to implement or review the authorization result for a single request. The [account dictionary](../../platform/identity-access.md) owns identities, roles and evaluated grants. The [people register](../../people/households-and-authority.md) owns verified authority over another person. A grant may permit representing a child for registration without permitting pickup, donor access, profile publication or access to siblings.

## Inputs the caller must supply or the service must resolve

| Input | Resolution rule | Failure outcome |
|---|---|---|
| Caller and operative organization | Resolve signed-in UserAccount, public visitor, kiosk operator or IntegrationPrincipal, plus assurance and live session. A submitted person identifier is never proof of identity. | Private entry points return a neutral unavailable response. Discard any retained context after an organization switch. |
| Beneficiary and represented subject | Record the real actor and the person whose affairs they are acting on. Obtain the exact RepresentationAuthority, qualifying action, activity, effective time and latest restrictions. | Route an expired or ambiguous claim to an authorized reviewer. Provide a safe generic reason to the caller. |
| Resource path | Resolve the actual record, field classification and authoritative parents. Determine whether the grant is scoped to organization, campus, group, self, a case or one transaction. | A hidden parent cannot be bypassed through a file, guessed record identifier, report or derived copy. |
| Operation and purpose | Distinguish discover/read/print/share/download/edit/review/approve/execute. Open a child record only under its own permitted purpose and parent path. | Reading a report does not confer the ability to send it or export its underlying detail. |
| Time and established state | Use the service decision instant, active policy edition and current authority revision. A dated report's as-of date selects business facts only. | Access formerly held at a historical date cannot be used to read a historical report today. |
| Obligations | Define masking, suppression, independent approval, justification, freshness, step-up verification, logging and residue expiry. | Return an obligation such as “verify again” only if revealing it is permitted. Retain no prohibited data while waiting. |

## Evaluation sequence

1. Capture one request context and a correlation reference. Identify the actor class, requested activity, fields and purpose. Reject mixed-organization batches before recording any business mutation. Business input never designates the request's own privileges.
2. Revalidate account and authoritative resource scope. Resolve independent grants applicable to this action. A secretary who is also a member may use self-service under the self grant even after a secretary grant expires.
3. Compute the intersection of permitted fields, purpose, scope, active representation and non-overrideable restrictions for the relevant actor pathway. Multiple positive grants can authorize different actions. They cannot be spliced to turn a camp registration right for one child and a pickup right for another into pickup of both. An active prohibition or missing required proof prevents the action.
4. Return an allow decision with a field mask, required evidence and expiry, or a protected rejection. A collection may omit unauthorised records and fields. A command that requests an unauthorized field fails as a unit. Distinguish a legitimate empty collection from an unavailable record without revealing its existence.
5. At every irreversible effect, compare the decision inputs with live account, source and purpose revisions. A queued dispatch, export, approval, refund or download is its own effect. Reauthorize the worker's execution authority and requested beneficiary's rights as applicable. Never adopt privileges from the staff account that enqueued a job.
6. Persist a minimal audit entry. Authorized investigators can see the controlling policy edition, actor, represented subject and outcome. The client, metrics and support logs receive a neutral disposition and correlation reference. Specially protected activities such as anonymous balloting use aggregate diagnostics that cannot relink votes.

## Worked eligibility trace

Two households share a phone. On 12 August, adult Mara has a verified guardian mandate for child Tali, permitting registration for the Lakeside class until 10:30 local. An independent person named Ayo holds a collection mandate from 10:00. At 10:15 a safeguarding officer activates a restriction on Ayo's collection. Class leader Nele has a Lakeside roster grant. A regional coordinator has a network reporting grant for aggregate attendance. Each person is in a different authenticated session.

| Request | Result and evidence | Effect elsewhere |
|---|---|---|
| 10:12 Mara registers Tali; the form omits unrelated fields | Allow a single registration. Record Mara as actor, Tali as subject, the authority edition and occurrence. | Attendance is still unobserved and no collection right is created. |
| 10:14 Ayo asks to view Tali's home address | Deny; the collection mandate does not confer profile access. | No suggestion, error title or contact preview shows the address. |
| 10:16 Ayo presents an earlier collection credential | Keep custody active and give staff the designated referral instruction. The current restriction supersedes prior evidence. | The volunteer sees no safeguarding case content. |
| 10:30 Mara begins another registration | The half-open mandate expired at 10:30. No new place is created. | Prior authorized registration retains its attribution and is not silently withdrawn. |
| Nele prints the roster and selects donor balances | The roster can be requested alone with its own permitted fields. Reject the mixed private-field print command. | No partly generated attachment remains downloadable. |
| The coordinator requests totals for a small class | Apply membership of that reporting population, then suppression on the aggregate. | Disallow underlying names, small-group complements and sensitive drill-down. |

## Public projection review

Separate fields used in an approved public edition from a private master. Publish only approved field values and a specific edition. Default an unpublished draft, withdrawn notice or expired release to undiscoverable. Re-evaluate at every public surface, including open graphs or previews, shared calendars, feeds, indexes, translated pages and file delivery. A public sermon may expose the public speaker name and date but the corresponding internal planning note, beneficiary addresses, draft transcript and source video each require separate review.

If a thumbnail was public at 09:00 and withdrawn at 11:00, stop new retrieval, invalidate controlled caches and record purge acknowledgements. Preserve earlier distribution evidence and contact the responsible editor about external copies when appropriate. A past download or printed handout has an independent custody history. An observer visiting a revoked link should receive the same neutral result as visiting an undiscoverable item.

## Release checks

Evaluate the full matrix of organization, account status, represented subject, operation, selected fields, execution time and access path. For every positive verdict record at least one neighboring negative case, for example the same actor and another child, the same file via a public preview or an action one instant after expiry. Run the cases against detail, search, bulk, export, attachment, support view and queued execution. An acceptance run passes when all surfaces produce their documented outcomes and the evidence identifies which policy controlled each decision.
