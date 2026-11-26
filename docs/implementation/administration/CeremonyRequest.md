# CeremonyRequest

[Weddings, funerals, memorials and cemetery administration](../../administration/life-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Can include multiple persons and one or more occurrences. A payment confirms a fee; an officiant records whether the ceremony took place.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `organization_id` | → Organization | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `type` | wedding, funeral, memorial, dedication or other configured service | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `requested_by_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `private_contact_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `preferred_dates` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `congregation_id` | → Congregation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `coordinator_id` | → Person | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `state` | enquiry, assessing, approved, scheduled, completed, cancelled or declined | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `responsible_payer_ref` | optional | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `CeremonyRequest.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CeremonyRequest·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Organization·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### type

Declared alternatives in owner order: `wedding`, `funeral`, `memorial`, `dedication`, `other configured service`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | wedding | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_type | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_by_ref

Use scoped or external reference for `CeremonyRequest.requested_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified requested_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped requested_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No requested_by_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### private_contact_ref

Use scoped or external reference for `CeremonyRequest.private_contact_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified private_contact_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped private_contact_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No private_contact_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### preferred_dates

Use typed value or bounded compound record for `CeremonyRequest.preferred_dates`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of preferred_dates matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for preferred_dates | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No preferred_dates at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### congregation_id

The target is [Congregation](../foundation/Congregation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Congregation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Congregation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Congregation·MISSING | Queue the missing Congregation mapping or reject the command before linking. |
| Wrong scope | Congregation·B01 | Do not attach another church’s Congregation without a supported exchange and local authority. |
| Target rename | Rename Congregation·A01 after linking | The existing congregation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No congregation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### coordinator_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing coordinator_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No coordinator_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `enquiry`, `assessing`, `approved`, `scheduled`, `completed`, `cancelled`, `declined`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | enquiry | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### responsible_payer_ref

Use scoped or external reference for `CeremonyRequest.responsible_payer_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified responsible_payer_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped responsible_payer_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No responsible_payer_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CeremonyBooking](CeremonyBooking.md).`request_id` | CeremonyRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CeremonyParty](CeremonyParty.md).`request_id` | CeremonyRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CeremonyRequirement](CeremonyRequirement.md).`request_id` | CeremonyRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IntermentRecord](IntermentRecord.md).`ceremony_ref` | CeremonyRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MemorialTribute](MemorialTribute.md).`request_id` | CeremonyRequest identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
