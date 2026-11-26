# FacilityRental

[Facilities, equipment and fleet](../../ministry/resources.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Finance owns deposit liability, invoicing, forfeiture approval and refunds. No facility operator can create cash or settle an invoice by completing a room inspection.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `booking_id` | → RoomBooking | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `agreement_ref` | id | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `payer_ref` | id | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `billing_order_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `deposit_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `insurance_review` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `inspection_outcome` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `settlement_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### booking_id

The target is [RoomBooking](RoomBooking.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RoomBooking·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RoomBooking·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RoomBooking·MISSING | Queue the missing RoomBooking mapping or reject the command before linking. |
| Wrong scope | RoomBooking·B01 | Do not attach another church’s RoomBooking without a supported exchange and local authority. |
| Target rename | Rename RoomBooking·A01 after linking | The existing booking_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No booking_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### agreement_ref

Use scoped or external reference for `FacilityRental.agreement_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified agreement_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped agreement_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No agreement_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### payer_ref

Use scoped or external reference for `FacilityRental.payer_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified payer_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped payer_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No payer_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### billing_order_ref

Use scoped or external reference for `FacilityRental.billing_order_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified billing_order_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped billing_order_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No billing_order_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### deposit_ref

Use scoped or external reference for `FacilityRental.deposit_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified deposit_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped deposit_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No deposit_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### insurance_review

Use versioned classification or status code for `FacilityRental.insurance_review`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active insurance_review code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped insurance_review code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No insurance_review provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### inspection_outcome

Use versioned classification or status code for `FacilityRental.inspection_outcome`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active inspection_outcome code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped inspection_outcome code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No inspection_outcome provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### settlement_state

Use versioned classification or status code for `FacilityRental.settlement_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active settlement_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped settlement_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No settlement_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
