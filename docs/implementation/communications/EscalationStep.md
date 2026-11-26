# EscalationStep

[Reminders and orchestration](../../communications/reminders-and-orchestration.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Exhaustion opens one operational task. A chain has a maximum depth, per-person contact limit, permitted role and expiry. Repeating the same cycle requires explicit review.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `rule_id` | ReminderRule ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sequence` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `wait_quantity` | duration | Required when the record reaches its applicable state | [duration](../value-conventions.md#duration) |
| `condition` | no_response/failed_delivery/overdue | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `recipient_selector` | permitted role/owner | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |
| `action` | alert/assign_task/offer_alternate_channel | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `template_id` | MessageTemplate ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `stop_when` | typed expression | Required when the record reaches its applicable state | [rule](../value-conventions.md#rule) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### rule_id

The target is [ReminderRule](ReminderRule.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReminderRule·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ReminderRule·MISSING | Queue the missing ReminderRule mapping or reject the command before linking. |
| Wrong scope | ReminderRule·B01 | Do not attach another church’s ReminderRule without a supported exchange and local authority. |
| Target rename | Rename ReminderRule·A01 after linking | The existing rule_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No rule_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sequence

Use whole-number measure for `EscalationStep.sequence`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No sequence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### wait_quantity

Use elapsed interval or named calendar duration for `EscalationStep.wait_quantity`. Preserve unit and distinguish elapsed minutes from a calendar day or working day.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 30 minutes in elapsed-time profile | Preserve unit and distinguish elapsed minutes from a calendar day or working day. |
| Malformed or unmapped | duration without resolvable unit | Request an interval unit. |
| A working-day deadline crosses a closure | a one-workday deadline starting on Friday | Use the named work-calendar edition. |
| A civil day crosses an offset change | a local civil day covers 23 or 25 elapsed hours | Do not assume 24 elapsed hours. |
| Zero-length interval | duration of zero units | Apply the owner’s validity or immediate-trigger rule. |
| Incomplete record | No wait_quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### condition

Declared alternatives in owner order: `no_response`, `failed_delivery`, `overdue`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | no_response | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_condition | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No condition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recipient_selector

Use typed value or bounded compound record for `EscalationStep.recipient_selector`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of recipient_selector matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for recipient_selector | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No recipient_selector at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### action

Declared alternatives in owner order: `alert`, `assign_task`, `offer_alternate_channel`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | alert | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_action | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No action at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### template_id

The target is [MessageTemplate](MessageTemplate.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MessageTemplate·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MessageTemplate·MISSING | Queue the missing MessageTemplate mapping or reject the command before linking. |
| Wrong scope | MessageTemplate·B01 | Do not attach another church’s MessageTemplate without a supported exchange and local authority. |
| Target rename | Rename MessageTemplate·A01 after linking | The existing template_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No template_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### stop_when

Use versioned structured decision or expression for `EscalationStep.stop_when`. Check types, dependencies, owner, version and scope before activation.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | approved clause for stop_when | Check types, dependencies, owner, version and scope before activation. |
| Malformed or unmapped | cyclic or unbound condition in stop_when | Reject activation; retain last accepted edition. |
| Two rules at the same scope conflict | two matching clauses of equal priority | Use documented precedence or block publication for review. |
| Rule changes after a decision | rule version 2 proposed after version 1 approved the event | Keep the prior decision bound to its evaluated edition. |
| Preview a rule on an eligible sample | dry-run edition on locally approved test inputs | Explain matched conditions; produce no live effect. |
| Incomplete record | No stop_when at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
