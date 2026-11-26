# RefundAllocation

[After-sale service and accounting](../../commerce/settlement.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique execution key. Refund through the original method up to amount captured less prior refunds and disputed sums under review. Explicit exceptions require authorization and evidence.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `refund_id` | ref Refund | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `order_line_id` | ref OrderLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `tender_allocation_id` | ref TenderAllocation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `original_capture_ref` | text? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `allocated_net` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `allocated_tax` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `allocated_gift` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `method` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `execution_key` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `provider_ref` | text? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `state` | planned/submitted/confirmed/failed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### refund_id

The target is [Refund](Refund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Refund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Refund·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Refund·MISSING | Queue the missing Refund mapping or reject the command before linking. |
| Wrong scope | Refund·B01 | Do not attach another church’s Refund without a supported exchange and local authority. |
| Target rename | Rename Refund·A01 after linking | The existing refund_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No refund_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### order_line_id

The target is [OrderLine](OrderLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderLine·MISSING | Queue the missing OrderLine mapping or reject the command before linking. |
| Wrong scope | OrderLine·B01 | Do not attach another church’s OrderLine without a supported exchange and local authority. |
| Target rename | Rename OrderLine·A01 after linking | The existing order_line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No order_line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tender_allocation_id

The target is [TenderAllocation](TenderAllocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TenderAllocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | TenderAllocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | TenderAllocation·MISSING | Queue the missing TenderAllocation mapping or reject the command before linking. |
| Wrong scope | TenderAllocation·B01 | Do not attach another church’s TenderAllocation without a supported exchange and local authority. |
| Target rename | Rename TenderAllocation·A01 after linking | The existing tender_allocation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No tender_allocation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### original_capture_ref

Use scoped or external reference for `RefundAllocation.original_capture_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified original_capture_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped original_capture_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No original_capture_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### allocated_net

Use exact monetary amount with currency for `RefundAllocation.allocated_net`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No allocated_net at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allocated_tax

Use exact monetary amount with currency for `RefundAllocation.allocated_tax`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No allocated_tax at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allocated_gift

Use exact monetary amount with currency for `RefundAllocation.allocated_gift`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No allocated_gift at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### method

Use versioned classification or status code for `RefundAllocation.method`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active method code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped method code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### execution_key

Use human-readable text for `RefundAllocation.execution_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered execution_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No execution_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### provider_ref

Use scoped or external reference for `RefundAllocation.provider_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified provider_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped provider_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No provider_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `planned`, `submitted`, `confirmed`, `failed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | planned | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AdmissionSaleAdjustment](../ministry/AdmissionSaleAdjustment.md).`refund_allocation_id` | RefundAllocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RefundTaxAllocation](RefundTaxAllocation.md).`refund_allocation_id` | RefundAllocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
