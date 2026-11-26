# FiscalPeriod

[Books, dimensions and double entry](../../finance/ledger.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Inclusive, contiguous non-overlapping accounting dates within book. A restricted period admits only designated closing entries with approval.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `book_id` | → FinanceBook | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `year_label` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `period_number` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `starts_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `ends_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `state` | {future,open,restricted,closed} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `allowed_batch_class` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `close_revision` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### book_id

The target is [FinanceBook](FinanceBook.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceBook·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FinanceBook·MISSING | Queue the missing FinanceBook mapping or reject the command before linking. |
| Wrong scope | FinanceBook·B01 | Do not attach another church’s FinanceBook without a supported exchange and local authority. |
| Target rename | Rename FinanceBook·A01 after linking | The existing book_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No book_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### year_label

Use human-readable text for `FiscalPeriod.year_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered year_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No year_label at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period_number

Use whole-number measure for `FiscalPeriod.period_number`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No period_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### starts_on

Use civil calendar date for `FiscalPeriod.starts_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No starts_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ends_on

Use civil calendar date for `FiscalPeriod.ends_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No ends_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `future`, `open`, `restricted`, `closed`. Approval and lifecycle guards still apply to transitions.
Field access: enforce the declared protection on reads, search, previews, exports and audit evidence as well as the underlying enum value.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | future | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allowed_batch_class

Use versioned classification or status code for `FiscalPeriod.allowed_batch_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active allowed_batch_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped allowed_batch_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No allowed_batch_class provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### close_revision

Use whole-number measure for `FiscalPeriod.close_revision`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No close_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccountingBasisBridge](AccountingBasisBridge.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AllocationDriver](AllocationDriver.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AllocationRun](AllocationRun.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BudgetLine](BudgetLine.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CloseCycle](CloseCycle.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DepreciationCharge](DepreciationCharge.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EndowmentDraw](EndowmentDraw.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FxValuationRun](FxValuationRun.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [JournalEntry](JournalEntry.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PayrollAccrual](PayrollAccrual.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecognitionInstallment](RecognitionInstallment.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StewardshipReview](StewardshipReview.md).`period_id` | FiscalPeriod identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
