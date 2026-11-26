# FinanceExchangeItem

[Financial controls, localization and exchanges](../../finance/controls.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One explicit outcome per source row. Error export masks sensitive content; replay selected corrected rows with version lineage.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `batch_id` | → FinanceExchangeBatch | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `source_key` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `row_number` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `validation_result` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `target_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `error_detail` | ? | Optional under owner conditions | [structured](../value-conventions.md#structured) |
| `previous_item_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### batch_id

The target is [FinanceExchangeBatch](FinanceExchangeBatch.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceExchangeBatch·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FinanceExchangeBatch·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FinanceExchangeBatch·MISSING | Queue the missing FinanceExchangeBatch mapping or reject the command before linking. |
| Wrong scope | FinanceExchangeBatch·B01 | Do not attach another church’s FinanceExchangeBatch without a supported exchange and local authority. |
| Target rename | Rename FinanceExchangeBatch·A01 after linking | The existing batch_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No batch_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_key

Use human-readable text for `FinanceExchangeItem.source_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered source_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No source_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### row_number

Use whole-number measure for `FinanceExchangeItem.row_number`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No row_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### validation_result

Use versioned classification or status code for `FinanceExchangeItem.validation_result`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active validation_result code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped validation_result code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No validation_result at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### target_ref

Use scoped or external reference for `FinanceExchangeItem.target_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified target_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped target_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No target_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### error_detail

Use typed value or bounded compound record for `FinanceExchangeItem.error_detail`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of error_detail matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for error_detail | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Absent in intake | No error_detail provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### previous_item_ref

Use scoped or external reference for `FinanceExchangeItem.previous_item_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified previous_item_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped previous_item_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No previous_item_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
