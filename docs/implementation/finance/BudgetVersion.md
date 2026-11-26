# BudgetVersion

[Budgeting, cost allocation and cash forecasting](../../finance/planning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Original approved, revised approved and latest forecast are independently selectable. Approved figures are immutable.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `plan_id` | → BudgetPlan | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `version` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `status` | {draft,submitted,returned,approved,superseded} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `takes_effect_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `approved_by_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `meeting_resolution_ref` | → Resolution? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `locked_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `predecessor_id` | → BudgetVersion? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### plan_id

The target is [BudgetPlan](BudgetPlan.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | BudgetPlan·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | BudgetPlan·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | BudgetPlan·MISSING | Queue the missing BudgetPlan mapping or reject the command before linking. |
| Wrong scope | BudgetPlan·B01 | Do not attach another church’s BudgetPlan without a supported exchange and local authority. |
| Target rename | Rename BudgetPlan·A01 after linking | The existing plan_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No plan_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### version

Use revision number or opaque revision token for `BudgetVersion.version`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Declared alternatives in owner order: `draft`, `submitted`, `returned`, `approved`, `superseded`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### takes_effect_on

Use civil calendar date for `BudgetVersion.takes_effect_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No takes_effect_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approved_by_ref

Use scoped or external reference for `BudgetVersion.approved_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approved_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approved_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No approved_by_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### meeting_resolution_ref

The target is [Resolution](../governance/Resolution.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Resolution·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Resolution·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Resolution·MISSING | Queue the missing Resolution mapping or reject the command before linking. |
| Wrong scope | Resolution·B01 | Do not attach another church’s Resolution without a supported exchange and local authority. |
| Target rename | Rename Resolution·A01 after linking | The existing meeting_resolution_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No meeting_resolution_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### locked_at

Use unambiguous point in time for `BudgetVersion.locked_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No locked_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### predecessor_id

The target is [BudgetVersion](BudgetVersion.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | BudgetVersion·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | BudgetVersion·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | BudgetVersion·MISSING | Queue the missing BudgetVersion mapping or reject the command before linking. |
| Wrong scope | BudgetVersion·B01 | Do not attach another church’s BudgetVersion without a supported exchange and local authority. |
| Target rename | Rename BudgetVersion·A01 after linking | The existing predecessor_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No predecessor_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [BudgetLine](BudgetLine.md).`version_id` | BudgetVersion identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BudgetVersion](BudgetVersion.md).`predecessor_id` | BudgetVersion identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
