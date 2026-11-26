# People and pastoral records

Start with the question the church needs to answer. A register entry, a place in a household, a ministry assignment, permission to act for another person and a sign-in are independent facts. A guest can be known by name without having any of the other four. A church may use its own terms while retaining these distinctions.

## Find a workflow

| Task | Responsible role | Specification |
|---|---|---|
| Record someone by one name, correct a partial birthday or resolve duplicate people | Registrar or data steward | [Personal register and identity resolution](personal-register.md) |
| Link siblings, move a family, record shared residence or check a pickup authority | Registrar and designated verifier | [Households, kinship and delegated authority](households-and-authority.md) |
| Admit, transfer or restore a member, or certify the roll at a past date | Membership clerk and authorizing body | [Membership, transfers and certified rolls](membership-and-rolls.md) |
| Determine whether someone is a guest, regular attender or member of another congregation, or record formation milestones | Registrar, ministry leader and member | [Participation categories and personal milestones](participation-and-personal-milestones.md) |
| Record a baptism, dedication, marriage, burial or other rite and issue a corrected certificate | Minister, registrar or archivist | [Rites, milestones and register books](rites-and-milestones.md) |
| Invite a member, verify a delegate, update a household contact or publish a directory | Member, approved delegate and directory editor | [Directory publication and member self-service](directory-and-self-service.md) |
| Welcome a visitor, hand over a request or stop a follow-up | Welcome coordinator and assigned worker | [Visitors, outreach and follow-up](visitors-and-follow-up.md) |
| Arrange a pastoral visit or distribute an approved prayer request | Assigned care coordinator | [Pastoral care, prayer and continuity](pastoral-care.md) |
| Receive a concern, restrict an activity or make a protected disclosure | Designated safeguarding lead or independent alternate | [Safeguarding concerns and protected disclosure](safeguarding-and-disclosure.md) |
| Approve food, vouchers or financial assistance and reconcile delivery | Welfare assessor, independent approver and treasury | [Benevolence and community aid](benevolence-and-community-aid.md) |

## Reading the data definitions

Each row declares a logical record, its fields and its integrity rules. ID is a stable identifier, “→” names the referenced record, “?” means optional, and other scalar fields are required unless the row describes a conditional exception. A bare cross-domain reference is an identifier owned and validated by the organization or service named in its description. A code references an allowed, versioned vocabulary; code sets contain distinct entries. Decimal quantities retain their declared precision. Date is a civil calendar day, year is a known year, and instant represents an unambiguous point in time. Time spans include their start and exclude their end unless a published policy explicitly describes a last included day. A displayed last day must be converted consistently at entry and reporting.

Ownership follows the referenced Organization, Congregation or parent record and must agree across references. UserAccount authenticates the actor; Person identifies the human in a church context. Each authenticated decision records the acting account, any person represented, delegated authority when applicable, the effective time, recording time and audit identifier. Sensitive reads and export, deletion, merge and correction actions record purpose and reviewer as required. Imports preserve origin and source identifiers. Dictionaries describe logical information; implementation storage, index choice and messaging technology are open.

## Common boundaries

| Producer | Consumer | Minimum exchange |
|---|---|---|
| People register | Attendance, groups, events and service teams | Stable approved person ID, allowed display name, age eligibility result and active scoped authority when needed. |
| Membership clerk | Meetings and reporting | Eligible roll or membership as of a cited policy/date. A meeting can freeze the roll it used. |
| Household and safeguarding verifier | Child check-in/out and enrollment | Allow, deny or refer for specific actor, child, action, time and activity. Case narrative and private addresses remain with their owners. |
| People and directory | Communications | Permitted contact endpoint, scope and effective dates. The communications service evaluates purpose-specific subscriptions, withdrawals and delivery outcomes. Directory publication consent is a separate decision. |
| Care and aid | Finance or inventory | Approved value or quantity, fund, payee and an opaque award reference. Reconciled execution returns to the award. |
| Identity steward | Accounting, commerce, service history and archive | Person alias/merge decision, acknowledgment and exception status. A posted payment, issued certificate or immutable meeting roll keeps its original facts. |
| Current member | Their own portal | Only entitled documents, event and volunteering records, messages, statements, orders and authorized family actions. Each authoritative domain checks current permissions at use. |

## Reference journey

A visitor arrives with a child and an aunt who lives elsewhere. The welcome desk records two named participants only if appropriate; an anonymous headcount remains possible. It records a family relationship separately from the child's current household. The aunt can collect the child once a verified activity-specific permission exists. Six months later the adult applies for membership and a clerk records admission effective on the approved date. The child and aunt retain their separate participation statuses. A search for the household never reveals the adult's confidential care contacts. At year end the clerk can reconcile changes in formal membership, the ministry lead can report attendance, and the finance team can produce giving statements under its own rules.
