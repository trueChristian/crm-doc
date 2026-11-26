# Rehearse a migration with errors still in the source

This rehearsal exercises the [migration and data-quality contract](../../platform/migration-data-quality.md). A clerk supplies people and households. A treasurer supplies opening balances. A communications custodian supplies suppression evidence. Each custodian accepts their own reconciled results. An apparently successful row count cannot establish that a child joined the church, that a gift belongs to the correct fund or that an old opt-out survived.

## Six source identities

The source church distinguishes text identifiers 007 and 7 and has two households called Daniel. Intake allows incomplete birth dates. The staging edition expects source text, names, household code, birth information and any dated membership episode. In this sample the person source has six rows with declared dispositions.

| Input | Evidence and expected first-run disposition |
|---|---|
| P007, Ada Daniel, H01; known birth year only; formal membership starts 2017-03-01 | Insert one person with year precision and one dated membership. Preserve the source key P007. Formal age on a date can be bounded but cannot be reported as an exact birthday age. |
| P7, Ada Daniel, H02; no birth detail; attended once | Insert a distinct guest, source key P7. Raise a possible duplicate with P007 for a steward. A similar spelling cannot join households or inherit membership. |
| P8, Jo Daniel, H01; shared family phone; child, membership unknown | Insert a person and household connection. No automatic official membership, portal account, SMS entitlement or right for household adults to collect Jo. |
| P9, Lin, H03; transferred out on 2024-06-01 | Insert one person with preserved mononym and historical end date. A census on and after the effective end omits their qualifying formal membership under the half-open interval convention. |
| P10, Emile, H99, missing parent household | Defer the household-dependent unit for review; retain a reference to the source row. A temporary guess at H01 would be an incorrect successful import. |
| P11, Tee, H04; supplied full birth date 2022-02-30 | Reject the invalid date, show a redacted row error and return to the steward. Keep the original value in restricted staging until approved expiry. |

First run yields four committed, one deferred and one rejected source people, totaling six. Before applying, the preview creates zero people and sends zero notices. On a corrected run H99 can be imported from independent evidence, and the steward can replace the impossible date with an explicitly confirmed partial date. Repeating the four previously accepted inputs returns their existing outcomes. Final totals are six source-person identities, one pending candidate pair, one explicitly documented active membership in this fixture and a formal membership history with its actual dates. A guest attending once counts under attendance only.

## Field mapping procedure

1. Review every column whose meaning changes across congregations. “Member” may indicate household news delivery, a formal roll entry or a volunteer group. Require dictionary edition, label, value map, owner and acceptance sample before using it to create official status.
2. Declare how missing columns, blank cells, “unknown”, placeholders supplied by the source, explicit clearing and contradictory values map. An omitted cell on an incremental update cannot erase a previously verified phone. Test names in differing scripts, leading zeros, multiline text, local decimal separators, negative amounts, date-only fields and missing time zones.
3. Establish a crosswalk keyed by organization, source identity, source record type and source key. Distinct external systems can both own row 7. Preserve whether the original key is case sensitive. A changing name or reissued phone never becomes the crosswalk.
4. Import scope, vocabulary, households and people before dependent memberships, authority, preferences, orders and open invoices. Where formal approval is required, stage an exception if the source has a claim without supporting evidence. Preserve independently signed original documents under their original edition and applicable reader restrictions.
5. Test the message and financial side-effect policy. Historical baptisms, pledges, paid orders and completed notice deliveries should not create new congratulations, charges, receipts or fundraising messages. Cutover enables new activity from an explicit source boundary. Record baseline event watermarks and already-completed effects.

## Finance and contact controls for the same cutover

The opening trial balance contains bank debits allocated 700 unrestricted and 200 restricted in the same physical bank account, unrestricted opening net assets credit of 700 and restricted opening net assets credit of 200, in one currency. The trial balance balances and leaves a restricted position of 200. If a mapper credits all 900 to unrestricted, both debit and credit control totals still agree. The fund-level test must fail. The accountant corrects the dimension mapping before opening and signs both account- and fund-level totals. These are migration opening balances. Replaying historical gifts that contributed to them as additional current-period revenue would duplicate the opening position.

The communications source contains a withdrawn newsletter permission for P007 represented by an older address and channel decision. The privacy custodian links it to the verified person and purpose; do not transfer it to P7 simply because the name matches. Unverified permissions remain unavailable for optional sending. Validate both whether an audience contains a person and which fields would reach the recipient. A directory field exclusion applies even when contact delivery is otherwise permitted.

## Go-live and reversal

Run the import twice in controlled conditions with the same source snapshot. Compare canonical IDs, emitted event counts, monetary totals by currency, links and candidate decisions. Then stage a realistic concurrent change on an accepted record. A later correction to the same field must report a conflict and retain its provenance. For large jobs, cut power after one logical unit commits but before the source row is acknowledged; resumption must reproduce the same target.

For an erroneous batch, build an impact report of mutable fields, shared links, downstream actions, approved documents and externally fulfilled transactions. Reverse only the affected changes still owned by that import. Preserve later legitimate work and route disputed fields to their stewards. Posted transactions use finance-approved reversals. A confirmed public delivery enters correction/recall rather than being erased from history. A second undo request returns the same outcome.

Sign-off lists row counts by disposition, source and target checksums of permitted attachments, rejected values by category, unmatched joins, consent exceptions, balance controls, responsible owners, decision times, open risks and retention of staged files. Keep identifiers necessary to explain the cutover even when temporary personal staging content expires.
