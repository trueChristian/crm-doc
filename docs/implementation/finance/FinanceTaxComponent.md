# FinanceTaxComponent

[Financial controls, localization and exchanges](../../finance/controls.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique version/component. Compound bases reference only earlier components in the same version. Specify precision, inclusive extraction, rounding method and deterministic allocation of document rounding to lines.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `tax_rule_version_id` | → TaxRuleVersion | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `component_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `calculation_order` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `rate` | decimal | Required when the record reaches its applicable state | [ratio](../value-conventions.md#ratio) |
| `recoverable_fraction` | decimal? | Optional under owner conditions | [ratio](../value-conventions.md#ratio) |
| `base_rule` | {net,net_plus_named_components,specific_units} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `included_component_refs` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `rounding_level` | {unit,line,document} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `rounding_method` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `liability_account_ref` | → LedgerAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `recovery_account_ref` | → LedgerAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### tax_rule_version_id

The target is [TaxRuleVersion](TaxRuleVersion.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TaxRuleVersion·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | TaxRuleVersion·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | TaxRuleVersion·MISSING | Queue the missing TaxRuleVersion mapping or reject the command before linking. |
| Wrong scope | TaxRuleVersion·B01 | Do not attach another church’s TaxRuleVersion without a supported exchange and local authority. |
| Target rename | Rename TaxRuleVersion·A01 after linking | The existing tax_rule_version_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No tax_rule_version_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### component_code

Use versioned classification or status code for `FinanceTaxComponent.component_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active component_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped component_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No component_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### calculation_order

Use whole-number measure for `FinanceTaxComponent.calculation_order`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No calculation_order at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rate

Use exact ratio, rate or weighting for `FinanceTaxComponent.rate`. Carry the declared unit, direction and calculation precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 1.125 under named rate basis | Carry the declared unit, direction and calculation precision. |
| Malformed or unmapped | rate with unknown direction | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | 0.125 fraction and 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | reciprocal quoted in opposite currency direction | Require explicit direction and an approved conversion. |
| Financial document already issued | historical line after a rate-table correction | Retain the original rate, effective date and rounding basis. |
| Incomplete record | No rate at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recoverable_fraction

Use exact ratio, rate or weighting for `FinanceTaxComponent.recoverable_fraction`. Carry the declared unit, direction and calculation precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 1.125 under named rate basis | Carry the declared unit, direction and calculation precision. |
| Malformed or unmapped | rate with unknown direction | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | 0.125 fraction and 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | reciprocal quoted in opposite currency direction | Require explicit direction and an approved conversion. |
| Financial document already issued | historical line after a rate-table correction | Retain the original rate, effective date and rounding basis. |
| Absent in intake | No recoverable_fraction provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### base_rule

Declared alternatives in owner order: `net`, `net_plus_named_components`, `specific_units`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | net | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_base_rule | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No base_rule at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### included_component_refs

Use ordered collection or mathematical set for `FinanceTaxComponent.included_component_refs`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No included_component_refs at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rounding_level

Declared alternatives in owner order: `unit`, `line`, `document`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | unit | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_rounding_level | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No rounding_level at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rounding_method

Use versioned classification or status code for `FinanceTaxComponent.rounding_method`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active rounding_method code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped rounding_method code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No rounding_method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### liability_account_ref

The target is [LedgerAccount](LedgerAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LedgerAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | LedgerAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | LedgerAccount·MISSING | Queue the missing LedgerAccount mapping or reject the command before linking. |
| Wrong scope | LedgerAccount·B01 | Do not attach another church’s LedgerAccount without a supported exchange and local authority. |
| Target rename | Rename LedgerAccount·A01 after linking | The existing liability_account_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No liability_account_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recovery_account_ref

The target is [LedgerAccount](LedgerAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LedgerAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | LedgerAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | LedgerAccount·MISSING | Queue the missing LedgerAccount mapping or reject the command before linking. |
| Wrong scope | LedgerAccount·B01 | Do not attach another church’s LedgerAccount without a supported exchange and local authority. |
| Target rename | Rename LedgerAccount·A01 after linking | The existing recovery_account_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No recovery_account_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [FinanceAppliedTaxComponent](FinanceAppliedTaxComponent.md).`tax_component_id` | FinanceTaxComponent identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [QuoteTax](../commerce/QuoteTax.md).`tax_component_id` | FinanceTaxComponent identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
