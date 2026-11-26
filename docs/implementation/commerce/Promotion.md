# Promotion

[Prices, tax and delivery quotes](../../commerce/pricing.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Set base, tier and promotion precedence. Fixed amount/caps require currency. Price floors cannot be breached. Anonymous redemption needs an explicitly enforceable rule.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `organization_id` | ref Organization | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `condition_version` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `eligible_offer_set` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `starts_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `ends_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `benefit_kind` | fixed/percent/free_delivery | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `benefit_value` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `cap` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `currency` | code? | Optional under owner conditions | [currency](../value-conventions.md#currency) |
| `precedence` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `stack_group` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `max_uses` | integer? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `customer_limit` | integer? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `state` | draft/approved/paused/closed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Organization·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### code

Use versioned classification or status code for `Promotion.code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### condition_version

Use human-readable text for `Promotion.condition_version`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered condition_version in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No condition_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligible_offer_set

Use scoped or external reference for `Promotion.eligible_offer_set`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified eligible_offer_set in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped eligible_offer_set | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No eligible_offer_set at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### starts_at

Use unambiguous point in time for `Promotion.starts_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No starts_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ends_at

Use unambiguous point in time for `Promotion.ends_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No ends_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### benefit_kind

Declared alternatives in owner order: `fixed`, `percent`, `free_delivery`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | fixed | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_benefit_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No benefit_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### benefit_value

Use exact decimal measure for `Promotion.benefit_value`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No benefit_value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cap

Use exact monetary amount with currency for `Promotion.cap`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No cap provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### currency

Use monetary unit code for `Promotion.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Absent in intake | No currency provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### precedence

Use whole-number measure for `Promotion.precedence`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No precedence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### stack_group

Use versioned classification or status code for `Promotion.stack_group`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active stack_group code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped stack_group code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No stack_group provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### max_uses

Use whole-number measure for `Promotion.max_uses`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No max_uses provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### customer_limit

Use whole-number measure for `Promotion.customer_limit`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No customer_limit provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `draft`, `approved`, `paused`, `closed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | draft | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [Coupon](Coupon.md).`promotion_id` | Promotion identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [QuoteLine](QuoteLine.md).`promotion_ids` | Promotion identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
