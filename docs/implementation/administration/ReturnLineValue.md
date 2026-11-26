# ReturnLineValue

[Dated rolls, denominational returns and annual reports](../../administration/annual-returns.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique instance and line. Manual override requires authority, reason and original computed result. Permission to view the return need not include drill-through to individuals.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `instance_id` | → ReturnInstance | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `line_id` | → ReturnLineDefinition | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `computed_value` | typed | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `reported_value` | typed | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `numerator` | optional | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `denominator` | optional | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `quality` | verified, estimate, incomplete, suppressed or unavailable | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `variance_explanation` | optional | Optional under owner conditions | [text](../value-conventions.md#text) |
| `source_snapshot_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ReturnLineValue.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReturnLineValue·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### instance_id

The target is [ReturnInstance](ReturnInstance.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReturnInstance·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ReturnInstance·MISSING | Queue the missing ReturnInstance mapping or reject the command before linking. |
| Wrong scope | ReturnInstance·B01 | Do not attach another church’s ReturnInstance without a supported exchange and local authority. |
| Target rename | Rename ReturnInstance·A01 after linking | The existing instance_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No instance_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### line_id

The target is [ReturnLineDefinition](ReturnLineDefinition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReturnLineDefinition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ReturnLineDefinition·MISSING | Queue the missing ReturnLineDefinition mapping or reject the command before linking. |
| Wrong scope | ReturnLineDefinition·B01 | Do not attach another church’s ReturnLineDefinition without a supported exchange and local authority. |
| Target rename | Rename ReturnLineDefinition·A01 after linking | The existing line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### computed_value

Use typed value or bounded compound record for `ReturnLineValue.computed_value`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of computed_value matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for computed_value | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No computed_value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reported_value

Use typed value or bounded compound record for `ReturnLineValue.reported_value`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of reported_value matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for reported_value | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No reported_value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### numerator

Use exact decimal measure for `ReturnLineValue.numerator`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No numerator provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### denominator

Use exact decimal measure for `ReturnLineValue.denominator`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No denominator provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### quality

Declared alternatives in owner order: `verified`, `estimate`, `incomplete`, `suppressed`, `unavailable`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_quality | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No quality at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### variance_explanation

Use human-readable text for `ReturnLineValue.variance_explanation`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered variance_explanation in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No variance_explanation provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_snapshot_ref

Use scoped or external reference for `ReturnLineValue.source_snapshot_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified source_snapshot_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped source_snapshot_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No source_snapshot_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
