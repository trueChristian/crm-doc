# VocabularyTerm

[Configuration, reusable forms and document custody](../../platform/configuration-content.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique vocabulary and term key. Retired terms remain resolvable in historic reports. No cycles in hierarchy or replacements.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `vocabulary_key` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `term_key` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `parent_id` | Ref(VocabularyTerm)? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `display_order` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `enabled_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `retired_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `replacement_id` | Ref(VocabularyTerm)? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### vocabulary_key

Use versioned classification or status code for `VocabularyTerm.vocabulary_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active vocabulary_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped vocabulary_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No vocabulary_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### term_key

Use versioned classification or status code for `VocabularyTerm.term_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active term_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped term_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No term_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_id

The target is [VocabularyTerm](VocabularyTerm.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VocabularyTerm·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | VocabularyTerm·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | VocabularyTerm·MISSING | Queue the missing VocabularyTerm mapping or reject the command before linking. |
| Wrong scope | VocabularyTerm·B01 | Do not attach another church’s VocabularyTerm without a supported exchange and local authority. |
| Target rename | Rename VocabularyTerm·A01 after linking | The existing parent_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### display_order

Use whole-number measure for `VocabularyTerm.display_order`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No display_order at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### enabled_from

Use civil calendar date for `VocabularyTerm.enabled_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No enabled_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### retired_on

Use civil calendar date for `VocabularyTerm.retired_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No retired_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### replacement_id

The target is [VocabularyTerm](VocabularyTerm.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | VocabularyTerm·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | VocabularyTerm·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | VocabularyTerm·MISSING | Queue the missing VocabularyTerm mapping or reject the command before linking. |
| Wrong scope | VocabularyTerm·B01 | Do not attach another church’s VocabularyTerm without a supported exchange and local authority. |
| Target rename | Rename VocabularyTerm·A01 after linking | The existing replacement_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No replacement_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [VocabularyTerm](VocabularyTerm.md).`parent_id` | VocabularyTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VocabularyTerm](VocabularyTerm.md).`replacement_id` | VocabularyTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
