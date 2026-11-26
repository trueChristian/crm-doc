# PublicationApproval

[Campaigns, audiences and content](../../communications/campaigns-and-content.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Scope approval to sender, channel targets, audience, content, schedule, cost threshold and purpose. Material changes require renewed approval.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `dispatch_id` | DispatchRequest ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `edition_ids` | identifier list | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `snapshot_id` | AudienceSnapshot ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `reviewer_id` | UserAccount ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `decision` | release/return/withdraw | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `decided_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `signed_preview_digest` | text | Required when the record reaches its applicable state | [digest](../value-conventions.md#digest) |
| `reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### dispatch_id

The target is [DispatchRequest](DispatchRequest.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DispatchRequest·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | DispatchRequest·MISSING | Queue the missing DispatchRequest mapping or reject the command before linking. |
| Wrong scope | DispatchRequest·B01 | Do not attach another church’s DispatchRequest without a supported exchange and local authority. |
| Target rename | Rename DispatchRequest·A01 after linking | The existing dispatch_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No dispatch_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### edition_ids

Use ordered collection or mathematical set for `PublicationApproval.edition_ids`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No edition_ids at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### snapshot_id

The target is [AudienceSnapshot](AudienceSnapshot.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AudienceSnapshot·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AudienceSnapshot·MISSING | Queue the missing AudienceSnapshot mapping or reject the command before linking. |
| Wrong scope | AudienceSnapshot·B01 | Do not attach another church’s AudienceSnapshot without a supported exchange and local authority. |
| Target rename | Rename AudienceSnapshot·A01 after linking | The existing snapshot_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No snapshot_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reviewer_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No reviewer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision

Declared alternatives in owner order: `release`, `return`, `withdraw`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | release | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_decision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No decision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decided_at

Use unambiguous point in time for `PublicationApproval.decided_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No decided_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### signed_preview_digest

Use integrity fingerprint or opaque verifier for `PublicationApproval.signed_preview_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Incomplete record | No signed_preview_digest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reason

Use human-readable text for `PublicationApproval.reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
