# ReportMappingLine

[Financial statements, close and consolidation](../../finance/reporting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique layout/line_code. Detect circular formulas and a detailed account mapped twice to additive subtotals. Export and print using the same calculation.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `layout_id` | → FinancialReportLayout | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `line_code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `parent_line_code` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `caption` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `order` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `calculation` | rule | Required when the record reaches its applicable state | [rule](../value-conventions.md#rule) |
| `account_filter` | rule? | Optional under owner conditions | [rule](../value-conventions.md#rule) |
| `dimension_filter` | rule? | Optional under owner conditions | [rule](../value-conventions.md#rule) |
| `subtotal_behavior` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### layout_id

The target is [FinancialReportLayout](FinancialReportLayout.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinancialReportLayout·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FinancialReportLayout·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FinancialReportLayout·MISSING | Queue the missing FinancialReportLayout mapping or reject the command before linking. |
| Wrong scope | FinancialReportLayout·B01 | Do not attach another church’s FinancialReportLayout without a supported exchange and local authority. |
| Target rename | Rename FinancialReportLayout·A01 after linking | The existing layout_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No layout_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### line_code

Use human-readable text for `ReportMappingLine.line_code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered line_code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No line_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_line_code

Use human-readable text for `ReportMappingLine.parent_line_code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered parent_line_code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No parent_line_code provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### caption

Use human-readable text for `ReportMappingLine.caption`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered caption in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No caption at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### order

Use whole-number measure for `ReportMappingLine.order`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No order at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### calculation

Use versioned structured decision or expression for `ReportMappingLine.calculation`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for calculation | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in calculation | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No calculation at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### account_filter

Use versioned structured decision or expression for `ReportMappingLine.account_filter`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for account_filter | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in account_filter | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Absent in intake | No account_filter provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### dimension_filter

Use versioned structured decision or expression for `ReportMappingLine.dimension_filter`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for dimension_filter | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in dimension_filter | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Absent in intake | No dimension_filter provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### subtotal_behavior

Use versioned classification or status code for `ReportMappingLine.subtotal_behavior`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active subtotal_behavior code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped subtotal_behavior code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No subtotal_behavior at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
