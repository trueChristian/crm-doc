# RiteFieldValue

[Rites, milestones and register books](../../people/rites-and-milestones.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One value per rite and field unless repetition is explicitly configured. The definition must belong to the rite's version.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `rite_id` | → RiteRecord | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `field_definition_id` | → RiteFieldDefinition | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `value` | typed according to definition | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `RiteFieldValue.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiteFieldValue·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### rite_id

The target is [RiteRecord](RiteRecord.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiteRecord·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | RiteRecord·MISSING | Queue the missing RiteRecord mapping or reject the command before linking. |
| Wrong scope | RiteRecord·B01 | Do not attach another church’s RiteRecord without a supported exchange and local authority. |
| Target rename | Rename RiteRecord·A01 after linking | The existing rite_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No rite_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### field_definition_id

The target is [RiteFieldDefinition](RiteFieldDefinition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiteFieldDefinition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | RiteFieldDefinition·MISSING | Queue the missing RiteFieldDefinition mapping or reject the command before linking. |
| Wrong scope | RiteFieldDefinition·B01 | Do not attach another church’s RiteFieldDefinition without a supported exchange and local authority. |
| Target rename | Rename RiteFieldDefinition·A01 after linking | The existing field_definition_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No field_definition_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### value

Use typed value or bounded compound record for `RiteFieldValue.value`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of value matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for value | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
