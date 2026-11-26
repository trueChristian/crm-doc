# OrderLine

[Checkout, orders and collection](../../commerce/orders.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Immutable commercial facts. Bundle allocation must avoid charging or posting price at both parent and child. Adjust an accepted order through separately approved actions.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `order_id` | ref Order | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `quote_line_id` | ref QuoteLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `variant_id` | ref ProductVariant? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `parent_line_id` | ref OrderLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `kind` | physical/digital/service/delivery/gift | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `sku_snapshot` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `title_snapshot` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `units` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `net_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `tax_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `gross_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `gift_fund_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `access_plan_version_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `recognition_rule_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `fulfilment_promise` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `price_policy_version` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |

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

### quote_line_id

The target is [QuoteLine](QuoteLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | QuoteLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | QuoteLine·MISSING | Queue the missing QuoteLine mapping or reject the command before linking. |
| Wrong scope | QuoteLine·B01 | Do not attach another church’s QuoteLine without a supported exchange and local authority. |
| Target rename | Rename QuoteLine·A01 after linking | The existing quote_line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No quote_line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### variant_id

The target is [ProductVariant](ProductVariant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProductVariant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ProductVariant·MISSING | Queue the missing ProductVariant mapping or reject the command before linking. |
| Wrong scope | ProductVariant·B01 | Do not attach another church’s ProductVariant without a supported exchange and local authority. |
| Target rename | Rename ProductVariant·A01 after linking | The existing variant_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No variant_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### parent_line_id

The target is [OrderLine](OrderLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OrderLine·MISSING | Queue the missing OrderLine mapping or reject the command before linking. |
| Wrong scope | OrderLine·B01 | Do not attach another church’s OrderLine without a supported exchange and local authority. |
| Target rename | Rename OrderLine·A01 after linking | The existing parent_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### kind

Declared alternatives in owner order: `physical`, `digital`, `service`, `delivery`, `gift`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | physical | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sku_snapshot

Use human-readable text for `OrderLine.sku_snapshot`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered sku_snapshot in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No sku_snapshot provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### title_snapshot

Use human-readable text for `OrderLine.title_snapshot`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title_snapshot in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title_snapshot at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### units

Use exact decimal measure for `OrderLine.units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### net_amount

Use exact monetary amount with currency for `OrderLine.net_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No net_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_amount

Use exact monetary amount with currency for `OrderLine.tax_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No tax_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### gross_amount

Use exact monetary amount with currency for `OrderLine.gross_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No gross_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### gift_fund_ref

Use scoped or external reference for `OrderLine.gift_fund_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified gift_fund_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped gift_fund_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No gift_fund_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### access_plan_version_ref

Use scoped or external reference for `OrderLine.access_plan_version_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified access_plan_version_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped access_plan_version_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No access_plan_version_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recognition_rule_ref

Use scoped or external reference for `OrderLine.recognition_rule_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified recognition_rule_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped recognition_rule_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No recognition_rule_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### fulfilment_promise

Use human-readable text for `OrderLine.fulfilment_promise`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered fulfilment_promise in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No fulfilment_promise at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### price_policy_version

Use human-readable text for `OrderLine.price_policy_version`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered price_policy_version in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No price_policy_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccessException](AccessException.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccessGrant](AccessGrant.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AdmissionSaleUnit](../ministry/AdmissionSaleUnit.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AdmissionSaleUnit](../ministry/AdmissionSaleUnit.md).`parent_bundle_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BillingAllocation](BillingAllocation.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FulfilmentLine](FulfilmentLine.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftClaim](GiftClaim.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderAmendment](OrderAmendment.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderHandoff](OrderHandoff.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderLine](OrderLine.md).`parent_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RefundAllocation](RefundAllocation.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReturnLine](ReturnLine.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReturnLine](ReturnLine.md).`replacement_order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SalesInvoiceLine](../finance/SalesInvoiceLine.md).`order_line_ref` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockReservation](StockReservation.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TenderAllocation](TenderAllocation.md).`order_line_id` | OrderLine identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
