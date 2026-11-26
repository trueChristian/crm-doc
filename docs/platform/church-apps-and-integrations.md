# Church apps, the API and MCP

A church can publish its service calendar on a website, build its own member app, accept an update from an existing system and authorize a staff assistant to perform church work. The public API is a product requirement for all four uses. The Model Context Protocol (MCP) makes approved church operations discoverable and callable by authorized tools. JCB is the intended delivery mechanism for these interfaces. This specification defines observable church behavior and leaves route names, tool identifiers, storage and component layout to implementation.

## Surfaces a church can enable

| Caller | Identity and scope | Examples of allowed work | Evidence returned |
| --- | --- | --- | --- |
| Public website or calendar | Anonymous reader of a church's published projection, or a connection with that same narrow scope | Read published services, accessible public venues, cancellations and registration windows. Submit an invitation response through an explicitly opened intake form. | Public edition, occurrence key, time zone, withdrawal or a private submission receipt. Public searches and counts cover published records only. |
| Member or guardian using a church-branded mobile or web app | Signed-in individual with the current self-service or representation grant for this church and activity | Read own household view, propose contact changes, update channel choices, register a named participant, accept a volunteer assignment or withdraw. | Per-operation result, authorized fields, change revision, review status and instructions for correcting a refusal. Members can inspect a pending submission after reconnecting. |
| Ministry worker or approved service | Named worker with scoped appointment or a dedicated connection linked to a custodian and purpose | Manage the assigned group's roster, submit attendance at one occurrence, request facilities availability or reconcile a returned delivery. | Scoped roster or status, origin, actor, action receipt and any conflict assigned to the record owner. |
| Staff assistant using MCP | Authenticated client acting for an identifiable worker, or an expressly authorized service acting in its own name | Discover permitted operations, find a published service, read the caller's open follow-up tasks, draft an announcement or submit an authorized roster change. | A structured outcome with the same source revision and authorization checks as the API. Draft, pending approval and committed have distinct meanings. |
| Partner service sending data to the church | Separate connection per church, external system, purpose and environment | Offer guest intake, registration, delivery outcomes, giving acknowledgements or qualification evidence under the church's published inbound contract. | Per-item accepted, pending, rejected or conflicted result. The partner can reconcile its own submission using the agreed operation key. |

A native app uses a delegated member or staff session. Never embed a privileged church connection credential in an app distributed to members. Bind the initiating account, client and represented subject separately. On each request apply the intersection of client grants, actor powers, current organization and ministry scope, field permissions, purpose and representation. Evaluate cached views, collection totals, attachments, event subscriptions, result polling and export downloads under that same authority. Provide a session exit that clears private local views on a shared device. The [offline rules](offline-continuity.md) govern information that may be retained during a service outage.

Publish a machine-readable description of supported reads, commands and event editions alongside human examples. State which product capabilities and scopes each operation requires and which operations the church enabled. For each enabled member-facing workflow document the API path through the whole task, including permissible choices, validation, review, status lookup and withdrawal or correction. Clients must be able to distinguish disabled capabilities, permission-safe denials, validation failures, stale revisions and temporary outages. An unsupported operation is absent or explicitly unavailable. The discovery response itself must protect private ministries, people and operational configuration.

## Exchange ownership and minimum payloads

A church enables only the connections it uses. Each row names an independently testable boundary. Confirm the sending and receiving owners, field map, permitted audience, event trigger and correction route before enabling a connection. The examples use business keys scoped to the participating churches and providers.

| Connection and church trigger | Outbound from CRM | Inbound to CRM | Who decides and how discrepancies close |
| --- | --- | --- | --- |
| Website, public kiosk and calendar after service publication | Public event occurrence, edition, public venue, time zone and availability | Intake request or registration, including the consent response when the form asks for it | Ministry owns publication and seats. Cancellation withdraws the public item. An external calendar edit is a proposal under an authorized scheduling connection. |
| Identity provider and church directory after sign-in or a directory change | Approved account linkage and permitted directory projection | Verified issuer and stable subject, or a proposed field change with source revision | Account custodian verifies linkage. Reassigned email, shared devices or a reused display name never grant access to a household. A revoked grant invalidates private projections. |
| Groups, facilities, check-in and volunteer scheduling | Authorized occurrence, available place, approved roster subset, service assignment or booking edition | Presence observation, serving response, room reservation request or conflict | The occurrence owner resolves duplicate arrivals and available places. A device's roster cannot authorize child release or override a newer safety decision. |
| Email, SMS, push, print or telephony following a church-approved contact | Delivery key, permitted destination, language, approved content and purpose | Acceptance, delivery result, reply, verified opt-out or invalid destination | Communications owns consent and the approved audience. A delivery failure updates the endpoint for review. An opt-out suppresses the relevant future delivery, including queued work. |
| Payments, giving and the church's existing accounting provider | Approved designation, source item and revision, currency, amount, allocation and correction reference as applicable | Processor result, external posting acknowledgement, refusal, reversal or reconciliation reference | The church owns gifts, acknowledgements to donors and registration effects. The processor owns capture status. The [admission payment notice](../implementation/ministry/AdmissionPaymentNotice.md) ties funding and refunds to the actual place. The accounting provider owns books and financial close. The treasurer resolves unsupported mappings or amount differences without resending a charge. |
| Separate learning manager after a member or volunteer accepts a referral | Approved referral key, permitted participant identifier and offering reference. A separate grant may send dated attendance for a named person and occurrence. | Dated completion or qualification evidence, external reference, expiry, replacement or withdrawal | The learning manager owns delivery and evaluation. The ministry custodian decides eligibility for a role from evidence plus current local permissions. A completion cannot approve a volunteer or admit a person to membership. |
| Worship planning, sermon media and livestream publishing | Approved service outline, participants' public display choices, channel and publication window | Recording reference, availability, caption or rights status and takedown acknowledgement | Worship or media custodian approves publication. Expired permission withdraws affected media or sends a correction to the distributor. Protect unpublished testimony and pastoral material. |
| Safeguarding screening or an authorized care referral | Approved case or referral reference, recipient, permitted fields and contact method | Status, verification date, issuer, expiry, referral acceptance or callback request | The designated church custodian reviews outcomes. General staff see the permitted eligibility or referral state. Detailed provider reports and pastoral narratives need separate explicit access. |
| Stock, lending, merchandise, staffing and specialist office systems | Approved church request, event or ministry reference, service date and permitted contact | Availability, confirmed provision, return, exception or staff-appointment evidence | Church staff own the ministry need and accountable handover. The specialist system owns its stock valuation, payroll or employment processing as applicable. |
| Network reports, joint ministries, charities or mission partners | Authorized aggregates, a purpose-limited joint roster or a referral allowed by both organizations | Receipt, correction, withdrawal or agreed distribution outcome | Each church retains local identity and authority. Use the [organization sharing agreement](organization-lifecycle.md) and reconcile corrections and expiry separately at each recipient. |
| Documents, signatures and archive services | Approved document edition or signing request, permitted signer and expiry | Signed edition reference, verification or refusal, archival proof or retrieval failure | The secretary checks edition, signer and authority before marking an act complete. Replacement content requires a new edition. A provider's delivery receipt cannot adopt minutes or issue a certificate. |

## Creating and updating church records from another system

1. Commission the connection for a bounded church purpose. Document stable external namespaces, editable fields, review-only fields, source clocks, explicit clearing, duplicate policy, service limits and which party may settle each disagreement. Separate sandbox and live connections. A sender cannot choose a different church by changing a field in a request.
2. Obtain authorized reference data or a scoped snapshot. Opaque external keys remain stable across a person's name and address changes. An ambiguous match enters the steward's queue. Reuse the [migration crosswalk](migration-data-quality.md) for known identities. Lookups and refusals must preserve confidentiality.
3. Submit a command carrying the contract edition, stable sender operation key, source object and revision where applicable, effective time and the minimum proposed fields. For edits carry the last CRM revision observed when the contract requires it. Retain missing, unknown and explicitly cleared values as distinct inputs. Enforce field ownership before applying a mutation. Publish atomicity per operation. For batch intake, return each unit's receipt, allowing a named dependent unit to remain pending without repeating committed siblings.
4. Recheck rights and business rules at commit. Unmatched identities, formal membership changes and protected fields follow the custodian's review policy. A committed attendance observation provides no permission to change an address. Atomically record the accepted mutation, replay identity and durable event intent. Retransmission with identical content returns its original business outcome to a still-authorized caller. A reused key with a different meaning returns a conflict.
5. Distinguish transport acceptance from domain completion. Expose authorized status lookup and publish only the fields a subscriber may read. An approver's later decision has its own actor, timestamp, revision and reason. Restrict access to sensitive reasons even when the submitter may learn the request's status. For divergent revisions send the caller to an authorized refreshed view or a steward. A correction supersedes the source change and propagates to eligible recipients.
6. Define supported contract editions, paging limits, retry timing and replay horizon for each connection. Document how to resume after service throttling, how terminal errors reach a custodian, and how to acquire a fresh authorized snapshot after a checkpoint expires. Preserve per-subscriber delivery receipts, outstanding reviews and a bounded replay procedure through upgrades. Administrative monitoring shows counts, oldest pending age, reason classes and last successful reconciliation. Restrict payload access to the owning ministry.

### Example inbound proposal and its response

In this example the welcome desk has verified that source visitor V-014 corresponds to a North church record. The website may propose a preferred name. The registrar owns the decision. The installed API supplies the concrete route and published schema. These illustrative values describe the business exchange.

```json
{
  "contract": "visitor-contact-proposal",
  "edition": 1,
  "operationKey": "form-7789",
  "sourcePerson": "V-014",
  "expectedRevision": 6,
  "effectiveAt": "2027-04-20T09:40:00Z",
  "changes": { "preferredName": "Jo" }
}
```

The connection establishes the source namespace and church. The server derives the acting principal from the authenticated request. It canonicalizes and checks the permitted change, reserves the operation key, associates the existing crosswalk, records the proposal and returns its receipt. This contract uses an all-or-nothing proposal and treats an omitted field as untouched. Clearing a field requires an explicit permitted change. The website cannot write a membership decision, select a different household or provide its own approval.

```json
{
  "receipt": "north-receipt-220",
  "operationKey": "form-7789",
  "state": "awaiting_review",
  "submittedAgainstRevision": 6
}
```

Polling the receipt under the same connection while review is pending returns that state with no private review notes. If a member has already edited the same field at revision 7, approval against revision 6 produces a conflict for the steward. The steward can close the stale proposal, or initiate a separately reviewed change against the current edition. On acceptance record the new church revision and actor. A retry after acceptance retrieves the existing receipt and current disposition, subject to present access. A renamed visitor, change of website vendor or duplicate notification cannot create a second person from this proposal.

## MCP operations and review

Describe each exposed tool with its church purpose, inputs and their meaning, required role, write effect, result shape and possible review state. Descriptions use stable business operation names shared with the API. A facility search, proposal to change a facility booking, and approval of the amended booking are distinct actions. Inspecting the tools catalogue or previewing a change is read-only. Structured results can include a permitted record reference, owner, edition, operation receipt and status. Free-text names are display data. Ambiguous references require clarification before a write.

Evaluate permissions again at execution, even after successful discovery. Bind an approval to the exact target and proposed edition, recheck it when applying the change, and present only information the reviewer may inspect. Reuse operation keys across API and MCP retries under the same authorized client identity and business command. Record how the operation was invoked and the real actor. A restricted case, attachment or hidden count must remain inaccessible by direct call, resource lookup, search, batch, error detail and cached output. Treat instructions embedded in retrieved content as data.

A church can enable a read-only assistant while permitting the same staff member to work through a separately authorized UI. Disable a client by revoking its own grant. Pending writes have their authority rechecked before commit. Keep completed church records and their audit evidence under the relevant custodian. Use the [assistance rules](assisted-intelligence.md) for sensitive decisions, drafting and evidence review.

## Commission, replace and retire a connection

Name the church custodian, provider contact, authorized scopes, support window and maximum acceptable delay for each business flow. Rehearse one valid event, one refused field, a repeated submission, a withdrawal and an outage using synthetic records. Compare source count, accepted count, queued review, rejections, unapplied changes and final state. Agree how staff continue the church task while the external provider is unavailable. For completed real-world actions keep the source proof and assign uncertain results to a named person before any resend.

At switchover record the final accepted source position, pending receipts and any overlap between old and new identifiers. Run read-only comparisons before designating one active writer per field or effect. Reconcile outstanding handoffs, revoke retired credentials and subscriptions, dispose of temporary copies under the agreed policy and retain the field mapping needed to interpret old references. Closing a connector must leave independent membership, services, calendars and attendance available.

The [app and MCP commissioning run](../acceptance/platform/app-and-mcp.md) exercises delegated reads and writes. The [subscriber cutover run](../acceptance/platform/exchange-cutover.md) exercises change feeds. The [exchange contract](exchange-events.md) defines their common records.

## Reference designs

| Reference | How to use it in a church implementation |
| --- | --- |
| [ERPNext integration services](https://github.com/vast-development-method/erpnext-doc/blob/61a1196824f8df82127627d475599266244b71ce/docs/services/external-integrations.md) | Compare source identity, callback state and reconciliation rules for inbound activity and delivery receipts. A visitor inquiry goes to the designated welcome team under its approved contact purpose. |
| [Dolibarr outbound targets](https://github.com/vast-development-method/dolibarr-doc/blob/640ff739840dca25015a704300b2e78ee7269656/docs/services/webhook.md) | Check separation between configuring an event destination, listing it and receiving an event. The church specifies an explicit purpose and allowed fields for each recipient. |
| [Odoo external integration contracts](https://github.com/vast-development-method/odoo-doc/blob/81a0c3fc2eb11fb7194a72e7bb537d395b9e46a0/docs/interfaces/external-integrations.md) | Use the contract categories to document direction, triggers, proof, failures, replay and records for the church's chosen provider. |
| [ChristianLight learning manager](https://github.com/ChristianLight/lms-doc) | Refer to the separate product for curriculum, assessment and learning delivery. The [church programme rules](../ministry/learning.md) govern referrals, separately authorized attendance observations and qualification evidence. An observation of presence carries no academic result. |
