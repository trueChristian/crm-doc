# Verify the archive before moving playback to church storage

A church has one private teaching recording on an external capture service. It has chosen to preserve its own copy and to serve approved edits from church storage. A second church chooses a managed archive. All claims concern systems the respective church controls or can reconcile. Storage preference never grants rights to record, distribute, translate or download.

## Storage choices and observable outcomes

| Approved church policy | After the service | After an archive is separately cleared |
| --- | --- | --- |
| Live only, recording disallowed | Disable recording on every selected source and destination, including remote automatic replay. An incompatible destination stays unavailable. Ended page shows the approved end state. | No master can be ingested from that transmission under this decision. An independently authorized recording requires its own provenance. |
| Private archive, no replay | If recording is authorized, ingest into protected storage and verify the master. Editors can inspect it within their scope. | Public and member players continue to show the approved end state until a new release is authorized. |
| Managed capture, managed playback | Accept the bound completion receipt, verify the asset and retain its protected identity. The capture locator stays out of the viewing page. | Issue access only for a released rendition under its current audience and use. Withdrawal blocks future controlled access. |
| Managed capture, church playback | Copy and verify bytes first. Keep the managed copy under the retention decision until the verified local copy can be recovered independently. | Switch the released rendition to the verified church origin after the access checks pass there. Preserve the edition and existing licensed access history. |
| Church capture, church playback | Restrict the local capture immediately. Independently verify its completeness and decodability, including any known service interruption. | Publish approved derivatives under a release. An existing file on the web host is never an authorization criterion. |
| Church capture with an additional preservation copy | Record custody and verification for each copy and test recovery at the selected storage location. | Changing the preservation target does not change the audience, entitlement or selected playback origin. |

A hosted player that automatically republishes a recording publicly cannot serve a private-only recording job unless its configuration has actually been verified to suppress that publication. A connection status of “working” establishes connectivity only.

## Reconcile one handover

Seed a 3,600-second synthetic master of 100,000,003 bytes, with a recorded source fingerprint and a known decodable first and last frame. Use one organization, service, LiveSession and protected MediaAsset for the authoritative master. A storage move preserves the identity of the logical content. A re-encoded public edit has its own asset and fingerprint. Additional preservation copies can use the archive custody records where the church operates that register.

| Boundary | Injection or action | Evidence expected before crossing the boundary |
| --- | --- | --- |
| Capture ends | The producer ends the session before external recording finalization | Keep a single expected completion pending. Do not calculate a permanent “missing” result from the absence of an immediate asset callback. |
| Receipt arrives | The provider reuses a short recording label also used by another church | Resolve the verified connection and external object mapping before attaching a result. The target stays the original church's delivery. |
| Copy begins | 40,000,000 bytes arrive and the connection drops | Record the partial transfer privately. It is neither a complete master nor a playable rendition. Advertised source size still exceeds received size by 60,000,003 bytes. |
| Retry starts | The remote contract can resume at the verified byte offset | Require the same immutable remote revision. Append exactly the verified remaining range, or restart from byte zero if identity or range support is uncertain. Never concatenate two full responses. |
| Size matches | A replacement has 100,000,003 bytes but one byte differs from the expected fingerprint | Keep it in failed or quarantined review and keep the previous trusted source. A correct length alone cannot make this copy ready. |
| Content matches | Full length and fingerprint match, but media inspection finds the last 30 seconds absent from the promised program | The transfer is byte-identical to its source. Record the capture discrepancy separately. The editor decides whether the incomplete program can be described and released. Another copy of the same bytes cannot restore the missing ending. |
| Duplicate completion | Two notifications describe the same remote revision and the same capture | Resolve one effect for the completion and one candidate master. Distinct transport attempts may remain visible to support. |
| Conflicting completion | The same sender message key now identifies different bytes | Quarantine the conflict. Preserve the verified asset and the earlier receipt. A genuinely corrected capture requires a new operation, provenance and editorial review. |
| Delivery selected | The church origin serves the test rendition but its private transcript is publicly retrievable | Fail the cutover. Retain the previously authorized route or display unavailability where it is no longer authorized. Retest download, subtitles, artwork and transcripts alongside video. |
| Recovery rehearsal | In an isolated environment, restore the preserved master and compare source fingerprint, duration, mapping, release state and rights withdrawal list | Record the independent recovery result. Keep network publishing disabled during the exercise. Only the operator's approved live cutover can change the public route. |
| Provider removal | The church approves deletion after a successful transfer | Evaluate holds, contractual retention, the independently verified recovery copy and any dependency still using the provider asset. Record request and confirmed completion independently. A timeout remains pending for the assigned custodian. |

## Cut a release and retime timed text

For this independent 60-second master, use half-open source intervals measured in milliseconds. Endpoints touching have zero overlap. The editor keeps [0,12000), [18000,30000) and [40000,60000) in that order. The result is 44,000 milliseconds. Map each retained interval to its start in the output, then add the source offset within that interval. The release must include a reviewed edited soundtrack, captions and descriptive metadata consistent with those boundaries.

| Source observation | Expected candidate edit | Release decision |
| --- | --- | --- |
| A cue occupies [11000,12000) | [11000,12000) | May retain after checking its exact surviving words. |
| A cue occupies [12000,18000) | No retained interval | No text, speaker hint, waveform label or chapter title from this removed cue can enter the public output. |
| A cue occupies [18000,19000) | [12000,13000) | Earliest retained frame after the first cut is at output offset 12000. |
| A cue occupies [29000,41000) | [23000,24000) and [24000,25000) | The fragments touch on the output clock but came from noncontiguous source material. A reviewer listens and rewrites text or splits cues before approving. Copying all original words into both fragments can disclose the removed passage. |
| A cue occupies [39000,40000) | No retained interval | A cue ending at the second retained boundary contributes no words. |
| A cue occupies [59500,60000) | [43500,44000) | The reviewed cue ends exactly at edition duration. |
| A caption is entered as [44000,44001) on the edited timeline | Beyond the edition | Reject the out-of-range edit with the edition reference and boundary. |
| Private contributor appears only in a removed interval | No surviving credit for this use | Check title, public contributors, still image and searchable text before approving a replacement. A person's presence in the master does not make their name publishable. |
| A viewer bookmarked source offset 35000 | The bookmarked instant is removed | Apply the church's documented revised-edition behavior and identify the change to the viewer. Do not seek outside the authorized edit or reveal what was cut. |

Record the master and edited edition separately. Set the edition's own duration, language and revision, point its renditions and timed text to it, and verify EditorialReview.reviewed_revision when authorizing release. Preserve the decision for the full source and for any independent audio-only, translated or members' version. A source-language withdrawal may reach translations, summaries and searchable text even when their file fingerprints differ.

## Withdraw an edition while storage is unavailable

1. Begin with one public church release, one members' release for a separately edited and cleared edition, and a paid download tied to the public edition. A rights reviewer withdraws future use of the public edition at 11:05. Its address is also in a syndication feed.
2. Block fresh delivery in controlled channels at the effective boundary. Record the affected releases and uses. Search and feed queries must consult current visibility until indexing catches up. A public title on an old cached listing cannot authorize a fresh media request.
3. Attempt the paid download after the boundary with an existing entitlement. The owner sees the approved unavailable/remedy route. Check existing playback grants against the architecture's actual revocation mechanism and record any exposure until previously issued access expires. Distinguish private purchaser notices from a public withdrawal explanation.
4. If storage or a remote distributor cannot acknowledge removal, retain the restriction at the church gateway, suspend unsafe routes, and leave that destination explicitly outstanding. Continue to permit the second edition only after tracing its sources and confirming its independent clearance.
5. Restore a snapshot taken at 11:00 to an isolated origin. Apply current authoritative withdrawals before enabling serving or outbound events. Replay the 11:05 withdrawal and reconcile the edition, derivative assets, feeds, search, access grants and customer remedies. One withdrawal gives one open remedy per affected purchase under the configured rules.
6. Close MediaWithdrawal.completed_at when the documented controllable actions and confirmations have completed or an accountable decision has recorded the treatment of a residual external limitation. A removal request, an acknowledged removal and an irrevocably downloaded copy are distinct observations to report.

[Media asset fields](../../implementation/commerce/MediaAsset.md) · [Timed text fields](../../implementation/commerce/TranscriptSegment.md) · [Withdrawal fields](../../implementation/commerce/MediaWithdrawal.md) · [Archives and custody](../../administration/archives.md)
