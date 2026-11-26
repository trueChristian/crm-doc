# CartLine

[Checkout, orders and collection](../../commerce/orders.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Sale requires one offer. Gift requires one approved giving designation and amount and carries no trading stock. Capture selected bundle components individually.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `cart_id` | ref Cart | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `offer_id` | ref Offer? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `component_kind` | sale/gift | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `units` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `gift_fund_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `gift_amount` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `recipient_claim_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `delivery_group_key` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `added_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### cart_id

The target is [Cart](Cart.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Cart·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Cart·MISSING | Queue the missing Cart mapping or reject the command before linking. |
| Wrong scope | Cart·B01 | Do not attach another church’s Cart without a supported exchange and local authority. |
| Target rename | Rename Cart·A01 after linking | The existing cart_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No cart_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### offer_id

The target is [Offer](Offer.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Offer·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Offer·MISSING | Queue the missing Offer mapping or reject the command before linking. |
| Wrong scope | Offer·B01 | Do not attach another church’s Offer without a supported exchange and local authority. |
| Target rename | Rename Offer·A01 after linking | The existing offer_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No offer_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### component_kind

Declared alternatives in owner order: `sale`, `gift`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | sale | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_component_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No component_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### units

Use exact decimal measure for `CartLine.units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### gift_fund_ref

Use scoped or external reference for `CartLine.gift_fund_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified gift_fund_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped gift_fund_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No gift_fund_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### gift_amount

Use exact monetary amount with currency for `CartLine.gift_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No gift_amount provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recipient_claim_ref

Use scoped or external reference for `CartLine.recipient_claim_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified recipient_claim_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped recipient_claim_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No recipient_claim_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### delivery_group_key

Use human-readable text for `CartLine.delivery_group_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered delivery_group_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No delivery_group_key provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### added_at

Use unambiguous point in time for `CartLine.added_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No added_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [QuoteLine](QuoteLine.md).`cart_line_id` | CartLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockReservation](StockReservation.md).`cart_line_id` | CartLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
