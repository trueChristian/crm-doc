# PayoutItem

[After-sale service and accounting](../../commerce/settlement.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique statement item per issuer account, even when reports overlap. Signed payout amount sums to payout net. Unidentified items enter suspense for review.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `finance_detail_id` | ref SettlementDetail? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `payout_id` | ref ProcessorPayout | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `issuer_item_ref` | text | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `kind` | capture/refund/fee/dispute_hold/dispute_release/reserve/fx/adjustment | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `source_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `source_currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `source_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `payout_amount_signed` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `exchange_rate` | rate? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `occurred_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### finance_detail_id

The target is [SettlementDetail](../finance/SettlementDetail.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SettlementDetail·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SettlementDetail·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SettlementDetail·MISSING | Queue the missing SettlementDetail mapping or reject the command before linking. |
| Wrong scope | SettlementDetail·B01 | Do not attach another church’s SettlementDetail without a supported exchange and local authority. |
| Target rename | Rename SettlementDetail·A01 after linking | The existing finance_detail_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No finance_detail_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### payout_id

The target is [ProcessorPayout](ProcessorPayout.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProcessorPayout·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProcessorPayout·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProcessorPayout·MISSING | Queue the missing ProcessorPayout mapping or reject the command before linking. |
| Wrong scope | ProcessorPayout·B01 | Do not attach another church’s ProcessorPayout without a supported exchange and local authority. |
| Target rename | Rename ProcessorPayout·A01 after linking | The existing payout_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No payout_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### issuer_item_ref

Use scoped or external reference for `PayoutItem.issuer_item_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified issuer_item_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped issuer_item_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No issuer_item_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `capture`, `refund`, `fee`, `dispute_hold`, `dispute_release`, `reserve`, `fx`, `adjustment`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | capture | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_ref

Use scoped or external reference for `PayoutItem.source_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified source_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped source_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No source_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_currency

Use monetary unit code for `PayoutItem.source_currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No source_currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_amount

Use exact monetary amount with currency for `PayoutItem.source_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No source_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### payout_amount_signed

Use exact monetary amount with currency for `PayoutItem.payout_amount_signed`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No payout_amount_signed at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### exchange_rate

Use exact decimal measure for `PayoutItem.exchange_rate`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No exchange_rate provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### occurred_at

Use unambiguous point in time for `PayoutItem.occurred_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No occurred_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
