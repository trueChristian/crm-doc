# StaffDeparture

[Staff, clergy and employment administration](../../administration/workforce.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Reassign open work, retrieve property, close specific staff grants, notify payroll and preserve independent member or volunteer roles.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `engagement_id` | → EmploymentEngagement | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `effective_at` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [instant](../value-conventions.md#instant) |
| `checklist_version` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `delegated_work_recipient` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [structured](../value-conventions.md#structured) |
| `return_items_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `account_review_ref` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |
| `final_pay_run_ref` | → PayrollRun | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `closed_by` | Owner-scoped business value; see the record rule | Required at applicable lifecycle step | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `StaffDeparture.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StaffDeparture·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### engagement_id

The target is [EmploymentEngagement](EmploymentEngagement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EmploymentEngagement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EmploymentEngagement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EmploymentEngagement·MISSING | Queue the missing EmploymentEngagement mapping or reject the command before linking. |
| Wrong scope | EmploymentEngagement·B01 | Do not attach another church’s EmploymentEngagement without a supported exchange and local authority. |
| Target rename | Rename EmploymentEngagement·A01 after linking | The existing engagement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No engagement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_at

Use unambiguous point in time for `StaffDeparture.effective_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No effective_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### checklist_version

Use typed value or bounded compound record for `StaffDeparture.checklist_version`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of checklist_version matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for checklist_version | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No checklist_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delegated_work_recipient

Use typed value or bounded compound record for `StaffDeparture.delegated_work_recipient`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of delegated_work_recipient matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for delegated_work_recipient | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No delegated_work_recipient at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### return_items_ref

Use scoped or external reference for `StaffDeparture.return_items_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified return_items_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped return_items_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No return_items_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### account_review_ref

Use scoped or external reference for `StaffDeparture.account_review_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified account_review_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped account_review_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No account_review_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### final_pay_run_ref

The target is [PayrollRun](../finance/PayrollRun.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PayrollRun·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PayrollRun·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PayrollRun·MISSING | Queue the missing PayrollRun mapping or reject the command before linking. |
| Wrong scope | PayrollRun·B01 | Do not attach another church’s PayrollRun without a supported exchange and local authority. |
| Target rename | Rename PayrollRun·A01 after linking | The existing final_pay_run_ref keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No final_pay_run_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### closed_by

Use scoped or external reference for `StaffDeparture.closed_by`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified closed_by in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped closed_by | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No closed_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
