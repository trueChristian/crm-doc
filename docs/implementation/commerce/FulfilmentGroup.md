# FulfilmentGroup

[Counter sales and fulfilment](../../commerce/fulfilment.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One order may split by campus, date or method. Do not delay a released digital item solely because a parcel is pending unless terms require a common release.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `order_id` | ref Order | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `method` | ship/collect/digital/service | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `delivery_method_id` | ref DeliveryMethod | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `assigned_location_id` | ref StockLocation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `dispatch_after` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `due_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `state` | waiting/ready/in_progress/partial/fulfilled/cancelled/exception | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### order_id

The target is [Order](Order.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Order·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Order·MISSING | Queue the missing Order mapping or reject the command before linking. |
| Wrong scope | Order·B01 | Do not attach another church’s Order without a supported exchange and local authority. |
| Target rename | Rename Order·A01 after linking | The existing order_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No order_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### method

Declared alternatives in owner order: `ship`, `collect`, `digital`, `service`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ship | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_method | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delivery_method_id

The target is [DeliveryMethod](DeliveryMethod.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DeliveryMethod·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | DeliveryMethod·MISSING | Queue the missing DeliveryMethod mapping or reject the command before linking. |
| Wrong scope | DeliveryMethod·B01 | Do not attach another church’s DeliveryMethod without a supported exchange and local authority. |
| Target rename | Rename DeliveryMethod·A01 after linking | The existing delivery_method_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No delivery_method_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assigned_location_id

The target is [StockLocation](StockLocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | StockLocation·MISSING | Queue the missing StockLocation mapping or reject the command before linking. |
| Wrong scope | StockLocation·B01 | Do not attach another church’s StockLocation without a supported exchange and local authority. |
| Target rename | Rename StockLocation·A01 after linking | The existing assigned_location_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No assigned_location_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### dispatch_after

Use unambiguous point in time for `FulfilmentGroup.dispatch_after`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No dispatch_after provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_at

Use unambiguous point in time for `FulfilmentGroup.due_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No due_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `waiting`, `ready`, `in_progress`, `partial`, `fulfilled`, `cancelled`, `exception`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | waiting | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [Collection](Collection.md).`group_id` | FulfilmentGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FulfilmentException](FulfilmentException.md).`group_id` | FulfilmentGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FulfilmentLine](FulfilmentLine.md).`group_id` | FulfilmentGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Shipment](Shipment.md).`group_id` | FulfilmentGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
