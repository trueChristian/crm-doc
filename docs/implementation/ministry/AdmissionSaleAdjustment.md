# AdmissionSaleAdjustment

[Registration, tickets and attendance](../../ministry/registration.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Many adjustments per unit, each tied to the approved amendment and, for a monetary return, the applicable commerce refund allocation. Unique unit, amendment, handoff generation and refund allocation leg. Unit credits across all legs cannot exceed the eligible remaining amount. Pending, applied, declined and failed are distinguishable.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `unit_id` | → AdmissionSaleUnit | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `amendment_id` | → OrderAmendment | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `refund_allocation_id` | → RefundAllocation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `handoff_id` | → OrderHandoff | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `kind` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `net_delta` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `tax_delta` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `applied_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `reason` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### unit_id

The target is [AdmissionSaleUnit](AdmissionSaleUnit.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AdmissionSaleUnit·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AdmissionSaleUnit·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AdmissionSaleUnit·MISSING | Queue the missing AdmissionSaleUnit mapping or reject the command before linking. |
| Wrong scope | AdmissionSaleUnit·B01 | Do not attach another church’s AdmissionSaleUnit without a supported exchange and local authority. |
| Target rename | Rename AdmissionSaleUnit·A01 after linking | The existing unit_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No unit_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amendment_id

The target is [OrderAmendment](../commerce/OrderAmendment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderAmendment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderAmendment·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderAmendment·MISSING | Queue the missing OrderAmendment mapping or reject the command before linking. |
| Wrong scope | OrderAmendment·B01 | Do not attach another church’s OrderAmendment without a supported exchange and local authority. |
| Target rename | Rename OrderAmendment·A01 after linking | The existing amendment_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No amendment_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### refund_allocation_id

The target is [RefundAllocation](../commerce/RefundAllocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RefundAllocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RefundAllocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RefundAllocation·MISSING | Queue the missing RefundAllocation mapping or reject the command before linking. |
| Wrong scope | RefundAllocation·B01 | Do not attach another church’s RefundAllocation without a supported exchange and local authority. |
| Target rename | Rename RefundAllocation·A01 after linking | The existing refund_allocation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No refund_allocation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### handoff_id

The target is [OrderHandoff](../commerce/OrderHandoff.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderHandoff·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderHandoff·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderHandoff·MISSING | Queue the missing OrderHandoff mapping or reject the command before linking. |
| Wrong scope | OrderHandoff·B01 | Do not attach another church’s OrderHandoff without a supported exchange and local authority. |
| Target rename | Rename OrderHandoff·A01 after linking | The existing handoff_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No handoff_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Use versioned classification or status code for `AdmissionSaleAdjustment.kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### net_delta

Use exact monetary amount with currency for `AdmissionSaleAdjustment.net_delta`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No net_delta at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_delta

Use exact monetary amount with currency for `AdmissionSaleAdjustment.tax_delta`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No tax_delta at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Use versioned classification or status code for `AdmissionSaleAdjustment.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### applied_at

Use unambiguous point in time for `AdmissionSaleAdjustment.applied_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No applied_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason

Use versioned classification or status code for `AdmissionSaleAdjustment.reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
