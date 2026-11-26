# ProgramIndicator

[Agreements, service rounds and relief distribution](../../administration/community-programs.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Specify distinct people versus service encounters. A ProjectOutcome holds the actual observation. Suppress identifying small cells and complementary subtotals.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `terms_id` | → ProgramServiceTerms | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `milestone_id` | → ProjectMilestone | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `label` | text | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `unit` | code | Required at applicable lifecycle step | [vocab](../value-conventions.md#vocab) |
| `numerator_rule` | versioned criteria | Required at applicable lifecycle step | [rule](../value-conventions.md#rule) |
| `denominator_rule` | versioned criteria | Required at applicable lifecycle step | [rule](../value-conventions.md#rule) |
| `permitted_breakdown` | list | Required at applicable lifecycle step | [list](../value-conventions.md#list) |
| `minimum_report_size` | count | Required at applicable lifecycle step | [integer](../value-conventions.md#integer) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ProgramIndicator.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProgramIndicator·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### terms_id

The target is [ProgramServiceTerms](ProgramServiceTerms.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProgramServiceTerms·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ProgramServiceTerms·MISSING | Queue the missing ProgramServiceTerms mapping or reject the command before linking. |
| Wrong scope | ProgramServiceTerms·B01 | Do not attach another church’s ProgramServiceTerms without a supported exchange and local authority. |
| Target rename | Rename ProgramServiceTerms·A01 after linking | The existing terms_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No terms_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### milestone_id

The target is [ProjectMilestone](../ministry/ProjectMilestone.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProjectMilestone·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ProjectMilestone·MISSING | Queue the missing ProjectMilestone mapping or reject the command before linking. |
| Wrong scope | ProjectMilestone·B01 | Do not attach another church’s ProjectMilestone without a supported exchange and local authority. |
| Target rename | Rename ProjectMilestone·A01 after linking | The existing milestone_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No milestone_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### label

Use human-readable text for `ProgramIndicator.label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No label at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit

Use versioned classification or status code for `ProgramIndicator.unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No unit at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### numerator_rule

Use versioned structured decision or expression for `ProgramIndicator.numerator_rule`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for numerator_rule | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in numerator_rule | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No numerator_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### denominator_rule

Use versioned structured decision or expression for `ProgramIndicator.denominator_rule`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for denominator_rule | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in denominator_rule | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No denominator_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### permitted_breakdown

Use ordered collection or mathematical set for `ProgramIndicator.permitted_breakdown`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No permitted_breakdown at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### minimum_report_size

Use whole-number measure for `ProgramIndicator.minimum_report_size`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No minimum_report_size at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
