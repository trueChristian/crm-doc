# Households, kinship and delegated authority

A household groups people for practical purposes such as mail, visits and family event registration. Family relationships describe how people relate. Authority describes exactly which actions someone may take for someone else. Model these separately. A child can live at two addresses, have parents in different congregations and be collected on Thursdays by a trusted neighbour.

## Logical records

| Record | Fields | Integrity and use |
|---|---|---|
| Household | id ID, organization_id → Organization, display_label text, correspondence_name text?, preferred_language text?, opened_on date, closed_on date?, state enum(active, closed), confidentiality code, revision integer | An active household can have one person. A draft created during intake can be empty until confirmed. Closure retains historical composition. |
| HouseholdPerson | id ID, household_id → Household, person_id → Person, role code, residence enum(primary, additional, occasional, correspondence_only), from_date date, until_date date?, mail_recipient boolean, ordering integer? | Many people per household and many households per person. Within one household the same person's residence episodes cannot overlap. At most one primary residence per person for a given date where the church uses that designation. An adult relative in another home can be linked solely through kinship. |
| HouseholdAddress | id ID, household_id → Household, use code, addressee text?, address_lines ordered text, locality text?, subdivision text?, postal_code text?, country_code code?, delivery_instructions restricted text?, valid_from date, valid_until date?, mail_allowed boolean, confidentiality code | Many effective-dated addresses including postal, residential and temporary. Permit rural directions and international formats. Only one preferred correspondence address per date. An address with protected visibility cannot appear via a person's linked household. |
| RelationshipType | id ID, organization_id → Organization, forward_label text, reverse_label text, symmetric boolean, category code, allows_multiple boolean, inference_policy enum(explicit_only, suggested) | Seed editable labels for parent/child, mother/child, father/child, step-, adoptive and foster relationships, sibling including brother/sister, partner/spouse, grandparent, caregiver and other. A person's chosen labels or unknown parentage are valid. |
| PersonRelationship | id ID, from_person_id → Person, to_person_id → Person, type_id → RelationshipType, detail_label text?, from_date date?, until_date date?, date_precision code?, confirmation code, recorded_by → UserAccount, visibility code | Two distinct people in the same organizational boundary. Store one directed assertion and display its inverse; symmetric types use a single unordered pair. Prevent overlapping duplicate facts and contradictory cycles for the configured ancestry types. |
| RepresentationAuthority | id ID, subject_person_id → Person, representative_person_id → Person, action enum(view_profile, edit_contact, enroll, attendance_consent, collect, emergency_contact, receive_notice), scope_kind enum(organization, congregation, activity), scope_key ID, effect enum(allow, restrict), begins_at instant, ends_at instant?, allowed_schedule text?, evidence_ref ID?, source code, verified_by → UserAccount?, verified_at instant?, state enum(proposed, verified, revoked, expired), review_due_on date? | One decision per representative, subject, action and scope per evidence item. The scope key resolves in its declared domain. An emergency contact may have only that action. A verifier must have authority for that purpose. |
| AuthorityReview | id ID, authority_id → RepresentationAuthority, reviewer_id → UserAccount, decision enum(verify, renew, narrow, revoke, dispute), decided_at instant, rationale restricted text, prior_revision integer | Append-only decision trail. Revocation stops future action immediately. Store custody evidence in the restricted document service; ordinary roster operators need only the current decision. |

## Living arrangements and correspondence

Register household members individually, including an attending guest, an infant and relatives who belong elsewhere. Creating a household never creates formal memberships, role privileges, financial statement units or contact subscriptions. For a blended household record biological, adoptive, step or other links only when volunteered for a defined purpose. A former spouse can retain a historical relationship and valid guardianship after moving. Sibling labels may be shown without guessing a person's sex, and inferred relationships require human confirmation. Do not identify unrelated roommates as family.

When people separate, close the relevant residence episodes and open new ones at the move date. Preview recipients before redirecting mail or merging households. Preserve each household's earlier addresses and correspondence history. The same child can appear on both family screens but counts once in a unique-person report. A family may change a display label without changing individually registered names. An opt-out, confidential address or unsafe-contact flag overrides a household mailing preference. Never send an envelope addressed to a deceased addressee simply because the household is active.

## Decisions at point of use

For a sensitive action, verify the acting identity, subject, purpose, scope, schedule, effective window and status. Restrictions take precedence over coinciding allows. If evidence conflicts or is missing, present a neutral “refer to authorized leader” decision and log the referral without showing private evidence. Policy can require on-site identity verification for pickup. A verified pickup permission confers no profile, financial or pastoral access. A household member's birthday, new residence or previously approved pickup does not renew a delegation.

An authorized guardian may request a time-limited delegate for a particular activity. The authorized verifier checks the request and action scope independently. The event service asks for a decision at release and records who physically received the child, which operator released them and when. A stale offline grant cannot override a later restriction; route unresolved cases to the designated supervisor and the church's supervised handover procedure. Record a disputed or withheld release without disclosing a protected address.

## Reports and verification

| Case | Expected result |
|---|---|
| Two parents and a guest grandparent share a home | One household and three people are counted. The formal member count includes only people with qualifying membership episodes. |
| A child changes primary home and continues visiting the other parent | A report as of last month shows the former primary home; today's shows the new one. Earlier mail still reflects its original address. |
| A neighbour can collect on Thursday but attempts Friday pickup | Decision is referred or denied under policy. The neighbour cannot inspect the child's directory profile. |
| A parent with an earlier collection grant receives a verified restriction before check-out | The current denial takes precedence, even if the person appears on a previously printed roster. A supervisor sees only the evidence their role allows. |
| A worker tries to see a restricted household address through printable labels | Direct view, print, export, search and household mailing previews all apply the same restriction. |
| The clerk needs the number of households with at least one formal member | Count distinct active households that have an effective HouseholdPerson linked to a qualifying Membership on the selected date. State whether additional residences count. |

## Review a family change across existing commitments

A household split may be disclosed in person while an event reminder, a directory print edition and a child release are already in progress. Accept a private correction request from an adult about their own information. If the request concerns another adult or a child, verify authority for that specific change. Give the office a way to keep a newly supplied address in a restricted review without exposing it to the previous household through a portal notification, household summary, failed validation response or old volunteer list.

| Existing commitment | Owner’s action after the effective change |
| --- | --- |
| Household correspondence for a general bulletin | Preview the next authorized addressee and destination. A household split can produce zero, one or several permitted copies. Recheck any batches still in church custody and record their replacement or withdrawal. |
| Child registered for an event at the former address | Keep the child's participation and event place. The check-out team requests the current collection decision at release. Moving residence alone cannot grant or revoke collection, guardianship or receipt of notices. |
| Shared email or phone used by two adults | Verify which person can still use it for which purpose. Suspend sensitive deliveries to a contested endpoint until a safe, independently verified route exists. A new subscriber cannot use the old destination to read past private threads. |
| Two people with a previously agreed joint pastoral visit | The assigned worker checks separately and privately which arrangements remain wanted. Offer separate contacts or neutral venues where appropriate. Each adult's response is visible only to those who need it. |
| Membership, financial correspondence or prior certified records | Tell each independent owner only what it may receive. A person's transfer needs its own authorized decision. Issued statements and earlier roll editions keep their original evidence. |

For a reversal, retain the original effective date and recording time of the disputed change. A steward distinguishes a mistaken record from a subsequent real move. Review downstream copies already issued, issue corrections where appropriate and record acknowledgment. Never restore a formerly shared route or a withdrawn authority just because the earlier address was restored.
