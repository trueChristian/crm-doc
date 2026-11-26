# Offline capture and synchronization

Rural campuses, temporary venues and home visits may lose connectivity during an activity. The organizer requests a short-lived pack for one activity and one device. It includes an explicit maximum offline duration, data list, end time and instructions for using paper or staffed support when freshness matters. A pack is optional and cannot become the primary source of eligibility, balances, emergency restrictions or current permissions.

## Logical records

| Entity | Fields | Relationship and constraint |
|---|---|---|
| RegisteredDevice | device_key opaque, assigned_to Ref(UserAccount), scope_ref ResourceRef, local_protection_state code, last_seen_at instant?, revoked_at instant?, lost_at instant? | Bind a device to an operator and scope. Shared devices need a new session when reassigned. |
| OfflinePack | device_id Ref(RegisteredDevice), activity_ref ResourceRef, prepared_for Ref(UserAccount), policy_revision integer, source_cutoff instant, permission_revision integer, permitted_operations set(code), field_manifest set(code), expires_at instant, last_ack_at instant?, state code | One scope and purpose per pack. Permission and data freshness have independent cutoffs. |
| OfflineItem | pack_id Ref(OfflinePack), item_ref ResourceRef, base_revision integer, allowed_fields set(code), classification code, erase_after instant | Unique pack/item. Exclude unrelated household contacts, donors, confidential notes and mixed-visibility attachments. |
| LocalChange | pack_id Ref(OfflinePack), operation_key opaque, sequence_no integer, actor_id Ref(UserAccount), target_ref ResourceRef?, temporary_key opaque?, operation_kind code, base_revision integer?, captured_at instant, payload_ref ResourceRef, dependency_keys set(opaque), result code | Unique operation key survives retries. Capture sequence separately from untrusted device time. |
| SyncAttempt | pack_id Ref(OfflinePack), started_at instant, completed_at instant?, acknowledged_through integer?, result code, accepted_count integer, rejected_count integer, conflict_count integer | Checkpoint only operations whose individual status is known. A finished attempt may contain review items. |
| SyncConflict | change_id Ref(LocalChange), current_revision integer?, conflict_kind code, proposed_fields set(code), assigned_to Ref(UserAccount), state code, disposition code?, decision_at instant?, reason text? | One open conflict per operation. Record resolution as a new authoritative command. |
| TemporaryLink | pack_id Ref(OfflinePack), temporary_key opaque, canonical_ref ResourceRef, resolved_at instant | Unique temporary key per pack. Link later submissions to the accepted canonical identity. |

## What can proceed

| Activity | Offline behavior | Reconnection decision |
|---|---|---|
| Attendance and headcount | Record provisional arrival with group, occurrence and observer. Show locally observed, awaiting sync and confirmed as distinct states. | Dedupe by occurrence, attendee and attendance type. Two observations can support one attendance fact. |
| New visitor or contact correction | Capture the minimum volunteered fields and notice edition. Queue same-device dependent facts under a temporary key. | Revalidate purpose, person match, current field rights and later edits. Queue unresolved matches for a steward. |
| Volunteer roster | View the permitted snapshot with “as of” time and accept a provisional response. | Confirm role, slot capacity, eligibility and overlap against current assignments. |
| Privileged access, financial posting or creating paid rights | Display staff fallback instructions only. | Online review must authorize and commit the official operation. No silent acceptance from queued input. |
| Child release or emergency restriction | Offline viewing cannot verify newly changed clearance. Staff use the church's documented supervised fallback and record evidence through the authorized procedure. | Record actual decision and time with source, reviewer and incident linkage. A stale pack cannot authorize release. |

## Synchronization rules

Issue packs only to authorized devices with protected local storage. Download a manifest and verify its completeness before showing ready. In disconnected mode, show expiry, last update, what can be done and where to obtain assistance. Disable restricted actions at expiry. A reported lost device is immediately barred from future access; local revocation can only be enforced once received or through the short local expiry. Open a supervised incident if exposure is possible.

Reconnect under a fresh authenticated session and verify that user, device, pack, organization and operation remain permitted. Forward operations in dependency order; return accepted, duplicate, conflict, rejected or retry-later per operation. Return canonical IDs for accepted provisional identities. Do not advance the durable checkpoint over a missing result. Failed validation or expired authority goes to review with the original observation preserved according to policy. Staff may record an observation as a separate authorized action after review.

Independent additions with matching identity and business keys can coalesce; exact repeats return the prior result. Conflicting changes to the same effective contact, status, custody or availability require a human decision. Never choose a winner solely from a device timestamp. Redact fields that have become restricted from review diffs. A denied reviewer can route a conflict without reading the protected values. On confirmed ingestion, erase local records when their pack's policy allows; erase expired content on launch and reconnection. Log outstanding device acknowledgements and withdraw downloadable packs after an incident.

## Acceptance

- Two ushers mark the same attendee on separate devices. Reports show one attendance with two observations. Distinct visitors with similar names remain separate until reviewed.
- A device disconnects after an upload succeeds but before acknowledgment. Reconnection returns the prior canonical record, and dependent attendance attaches to the same person.
- A secretary corrects an address while another user edits it offline. Both proposals and the base revision reach a suitably authorized reviewer; preservation of the newer address is independent of device clocks.
- A device is lost and its grant revoked. Server access ends immediately. Unconfirmed local cleanup remains visible in the incident record until expiry or a device acknowledgement.
- An operator opens an expired pack during child collection. The screen identifies the supervised fallback and records no authorized pickup from stale data.
