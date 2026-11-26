# SeriesSermon

[Sermon library and publication](../../commerce/media.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Many-to-many. Deterministic order. A private item cannot appear as a revealing gap with title in a public list.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `series_id` | ref SermonSeries | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sermon_id` | ref Sermon | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sequence_number` | integer? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `label` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### series_id

The target is [SermonSeries](SermonSeries.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SermonSeries·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SermonSeries·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SermonSeries·MISSING | Queue the missing SermonSeries mapping or reject the command before linking. |
| Wrong scope | SermonSeries·B01 | Do not attach another church’s SermonSeries without a supported exchange and local authority. |
| Target rename | Rename SermonSeries·A01 after linking | The existing series_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No series_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sermon_id

The target is [Sermon](Sermon.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Sermon·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Sermon·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Sermon·MISSING | Queue the missing Sermon mapping or reject the command before linking. |
| Wrong scope | Sermon·B01 | Do not attach another church’s Sermon without a supported exchange and local authority. |
| Target rename | Rename Sermon·A01 after linking | The existing sermon_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No sermon_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sequence_number

Use whole-number measure for `SeriesSermon.sequence_number`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No sequence_number provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### label

Use human-readable text for `SeriesSermon.label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No label provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
