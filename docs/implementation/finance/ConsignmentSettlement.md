# ConsignmentSettlement

[Inventory accounting and stock valuation](../../finance/inventory-accounting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Reconcile opening units, deliveries, returns, sales and closing third-party units. Do not capitalize third-party inventory merely because it is physically on premises.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `agreement_id` | → ConsignmentAgreement | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `from_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `until_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `sale_source_refs` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `gross_collections` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `church_share` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `tax` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `supplier_due` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `remittance_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `reviewer_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### agreement_id

The target is [ConsignmentAgreement](ConsignmentAgreement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ConsignmentAgreement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ConsignmentAgreement·MISSING | Queue the missing ConsignmentAgreement mapping or reject the command before linking. |
| Wrong scope | ConsignmentAgreement·B01 | Do not attach another church’s ConsignmentAgreement without a supported exchange and local authority. |
| Target rename | Rename ConsignmentAgreement·A01 after linking | The existing agreement_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No agreement_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### from_on

Use civil calendar date for `ConsignmentSettlement.from_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No from_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### until_on

Use civil calendar date for `ConsignmentSettlement.until_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No until_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sale_source_refs

Use ordered collection or mathematical set for `ConsignmentSettlement.sale_source_refs`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No sale_source_refs at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### gross_collections

Use exact monetary amount with currency for `ConsignmentSettlement.gross_collections`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No gross_collections at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### church_share

Use exact monetary amount with currency for `ConsignmentSettlement.church_share`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No church_share at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### tax

Use exact monetary amount with currency for `ConsignmentSettlement.tax`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No tax at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### supplier_due

Use exact monetary amount with currency for `ConsignmentSettlement.supplier_due`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No supplier_due at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### remittance_ref

Use scoped or external reference for `ConsignmentSettlement.remittance_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified remittance_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped remittance_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No remittance_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reviewer_ref

Use scoped or external reference for `ConsignmentSettlement.reviewer_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified reviewer_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped reviewer_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No reviewer_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
