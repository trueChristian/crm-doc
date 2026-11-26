# CloseTask

[Financial statements, close and consolidation](../../finance/reporting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Required controls need approved evidence or explicit authorized waiver. Material imbalances block signature.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `cycle_id` | → CloseCycle | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `task_code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `owner_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `independent_reviewer_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `due_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `source_control_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `expected_result` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `evidence` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `status` | {open,blocked,done,waived} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `exception_reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### cycle_id

The target is [CloseCycle](CloseCycle.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CloseCycle·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CloseCycle·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CloseCycle·MISSING | Queue the missing CloseCycle mapping or reject the command before linking. |
| Wrong scope | CloseCycle·B01 | Do not attach another church’s CloseCycle without a supported exchange and local authority. |
| Target rename | Rename CloseCycle·A01 after linking | The existing cycle_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No cycle_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### task_code

Use human-readable text for `CloseTask.task_code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered task_code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No task_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### owner_ref

Use scoped or external reference for `CloseTask.owner_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified owner_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped owner_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No owner_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### independent_reviewer_ref

Use scoped or external reference for `CloseTask.independent_reviewer_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified independent_reviewer_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped independent_reviewer_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No independent_reviewer_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_on

Use civil calendar date for `CloseTask.due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No due_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_control_ref

Use scoped or external reference for `CloseTask.source_control_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified source_control_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped source_control_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No source_control_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### expected_result

Use human-readable text for `CloseTask.expected_result`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered expected_result in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No expected_result at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence

Use scoped or external reference for `CloseTask.evidence`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### status

Declared alternatives in owner order: `open`, `blocked`, `done`, `waived`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | open | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### exception_reason

Use human-readable text for `CloseTask.exception_reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered exception_reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No exception_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
