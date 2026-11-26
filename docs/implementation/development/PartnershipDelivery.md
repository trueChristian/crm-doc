# PartnershipDelivery

[Partnerships, sponsorships and impact](../../development/partnerships.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Map evidence to the actual contribution, sale, approved supply or service event once. Each booked allocation is reported only up to its real amount, regardless of the number of partners sharing the public result.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `promise_id` | ref PartnerPromise | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `delivered_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `unit` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `evidence_ref` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `verified_by` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `gift_allocation_id` | ref GiftAllocation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `in_kind_gift_id` | ref InKindGift? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `invoice_line_id` | ref SalesInvoiceLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `service_entry_id` | ref ServiceTimeEntry? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `source_delivery_key` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `disposition` | offered/verified/disputed/reversed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `reversal_of_id` | ref PartnershipDelivery? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### promise_id

The target is [PartnerPromise](PartnerPromise.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PartnerPromise·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PartnerPromise·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PartnerPromise·MISSING | Queue the missing PartnerPromise mapping or reject the command before linking. |
| Wrong scope | PartnerPromise·B01 | Do not attach another church’s PartnerPromise without a supported exchange and local authority. |
| Target rename | Rename PartnerPromise·A01 after linking | The existing promise_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No promise_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delivered_at

Use unambiguous point in time for `PartnershipDelivery.delivered_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No delivered_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quantity

Use exact decimal measure for `PartnershipDelivery.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit

Use versioned classification or status code for `PartnershipDelivery.unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No unit at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_ref

Use scoped or external reference for `PartnershipDelivery.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No evidence_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### verified_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing verified_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No verified_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### gift_allocation_id

The target is [GiftAllocation](../finance/GiftAllocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftAllocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GiftAllocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GiftAllocation·MISSING | Queue the missing GiftAllocation mapping or reject the command before linking. |
| Wrong scope | GiftAllocation·B01 | Do not attach another church’s GiftAllocation without a supported exchange and local authority. |
| Target rename | Rename GiftAllocation·A01 after linking | The existing gift_allocation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No gift_allocation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### in_kind_gift_id

The target is [InKindGift](../finance/InKindGift.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | InKindGift·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | InKindGift·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | InKindGift·MISSING | Queue the missing InKindGift mapping or reject the command before linking. |
| Wrong scope | InKindGift·B01 | Do not attach another church’s InKindGift without a supported exchange and local authority. |
| Target rename | Rename InKindGift·A01 after linking | The existing in_kind_gift_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No in_kind_gift_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### invoice_line_id

The target is [SalesInvoiceLine](../finance/SalesInvoiceLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SalesInvoiceLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SalesInvoiceLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SalesInvoiceLine·MISSING | Queue the missing SalesInvoiceLine mapping or reject the command before linking. |
| Wrong scope | SalesInvoiceLine·B01 | Do not attach another church’s SalesInvoiceLine without a supported exchange and local authority. |
| Target rename | Rename SalesInvoiceLine·A01 after linking | The existing invoice_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No invoice_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### service_entry_id

The target is [ServiceTimeEntry](../ministry/ServiceTimeEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ServiceTimeEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ServiceTimeEntry·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ServiceTimeEntry·MISSING | Queue the missing ServiceTimeEntry mapping or reject the command before linking. |
| Wrong scope | ServiceTimeEntry·B01 | Do not attach another church’s ServiceTimeEntry without a supported exchange and local authority. |
| Target rename | Rename ServiceTimeEntry·A01 after linking | The existing service_entry_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No service_entry_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_delivery_key

Use human-readable text for `PartnershipDelivery.source_delivery_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered source_delivery_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No source_delivery_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### disposition

Declared alternatives in owner order: `offered`, `verified`, `disputed`, `reversed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | offered | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_disposition | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No disposition at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reversal_of_id

The target is [PartnershipDelivery](PartnershipDelivery.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PartnershipDelivery·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PartnershipDelivery·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PartnershipDelivery·MISSING | Queue the missing PartnershipDelivery mapping or reject the command before linking. |
| Wrong scope | PartnershipDelivery·B01 | Do not attach another church’s PartnershipDelivery without a supported exchange and local authority. |
| Target rename | Rename PartnershipDelivery·A01 after linking | The existing reversal_of_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reversal_of_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PartnershipDelivery](PartnershipDelivery.md).`reversal_of_id` | PartnershipDelivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
