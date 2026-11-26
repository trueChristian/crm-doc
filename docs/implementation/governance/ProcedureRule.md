# ProcedureRule

[Governing bodies, office terms and delegated authority](../../governance/bodies-and-terms.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique charter/meeting class/rule key. Values have named units, permitted choices and a readable explanation. No executable text.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `charter_id` | CharterEdition ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `meeting_class` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `rule_key` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `value_kind` | count/ratio/duration/choice/set/text | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `value` | validated value | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |
| `scope_note` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `effective_exception` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### charter_id

The target is [CharterEdition](CharterEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CharterEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | CharterEdition·MISSING | Queue the missing CharterEdition mapping or reject the command before linking. |
| Wrong scope | CharterEdition·B01 | Do not attach another church’s CharterEdition without a supported exchange and local authority. |
| Target rename | Rename CharterEdition·A01 after linking | The existing charter_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No charter_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### meeting_class

Use versioned classification or status code for `ProcedureRule.meeting_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active meeting_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped meeting_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No meeting_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rule_key

Use versioned classification or status code for `ProcedureRule.rule_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active rule_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped rule_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No rule_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### value_kind

Declared alternatives in owner order: `count`, `ratio`, `duration`, `choice`, `set`, `text`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | count | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_value_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No value_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### value

Use typed value or bounded compound record for `ProcedureRule.value`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of value matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for value | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scope_note

Use human-readable text for `ProcedureRule.scope_note`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered scope_note in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No scope_note provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### effective_exception

Use human-readable text for `ProcedureRule.effective_exception`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered effective_exception in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No effective_exception provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
