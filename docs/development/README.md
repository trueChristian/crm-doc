# Fundraising, partnerships and donor service

A fundraising team can invite support, apply for funding, care for existing supporters and report the results of a church project. This area owns the invitation, documented permissions, commitments to supporters and evidence of delivery. The church giving desk verifies gifts and issues permitted acknowledgements. An independent accounting service owns financial recognition and any formal receipt assigned to it under local policy. Providing assistance or access to pastoral care never depends on becoming a donor.

| Task | Where to start | Accountable person |
| --- | --- | --- |
| Launch an appeal, link its messages to gifts and explain progress against a target | [Appeals and attribution](appeals.md) | Development lead and finance reviewer |
| Honour a preference, acknowledge a tribute or follow up a matching gift or bequest | [Donor service and gift acceptance](donor-service.md) | Relationship steward and gift acceptance committee |
| Prepare a grant application and submit the sponsor's progress or final report | [Grant applications and reporting](grant-applications.md) | Grant coordinator and authorized signatory |
| Agree what a partner, sponsor and church will deliver, and release verified results | [Partnerships, sponsorships and impact](partnerships.md) | Partnership manager and programme lead |

## Sources for supporter and sponsor reporting

| Records of authority | How development uses them |
| --- | --- |
| GivingParty, Gift, GiftAllocation, GiftAttribution | One verified transaction per receipt. Attribution and volunteer credit can describe influence without changing the legal donor or increasing actual income. |
| Pledge, PledgeInstallment, InKindGift, GivingDocument | Link accepted promises, received goods and authorized receipt or statement. An expression of interest, intention to leave a legacy, draft offer or thank-you message cannot generate an official receipt. |
| GrantAward, AwardMilestone, FundRestriction | The CRM keeps signed awards, due obligations and donor terms. Accounting supplies approved cost evidence, draw and payment references or a dated aggregate. The sponsor report records the source and edition authorized for its audience. |
| Ministry MinistryPartner, MissionProject, ProjectPartnerRole, ProjectMilestone, ProjectOutcome, EventOccurrence | Use the existing programme, partner, role, event and outcome. Share approved summaries under the partner agreement. |
| Communications Campaign, AudienceSnapshot, ContactDecision, DispatchRequest, Delivery | Communications applies purpose, channel, consent and suppression to each recipient at dispatch. Development records the purpose, invitation and disposition. |

All records have an opaque primary key and inherit one organization from an explicit parent or carry `organization_id`. Organization, identity, role and disclosure permissions must agree across a link. Fields marked `?` are optional. A named reference targets one record, permitting many children unless a uniqueness constraint says otherwise. Currency amounts are exact in the stated currency. A period specifies both boundaries and the church's reporting zone. An instant is an absolute point in time. Each revision, authorization, reversal and release preserves actor, time, organization, reason and prior state.

An accountable steward needs a queue showing promised action, contact permissions, deadline and assigned colleague. A treasurer needs a list of unreconciled allocation links and accepted restrictions. Ministry leads need approved goals and evidence due. Supporters should be able to request anonymity, change contact preferences or correct an attribution through a safe channel. Aggregate reports for a public meeting disclose only approved totals and a dated reporting basis. Forecast asks, pledged support, cash, recognized gifts, donated property, benefit income and influence credit each have their own measures.

The [giving and stewardship specification](../finance/README.md) defines the relationship register and the [accounting exchange](../finance/accounting-exchange.md) covers delivery and acknowledgements. For background on separately identified organizations, contacts and follow-up ownership, see the [Dolibarr parties and contacts specification](https://github.com/vast-development-method/dolibarr-doc/blob/main/docs/sales/parties-and-contacts.md) and [ERPNext customer relationships specification](https://github.com/vast-development-method/erpnext-doc/blob/main/docs/people-and-services/customer-relationships-and-sales.md). Church supporter workflows use the purpose and contact permission the person granted. Commercial lead scores, projected sales and purchase history play no part in pastoral care or membership decisions.
