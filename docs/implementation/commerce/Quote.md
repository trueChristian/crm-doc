# Quote

[Prices, tax and delivery quotes](../../commerce/pricing.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One current revision per cart. Document an explicit acceptance instant and matching order.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `cart_id` | ref Cart | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `quoted_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `expires_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `address_scope_snapshot` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `tax_rule_version_set` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `delivery_method_id` | ref DeliveryMethod? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `calculated_by` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `rounding_policy` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `net_total` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `tax_total` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `gift_total` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `amount_due` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `status` | current/superseded/accepted/expired | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### cart_id

The target is [Cart](Cart.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Cart·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Cart·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Cart·MISSING | Queue the missing Cart mapping or reject the command before linking. |
| Wrong scope | Cart·B01 | Do not attach another church’s Cart without a supported exchange and local authority. |
| Target rename | Rename Cart·A01 after linking | The existing cart_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No cart_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### revision

Use revision number or opaque revision token for `Quote.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `Quote.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quoted_at

Use unambiguous point in time for `Quote.quoted_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No quoted_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expires_at

Use unambiguous point in time for `Quote.expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No expires_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### address_scope_snapshot

Use human-readable text for `Quote.address_scope_snapshot`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered address_scope_snapshot in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No address_scope_snapshot provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### tax_rule_version_set

Use human-readable text for `Quote.tax_rule_version_set`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered tax_rule_version_set in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No tax_rule_version_set at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### delivery_method_id

The target is [DeliveryMethod](DeliveryMethod.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DeliveryMethod·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DeliveryMethod·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DeliveryMethod·MISSING | Queue the missing DeliveryMethod mapping or reject the command before linking. |
| Wrong scope | DeliveryMethod·B01 | Do not attach another church’s DeliveryMethod without a supported exchange and local authority. |
| Target rename | Rename DeliveryMethod·A01 after linking | The existing delivery_method_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No delivery_method_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### calculated_by

Use versioned classification or status code for `Quote.calculated_by`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active calculated_by code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped calculated_by code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No calculated_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rounding_policy

Use versioned classification or status code for `Quote.rounding_policy`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active rounding_policy code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped rounding_policy code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No rounding_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### net_total

Use exact monetary amount with currency for `Quote.net_total`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No net_total at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_total

Use exact monetary amount with currency for `Quote.tax_total`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No tax_total at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### gift_total

Use exact monetary amount with currency for `Quote.gift_total`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No gift_total at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount_due

Use exact monetary amount with currency for `Quote.amount_due`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount_due at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Declared alternatives in owner order: `current`, `superseded`, `accepted`, `expired`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | current | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [Order](Order.md).`quote_id` | Quote identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [QuoteLine](QuoteLine.md).`quote_id` | Quote identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
