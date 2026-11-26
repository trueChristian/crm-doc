# OrganizationChangeUnit

[Churches, congregations, campuses and governing networks](../../foundation/organization.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique combination per change. Mapping is lineage only. A person, room booking or journal entry is reassigned by its own owner with separate evidence.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `change_id` | → OrganizationChange | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `unit_kind` | organization, congregation or campus | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `unit_id` | matching ref | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `role` | predecessor, successor or affected | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### change_id

The target is [OrganizationChange](OrganizationChange.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrganizationChange·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrganizationChange·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrganizationChange·MISSING | Queue the missing OrganizationChange mapping or reject the command before linking. |
| Wrong scope | OrganizationChange·B01 | Do not attach another church’s OrganizationChange without a supported exchange and local authority. |
| Target rename | Rename OrganizationChange·A01 after linking | The existing change_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No change_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit_kind

Declared alternatives in owner order: `organization`, `congregation`, `campus`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | organization | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_unit_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No unit_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit_id

Use scoped or external reference for `OrganizationChangeUnit.unit_id`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified unit_id in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped unit_id | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No unit_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### role

Declared alternatives in owner order: `predecessor`, `successor`, `affected`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | predecessor | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_role | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
