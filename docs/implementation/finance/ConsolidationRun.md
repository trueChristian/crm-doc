# ConsolidationRun

[Financial statements, close and consolidation](../../finance/reporting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One complete, traceable set of member submissions, adjustments, eliminations and translation differences. Changes produce a new version.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `group_id` | → ConsolidationGroup | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `period_end` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `member_snapshot_refs` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `fx_rate_set_version` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `layout_id` | → FinancialReportLayout | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `state` | {draft,reviewed,issued} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `approved_by_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### group_id

The target is [ConsolidationGroup](ConsolidationGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ConsolidationGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ConsolidationGroup·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ConsolidationGroup·MISSING | Queue the missing ConsolidationGroup mapping or reject the command before linking. |
| Wrong scope | ConsolidationGroup·B01 | Do not attach another church’s ConsolidationGroup without a supported exchange and local authority. |
| Target rename | Rename ConsolidationGroup·A01 after linking | The existing group_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No group_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period_end

Use civil calendar date for `ConsolidationRun.period_end`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No period_end at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### member_snapshot_refs

Use ordered collection or mathematical set for `ConsolidationRun.member_snapshot_refs`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No member_snapshot_refs at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fx_rate_set_version

Use human-readable text for `ConsolidationRun.fx_rate_set_version`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered fx_rate_set_version in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No fx_rate_set_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### state

Declared alternatives in owner order: `draft`, `reviewed`, `issued`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_by_ref

Use scoped or external reference for `ConsolidationRun.approved_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approved_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approved_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No approved_by_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [ConsolidationAdjustment](ConsolidationAdjustment.md).`run_id` | ConsolidationRun identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
