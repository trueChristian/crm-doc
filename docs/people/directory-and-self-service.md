# Directory publication and member self-service

A member should be able to find another member who has chosen to be listed. A clerk needs a current working register even when the person has chosen to share nothing in the directory. Design separate views for the individual, their verified representative, the office, a ministry team, logged-in directory users and an approved public audience.

## Logical records

| Record | Fields | Integrity and use |
|---|---|---|
| ProfileLink | id ID, person_id → Person, user_account_id → UserAccount, status enum(invited, asserted, verified, suspended, revoked), verification_method code?, verified_by → UserAccount?, verified_at instant?, revoked_at instant?, revision integer | A verified personal sign-in belongs to one person in the organization. At most one primary verified personal account per person. Delegates use their own accounts and RepresentationAuthority. Identity policy governs account recovery. |
| ProfileInvitation | id ID, person_id → Person, delivery_contact_id → PersonContactPoint?, issued_by → UserAccount, expires_at instant, consumed_at instant?, state enum(issued, consumed, expired, cancelled), proof_ref private ID | Single-use, scoped to its person, church and intended action. A verified shared address alone cannot identify which family member accepted it. Reissues cancel the replaced invitation. |
| DirectoryEdition | id ID, congregation_id → Congregation, name text, audience code, permitted_fields code set, household_layout boolean, eligibility_rule code, publication_mode enum(live, dated_export), publication_policy_revision text | One edition per audience/purpose. Default audience is limited and fields are explicitly allowed. Deny public discovery until a church chooses a publication policy and individuals supply applicable permission. |
| DirectoryDisclosure | id ID, edition_id → DirectoryEdition, person_id → Person, field_key code, decision enum(show, hide), purpose code, authority_id → RepresentationAuthority?, decided_by → UserAccount?, recorded_by → UserAccount?, effective_at instant, withdrawn_at instant?, evidence_ref ID? | Field and audience specific. Record a named clerk for paper choices, the verified person or lawful delegate for self-service. An active restriction overrides an allow. When a person's status changes, recompute eligibility and any delegate authority. |
| ProfileChangeRequest | id ID, person_id → Person, requested_by → UserAccount, authority_id → RepresentationAuthority?, field_key code, old_revision integer, proposed_value restricted typed value, submitted_at instant, status enum(submitted, verifying, approved, rejected, withdrawn, conflict), reviewed_by → UserAccount?, decided_at instant?, public_reason text? | One scoped editable field per item; group several items under one intake reference if the church reviews them together. Names on issued records, membership status and financial facts require their owning workflows. |
| DirectoryExport | id ID, edition_id → DirectoryEdition, created_by → UserAccount, created_at instant, purpose text, recipient_scope code, expires_at instant?, policy_revision text, protected_artifact_ref ID?, destroyed_at instant?, withdrawal_notice_at instant? | Record generation and retrieval of approved print/export editions. Apply permissions at creation and retrieval. Once physical copies leave church control, record recipients, expiry and withdrawal notices under policy. |

## Account and directory boundaries

A clerk invites the person or the person requests access. Return a generic response when a submitted address has no match or matches a restricted person. Resolve ambiguous identifiers through independent verification. Adults sharing an email can use separate sign-in identities where the authentication service supports them. Require fresh verification before owner changes, sensitive exports, or adding delegates. Revoking a login stops its access while retaining the person's register history.

A verified member can update permitted contact details, language and message preferences, request a register-name change, review directory visibility, see their own groups and register for activities. For self or delegated actions, show who is acting and for whom. Date-limited authority is evaluated per action and per subject. An address change involving multiple household members becomes an explicit request showing only affected people the actor can represent. A member never sees someone's giving, pastoral notes, case status or blocked contact through household membership. Individual giving statements and order history use controls in their owning domains.

For each search, first restrict candidates by audience and current eligibility, then include fields permitted by policy, consent and protective restrictions. Apply equivalent filtering to autocomplete, search counts, previews, direct record routes, photo thumbnails, maps, event displays, downloads, exports and group listings. Prevent a visible street name or household label from revealing a concealed person. A directory photo requires its own permission; verify all identifiable people before using a shared family photo. Directory access must not grant bulk export or bulk messaging.

## Corrections and publication

* Members may submit corrections offline at the office. Record who took the instruction, verification level and which items require approval. Produce a confirmation by a safe contact route selected by the person.
* Concurrent change requests include the baseline revision. On conflict show the submitter their proposed change and only fields they may currently view; allow a new request. Never overwrite another household member's protected information as a side effect.
* Opt-out takes effect for new live requests and future exports. Invalidate generated views and expiring digital download links as policy dictates. Maintain the distribution history of printed copies and disclose the limitation before publication.
* A church may enable a moderated skills or language directory. The person selects expertise, intended audience and allowed contact route. A feedback request routes through the service if personal contact details are hidden. Membership, regular attendance or service does not enroll someone automatically.

## Acceptance

| Situation | Observable outcome |
|---|---|
| A visitor asks for portal access and a verified member shares their name | Staff verify identity against permitted evidence before linking; the visitor does not inherit the member's account. |
| A child belongs to two households and one residence is protected | A household card cannot reveal the protected address or unrelated household members. The other household sees only actions specifically delegated. |
| A member hides their phone but permits direct contact through a relay | Name remains searchable for the approved audience; relay sends without exposing the phone. Search, print and export omit it. |
| A former elder requests last year's directory download | Current retrieval permissions govern access and a revoked link fails. Staff can identify which editions were distributed. |
| A member edits their name while the clerk verifies a different spelling | Old revision triggers a conflict; neither silently overwrites the other. A previously issued certificate retains the original wording. |
