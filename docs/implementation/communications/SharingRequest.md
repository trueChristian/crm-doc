# SharingRequest

[Community communication](../../communications/community-communication.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Submission and permission to distribute are different steps. A submitter cannot authorize naming a third person by default. Provide a private submission and response option.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `organization_id` | Organization ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `submitted_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `subject_person_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `representation_id` | RepresentationAuthority ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `topic` | prayer/testimony/celebration/community_need | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `original_text` | restricted text | Required when the record reaches its applicable state | [protected](../value-conventions.md#protected) |
| `requested_audience` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `requested_until` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `received_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `state` | private/review/approved/withdrawn/expired | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

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

### submitted_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing submitted_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No submitted_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### subject_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing subject_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No subject_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### representation_id

The target is [RepresentationAuthority](../people/RepresentationAuthority.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RepresentationAuthority·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | RepresentationAuthority·MISSING | Queue the missing RepresentationAuthority mapping or reject the command before linking. |
| Wrong scope | RepresentationAuthority·B01 | Do not attach another church’s RepresentationAuthority without a supported exchange and local authority. |
| Target rename | Rename RepresentationAuthority·A01 after linking | The existing representation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No representation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### topic

Declared alternatives in owner order: `prayer`, `testimony`, `celebration`, `community_need`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | prayer | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_topic | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No topic at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### original_text

Use restricted value or protected content reference for `SharingRequest.original_text`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted original_text supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Incomplete record | No original_text at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_audience

Use versioned classification or status code for `SharingRequest.requested_audience`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active requested_audience code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped requested_audience code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No requested_audience at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_until

Use civil calendar date for `SharingRequest.requested_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No requested_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### received_at

Use unambiguous point in time for `SharingRequest.received_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No received_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `private`, `review`, `approved`, `withdrawn`, `expired`. Approval and lifecycle guards still apply to transitions.
Field access: enforce the declared protection on reads, search, previews, exports and audit evidence as well as the underlying enum value.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | private | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [SharingRelease](SharingRelease.md).`request_id` | SharingRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
