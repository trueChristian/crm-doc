# CeremonyParty

[Weddings, funerals, memorials and cemetery administration](../../administration/life-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Offices and relationships belong to this ceremony only. A witness does not gain access to the other participants' records.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `request_id` | → CeremonyRequest | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `person_id` | optional Person | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `name_as_recorded` | text | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `role` | subject, representative, officiant, witness or contact | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `authority_evidence_ref` | optional | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `publication_permission_ref` | optional | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `CeremonyParty.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CeremonyParty·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### request_id

The target is [CeremonyRequest](CeremonyRequest.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CeremonyRequest·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CeremonyRequest·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CeremonyRequest·MISSING | Queue the missing CeremonyRequest mapping or reject the command before linking. |
| Wrong scope | CeremonyRequest·B01 | Do not attach another church’s CeremonyRequest without a supported exchange and local authority. |
| Target rename | Rename CeremonyRequest·A01 after linking | The existing request_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No request_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### person_id

Use scoped or external reference for `CeremonyParty.person_id`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified person_id in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped person_id | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### name_as_recorded

Use human-readable text for `CeremonyParty.name_as_recorded`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered name_as_recorded in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No name_as_recorded at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### role

Declared alternatives in owner order: `subject`, `representative`, `officiant`, `witness`, `contact`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | subject | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_role | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authority_evidence_ref

Use scoped or external reference for `CeremonyParty.authority_evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified authority_evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped authority_evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No authority_evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### publication_permission_ref

Use scoped or external reference for `CeremonyParty.publication_permission_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified publication_permission_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped publication_permission_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No publication_permission_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
