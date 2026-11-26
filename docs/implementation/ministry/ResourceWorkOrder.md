# ResourceWorkOrder

[Facilities, equipment and fleet](../../ministry/resources.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One primary asset or space per order. Link related orders for multi-asset work. Log triage, assignment, completion evidence, independent acceptance where needed and next inspection.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `space_id` | → FacilitySpace? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `item_id` | → EquipmentItem? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `vehicle_id` | → MinistryVehicle? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `reported_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `priority` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `assigned_to` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `due_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `cost_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `reopened_from_id` | → ResourceWorkOrder? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### space_id

The target is [FacilitySpace](FacilitySpace.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FacilitySpace·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FacilitySpace·MISSING | Queue the missing FacilitySpace mapping or reject the command before linking. |
| Wrong scope | FacilitySpace·B01 | Do not attach another church’s FacilitySpace without a supported exchange and local authority. |
| Target rename | Rename FacilitySpace·A01 after linking | The existing space_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No space_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### item_id

The target is [EquipmentItem](EquipmentItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EquipmentItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | EquipmentItem·MISSING | Queue the missing EquipmentItem mapping or reject the command before linking. |
| Wrong scope | EquipmentItem·B01 | Do not attach another church’s EquipmentItem without a supported exchange and local authority. |
| Target rename | Rename EquipmentItem·A01 after linking | The existing item_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No item_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### vehicle_id

The target is [MinistryVehicle](MinistryVehicle.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryVehicle·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MinistryVehicle·MISSING | Queue the missing MinistryVehicle mapping or reject the command before linking. |
| Wrong scope | MinistryVehicle·B01 | Do not attach another church’s MinistryVehicle without a supported exchange and local authority. |
| Target rename | Rename MinistryVehicle·A01 after linking | The existing vehicle_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No vehicle_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reported_at

Use unambiguous point in time for `ResourceWorkOrder.reported_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No reported_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### priority

Use versioned classification or status code for `ResourceWorkOrder.priority`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active priority code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped priority code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No priority at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### description

Use human-readable text for `ResourceWorkOrder.description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assigned_to

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing assigned_to keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No assigned_to provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_on

Use civil calendar date for `ResourceWorkOrder.due_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No due_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Use versioned classification or status code for `ResourceWorkOrder.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cost_ref

Use scoped or external reference for `ResourceWorkOrder.cost_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified cost_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped cost_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No cost_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reopened_from_id

The target is [ResourceWorkOrder](ResourceWorkOrder.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ResourceWorkOrder·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ResourceWorkOrder·MISSING | Queue the missing ResourceWorkOrder mapping or reject the command before linking. |
| Wrong scope | ResourceWorkOrder·B01 | Do not attach another church’s ResourceWorkOrder without a supported exchange and local authority. |
| Target rename | Rename ResourceWorkOrder·A01 after linking | The existing reopened_from_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reopened_from_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [FacilityClosure](FacilityClosure.md).`work_order_id` | ResourceWorkOrder identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResourceWorkOrder](ResourceWorkOrder.md).`reopened_from_id` | ResourceWorkOrder identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
