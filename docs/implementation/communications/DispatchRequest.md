# DispatchRequest

[Campaigns, audiences and content](../../communications/campaigns-and-content.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exactly one audience snapshot or channel publication target. Unique organization/purpose/dedupe key for the intended occurrence. A repeated request returns its existing id or conflicts when material inputs differ.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `organization_id` | Organization ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `campaign_id` | Campaign ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `owner_id` | UserAccount ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `initiating_actor_ref` | text | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `purpose_id` | CommunicationPurpose ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `origin_kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `origin_id` | opaque | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `origin_revision` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `dedupe_key` | opaque | Required when the record reaches its applicable state | [key](../value-conventions.md#key) |
| `audience_id` | AudienceSnapshot ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `publication_target_id` | ChannelPublicationTarget ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `source_template_id` | MessageTemplate ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `release_manifest` | approved editions | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `due_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `deadline_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `priority` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `fallback_policy` | ordered channel rules | Required when the record reaches its applicable state | [rule](../value-conventions.md#rule) |
| `state` | draft/review/approved/scheduled/processing/settled/cancelled | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### campaign_id

The target is [Campaign](Campaign.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Campaign·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Campaign·MISSING | Queue the missing Campaign mapping or reject the command before linking. |
| Wrong scope | Campaign·B01 | Do not attach another church’s Campaign without a supported exchange and local authority. |
| Target rename | Rename Campaign·A01 after linking | The existing campaign_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No campaign_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### owner_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing owner_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No owner_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### initiating_actor_ref

Use scoped or external reference for `DispatchRequest.initiating_actor_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified initiating_actor_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped initiating_actor_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No initiating_actor_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose_id

The target is [CommunicationPurpose](CommunicationPurpose.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CommunicationPurpose·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | CommunicationPurpose·MISSING | Queue the missing CommunicationPurpose mapping or reject the command before linking. |
| Wrong scope | CommunicationPurpose·B01 | Do not attach another church’s CommunicationPurpose without a supported exchange and local authority. |
| Target rename | Rename CommunicationPurpose·A01 after linking | The existing purpose_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No purpose_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### origin_kind

Use versioned classification or status code for `DispatchRequest.origin_kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active origin_kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped origin_kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No origin_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### origin_id

Use scoped or external reference for `DispatchRequest.origin_id`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified origin_id in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped origin_id | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No origin_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### origin_revision

Use human-readable text for `DispatchRequest.origin_revision`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered origin_revision in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No origin_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### dedupe_key

Use opaque identity or token for `DispatchRequest.dedupe_key`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DispatchRequest·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Incomplete record | No dedupe_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### audience_id

The target is [AudienceSnapshot](AudienceSnapshot.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AudienceSnapshot·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AudienceSnapshot·MISSING | Queue the missing AudienceSnapshot mapping or reject the command before linking. |
| Wrong scope | AudienceSnapshot·B01 | Do not attach another church’s AudienceSnapshot without a supported exchange and local authority. |
| Target rename | Rename AudienceSnapshot·A01 after linking | The existing audience_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No audience_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### publication_target_id

The target is [ChannelPublicationTarget](ChannelPublicationTarget.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ChannelPublicationTarget·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ChannelPublicationTarget·MISSING | Queue the missing ChannelPublicationTarget mapping or reject the command before linking. |
| Wrong scope | ChannelPublicationTarget·B01 | Do not attach another church’s ChannelPublicationTarget without a supported exchange and local authority. |
| Target rename | Rename ChannelPublicationTarget·A01 after linking | The existing publication_target_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No publication_target_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_template_id

The target is [MessageTemplate](MessageTemplate.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MessageTemplate·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MessageTemplate·MISSING | Queue the missing MessageTemplate mapping or reject the command before linking. |
| Wrong scope | MessageTemplate·B01 | Do not attach another church’s MessageTemplate without a supported exchange and local authority. |
| Target rename | Rename MessageTemplate·A01 after linking | The existing source_template_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No source_template_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### release_manifest

Use ordered collection or mathematical set for `DispatchRequest.release_manifest`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No release_manifest at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### due_at

Use unambiguous point in time for `DispatchRequest.due_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No due_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### deadline_at

Use unambiguous point in time for `DispatchRequest.deadline_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No deadline_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### priority

Use versioned classification or status code for `DispatchRequest.priority`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active priority code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped priority code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No priority at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fallback_policy

Use versioned structured decision or expression for `DispatchRequest.fallback_policy`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for fallback_policy | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in fallback_policy | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No fallback_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `draft`, `review`, `approved`, `scheduled`, `processing`, `settled`, `cancelled`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [Delivery](Delivery.md).`dispatch_id` | DispatchRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DigestEdition](DigestEdition.md).`dispatch_id` | DispatchRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DispatchRecipient](DispatchRecipient.md).`dispatch_id` | DispatchRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentBulletin](IncidentBulletin.md).`dispatch_id` | DispatchRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MeetingNotice](../governance/MeetingNotice.md).`dispatch_request_id` | DispatchRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PrintBatch](PrintBatch.md).`dispatch_id` | DispatchRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PublicationApproval](PublicationApproval.md).`dispatch_id` | DispatchRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReminderInstance](ReminderInstance.md).`dispatch_id` | DispatchRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StewardshipAction](../development/StewardshipAction.md).`dispatch_ref` | DispatchRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
