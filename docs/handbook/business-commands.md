# Commands, outcomes and ownership at department boundaries

A command asks the business owner to do something. A receipt records the decision actually made. An event reports a committed fact to another owner. Keep these meanings distinct in a web form, staff workstation, file import or external integration. This chapter gives a common contract; a church can choose its transport and storage technology.

## Common request and receipt

| Request element | Meaning and validation |
| --- | --- |
| operation | Stable business verb with a versioned meaning, such as accepting a membership application or recording a returned stock item. A generic field edit cannot imply an approval or posting. |
| organization and acting scope | Identify the controlling church, any congregation/campus and the authorized actor or service. A supplied identifier alone cannot establish authority. |
| subject and target | Name the person or record affected and the target revision when it exists. Distinguish the person acting, the subject of the work, the counterparty, and any approved representative. |
| operation key and material inputs | Scope the key to the originating application, church and action. Define which fields materially alter amount, authority, dates, beneficiary, destination or purpose. |
| effective time and submitted time | Preserve an explicitly backdated or future-effective event and when it was recorded. Use the approved time zone for civil deadlines. |
| input proof | Identify supporting evidence, approved policy edition, required signatures or prior decision. A document reference indicates where to verify evidence, not that it was accepted. |
| response route | Identify the permitted recipient for the receipt and subsequent updates. Sensitive case details and private names are never broadcast just because the event affected a group. |

Return an owner receipt with the requested or assigned record identifier, accepted revision, result, effect or absence of effect, safe explanation, timestamp at the appropriate resolution and relevant next review route. If the source disallows individual linkage, issue evidence of the administrative action separately from protected content. In particular a secret ballot cannot include a voter-account key, fine-grained cast time or a linkable command receipt on the ballot.

| Result | What the operator can rely on | Permitted next action |
| --- | --- | --- |
| Accepted | The named owner committed the specified effect and can reproduce its receipt. | Read the resulting record; follow any separately pending handoffs. |
| Accepted for review | A request or waiting item exists. Membership, payment, publication or other final authority is still outstanding. | Supply evidence, withdraw where allowed, or await the named reviewer. |
| Already applied | Identical material inputs matched the accepted operation in scope. | Return the same effect identity. No second delivery, posting or allocation. |
| Conflict | Expected revision is stale or an existing operation key was reused with different material inputs. | Inspect the permitted difference and submit a properly authorized new operation or correction. |
| Ineligible or insufficient capacity | A real business rule failed at the decision point. | Return an authorized explanation or safe alternative; preserve remaining capacity and balances. |
| Unavailable to caller | Actor, scope, purpose, representation or field visibility failed. | Return only a safe explanation that does not disclose a secret record’s existence. |
| External outcome unknown | External execution may have occurred and the acknowledgement is missing. | Reconcile against the existing external operation. Block a second independent money movement or entitlement grant. |
| Superseded or reversed | A new accepted decision adjusts or replaces a prior one. | Preserve the original, link the correction, and inform downstream owners of the changed disposition. |

## Business action contracts

| Action and owner | Minimum material inputs | Accepted effects | A rejection that must preserve existing state |
| --- | --- | --- | --- |
| Accept admission — registrar | Application, person, congregation, class, decision date, effective date, authority, prior revision | One MembershipDecision and the applicable MembershipPeriod. Report eligibility can recompute from the effective date. | Shared family surname or existing directory account without a membership decision cannot add a person to the roll. |
| Verify representation — authorized custodian | Actor person, subject person, allowed action, scope, evidence, validity and review authority | One dated RepresentationAuthority. Account-access projections can refresh. | A family relationship or emergency contact on its own cannot grant collection or financial access. |
| Allocate a place with fee evidence — admissions | RegistrationPlace, event, hold, scoped provider notice, component, amount, currency and revision | One AdmissionPaymentNotice links the external fact to the requested place. The admissions owner confirms only if capacity and eligibility still hold. | A late notice after the hold expires prompts a review. A returned payment cannot evict an unrelated person. |
| Complete child handover — supervising team | Check-in, current supervised location, verified collector, current action-specific authority and required witness/evidence | One accepted transfer of custody and updated reconciliation of outstanding children. | Conflicting authority or obsolete collection credential leaves the child supervised and escalates privately. |
| Confirm minutes — authorized meeting body | Exact minute edition, quorum/procedural basis where applicable, required attestation, publication audiences | One confirmed MinuteEdition, approved internal or public renditions and linked resolutions/actions. | A later clerical correction cannot overwrite the confirmed wording or infer a second vote. |
| Authorize outgoing notice — communication owner | Purpose, template edition, sender, intended scope, channel bindings, schedule, approval and snapshot | One DispatchRequest with permitted recipients, independent deliveries and at-send suppression checks. | Withdrawing consent before dispatch prevents an optional delivery even if the person was in an earlier snapshot. |
| Accept gift — giving owner | Giving party or approved anonymous classification, instrument/capture reference, date, currency, gross value, allocations and required evidence | One Gift, its GiftAllocation rows, any approved statement eligibility and one defined finance handoff. | A voluntary gift in a mixed checkout cannot be booked again when its payment processor later settles. |
| Send giving facts — authorized exchange owner | Approved giving revision, exact designation and amount, currency, effective date, destination and mapping | One traceable FinanceExchangeItem; track sent, accepted, exception and any subsequent correction. An external reference identifies the accounting outcome. | A disabled or mismatched route leaves the gift and its pending handoff visible. An acknowledgement for another church cannot close it. |
| Request correction of an event fee — event desk | Original external receipt and affected place, currency and amount, approval and correction key | A pending request while the provider assesses the refund; a later receipt reconciles the named component. | A repeated confirmation cannot refund an independent gift or release the second seat. |
| Withdraw a media release — church publisher | Affected release, speaker permission or rights decision, approved editions, effective instant and authorized audience | Mark the church release withdrawn, suppress its listings and ask each delivery destination for confirmation. | A failed downstream recall remains assigned; the public view cannot continue offering a withdrawn edition. |
| Approve aid fulfilment — authorized case and execution owners | AidAward, instalment, payee or item/units, fund, expiry, independent approval, execution key | One authorized AidFulfillment and one accepted stock or finance effect. | A sensitive beneficiary narrative is excluded from the vendor payment or donor impact report. |
| Issue protected record — archive issuer | Source record and edition, requester authority, permitted fields/pages, recipient and purpose | One DocumentIssue bound to the exact permitted extract and its serial. Preserve custody and revocation evidence. | A second print of one issued copy cannot acquire independent authority or a new serial accidentally. |

## Handoff reconciliation

For a provider receipt of 45 with seats priced 30 and 10 plus a gift of 5, admissions sees the two places and giving sees 5. A refund of the 10 component leaves a net provider movement of 35 and the adult place intact. Accounting may confirm the church handoff before or after a courtesy notice. Match each receipt to its own component, recipient and status. A missing response remains pending until investigated.

A daily exception list should show source operations without accepted receiver receipts, receiver entries without matching authorized sources, and components whose totals cannot reconcile. Show age, owner, safe discrepancy classification and next action. A person investigating duplicated bank movement must not automatically receive care-case or guardian information because the original order also involved a family.

[Worked journeys](../verification/journeys.md) · [Field specifications](../implementation/README.md) · [Handbook](README.md)
