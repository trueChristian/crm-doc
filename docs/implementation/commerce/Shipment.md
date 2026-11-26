# Shipment

[Counter sales and fulfilment](../../commerce/fulfilment.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One physical parcel per shipment. Mask tracking and addresses when contacting an unrelated recipient. Carrier updates cannot change an order's price.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `group_id` | ref FulfilmentGroup | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `packing_location_id` | ref StockLocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `address_version_id` | ref OrderContact | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `carrier_code` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `tracking_reference` | protected_text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `package_reference` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `packed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `dispatched_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `delivered_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `evidence_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `state` | preparing/packed/dispatched/delivered/lost/returned | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### group_id

The target is [FulfilmentGroup](FulfilmentGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FulfilmentGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FulfilmentGroup·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FulfilmentGroup·MISSING | Queue the missing FulfilmentGroup mapping or reject the command before linking. |
| Wrong scope | FulfilmentGroup·B01 | Do not attach another church’s FulfilmentGroup without a supported exchange and local authority. |
| Target rename | Rename FulfilmentGroup·A01 after linking | The existing group_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No group_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### packing_location_id

The target is [StockLocation](StockLocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockLocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockLocation·MISSING | Queue the missing StockLocation mapping or reject the command before linking. |
| Wrong scope | StockLocation·B01 | Do not attach another church’s StockLocation without a supported exchange and local authority. |
| Target rename | Rename StockLocation·A01 after linking | The existing packing_location_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No packing_location_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### address_version_id

The target is [OrderContact](OrderContact.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderContact·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderContact·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderContact·MISSING | Queue the missing OrderContact mapping or reject the command before linking. |
| Wrong scope | OrderContact·B01 | Do not attach another church’s OrderContact without a supported exchange and local authority. |
| Target rename | Rename OrderContact·A01 after linking | The existing address_version_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No address_version_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### carrier_code

Use versioned classification or status code for `Shipment.carrier_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active carrier_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped carrier_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No carrier_code provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### tracking_reference

Use restricted value or protected content reference for `Shipment.tracking_reference`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted tracking_reference supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No tracking_reference provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### package_reference

Use human-readable text for `Shipment.package_reference`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered package_reference in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No package_reference at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### packed_at

Use unambiguous point in time for `Shipment.packed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No packed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### dispatched_at

Use unambiguous point in time for `Shipment.dispatched_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No dispatched_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### delivered_at

Use unambiguous point in time for `Shipment.delivered_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No delivered_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### evidence_ref

Use scoped or external reference for `Shipment.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `preparing`, `packed`, `dispatched`, `delivered`, `lost`, `returned`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | preparing | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [FulfilmentException](FulfilmentException.md).`shipment_id` | Shipment identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ShipmentLine](ShipmentLine.md).`shipment_id` | Shipment identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
