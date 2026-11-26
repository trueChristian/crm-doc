# Import and certify the register

The source is a signed register for congregation North within church A. A second church B uses similar source keys and shares a venue. Each church has its own staff authority and data perimeter. The sample dates below are civil dates at North. The local policy includes an approved ordinary membership period on each date from its first day up to, and excluding, its end date. Guests and household relationships never confer membership.

## People input

Each of the first six source rows represents one person. The seventh is deliberately a replay of the third. Names and endpoint symbols are synthetic. A blank here means no value was supplied. The migration does not send mail.

| Row | Source key | Person | Household | Contact endpoint | Birth evidence |
| --- | --- | --- | --- | --- | --- |
| 01 | 0008 | P1 Ada Reed | H1 | E1 shared | Unknown |
| 02 | 0080 | P2 Ben Reed | H1 | E1 shared | Year 1988 |
| 03 | 0081 | P3 Iri | H1 | None | Year and month, July 2015 |
| 04 | 0082 | P4 Mara Lin | H2 | E2 | Unknown |
| 05 | 0083 | P5 Neri | H3 | E3 | Unknown |
| 06 | 0084 | P6 Ada Reed | H4 | E4 | Unknown |
| 07 | 0081 | P3 Iri | H1 | None | Identical source object and revision to row 03 |

For a cross-scope control, create a seventh distinct person in church B with source key 0008 and display name Ada Reed. The operator who runs North's import has authority only in church A. A matching facility or key does not let that operator discover the other person.

A successful run accounts for seven physical source rows as six new person identities and one unchanged replay. It creates six source-object mappings in church A, four household identities, and no January birthday or first-of-month day for P2 or P3. The shared delivery address binds P1 and P2 to their own contact records. P1 and P6 have different source evidence and remain distinct after review. Source keys 0008 and 0080 survive a round trip with their leading zeros. Re-importing all seven rows with the same approved mapping produces zero new people and zero new households.

## Membership facts and dated reports

| Person | Membership evidence | Known at first certification |
| --- | --- | --- |
| P1 | Ordinary North membership from 2 January 2025, open end | Yes |
| P2 | Ordinary North membership from 1 May 2025, end effective 1 June 2026 | Start known. End reaches the clerk on 3 June. |
| P3 | Household association only | Yes |
| P4 | Ordinary North membership starts 1 June 2026, open end | Yes |
| P5 | Ordinary North membership from 1 January 2025, end effective 1 June 2026 | Start and end known |
| P6 | Guest, no membership application or admission | Yes |

At 18:00 on 1 June certify two rolls with the facts then known. At 09:00 on 3 June accept the previously missing end decision for P2. Create an amended June edition under independent authority and leave the originally issued edition available to its authorized readers.

| As-of date | Knowledge available | North's included identities | Count |
| --- | --- | --- | ---: |
| 31 May | 1 June at 18:00 | P1, P2, P5 | 3 |
| 1 June | 1 June at 18:00, certified original | P1, P2, P4 | 3 |
| 31 May | 3 June after correction | P1, P2, P5 | 3 |
| 1 June | 3 June after correction, amended | P1, P4 | 2 |

A summary checking only the two original headcounts would miss both the arrival of P4 and the departure of P5. Compare the sets as well as the totals. The June amendment removes exactly P2. The original still establishes who was on the roll used on 1 June. A public bulletin receives its permitted audience through a separate decision. A donor record, contact or household membership never supplies missing admission evidence.

## Handoff evidence

The migration lead retains the batch receipt and source-key reconciliation. The clerk retains the two original roll editions and the June amendment with knowledge cutoffs. A reviewer checks one guest, both people named Ada Reed, the shared contact and the two changed periods. The communications lead needs its own approved audience, purpose and per-person choices. The treasurer receives no register export for the purpose of recording the weekend's transactions.

[Migration records](../../platform/migration-data-quality.md) · [Personal register](../../people/personal-register.md) · [Membership periods and rolls](../../people/membership-and-rolls.md)
