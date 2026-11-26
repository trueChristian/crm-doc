# ArchiveItem

[Documents, archives, certificates and custody](../../administration/archives.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Accession code unique in issuing organization. Uncertain dates display as uncertain. Retain a tombstone after authorized disposal where policy permits.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `collection_id` | → ArchiveCollection | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `accession_code` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [vocab](../value-conventions.md#vocab) |
| `title` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `description` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `record_kind` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [vocab](../value-conventions.md#vocab) |
| `date_value` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `date_precision` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `originator` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `related_record_type` | optional code | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `related_record_id` | optional reference | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `access_class_override` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `physical_location` | optional | Optional under owner conditions | [structured](../value-conventions.md#structured) |
| `state` | active, loaned, missing, transferred, disposed | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ArchiveItem.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ArchiveItem·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### collection_id

The target is [ArchiveCollection](ArchiveCollection.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ArchiveCollection·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ArchiveCollection·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ArchiveCollection·MISSING | Queue the missing ArchiveCollection mapping or reject the command before linking. |
| Wrong scope | ArchiveCollection·B01 | Do not attach another church’s ArchiveCollection without a supported exchange and local authority. |
| Target rename | Rename ArchiveCollection·A01 after linking | The existing collection_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No collection_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### accession_code

Use versioned classification or status code for `ArchiveItem.accession_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active accession_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped accession_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No accession_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `ArchiveItem.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### description

Use human-readable text for `ArchiveItem.description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### record_kind

Use versioned classification or status code for `ArchiveItem.record_kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active record_kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped record_kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No record_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### date_value

Use typed value or bounded compound record for `ArchiveItem.date_value`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of date_value matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for date_value | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No date_value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### date_precision

Use typed value or bounded compound record for `ArchiveItem.date_precision`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of date_precision matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for date_precision | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No date_precision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### originator

Use typed value or bounded compound record for `ArchiveItem.originator`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of originator matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for originator | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No originator at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### related_record_type

Use versioned classification or status code for `ArchiveItem.related_record_type`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active related_record_type code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped related_record_type code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No related_record_type provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### related_record_id

Use scoped or external reference for `ArchiveItem.related_record_id`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified related_record_id in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped related_record_id | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No related_record_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### access_class_override

Use typed value or bounded compound record for `ArchiveItem.access_class_override`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of access_class_override matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for access_class_override | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No access_class_override at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### physical_location

Use typed value or bounded compound record for `ArchiveItem.physical_location`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of physical_location matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for physical_location | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Absent in intake | No physical_location provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `active`, `loaned`, `missing`, `transferred`, `disposed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [ArchiveCopy](ArchiveCopy.md).`item_id` | ArchiveItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DocumentIssue](DocumentIssue.md).`item_id` | ArchiveItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
