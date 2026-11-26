# PathDependency

[Learning and formation](../../ministry/learning.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

An actual predecessor in the same path. Each logic group accepts any satisfied option; all required groups must be met. Disallow cycles.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `step_id` | → PathStep | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `requires_step_id` | → PathStep | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `logic_group` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### step_id

The target is [PathStep](PathStep.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PathStep·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | PathStep·MISSING | Queue the missing PathStep mapping or reject the command before linking. |
| Wrong scope | PathStep·B01 | Do not attach another church’s PathStep without a supported exchange and local authority. |
| Target rename | Rename PathStep·A01 after linking | The existing step_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No step_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requires_step_id

The target is [PathStep](PathStep.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PathStep·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | PathStep·MISSING | Queue the missing PathStep mapping or reject the command before linking. |
| Wrong scope | PathStep·B01 | Do not attach another church’s PathStep without a supported exchange and local authority. |
| Target rename | Rename PathStep·A01 after linking | The existing requires_step_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No requires_step_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### logic_group

Use versioned classification or status code for `PathDependency.logic_group`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active logic_group code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped logic_group code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No logic_group at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
