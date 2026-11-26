# OfferLimit

[Catalogue and offers](../../commerce/catalogue.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Identify enforced scope and how guest orders qualify before publishing. Avoid collecting extra identifying data solely to enforce a weak limit.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `offer_id` | ref Offer | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `unit_limit` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `period` | once/day/week/event | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `subject` | account/verified_customer/order | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `event_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### offer_id

The target is [Offer](Offer.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Offer·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Offer·MISSING | Queue the missing Offer mapping or reject the command before linking. |
| Wrong scope | Offer·B01 | Do not attach another church’s Offer without a supported exchange and local authority. |
| Target rename | Rename Offer·A01 after linking | The existing offer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No offer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit_limit

Use exact decimal measure for `OfferLimit.unit_limit`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No unit_limit at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period

Declared alternatives in owner order: `once`, `day`, `week`, `event`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | once | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_period | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No period at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### subject

Declared alternatives in owner order: `account`, `verified_customer`, `order`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | account | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_subject | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No subject at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### event_ref

Use scoped or external reference for `OfferLimit.event_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified event_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped event_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No event_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
