# PlaybackSession

[Subscriptions, grants and playback](../../commerce/access.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Permit guest sessions only for eligible public releases. Finite concurrency leases reclaim disconnected sessions after a defined timeout. Continuing sessions recheck restrictive changes within the declared revocation window.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `grant_id` | ref AccessGrant? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `release_id` | ref MediaRelease | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `beneficiary_account_id` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `started_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `last_seen_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `expires_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `revoked_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `session_fingerprint` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `purpose` | preview/stream/download | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### grant_id

The target is [AccessGrant](AccessGrant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessGrant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AccessGrant·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AccessGrant·MISSING | Queue the missing AccessGrant mapping or reject the command before linking. |
| Wrong scope | AccessGrant·B01 | Do not attach another church’s AccessGrant without a supported exchange and local authority. |
| Target rename | Rename AccessGrant·A01 after linking | The existing grant_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No grant_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### release_id

The target is [MediaRelease](MediaRelease.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MediaRelease·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MediaRelease·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MediaRelease·MISSING | Queue the missing MediaRelease mapping or reject the command before linking. |
| Wrong scope | MediaRelease·B01 | Do not attach another church’s MediaRelease without a supported exchange and local authority. |
| Target rename | Rename MediaRelease·A01 after linking | The existing release_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No release_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### beneficiary_account_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing beneficiary_account_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No beneficiary_account_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### started_at

Use unambiguous point in time for `PlaybackSession.started_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No started_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### last_seen_at

Use unambiguous point in time for `PlaybackSession.last_seen_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No last_seen_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### expires_at

Use unambiguous point in time for `PlaybackSession.expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No expires_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revoked_at

Use unambiguous point in time for `PlaybackSession.revoked_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No revoked_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### session_fingerprint

Use integrity fingerprint or opaque verifier for `PlaybackSession.session_fingerprint`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No session_fingerprint at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose

Declared alternatives in owner order: `preview`, `stream`, `download`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | preview | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_purpose | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
