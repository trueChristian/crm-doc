# SpaceConflict

[Facilities, equipment and fleet](../../ministry/resources.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Undirected exclusion or shared-layout rule. Reserve a hall and prevent concurrent use of its partitioned halves, while independent halves can be reserved together. Canonicalize pair order, reject self-reference.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `space_id` | → FacilitySpace | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `other_space_id` | → FacilitySpace | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `conflict_kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `reason` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### space_id

The target is [FacilitySpace](FacilitySpace.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FacilitySpace·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FacilitySpace·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FacilitySpace·MISSING | Queue the missing FacilitySpace mapping or reject the command before linking. |
| Wrong scope | FacilitySpace·B01 | Do not attach another church’s FacilitySpace without a supported exchange and local authority. |
| Target rename | Rename FacilitySpace·A01 after linking | The existing space_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No space_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### other_space_id

The target is [FacilitySpace](FacilitySpace.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FacilitySpace·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FacilitySpace·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FacilitySpace·MISSING | Queue the missing FacilitySpace mapping or reject the command before linking. |
| Wrong scope | FacilitySpace·B01 | Do not attach another church’s FacilitySpace without a supported exchange and local authority. |
| Target rename | Rename FacilitySpace·A01 after linking | The existing other_space_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No other_space_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### conflict_kind

Use versioned classification or status code for `SpaceConflict.conflict_kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active conflict_kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped conflict_kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No conflict_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reason

Use human-readable text for `SpaceConflict.reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
