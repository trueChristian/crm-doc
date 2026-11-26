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
| Allocate paid place — admissions | RegistrationPlace, event occurrence, order line/unit, applicable hold, accepted tender component and amount, decision revision | One place changes to its eligible admission state with an AdmissionSaleUnit and traceable matching reference. | A late payment against a sold-out expired hold needs disposition; never overbook or create another capture. |
| Complete child handover — supervising team | Check-in, current supervised location, verified collector, current action-specific authority and required witness/evidence | One accepted transfer of custody and updated reconciliation of outstanding children. | Conflicting authority or obsolete collection credential leaves the child supervised and escalates privately. |
| Confirm minutes — authorized meeting body | Exact minute edition, quorum/procedural basis where applicable, required attestation, publication audiences | One confirmed MinuteEdition, approved internal or public renditions and linked resolutions/actions. | A later clerical correction cannot overwrite the confirmed wording or infer a second vote. |
| Authorize outgoing notice — communication owner | Purpose, template edition, sender, intended scope, channel bindings, schedule, approval and snapshot | One DispatchRequest with permitted recipients, independent deliveries and at-send suppression checks. | Withdrawing consent before dispatch prevents an optional delivery even if the person was in an earlier snapshot. |
| Accept gift — giving owner | Giving party or approved anonymous classification, instrument/capture reference, date, currency, gross value, allocations and required evidence | One Gift, its GiftAllocation rows, any approved statement eligibility and one defined finance handoff. | A voluntary gift in a mixed checkout cannot be booked again when its payment processor later settles. |
| Post journal — finance book owner | Book, open/authorized period, source/purpose, currency basis, debit/credit lines, funds, dimensions and approval | One numbered posted JournalEntry with balanced JournalLine rows. Affected balances reconcile to the same effective cutoff. | Unbalanced entry, expired signing authority or forbidden closed-period write produces no posted lines. |
| Refund one order component — commercial and finance owners | Original captured component, currency, original allocation, remaining refundable amount, reason, approval and provider execution identity | A commercial credit or refund payable, then clearing only on confirmed provider execution under the selected posting rule. | Repeated provider confirmation cannot refund a donation or unrelated second ticket. |
| Revoke paid media access — media owner | AccessGrant or affected release, reason, effective instant, current rights edition, allowed replacement/refund route | Re-evaluate playback, download and preview rights under the agreed terms. Identify affected purchases for commercial review. | Revoking media rights cannot erase the original sale or silently post a cash refund. |
| Approve aid fulfilment — authorized case and execution owners | AidAward, instalment, payee or item/units, fund, expiry, independent approval, execution key | One authorized AidFulfillment and one accepted stock or finance effect. | A sensitive beneficiary narrative is excluded from the vendor payment or donor impact report. |
| Issue protected record — archive issuer | Source record and edition, requester authority, permitted fields/pages, recipient and purpose | One DocumentIssue bound to the exact permitted extract and its serial. Preserve custody and revocation evidence. | A second print of one issued copy cannot acquire independent authority or a new serial accidentally. |

## Handoff reconciliation

For a mixed sale of 45 with seats priced 30 and 10 plus an unrestricted gift of 5, a successful capture carries one shared source identity. Admissions sees the two priced places. Giving sees the gift of 5. Finance either posts the complete collection or receives split instructions under one named cash owner. Across those paths, the cash effect totals 45 once. Refunding just the 10 component leaves 35 net cash in this no-fee illustration; gift remains 5 and the 30 seat remains valid. A duplicate receipt or a failure to dispatch a courtesy notice leaves those financial and admission facts unchanged.

A daily exception list should show source operations without accepted receiver receipts, receiver entries without matching authorized sources, and components whose totals cannot reconcile. Show age, owner, safe discrepancy classification and next action. A person investigating duplicated bank movement must not automatically receive care-case or guardian information because the original order also involved a family.

[Worked journeys](../verification/journeys.md) · [Field specifications](../implementation/README.md) · [Handbook](README.md)
