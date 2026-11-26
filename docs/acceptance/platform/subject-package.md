# Supply a subject-access package after representation and custody change

Subject P requests their own records. Representative R initially has verified scope to collect a specified package for P. Steward S prepares it; designated reviewer V approves release. Privacy decisions and deadlines in this run are local fixture policy, and every class has a named custodian. Use fictitious evidence.

| Fixture part | Source owner and contents | Approved disposition in edition K1 |
| --- | --- | --- |
| 1 | People register: P's own contact details, including an obsolete address marked historical. | Include P's permitted fields with correct effective dates; omit protected handling notes. |
| 2 | Communications: P's purpose decision with a third party's private phone number in an attachment. | Include P's decision and its date. Redact the phone and the identifying portion of the attachment. |
| 3 | Governance: approved minute extract concerning P followed by an unrelated disciplinary matter. | Export the permitted extract. The private neighboring topic and title remain unavailable. |
| 4 | Finance: P's own receipt and a correction; another person receives separate matching credit. | Include P's original and correction with linked identities. Apply the class custodian's decision to exclude the other person's identity. |
| 5 | Held case evidence: a preservation hold covers the original, whose disclosure requires separate review. | Keep the original in custody. Under this fixture the reviewer withholds it from the issued package and provides the subject only the explanation approved by the custodian. |

## Produce and challenge the package

1. Verify which person is requesting, who is represented, the requested scope, identity evidence, request date and authorized collection route. Receiving an email at a household address or creating an account for R supplies no proof of the required representation.
2. Snapshot the five source parts at 09:00 with exact document/record revisions and accountable custodians. Reconcile five dispositions: four parts included in reviewed form, one withheld under its decision. Count logical parts independently from individual files or receipt lines.
3. Reconstruct the redacted artifacts, including filenames, selectable text, properties, annotations, hidden spreadsheet columns, attachment names and navigation indexes. Search all recipient-visible representations for the synthetic third-party tokens. Expected token hits = 0. Restricted provenance can retain approved references under separate custody.
4. S submits K1 and V approves its digest at 09:15. Only the protected redaction log identifies the portions removed. The recipient manifest cannot reveal a protected title, the unrelated person's identifier or the raw source location.
5. At 09:20 R's representation is revoked. Try the saved link, a direct file request, an existing signed-in viewer, the manual issue desk, and a previously prepared mail queue. K1 cannot be newly released to R after revocation. The prior approval remains historically valid with its original scope and does not grant present collection authority.
6. At 09:25 a financial custodian supplies a new corrected receipt for P. Whether the correction belongs in this issue depends on the recorded cutoff. This fixture requires an up-to-date package before first release. Create K2, re-snapshot the changed part, retain the rest's approved revisions if still current, verify redactions and obtain approval for K2. A previously signed K1 digest cannot authorize the changed file.
7. At 09:35 P collects K2 directly after independent verification. Count one retrieval by P, zero retrievals by R since revocation. Record the actual approved edition, time and recipient authorization. Access attempts remain separately auditable without storing a second copy of the private response in logs.
8. At 10:00 the package expires under this fixture's half-open interval. A request arriving exactly at expiry cannot download again. Renewed access requires the approved process. The held original remains available solely to the nominated custodian for its own purpose.

## Reconcile three exceptional histories

| Variation | Expected evidence and action |
| --- | --- |
| R actually downloaded K1 at 09:18, two minutes before revocation | Keep that truthful retrieval in the historic totals. Block future access by R. If a later correction requires notice, the custodian applies the authorized route and records acknowledgement or unresolved response. |
| A third-party token appears in the searchable text of the visually masked extract during testing | Fail the package before release. Withdraw the artifact, correct the rendition, verify all representations and approve its new digest. Source evidence remains intact. |
| Disaster recovery reintroduces the 09:15 approval and R's old grant | Keep package retrieval closed until the recorded revocation, K2 issuance and expiry are replayed. Reconcile actual retrieval evidence and the designated held source before the owner releases the service. Recovery alone triggers zero disclosures. |

The subject-facing response lists the outcome and approved explanation for each permitted part and describes how to seek a review. The oversight record separately reconciles identity, redaction, withheld custody, approval and actual retrieval. An elapsed deadline escalates the request to its owner and never authorizes automatic release of unreviewed data.

Use [SubjectRequest](../../implementation/platform/SubjectRequest.md), [DisclosurePackage](../../implementation/platform/DisclosurePackage.md), [RepresentationGrant](../../implementation/platform/RepresentationGrant.md), [DocumentRevision](../../implementation/platform/DocumentRevision.md), [HandlingRestriction](../../implementation/platform/HandlingRestriction.md) and [PreservationHold](../../implementation/platform/PreservationHold.md).
