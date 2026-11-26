# RiteFieldDefinition

[Rites, milestones and register books](../../people/rites-and-milestones.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

A structured extension for denomination- and location-specific details such as place of burial or book page. Unique key per definition version; evaluate conditions only against declared fields.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `definition_id` | → RiteDefinition | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `field_key` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `label` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `value_type` | enum(text, date, year, code, boolean, number) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `allowed_values` | code set? | Optional under owner conditions | [list](../value-conventions.md#list) |
| `required_condition` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `visibility` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `ordering` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `RiteFieldDefinition.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiteFieldDefinition·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### definition_id

The target is [RiteDefinition](RiteDefinition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RiteDefinition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RiteDefinition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RiteDefinition·MISSING | Queue the missing RiteDefinition mapping or reject the command before linking. |
| Wrong scope | RiteDefinition·B01 | Do not attach another church’s RiteDefinition without a supported exchange and local authority. |
| Target rename | Rename RiteDefinition·A01 after linking | The existing definition_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No definition_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### field_key

Use versioned classification or status code for `RiteFieldDefinition.field_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active field_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped field_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No field_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### label

Use human-readable text for `RiteFieldDefinition.label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No label at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### value_type

Declared alternatives in owner order: `text`, `date`, `year`, `code`, `boolean`, `number`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | text | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_value_type | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No value_type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allowed_values

Use ordered collection or mathematical set for `RiteFieldDefinition.allowed_values`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Absent in intake | No allowed_values provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### required_condition

Use human-readable text for `RiteFieldDefinition.required_condition`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered required_condition in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No required_condition provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### visibility

Use versioned classification or status code for `RiteFieldDefinition.visibility`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active visibility code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped visibility code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No visibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ordering

Use whole-number measure for `RiteFieldDefinition.ordering`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No ordering at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [RiteFieldValue](RiteFieldValue.md).`field_definition_id` | RiteFieldDefinition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
