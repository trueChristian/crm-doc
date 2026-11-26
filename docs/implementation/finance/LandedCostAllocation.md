# LandedCostAllocation

[Inventory accounting and stock valuation](../../finance/inventory-accounting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Freight and duties follow capitalization policy. Allocation amounts add to approved charge; recoverable tax is separate. Allocate later costs to stock on hand, sold cost or approved variance as appropriate.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `supplier_charge_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `layer_id` | → StockCostLayer | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `basis` | {units,value,weight,manual} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `driver` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `allocated` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `policy_version` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `approved_by_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### supplier_charge_ref

Use scoped or external reference for `LandedCostAllocation.supplier_charge_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified supplier_charge_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped supplier_charge_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No supplier_charge_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### layer_id

The target is [StockCostLayer](StockCostLayer.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockCostLayer·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockCostLayer·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockCostLayer·MISSING | Queue the missing StockCostLayer mapping or reject the command before linking. |
| Wrong scope | StockCostLayer·B01 | Do not attach another church’s StockCostLayer without a supported exchange and local authority. |
| Target rename | Rename StockCostLayer·A01 after linking | The existing layer_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No layer_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### basis

Declared alternatives in owner order: `units`, `value`, `weight`, `manual`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | units | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_basis | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### driver

Use exact decimal measure for `LandedCostAllocation.driver`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No driver at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allocated

Use exact monetary amount with currency for `LandedCostAllocation.allocated`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No allocated at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### policy_version

Use human-readable text for `LandedCostAllocation.policy_version`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered policy_version in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No policy_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_by_ref

Use scoped or external reference for `LandedCostAllocation.approved_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approved_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approved_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No approved_by_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
