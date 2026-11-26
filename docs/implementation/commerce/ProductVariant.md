# ProductVariant

[Catalogue and offers](../../commerce/catalogue.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Each sellable line references one variant. All measures positive when set. SKU unique per organization. Shipping requires enough dimensions for the chosen rate method.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `product_id` | ref Product | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sku` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `unit_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `format` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `mass` | quantity? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `mass_unit` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `depth` | quantity? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `width` | quantity? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `height` | quantity? | Optional under owner conditions | [decimal](../value-conventions.md#decimal) |
| `length_unit` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `inventory_policy` | tracked/untracked/made_to_order | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `fulfilment_kind` | ship/collect/digital/service | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `tax_class` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `state` | active/retired | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### product_id

The target is [Product](Product.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Product·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Product·MISSING | Queue the missing Product mapping or reject the command before linking. |
| Wrong scope | Product·B01 | Do not attach another church’s Product without a supported exchange and local authority. |
| Target rename | Rename Product·A01 after linking | The existing product_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No product_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sku

Use versioned classification or status code for `ProductVariant.sku`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active sku code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped sku code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No sku at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit_code

Use versioned classification or status code for `ProductVariant.unit_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active unit_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped unit_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No unit_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### format

Use versioned classification or status code for `ProductVariant.format`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active format code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped format code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No format provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### mass

Use exact decimal measure for `ProductVariant.mass`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No mass provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### mass_unit

Use versioned classification or status code for `ProductVariant.mass_unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active mass_unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped mass_unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No mass_unit provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### depth

Use exact decimal measure for `ProductVariant.depth`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No depth provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### width

Use exact decimal measure for `ProductVariant.width`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No width provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### height

Use exact decimal measure for `ProductVariant.height`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Absent in intake | No height provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### length_unit

Use versioned classification or status code for `ProductVariant.length_unit`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active length_unit code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped length_unit code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No length_unit provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### inventory_policy

Declared alternatives in owner order: `tracked`, `untracked`, `made_to_order`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | tracked | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_inventory_policy | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No inventory_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fulfilment_kind

Declared alternatives in owner order: `ship`, `collect`, `digital`, `service`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ship | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_fulfilment_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No fulfilment_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_class

Use versioned classification or status code for `ProductVariant.tax_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active tax_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped tax_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No tax_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `active`, `retired`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [BundlePart](BundlePart.md).`bundle_variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BundlePart](BundlePart.md).`component_variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CountLine](CountLine.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InventoryValuationEvent](../finance/InventoryValuationEvent.md).`product_variant_ref` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Offer](Offer.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderLine](OrderLine.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PriceTier](PriceTier.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProductAsset](ProductAsset.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProductIdentifier](ProductIdentifier.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReplenishmentRule](ReplenishmentRule.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockLot](StockLot.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockMovement](StockMovement.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockRecall](StockRecall.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockReceiptLine](StockReceiptLine.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockReservation](StockReservation.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockTransferLine](StockTransferLine.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VariantOptionValue](VariantOptionValue.md).`variant_id` | ProductVariant identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
