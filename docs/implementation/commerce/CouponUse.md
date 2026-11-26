# CouponUse

[Prices, tax and delivery quotes](../../commerce/pricing.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Concurrent admissions cannot exceed either limit. Releasing after a refund follows published terms and is traceable.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `coupon_id` | ref Coupon | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `cart_id` | ref Cart? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `order_id` | ref Order? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `units` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `expires_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `state` | reserved/consumed/released | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `customer_key` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### coupon_id

The target is [Coupon](Coupon.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Coupon·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Coupon·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Coupon·MISSING | Queue the missing Coupon mapping or reject the command before linking. |
| Wrong scope | Coupon·B01 | Do not attach another church’s Coupon without a supported exchange and local authority. |
| Target rename | Rename Coupon·A01 after linking | The existing coupon_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No coupon_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cart_id

The target is [Cart](Cart.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Cart·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Cart·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Cart·MISSING | Queue the missing Cart mapping or reject the command before linking. |
| Wrong scope | Cart·B01 | Do not attach another church’s Cart without a supported exchange and local authority. |
| Target rename | Rename Cart·A01 after linking | The existing cart_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No cart_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### order_id

The target is [Order](Order.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Order·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Order·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Order·MISSING | Queue the missing Order mapping or reject the command before linking. |
| Wrong scope | Order·B01 | Do not attach another church’s Order without a supported exchange and local authority. |
| Target rename | Rename Order·A01 after linking | The existing order_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No order_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### units

Use whole-number measure for `CouponUse.units`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expires_at

Use unambiguous point in time for `CouponUse.expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No expires_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `reserved`, `consumed`, `released`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | reserved | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### customer_key

Use human-readable text for `CouponUse.customer_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered customer_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No customer_key provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
