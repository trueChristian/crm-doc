# PaymentAttempt

[Checkout, orders and collection](../../commerce/orders.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique organization/request key. Same key and different business amount returns a conflict. A confirmed sale may use more than one tender. No raw account secrets or card details in the CRM.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `order_id` | ref Order | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `request_key` | text | Required when the record reaches its applicable state | [operation](../value-conventions.md#operation) |
| `method` | card/bank/cash/voucher/account_credit | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `processor_account_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `external_ref` | text? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `requested_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `authorized_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `captured_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `authorized_until` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `initiated_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `state` | initiated/awaiting_action/authorized/part_captured/captured/declined/voided/unknown | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### order_id

The target is [Order](Order.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Order·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Order·MISSING | Queue the missing Order mapping or reject the command before linking. |
| Wrong scope | Order·B01 | Do not attach another church’s Order without a supported exchange and local authority. |
| Target rename | Rename Order·A01 after linking | The existing order_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No order_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### request_key

Use operation identity for exactly-once business effects for `PaymentAttempt.request_key`. Bind the key to the original material inputs and outcome; retain it throughout the replay window.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | KEY-007 with original inputs | Bind the key to the original material inputs and outcome; retain it throughout the replay window. |
| Malformed or unmapped | KEY-007 with changed material inputs | Reject conflicting reuse and reconcile against the first accepted or in-flight operation. |
| Duplicate after successful commit | two equivalent submissions using KEY-007 | Return the original business receipt with no second payment, membership change, booking or notice. |
| Timeout before outcome is known | provider accepted work but acknowledgement delayed | Look up or reconcile the pending operation before issuing a replacement. |
| A genuine correction has a new key | COR-008 points to original KEY-007 | Link the correction to the original effect and apply its ordinary authorization and reversal rules. |
| Incomplete record | No request_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### method

Declared alternatives in owner order: `card`, `bank`, `cash`, `voucher`, `account_credit`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | card | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_method | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### processor_account_ref

Use scoped or external reference for `PaymentAttempt.processor_account_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified processor_account_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped processor_account_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No processor_account_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### external_ref

Use scoped or external reference for `PaymentAttempt.external_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified external_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped external_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No external_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### requested_amount

Use exact monetary amount with currency for `PaymentAttempt.requested_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No requested_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authorized_amount

Use exact monetary amount with currency for `PaymentAttempt.authorized_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No authorized_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### captured_amount

Use exact monetary amount with currency for `PaymentAttempt.captured_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No captured_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `PaymentAttempt.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authorized_until

Use unambiguous point in time for `PaymentAttempt.authorized_until`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No authorized_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### initiated_at

Use unambiguous point in time for `PaymentAttempt.initiated_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No initiated_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `initiated`, `awaiting_action`, `authorized`, `part_captured`, `captured`, `declined`, `voided`, `unknown`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | initiated | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CashMovement](CashMovement.md).`attempt_id` | PaymentAttempt identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CommerceDisputeCase](CommerceDisputeCase.md).`payment_attempt_id` | PaymentAttempt identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CreditMovement](CreditMovement.md).`attempt_id` | PaymentAttempt identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PaymentEvent](PaymentEvent.md).`attempt_id` | PaymentAttempt identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TenderAllocation](TenderAllocation.md).`attempt_id` | PaymentAttempt identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
