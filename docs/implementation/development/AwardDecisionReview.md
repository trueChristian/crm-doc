# AwardDecisionReview

[Grant applications and reporting](../../development/grant-applications.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Receiving an offer triggers terms review. Acceptance plus finance acknowledgement creates one authoritative incoming award. Rejecting a partial offer cannot post the requested amount or mark it earned.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `application_id` | ref GrantApplication | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `offer_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `received_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `conditions_ref` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `revised_scope_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `decision` | accepted/renegotiate/declined | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `authorized_by` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `authorized_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `finance_award_id` | ref GrantAward? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### application_id

The target is [GrantApplication](GrantApplication.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GrantApplication·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GrantApplication·MISSING | Queue the missing GrantApplication mapping or reject the command before linking. |
| Wrong scope | GrantApplication·B01 | Do not attach another church’s GrantApplication without a supported exchange and local authority. |
| Target rename | Rename GrantApplication·A01 after linking | The existing application_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No application_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### offer_amount

Use exact monetary amount with currency for `AwardDecisionReview.offer_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No offer_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `AwardDecisionReview.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### received_at

Use unambiguous point in time for `AwardDecisionReview.received_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No received_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### conditions_ref

Use scoped or external reference for `AwardDecisionReview.conditions_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified conditions_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped conditions_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No conditions_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revised_scope_ref

Use scoped or external reference for `AwardDecisionReview.revised_scope_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified revised_scope_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped revised_scope_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No revised_scope_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### decision

Declared alternatives in owner order: `accepted`, `renegotiate`, `declined`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | accepted | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_decision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No decision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authorized_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing authorized_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No authorized_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authorized_at

Use unambiguous point in time for `AwardDecisionReview.authorized_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No authorized_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### finance_award_id

The target is [GrantAward](../finance/GrantAward.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GrantAward·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GrantAward·MISSING | Queue the missing GrantAward mapping or reject the command before linking. |
| Wrong scope | GrantAward·B01 | Do not attach another church’s GrantAward without a supported exchange and local authority. |
| Target rename | Rename GrantAward·A01 after linking | The existing finance_award_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No finance_award_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
