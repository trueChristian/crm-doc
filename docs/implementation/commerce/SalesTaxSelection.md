# SalesTaxSelection

[Prices, tax and delivery quotes](../../commerce/pricing.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Commerce records why the finance-approved treatment applies. Finance tax controls own TaxRuleVersion and FinanceTaxComponent, including unit, line or document rounding and component order and base. Multiple applicable jurisdictions have independent selections.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `quote_line_id` | ref QuoteLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `tax_rule_version_id` | ref TaxRuleVersion | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `jurisdiction` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `decision_date` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `evidence_rule_ref` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `evidence_snapshot_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `reason` | tax_due/exempt/outside_scope/under_review | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `selected_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `reviewed_by` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### quote_line_id

The target is [QuoteLine](QuoteLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | QuoteLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | QuoteLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | QuoteLine·MISSING | Queue the missing QuoteLine mapping or reject the command before linking. |
| Wrong scope | QuoteLine·B01 | Do not attach another church’s QuoteLine without a supported exchange and local authority. |
| Target rename | Rename QuoteLine·A01 after linking | The existing quote_line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No quote_line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax_rule_version_id

The target is [TaxRuleVersion](../finance/TaxRuleVersion.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TaxRuleVersion·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | TaxRuleVersion·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | TaxRuleVersion·MISSING | Queue the missing TaxRuleVersion mapping or reject the command before linking. |
| Wrong scope | TaxRuleVersion·B01 | Do not attach another church’s TaxRuleVersion without a supported exchange and local authority. |
| Target rename | Rename TaxRuleVersion·A01 after linking | The existing tax_rule_version_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No tax_rule_version_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### jurisdiction

Use versioned classification or status code for `SalesTaxSelection.jurisdiction`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active jurisdiction code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped jurisdiction code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No jurisdiction at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision_date

Use civil calendar date for `SalesTaxSelection.decision_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No decision_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_rule_ref

Use scoped or external reference for `SalesTaxSelection.evidence_rule_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_rule_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_rule_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No evidence_rule_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_snapshot_ref

Use scoped or external reference for `SalesTaxSelection.evidence_snapshot_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_snapshot_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_snapshot_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_snapshot_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason

Declared alternatives in owner order: `tax_due`, `exempt`, `outside_scope`, `under_review`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | tax_due | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_reason | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### selected_at

Use unambiguous point in time for `SalesTaxSelection.selected_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No selected_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reviewed_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewed_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reviewed_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [QuoteTax](QuoteTax.md).`selection_id` | SalesTaxSelection identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
