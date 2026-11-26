# CareNote

[Pastoral care, prayer and continuity](../../people/pastoral-care.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Signed case notes are amended with a linked correction. Access, print and export are audited with purpose. Irrelevant details should not enter the church record.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `case_id` | → CareCase | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `author_id` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `recorded_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `effective_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `classification` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `text` | restricted text | Required when the record reaches its applicable state | [protected](../value-conventions.md#protected) |
| `permitted_purpose` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `supersedes_id` | → CareNote? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `CareNote.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CareNote·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### case_id

The target is [CareCase](CareCase.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CareCase·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CareCase·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CareCase·MISSING | Queue the missing CareCase mapping or reject the command before linking. |
| Wrong scope | CareCase·B01 | Do not attach another church’s CareCase without a supported exchange and local authority. |
| Target rename | Rename CareCase·A01 after linking | The existing case_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No case_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### author_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing author_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No author_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recorded_at

Use unambiguous point in time for `CareNote.recorded_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No recorded_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_on

Use civil calendar date for `CareNote.effective_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No effective_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### classification

Use versioned classification or status code for `CareNote.classification`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active classification code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped classification code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No classification at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### text

Use restricted value or protected content reference for `CareNote.text`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted text supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Incomplete record | No text at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### permitted_purpose

Use versioned classification or status code for `CareNote.permitted_purpose`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active permitted_purpose code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped permitted_purpose code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No permitted_purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### supersedes_id

The target is [CareNote](CareNote.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CareNote·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CareNote·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CareNote·MISSING | Queue the missing CareNote mapping or reject the command before linking. |
| Wrong scope | CareNote·B01 | Do not attach another church’s CareNote without a supported exchange and local authority. |
| Target rename | Rename CareNote·A01 after linking | The existing supersedes_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No supersedes_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CareNote](CareNote.md).`supersedes_id` | CareNote identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
