# InKindGift

[Offerings, gifts and donor service](../../finance/giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Separate donor description, church valuation and permitted receipt wording. Donated services, use of space and donated goods may follow different policy.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `gift_id` | → Gift | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `item_description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `quantity` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `valuation` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `valuation_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `method` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `evidence` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `receiving_asset_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `disposition_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `recognized` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### gift_id

The target is [Gift](Gift.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Gift·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Gift·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Gift·MISSING | Queue the missing Gift mapping or reject the command before linking. |
| Wrong scope | Gift·B01 | Do not attach another church’s Gift without a supported exchange and local authority. |
| Target rename | Rename Gift·A01 after linking | The existing gift_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No gift_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### item_description

Use human-readable text for `InKindGift.item_description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered item_description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No item_description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quantity

Use exact decimal measure for `InKindGift.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valuation

Use exact monetary amount with currency for `InKindGift.valuation`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No valuation provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### valuation_on

Use civil calendar date for `InKindGift.valuation_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No valuation_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### method

Use human-readable text for `InKindGift.method`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered method in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No method provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### evidence

Use scoped or external reference for `InKindGift.evidence`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### receiving_asset_ref

Use scoped or external reference for `InKindGift.receiving_asset_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified receiving_asset_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped receiving_asset_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No receiving_asset_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### disposition_ref

Use scoped or external reference for `InKindGift.disposition_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified disposition_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped disposition_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No disposition_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recognized

Use explicit logical choice for `InKindGift.recognized`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No recognized at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AcceptedGiftLink](../development/AcceptedGiftLink.md).`in_kind_gift_id` | InKindGift identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [NonCashDisposition](NonCashDisposition.md).`in_kind_gift_id` | InKindGift identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PartnershipDelivery](../development/PartnershipDelivery.md).`in_kind_gift_id` | InKindGift identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
