# WorkflowStepResult

[Work queues, workflow editions and approvals](../../platform/workflow-approvals.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Uniquely track each action and attempt. Business effects must have a separately deduplicated operation key.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `instance_id` | Ref(WorkflowInstance) | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `operation_key` | text | Required when the record reaches its applicable state | [operation](../value-conventions.md#operation) |
| `attempt_no` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `input_revision` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `result_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `result_ref` | ResourceRef? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `occurred_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `error_key` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### instance_id

The target is [WorkflowInstance](WorkflowInstance.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | WorkflowInstance·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | WorkflowInstance·MISSING | Queue the missing WorkflowInstance mapping or reject the command before linking. |
| Wrong scope | WorkflowInstance·B01 | Do not attach another church’s WorkflowInstance without a supported exchange and local authority. |
| Target rename | Rename WorkflowInstance·A01 after linking | The existing instance_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No instance_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### operation_key

Use operation identity for exactly-once business effects for `WorkflowStepResult.operation_key`. Bind the key to the original material inputs and outcome; retain it throughout the replay window.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | KEY-007 with original inputs | Bind the key to the original material inputs and outcome; retain it throughout the replay window. |
| Malformed or unmapped | KEY-007 with changed material inputs | Reject conflicting reuse and reconcile against the first accepted or in-flight operation. |
| Duplicate after successful commit | two equivalent submissions using KEY-007 | Return the original business receipt with no second payment, membership change, booking or notice. |
| Timeout before outcome is known | provider accepted work but acknowledgement delayed | Look up or reconcile the pending operation before issuing a replacement. |
| A genuine correction has a new key | COR-008 points to original KEY-007 | Link the correction to the original effect and apply its ordinary authorization and reversal rules. |
| Incomplete record | No operation_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### attempt_no

Use whole-number measure for `WorkflowStepResult.attempt_no`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No attempt_no at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### input_revision

Use whole-number measure for `WorkflowStepResult.input_revision`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No input_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### result_code

Use versioned classification or status code for `WorkflowStepResult.result_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active result_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped result_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No result_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### result_ref

Use scoped or external reference for `WorkflowStepResult.result_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified result_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped result_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No result_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### occurred_at

Use unambiguous point in time for `WorkflowStepResult.occurred_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No occurred_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### error_key

Use versioned classification or status code for `WorkflowStepResult.error_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active error_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped error_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No error_key provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
