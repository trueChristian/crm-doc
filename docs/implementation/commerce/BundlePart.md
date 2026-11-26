# BundlePart

[Catalogue and offers](../../commerce/catalogue.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Reject self-reference and cycles across bundles. For chosen components, freeze quantities and allocated amounts at checkout.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `bundle_variant_id` | ref ProductVariant | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `component_variant_id` | ref ProductVariant | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `units` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `price_weight` | rate | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `fulfilment_rule` | included/optional_choice | Optional under owner conditions | [enum](../value-conventions.md#enum) |
| `choice_group` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### bundle_variant_id

The target is [ProductVariant](ProductVariant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProductVariant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ProductVariant·MISSING | Queue the missing ProductVariant mapping or reject the command before linking. |
| Wrong scope | ProductVariant·B01 | Do not attach another church’s ProductVariant without a supported exchange and local authority. |
| Target rename | Rename ProductVariant·A01 after linking | The existing bundle_variant_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No bundle_variant_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### component_variant_id

The target is [ProductVariant](ProductVariant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProductVariant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ProductVariant·MISSING | Queue the missing ProductVariant mapping or reject the command before linking. |
| Wrong scope | ProductVariant·B01 | Do not attach another church’s ProductVariant without a supported exchange and local authority. |
| Target rename | Rename ProductVariant·A01 after linking | The existing component_variant_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No component_variant_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### units

Use exact decimal measure for `BundlePart.units`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No units at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### price_weight

Use exact decimal measure for `BundlePart.price_weight`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No price_weight at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fulfilment_rule

Declared alternatives in owner order: `included`, `optional_choice`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | included | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_fulfilment_rule | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No fulfilment_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### choice_group

Use versioned classification or status code for `BundlePart.choice_group`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active choice_group code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped choice_group code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No choice_group provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
