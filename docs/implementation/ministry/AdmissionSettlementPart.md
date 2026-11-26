# AdmissionSettlementPart

[Registration, tickets and attendance](../../ministry/registration.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Many-to-many between units and capture allocations permits split tenders and one line with several seats. Unique unit and tender allocation pair. Reconcile unit totals to the quoted settlement requirement and line totals to commerce acknowledgements. No local payment is posted.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `unit_id` | → AdmissionSaleUnit | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `tender_allocation_id` | → TenderAllocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `handoff_id` | → OrderHandoff | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `allocated_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `recorded_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### unit_id

The target is [AdmissionSaleUnit](AdmissionSaleUnit.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AdmissionSaleUnit·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AdmissionSaleUnit·MISSING | Queue the missing AdmissionSaleUnit mapping or reject the command before linking. |
| Wrong scope | AdmissionSaleUnit·B01 | Do not attach another church’s AdmissionSaleUnit without a supported exchange and local authority. |
| Target rename | Rename AdmissionSaleUnit·A01 after linking | The existing unit_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No unit_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tender_allocation_id

The target is [TenderAllocation](../commerce/TenderAllocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TenderAllocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | TenderAllocation·MISSING | Queue the missing TenderAllocation mapping or reject the command before linking. |
| Wrong scope | TenderAllocation·B01 | Do not attach another church’s TenderAllocation without a supported exchange and local authority. |
| Target rename | Rename TenderAllocation·A01 after linking | The existing tender_allocation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No tender_allocation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### handoff_id

The target is [OrderHandoff](../commerce/OrderHandoff.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderHandoff·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OrderHandoff·MISSING | Queue the missing OrderHandoff mapping or reject the command before linking. |
| Wrong scope | OrderHandoff·B01 | Do not attach another church’s OrderHandoff without a supported exchange and local authority. |
| Target rename | Rename OrderHandoff·A01 after linking | The existing handoff_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No handoff_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allocated_amount

Use exact monetary amount with currency for `AdmissionSettlementPart.allocated_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No allocated_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recorded_at

Use unambiguous point in time for `AdmissionSettlementPart.recorded_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No recorded_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
