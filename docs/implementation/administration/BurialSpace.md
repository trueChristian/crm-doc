# BurialSpace

[Weddings, funerals, memorials and cemetery administration](../../administration/life-events.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique mapped position within a ground. A memorial panel, an urn niche and a grave have configurable capacity and different rights.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `ground_id` | → BurialGround | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `section` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `plot_reference` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `space_kind` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [vocab](../value-conventions.md#vocab) |
| `capacity` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [integer](../value-conventions.md#integer) |
| `accessibility_notes` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `condition` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `BurialSpace.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | BurialSpace·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### ground_id

The target is [BurialGround](BurialGround.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | BurialGround·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | BurialGround·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | BurialGround·MISSING | Queue the missing BurialGround mapping or reject the command before linking. |
| Wrong scope | BurialGround·B01 | Do not attach another church’s BurialGround without a supported exchange and local authority. |
| Target rename | Rename BurialGround·A01 after linking | The existing ground_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No ground_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### section

Use typed value or bounded compound record for `BurialSpace.section`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of section matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for section | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No section at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### plot_reference

Use typed value or bounded compound record for `BurialSpace.plot_reference`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of plot_reference matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for plot_reference | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No plot_reference at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### space_kind

Use versioned classification or status code for `BurialSpace.space_kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active space_kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped space_kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No space_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### capacity

Use whole-number measure for `BurialSpace.capacity`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No capacity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### accessibility_notes

Use human-readable text for `BurialSpace.accessibility_notes`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered accessibility_notes in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No accessibility_notes at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### condition

Use typed value or bounded compound record for `BurialSpace.condition`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of condition matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for condition | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No condition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [BurialRight](BurialRight.md).`space_id` | BurialSpace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IntermentRecord](IntermentRecord.md).`space_id` | BurialSpace identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
