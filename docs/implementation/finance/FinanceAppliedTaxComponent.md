# FinanceAppliedTaxComponent

[Financial controls, localization and exchanges](../../finance/controls.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Immutable for each invoice, credit, purchase or gift-benefit portion. Sum of components matches issued line tax and reported document totals. Credit components reference the originals and support multiple partial reversals up to the original base/tax, absorbing remaining rounding on the final credit.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `tax_rule_version_id` | → TaxRuleVersion | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `tax_component_id` | → FinanceTaxComponent | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `source_line_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `quote_tax_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `original_applied_id` | → FinanceAppliedTaxComponent? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `jurisdiction_at_supply` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `component_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `order_applied` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `taxable_base` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `rate_used` | decimal | Required when the record reaches its applicable state | [ratio](../value-conventions.md#ratio) |
| `included` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `tax_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `recoverable_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `evidence_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `allocation_rounding_delta` | signed_money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `document_revision` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |

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

### tax_component_id

The target is [FinanceTaxComponent](FinanceTaxComponent.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceTaxComponent·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FinanceTaxComponent·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FinanceTaxComponent·MISSING | Queue the missing FinanceTaxComponent mapping or reject the command before linking. |
| Wrong scope | FinanceTaxComponent·B01 | Do not attach another church’s FinanceTaxComponent without a supported exchange and local authority. |
| Target rename | Rename FinanceTaxComponent·A01 after linking | The existing tax_component_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No tax_component_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### source_line_ref

Use scoped or external reference for `FinanceAppliedTaxComponent.source_line_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified source_line_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped source_line_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No source_line_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quote_tax_ref

Use scoped or external reference for `FinanceAppliedTaxComponent.quote_tax_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified quote_tax_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped quote_tax_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No quote_tax_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### original_applied_id

The target is [FinanceAppliedTaxComponent](FinanceAppliedTaxComponent.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceAppliedTaxComponent·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FinanceAppliedTaxComponent·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FinanceAppliedTaxComponent·MISSING | Queue the missing FinanceAppliedTaxComponent mapping or reject the command before linking. |
| Wrong scope | FinanceAppliedTaxComponent·B01 | Do not attach another church’s FinanceAppliedTaxComponent without a supported exchange and local authority. |
| Target rename | Rename FinanceAppliedTaxComponent·A01 after linking | The existing original_applied_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No original_applied_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### jurisdiction_at_supply

Use versioned classification or status code for `FinanceAppliedTaxComponent.jurisdiction_at_supply`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active jurisdiction_at_supply code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped jurisdiction_at_supply code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No jurisdiction_at_supply at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### component_code

Use versioned classification or status code for `FinanceAppliedTaxComponent.component_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active component_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped component_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No component_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### order_applied

Use whole-number measure for `FinanceAppliedTaxComponent.order_applied`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No order_applied at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### taxable_base

Use exact monetary amount with currency for `FinanceAppliedTaxComponent.taxable_base`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No taxable_base at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### rate_used

Use exact ratio, rate or weighting for `FinanceAppliedTaxComponent.rate_used`. Carry the declared unit, direction and calculation precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 1.125 under named rate basis | Carry the declared unit, direction and calculation precision. |
| Malformed or unmapped | rate with unknown direction | Record an undefined result or reject calculation as the owning rule specifies. |
| 0.125 versus 12.5 percent | 0.125 fraction and 12.5 percent | Require the unit before comparing or converting. |
| Inverse rate provided | reciprocal quoted in opposite currency direction | Require explicit direction and an approved conversion. |
| Financial document already issued | historical line after a rate-table correction | Retain the original rate, effective date and rounding basis. |
| Incomplete record | No rate_used at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### included

Use explicit logical choice for `FinanceAppliedTaxComponent.included`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No included at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_amount

Use exact monetary amount with currency for `FinanceAppliedTaxComponent.tax_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No tax_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recoverable_amount

Use exact monetary amount with currency for `FinanceAppliedTaxComponent.recoverable_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No recoverable_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_ref

Use scoped or external reference for `FinanceAppliedTaxComponent.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### allocation_rounding_delta

Use exact monetary amount with currency for `FinanceAppliedTaxComponent.allocation_rounding_delta`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No allocation_rounding_delta at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### document_revision

Use human-readable text for `FinanceAppliedTaxComponent.document_revision`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered document_revision in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No document_revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [FinanceAppliedTaxComponent](FinanceAppliedTaxComponent.md).`original_applied_id` | FinanceAppliedTaxComponent identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RefundTaxAllocation](../commerce/RefundTaxAllocation.md).`credited_component_id` | FinanceAppliedTaxComponent identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RefundTaxAllocation](../commerce/RefundTaxAllocation.md).`original_applied_component_id` | FinanceAppliedTaxComponent identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SalesInvoiceLine](SalesInvoiceLine.md).`tax_component_refs` | FinanceAppliedTaxComponent identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
