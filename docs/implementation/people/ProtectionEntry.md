# ProtectionEntry

[Safeguarding concerns and protected disclosure](../../people/safeguarding-and-disclosure.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Factual chronology distinguishes reported facts, direct observations and opinion. Corrections append; source and previous wording remain identifiable to authorized reviewers.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `case_id` | → ProtectionCase | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `kind` | enum(disclosure, direct_observation, third_party_account, action, professional_opinion, correction) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `source_party_id` | → ProtectionParty? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `text` | restricted text | Required when the record reaches its applicable state | [protected](../value-conventions.md#protected) |
| `event_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `recorded_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `recorded_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `corrects_id` | → ProtectionEntry? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `document_ref` | restricted ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ProtectionEntry.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProtectionEntry·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### case_id

The target is [ProtectionCase](ProtectionCase.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProtectionCase·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProtectionCase·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProtectionCase·MISSING | Queue the missing ProtectionCase mapping or reject the command before linking. |
| Wrong scope | ProtectionCase·B01 | Do not attach another church’s ProtectionCase without a supported exchange and local authority. |
| Target rename | Rename ProtectionCase·A01 after linking | The existing case_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No case_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `disclosure`, `direct_observation`, `third_party_account`, `action`, `professional_opinion`, `correction`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | disclosure | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_party_id

The target is [ProtectionParty](ProtectionParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProtectionParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProtectionParty·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProtectionParty·MISSING | Queue the missing ProtectionParty mapping or reject the command before linking. |
| Wrong scope | ProtectionParty·B01 | Do not attach another church’s ProtectionParty without a supported exchange and local authority. |
| Target rename | Rename ProtectionParty·A01 after linking | The existing source_party_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No source_party_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### text

Use restricted value or protected content reference for `ProtectionEntry.text`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted text supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Incomplete record | No text at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### event_at

Use unambiguous point in time for `ProtectionEntry.event_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No event_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recorded_at

Use unambiguous point in time for `ProtectionEntry.recorded_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No recorded_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recorded_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing recorded_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No recorded_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### corrects_id

The target is [ProtectionEntry](ProtectionEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProtectionEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProtectionEntry·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProtectionEntry·MISSING | Queue the missing ProtectionEntry mapping or reject the command before linking. |
| Wrong scope | ProtectionEntry·B01 | Do not attach another church’s ProtectionEntry without a supported exchange and local authority. |
| Target rename | Rename ProtectionEntry·A01 after linking | The existing corrects_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No corrects_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### document_ref

Use scoped or external reference for `ProtectionEntry.document_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified document_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped document_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No document_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [ProtectionEntry](ProtectionEntry.md).`corrects_id` | ProtectionEntry identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
