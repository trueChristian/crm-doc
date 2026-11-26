# LeavePlan

[Staff, clergy and employment administration](../../administration/workforce.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Compute balance as of date. Keep opening balances and posted adjustments. One approved request can create multiple movements for partial days.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `unit` | hours/days | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `accrual_rule` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [rule](../value-conventions.md#rule) |
| `cap` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [decimal](../value-conventions.md#decimal) |
| `carry_rule` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [rule](../value-conventions.md#rule) |
| `effective_from` | date | Required at applicable lifecycle step | [date](../value-conventions.md#date) |
| `effective_until` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `LeavePlan.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LeavePlan·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### unit

Declared alternatives in owner order: `hours`, `days`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | hours | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_unit | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No unit at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### accrual_rule

Use versioned structured decision or expression for `LeavePlan.accrual_rule`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for accrual_rule | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in accrual_rule | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No accrual_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cap

Use exact decimal measure for `LeavePlan.cap`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No cap at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### carry_rule

Use versioned structured decision or expression for `LeavePlan.carry_rule`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for carry_rule | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in carry_rule | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No carry_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_from

Use civil calendar date for `LeavePlan.effective_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No effective_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_until

Use civil calendar date for `LeavePlan.effective_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No effective_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [LeaveMovement](LeaveMovement.md).`plan_id` | LeavePlan identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
