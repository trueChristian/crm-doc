# LiveSession

[Sermon library and publication](../../commerce/media.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Concurrent sessions keep isolated source credentials, audience, archive and notices. A late callback cannot reopen an ended session.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `delivery_id` | ref SermonDelivery | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `expected_start` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `expected_end` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `producer_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `source_label` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `audience_policy_ref` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `live_rights_ref` | ref MediaRights | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `recording_allowed` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `state` | scheduled/testing/live/interrupted/ended/cancelled | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `private_recording_ref` | ref MediaAsset? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### delivery_id

The target is [SermonDelivery](SermonDelivery.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SermonDelivery·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | SermonDelivery·MISSING | Queue the missing SermonDelivery mapping or reject the command before linking. |
| Wrong scope | SermonDelivery·B01 | Do not attach another church’s SermonDelivery without a supported exchange and local authority. |
| Target rename | Rename SermonDelivery·A01 after linking | The existing delivery_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No delivery_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expected_start

Use unambiguous point in time for `LiveSession.expected_start`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No expected_start at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expected_end

Use unambiguous point in time for `LiveSession.expected_end`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No expected_end provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### producer_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing producer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No producer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_label

Use human-readable text for `LiveSession.source_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered source_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No source_label at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### audience_policy_ref

Use scoped or external reference for `LiveSession.audience_policy_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified audience_policy_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped audience_policy_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No audience_policy_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### live_rights_ref

The target is [MediaRights](MediaRights.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MediaRights·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MediaRights·MISSING | Queue the missing MediaRights mapping or reject the command before linking. |
| Wrong scope | MediaRights·B01 | Do not attach another church’s MediaRights without a supported exchange and local authority. |
| Target rename | Rename MediaRights·A01 after linking | The existing live_rights_ref keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No live_rights_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recording_allowed

Use explicit logical choice for `LiveSession.recording_allowed`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No recording_allowed at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `scheduled`, `testing`, `live`, `interrupted`, `ended`, `cancelled`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | scheduled | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### private_recording_ref

The target is [MediaAsset](MediaAsset.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MediaAsset·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MediaAsset·MISSING | Queue the missing MediaAsset mapping or reject the command before linking. |
| Wrong scope | MediaAsset·B01 | Do not attach another church’s MediaAsset without a supported exchange and local authority. |
| Target rename | Rename MediaAsset·A01 after linking | The existing private_recording_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No private_recording_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
