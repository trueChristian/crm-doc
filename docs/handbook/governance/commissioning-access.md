# Commissioning people, grants and safe recipients

Apply these identities to the [Alder Crossing profile](commissioning-profile.md). Nine Person records, one explicitly bundled household and six enabled UserAccount records exist by the August meeting. The newly admitted member Anu uses assisted service and has no login. Household collection remains optional for the other six people; leave their household relationships unknown in this rehearsal.

| ID and name | Status, scope and account | Authorized receiving route |
| --- | --- | --- |
| P01 Mira Nela | Adult, Wells, founding member and clerk. Account U01. | Verified individual email for governance service. Nela household phone is shared and excluded from private business. |
| P02 Tomas Nela | Adult, Wells regular attendee and Mira's spouse; no formal membership or account. | Named household postal recipient for a general bulletin only. |
| P03 Rina Nela | Born 3 June 2014; Wells attendee and child of P01/P02. No membership or account. | Class notices through the specifically verified representative. No direct route for adult governance or giving. |
| P04 Ena Vale | Adult, Ridge founding member and assembly chair. Account U04. | Verified individual email for governance service. |
| P05 Joel Vale | Adult, Ridge founding member and treasurer. Account U05. | Individually delivered, acknowledged member-inbox notice. The shared surname with Ena establishes no family authority. |
| P06 Malu Kade | Adult, Wells founding member and finance reviewer. Account U06. | Receipt of formal notice by documented hand delivery. |
| P07 Tavi Dume | Adult, Ridge founding member and private donor. Account U07. | Verified individual email for meeting notices, private member inbox for giving acknowledgment. Declines optional giving appeals. |
| P08 Anu Kito | Adult Wells guest with no account; applies 2 August and is admitted effective 10 August. | Opted-in neutral general bulletin through verified email. Formal support is available by hand when entitled. |
| P09 Suri Kito | Adult Wells guest, no membership. Account U09 verified for self-service only. | No subscription to optional announcements. An account does not add a person to the member roll. |

Create Household HH-NELA with three current HouseholdPerson links. Represent Mira and Tomas as spouses and each parent-child relationship explicitly through PersonRelationship. Project only verified powers from RepresentationAuthority to RepresentationGrant. In this fixture Mira may receive Rina's class-change notices through 31 December 2027; Tomas may collect Rina from class on Saturdays until 31 August only. Access intervals end at the start of the next day after each stated last day. His permission to collect does not authorize receiving attendance lists, changing Mira's contact details or viewing a household giving statement. Protected details about evidence are visible only to the verifier. The family elects no directory publication for Rina. A shared household telephone provides no personal credentials.

## Minimum grants under test

| Principal | Scoped actions | Denial to demonstrate |
| --- | --- | --- |
| U01 clerk | Prepare membership records and meeting roll within ACF; issue approved notices, draft minutes, prepare annual membership report. As an independent family role, receive only Rina's authorized class notice. | Cannot approve the clerk's own membership correction without the designated reviewer, read Tavi's contribution amount or release bank payments. |
| U04 chair | Confirm membership decisions, authorize notices, attest minutes and release the approved public extract; certify the aggregate annual report. Founding witness confirms the administrator recovery route. | Chair can review released fund totals, but cannot open individual receipts or edit an accountant’s signed release. |
| U05 treasurer | Record a gift, map its two designations to ACF-01, prepare an expenditure request and attach the approved external report. | Cannot self-authorize an outgoing payment; cannot use the contributor register to create an appeal audience. |
| U06 finance reviewer | Verify fund allocations, approve the outgoing payment request against evidence, approve private gift acknowledgment and sign the finance pack independently. | Cannot change donor contact permissions, publish the donor's identity or approve a draft that the same user prepared. |
| U07 member/donor | See own published content and own protected giving acknowledgment. | Cannot open assembly drafts, another donor's statement or a clerk export. |
| U09 guest | Review own permitted profile and read public extracts. | Cannot browse member-only papers, cast a member vote or gain access by knowing a restricted document number. |
| Isolated dispatch principal | Process permitted dispatch records and return scoped delivery evidence. | Cannot enumerate donor, household or voting records, confer capacity on a household representative, or approve new content. |

Create AccessRole and RoleCapability records for the listed actions and date each RoleGrant at actual verification or commencement, whichever is later. Bootstrap the first appointment from the independently verified founding instrument; record the second person's recovery confirmation. The same people may have multiple unrelated roles. Use personal member access separately from chair, treasurer or family representation. Revoke an office grant at 1 February 2028 at 00:00; a separately authorized personal member role continues. No later exercise should inherit elevated access from previously loaded pages, downloads still on the server or search results.

**Ready check.** With U09 signed in, a direct request for the donor document is denied and a directory search reveals no Rina record. With U01, a class notice for Rina arrives only through the approved individual route; no message to Tomas, Rina or the shared number. With U07, the gift acknowledgment is available after finance releases it, even though fundraising appeals are declined. The [rehearsal](commissioning-rehearsal.md) tests those same recipients against the live fixture facts.
