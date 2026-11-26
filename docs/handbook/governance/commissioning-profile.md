# Commissioning Alder Crossing Fellowship

Alder Crossing Fellowship is fictional. Use these values to rehearse a clean installation and compare results end to end. They are choices made by this example church. Another church must choose its own authority, membership policy, accounting exchange route, privacy settings, time zone and calendar. All dates and times below use Africa/Windhoek, UTC+02:00 throughout the fixture. Effective intervals include their start and exclude their end. Human-readable codes identify these fixture records across the three documents.

## Congregations, officers and accounting connection

| Record | Fixture values effective 1 January 2027 at 00:00 |
| --- | --- |
| Organization ACF | Legal and display name Alder Crossing Fellowship. Type local church, default language English, locality Windhoek, default currency NAD. One accountable entity, no subsidiaries, no automatic external sharing. |
| Congregations WELL and RIDGE | Wells Congregation and Ridge Congregation. Both belong to ACF and conduct separate worship and registration; their assembly is joint. Each official member has one primary congregation in this fixture. |
| Campuses HALL and STREAM | Crossing Hall is physical; Crossing Online is virtual. Both congregations use HALL as primary for worship and STREAM as additional for worship. Create four CongregationCampus records. One hall, two communities and two locations still make one legal church. |
| External accounting connection ACF-01 | ACF authorizes an accountant to acknowledge giving handoffs in NAD, supply an external spending result and release a calendar-year summary. General and Outreach are distinct mapped designations. The church retains the donor’s restriction for Outreach. The accountant owns bank and book records. |
| Assembly and officers | GoverningBody ASSEM represents ACF. CharterEdition C1 was adopted by an independently evidenced founding instrument on 15 December 2026, effective 1 January 2027. The chair, clerk and treasurer have distinct Office and OfficeTerm records starting 1 January, ending 1 February 2028. |

The paper founding instrument appoints Mira Nela as clerk, Ena Vale as chair, Joel Vale as treasurer and Malu Kade as independent finance reviewer. Verify the instrument and the first two human identities independently before releasing production-equivalent privileges. Keep the founding instrument in the restricted archive. Record the actual activation actors and times; a historic office effective date does not mean a user authenticated before account creation. [Organization scope](../../foundation/organization.md) and [identity and access](../../platform/identity-access.md) define the owning records.

## Adopted policy edition C1

| Decision | Example value and effective-time check |
| --- | --- |
| Official membership | Full, active MembershipPeriod in WELL or RIDGE counts on the organization roll. Visitors, applications and resident relatives count only in their separately defined categories. Adult standing and age are independently verified when the voter roll is certified. |
| Electorate for the 28 August business meeting | Qualified adult members, one equal right per distinct person across both congregations, aged at least 18 and active at the special cutoff, 1 August 2027 at 00:00. A person turning 18 or joining after cutoff can attend by invitation, with zero voting entitlement for that meeting. |
| Notice | Give every qualified voter individual service at least seven clear calendar days before the meeting. Approved channels are individual verified email dispatch, acknowledged private-inbox service, and evidenced hand delivery. Deadline is 20 August at 23:59:59 for the 28 August meeting; the 21st through 27th are the seven clear days. A public post is supplementary. The charter permits no short-notice waiver in this fixture. |
| Meeting procedure | 28 August at 10:00, HALL. Count verified live participants only; proxies are disabled. Quorum is at least half the frozen eligible population, rounded up. A simple substantive motion passes with more than half of decisive yes/no votes. Abstentions remain in the participation count and outside the decisive-vote denominator. Tie fails. No chair's extra vote. |
| Minutes | A decision takes effect when passed. Clerk prepares minutes, chair and clerk attest the exact same edition under the charter's delegated confirmation procedure. Only its reviewed public extract may be published. Restricted papers and named voter details stay private. |
| Spend authority | General supplies may use General. A resolution sets a ceiling and an expiry. A treasurer prepares the request, an independent reviewer authorizes it, and the external accounting service confirms or declines execution. |
| Giving and receipts | Identify the donor privately if known, use only their authorized receipt route, keep general and restricted allocations on separate fund lines. Issue one numbered private acknowledgment per verified gift. This profile makes no assertion of tax deductibility. |
| Annual pack | Freeze year-end population at the close of 31 December. Calculate using evidence available by 5 January 2028 at 12:00. Only approved aggregate figures go in the member edition. Financial statements, membership return and public minute extracts remain separately versioned. |

Load [the people and access assignments](commissioning-access.md) before running [the connected rehearsal](commissioning-rehearsal.md). The profile contains no actual contact endpoints, login secrets, bank credentials, live dispatch routes or payment destinations. All tests use isolated recipient and payment channels identified by the fixture codes.
