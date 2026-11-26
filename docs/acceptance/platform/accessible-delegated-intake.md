# Resume an accessible registration when the delegate's authority changes

A representative R can register P for a church retreat, and can separately register themself. R has no authority to register Q. The retreat has two available places. A prepared registration has no seat effect until an authorized submission enters the configured accepted state. This fixture has no fee, waitlist automation, medical form or consent implied by registration.

## Seed the form

| Datum | Value and usage |
| --- | --- |
| Form F7 | Approved revision 7, open until 15:00, actual venue language A and approved alternate language B. Coordinates and map images are optional. |
| Accessible path | Plain text, operable labels, focusable error summary, keyboard and screen-reader confirmation. A common shared kiosk forgets prior drafts at sign-out. |
| Delegated authority | R→P, allowed scope registration for this retreat, starts 08:00 and ends 14:30 exclusive. R→Q has no corresponding grant. |
| Draft D | R starts at 14:20 for P and saves revision 7 on R's personal device. It remains a draft until submitted. An authorized retreat coordinator can inspect only permitted completed records. |
| Promotion rule | F8 adds a compulsory transport choice newly relevant to the venue. F8 must be shown before any new final submission. Preserve harmless entered data for authorized users only. |

1. At 14:22 enter a valid language choice and an invalid retreat-session selection. The form announces an error once, returns focus to the erroneous control via the summary, retains the authorized entries and creates no submission or registration. Switching from visual to text view retains the same underlying answers.
2. At 14:24 F8 takes effect. Resuming D while the representation is still valid identifies the changed question and asks R to choose. An earlier missing value is not silently converted to “transport required” or “transport declined.” The draft can retain its F7 provenance alongside the reviewed F8 entry.
3. At 14:28 save the F8 draft. Network service drops before a final confirmation is sent. A local “saved” acknowledgement does not reserve a seat or claim that the organization has accepted the form.
4. Connectivity returns at exactly 14:30. Re-evaluate R's representation before revealing P's saved answers or accepting a queued request. The half-open authority interval excludes this instant. Return a neutral status with a route to a permitted human contact. R's personal account remains available. Inspect history, browser back, direct resumption and print view for stale access.
5. At 14:31 R submits a distinct application for R. Confirm actor = R, subject = R, one successful form receipt and one occupied place. A retry with that receipt does not consume a second place. A changed subject under the same logical submission cannot reuse R's receipt to seat P or Q.
6. At 14:35 P signs in in their own right. P may initiate or adopt the work only through an explicitly permitted subject path; store which user actually confirmed the reviewed F8 answers. This fixture requires a fresh subject confirmation and uses one final seat. A staff service account cannot convert R's expired authority into P's consent.
7. At 14:40 the operator counts two valid final registrations, two distinct people, two occupied places, zero additional seats from R's abandoned delegated request, and zero registrations for Q. A fresh authorized request from another eligible person gets the configured full result. A double tap on P's accepted confirmation returns the same receipt.

## Separate failure evidence

| Exercise | Pass condition |
| --- | --- |
| R follows a saved link while signed in as Q or using another church | No prior subject details or draft values appear, including in title text, metadata, downloadable receipt or session restoration. |
| Available assistive translation is still based on F7 | Label its language and stale edition accurately. Offer a reviewed accessible F8 path or authorized staff assistance. Record the actual material reviewed. |
| A staff member enters a paper submission after cutoff | Store the actual received and recorded times with the documentary evidence. The designated owner applies the local late-entry rule and seat availability; the entry operator cannot backdate authority. |
| A kiosk runs out of time at the final step | A warning and permitted accessible extension respect the form and authority deadlines. Expiry cannot submit, reserve a place or reveal work to the next user. |
| A coordinator opens review with rights limited to registrations | Shows only permitted submitted registration data. Browser progress, draft values, representation evidence and restricted form attachments are individually controlled. |
| A duplicate request arrives concurrently with the last seat | Reserve once for the first valid accepted logical submission. Record the deterministic full or duplicate outcome for the other request, with totals checked against current registrations. |

Inspect [FormEdition](../../implementation/platform/FormEdition.md), [FormDraft](../../implementation/platform/FormDraft.md), [FormSubmission](../../implementation/platform/FormSubmission.md), [RepresentationGrant](../../implementation/platform/RepresentationGrant.md), [UsabilityTest](../../implementation/platform/UsabilityTest.md), [EventOccurrence](../../implementation/ministry/EventOccurrence.md) and [EventRegistration](../../implementation/ministry/EventRegistration.md).
