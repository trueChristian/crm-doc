# QuoteTax

[Prices, tax and delivery quotes](../../commerce/pricing.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Freeze selected parameters and amount at quote acceptance. Unique quote line/selection/component. Component must belong to selected rule. Posted FinanceAppliedTaxComponent preserves the originating quote component. Original immutable rows remain accessible when a rule or exemption expires.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `quote_line_id` | ref QuoteLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `selection_id` | ref SalesTaxSelection | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `tax_rule_version_id` | ref TaxRuleVersion | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `tax_component_id` | ref FinanceTaxComponent | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `jurisdiction` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `component_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `taxable_basis` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `rate` | rate | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `included` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `tax_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `calculation_order` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `compound_basis_snapshot` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `rounding_method` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `rounding_level` | unit/line/document | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `allocated_residual` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `exemption_id` | ref ExemptionEvidence? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

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

### selection_id

The target is [SalesTaxSelection](SalesTaxSelection.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SalesTaxSelection·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | SalesTaxSelection·MISSING | Queue the missing SalesTaxSelection mapping or reject the command before linking. |
| Wrong scope | SalesTaxSelection·B01 | Do not attach another church’s SalesTaxSelection without a supported exchange and local authority. |
| Target rename | Rename SalesTaxSelection·A01 after linking | The existing selection_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No selection_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_rule_version_id

The target is [TaxRuleVersion](../finance/TaxRuleVersion.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TaxRuleVersion·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | TaxRuleVersion·MISSING | Queue the missing TaxRuleVersion mapping or reject the command before linking. |
| Wrong scope | TaxRuleVersion·B01 | Do not attach another church’s TaxRuleVersion without a supported exchange and local authority. |
| Target rename | Rename TaxRuleVersion·A01 after linking | The existing tax_rule_version_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No tax_rule_version_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_component_id

The target is [FinanceTaxComponent](../finance/FinanceTaxComponent.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceTaxComponent·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FinanceTaxComponent·MISSING | Queue the missing FinanceTaxComponent mapping or reject the command before linking. |
| Wrong scope | FinanceTaxComponent·B01 | Do not attach another church’s FinanceTaxComponent without a supported exchange and local authority. |
| Target rename | Rename FinanceTaxComponent·A01 after linking | The existing tax_component_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No tax_component_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### jurisdiction

Use versioned classification or status code for `QuoteTax.jurisdiction`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active jurisdiction code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped jurisdiction code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No jurisdiction at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### component_code

Use versioned classification or status code for `QuoteTax.component_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active component_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped component_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No component_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### taxable_basis

Use exact monetary amount with currency for `QuoteTax.taxable_basis`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No taxable_basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rate

Use exact decimal measure for `QuoteTax.rate`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No rate at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### included

Use explicit logical choice for `QuoteTax.included`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No included at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_amount

Use exact monetary amount with currency for `QuoteTax.tax_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No tax_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### calculation_order

Use whole-number measure for `QuoteTax.calculation_order`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No calculation_order at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### compound_basis_snapshot

Use human-readable text for `QuoteTax.compound_basis_snapshot`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered compound_basis_snapshot in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No compound_basis_snapshot at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rounding_method

Use versioned classification or status code for `QuoteTax.rounding_method`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active rounding_method code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped rounding_method code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No rounding_method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### allocated_residual

Use exact monetary amount with currency for `QuoteTax.allocated_residual`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No allocated_residual at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### exemption_id

The target is [ExemptionEvidence](ExemptionEvidence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ExemptionEvidence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ExemptionEvidence·MISSING | Queue the missing ExemptionEvidence mapping or reject the command before linking. |
| Wrong scope | ExemptionEvidence·B01 | Do not attach another church’s ExemptionEvidence without a supported exchange and local authority. |
| Target rename | Rename ExemptionEvidence·A01 after linking | The existing exemption_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No exemption_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [RefundTaxAllocation](RefundTaxAllocation.md).`quote_tax_id` | QuoteTax identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
