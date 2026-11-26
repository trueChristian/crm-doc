# FixedAsset

[Long-lived assets, borrowing and leases](../../finance/assets.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique book/number. Capture original cost or supported noncash valuation, separately identifiable components, custodian and restrictions. Depreciation begins according to approved in-service convention.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `class_id` | → AssetClass | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `parent_asset_id` | → FixedAsset? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `asset_number` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `physical_asset_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `legal_owner_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `funding_source_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `acquired_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `available_for_use_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `acquisition_cost` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `residual_value` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `useful_life_periods` | integer? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `method` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `status` | {construction,ready,in_service,impaired,held_for_disposal,disposed} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### class_id

The target is [AssetClass](AssetClass.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AssetClass·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AssetClass·MISSING | Queue the missing AssetClass mapping or reject the command before linking. |
| Wrong scope | AssetClass·B01 | Do not attach another church’s AssetClass without a supported exchange and local authority. |
| Target rename | Rename AssetClass·A01 after linking | The existing class_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No class_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_asset_id

The target is [FixedAsset](FixedAsset.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FixedAsset·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FixedAsset·MISSING | Queue the missing FixedAsset mapping or reject the command before linking. |
| Wrong scope | FixedAsset·B01 | Do not attach another church’s FixedAsset without a supported exchange and local authority. |
| Target rename | Rename FixedAsset·A01 after linking | The existing parent_asset_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_asset_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### asset_number

Use human-readable text for `FixedAsset.asset_number`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered asset_number in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No asset_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### physical_asset_ref

Use scoped or external reference for `FixedAsset.physical_asset_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified physical_asset_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped physical_asset_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No physical_asset_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### legal_owner_ref

Use scoped or external reference for `FixedAsset.legal_owner_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified legal_owner_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped legal_owner_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No legal_owner_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### funding_source_ref

Use scoped or external reference for `FixedAsset.funding_source_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified funding_source_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped funding_source_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No funding_source_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### description

Use human-readable text for `FixedAsset.description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### acquired_on

Use civil calendar date for `FixedAsset.acquired_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No acquired_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### available_for_use_on

Use civil calendar date for `FixedAsset.available_for_use_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No available_for_use_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### acquisition_cost

Use exact monetary amount with currency for `FixedAsset.acquisition_cost`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No acquisition_cost at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### residual_value

Use exact monetary amount with currency for `FixedAsset.residual_value`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No residual_value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### useful_life_periods

Use whole-number measure for `FixedAsset.useful_life_periods`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No useful_life_periods provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### method

Use versioned classification or status code for `FixedAsset.method`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active method code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped method code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Declared alternatives in owner order: `construction`, `ready`, `in_service`, `impaired`, `held_for_disposal`, `disposed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | construction | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AssetCostEvent](AssetCostEvent.md).`asset_id` | FixedAsset identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssetDisposal](AssetDisposal.md).`asset_id` | FixedAsset identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssetFundingPart](AssetFundingPart.md).`asset_id` | FixedAsset identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DepreciationSchedule](DepreciationSchedule.md).`asset_id` | FixedAsset identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FixedAsset](FixedAsset.md).`parent_asset_id` | FixedAsset identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LoanCopy](../administration/LoanCopy.md).`linked_asset_ref` | FixedAsset identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
