# MinuteItem

[Minutes, resolutions and the archive](../../governance/minutes-and-resolutions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Supports business added from the floor, with an authority note. Collect only the discussion detail the adopted policy permits. Closed material can have an independently reviewed extract.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `edition_id` | MinuteEdition ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `agenda_item_id` | AgendaItem ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `sequence` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `heading` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `discussion_summary` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `decision_text` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `disclosure_class` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `chair_statement` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `decision_round_id` | DecisionRound ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `recusal_public_text` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### edition_id

The target is [MinuteEdition](MinuteEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinuteEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinuteEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinuteEdition·MISSING | Queue the missing MinuteEdition mapping or reject the command before linking. |
| Wrong scope | MinuteEdition·B01 | Do not attach another church’s MinuteEdition without a supported exchange and local authority. |
| Target rename | Rename MinuteEdition·A01 after linking | The existing edition_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No edition_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### agenda_item_id

The target is [AgendaItem](AgendaItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AgendaItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AgendaItem·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AgendaItem·MISSING | Queue the missing AgendaItem mapping or reject the command before linking. |
| Wrong scope | AgendaItem·B01 | Do not attach another church’s AgendaItem without a supported exchange and local authority. |
| Target rename | Rename AgendaItem·A01 after linking | The existing agenda_item_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No agenda_item_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### sequence

Use whole-number measure for `MinuteItem.sequence`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No sequence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### heading

Use human-readable text for `MinuteItem.heading`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered heading in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No heading at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### discussion_summary

Use human-readable text for `MinuteItem.discussion_summary`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered discussion_summary in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No discussion_summary provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### decision_text

Use human-readable text for `MinuteItem.decision_text`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered decision_text in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No decision_text provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### disclosure_class

Use versioned classification or status code for `MinuteItem.disclosure_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active disclosure_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped disclosure_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No disclosure_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### chair_statement

Use human-readable text for `MinuteItem.chair_statement`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered chair_statement in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No chair_statement provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### decision_round_id

The target is [DecisionRound](DecisionRound.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DecisionRound·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DecisionRound·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DecisionRound·MISSING | Queue the missing DecisionRound mapping or reject the command before linking. |
| Wrong scope | DecisionRound·B01 | Do not attach another church’s DecisionRound without a supported exchange and local authority. |
| Target rename | Rename DecisionRound·A01 after linking | The existing decision_round_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No decision_round_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recusal_public_text

Use human-readable text for `MinuteItem.recusal_public_text`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered recusal_public_text in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No recusal_public_text provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [OfficialExtract](OfficialExtract.md).`item_id` | MinuteItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Resolution](Resolution.md).`item_id` | MinuteItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
