# SubscriptionTerm

[Subscriptions, grants and playback](../../commerce/access.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique subscription/term number and nonoverlapping service windows. Each charge has separate transaction evidence and refund disposition.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `subscription_id` | ref Subscription | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `plan_version_id` | ref AccessPlan | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `term_number` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `starts_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `ends_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `grace_until` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `price` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `renewal_order_id` | ref Order? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `state` | scheduled/in_trial/awaiting_payment/paid/grace/expired/refunded | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### subscription_id

The target is [Subscription](Subscription.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Subscription·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Subscription·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Subscription·MISSING | Queue the missing Subscription mapping or reject the command before linking. |
| Wrong scope | Subscription·B01 | Do not attach another church’s Subscription without a supported exchange and local authority. |
| Target rename | Rename Subscription·A01 after linking | The existing subscription_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No subscription_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### plan_version_id

The target is [AccessPlan](AccessPlan.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessPlan·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AccessPlan·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AccessPlan·MISSING | Queue the missing AccessPlan mapping or reject the command before linking. |
| Wrong scope | AccessPlan·B01 | Do not attach another church’s AccessPlan without a supported exchange and local authority. |
| Target rename | Rename AccessPlan·A01 after linking | The existing plan_version_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No plan_version_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### term_number

Use whole-number measure for `SubscriptionTerm.term_number`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No term_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### starts_at

Use unambiguous point in time for `SubscriptionTerm.starts_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No starts_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ends_at

Use unambiguous point in time for `SubscriptionTerm.ends_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No ends_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### grace_until

Use unambiguous point in time for `SubscriptionTerm.grace_until`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No grace_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### currency

Use monetary unit code for `SubscriptionTerm.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### price

Use exact monetary amount with currency for `SubscriptionTerm.price`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No price at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### renewal_order_id

The target is [Order](Order.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Order·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Order·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Order·MISSING | Queue the missing Order mapping or reject the command before linking. |
| Wrong scope | Order·B01 | Do not attach another church’s Order without a supported exchange and local authority. |
| Target rename | Rename Order·A01 after linking | The existing renewal_order_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No renewal_order_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `scheduled`, `in_trial`, `awaiting_payment`, `paid`, `grace`, `expired`, `refunded`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | scheduled | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccessGrant](AccessGrant.md).`subscription_term_id` | SubscriptionTerm identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
