# AudienceSnapshot

[Campaigns, audiences and content](../../communications/campaigns-and-content.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Freeze the release audience with its source revisions. Added people require a separately authorized supplemental dispatch.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `definition_id` | AudienceDefinition ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `definition_edition` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `as_of` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `built_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `built_by` | UserAccount ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `scope_revision` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `eligible_count` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `excluded_count` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `state` | working/frozen/expired | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### definition_id

The target is [AudienceDefinition](AudienceDefinition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AudienceDefinition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AudienceDefinition·MISSING | Queue the missing AudienceDefinition mapping or reject the command before linking. |
| Wrong scope | AudienceDefinition·B01 | Do not attach another church’s AudienceDefinition without a supported exchange and local authority. |
| Target rename | Rename AudienceDefinition·A01 after linking | The existing definition_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No definition_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### definition_edition

Use whole-number measure for `AudienceSnapshot.definition_edition`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No definition_edition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### as_of

Use unambiguous point in time for `AudienceSnapshot.as_of`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No as_of at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### built_at

Use unambiguous point in time for `AudienceSnapshot.built_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No built_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### built_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing built_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No built_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### scope_revision

Use human-readable text for `AudienceSnapshot.scope_revision`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered scope_revision in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No scope_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligible_count

Use whole-number measure for `AudienceSnapshot.eligible_count`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No eligible_count at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### excluded_count

Use whole-number measure for `AudienceSnapshot.excluded_count`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No excluded_count at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `working`, `frozen`, `expired`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | working | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AppealChannel](../development/AppealChannel.md).`audience_ref` | AudienceSnapshot identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AudienceEntry](AudienceEntry.md).`snapshot_id` | AudienceSnapshot identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DispatchRequest](DispatchRequest.md).`audience_id` | AudienceSnapshot identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PublicationApproval](PublicationApproval.md).`snapshot_id` | AudienceSnapshot identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
