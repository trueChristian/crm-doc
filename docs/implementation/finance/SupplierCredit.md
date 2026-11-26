# SupplierCredit

[Purchasing, payables and reimbursements](../../finance/payables.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Preserve tax, quantity and fund dimensions. Unapplied credit remains in the supplier account and aging.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `supplier_id` | → SupplierAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `original_bill_id` | → SupplierBill? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `number` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `credit_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `line_allocations` | allocation_set | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |
| `reason` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `posting_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### supplier_id

The target is [SupplierAccount](SupplierAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SupplierAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SupplierAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SupplierAccount·MISSING | Queue the missing SupplierAccount mapping or reject the command before linking. |
| Wrong scope | SupplierAccount·B01 | Do not attach another church’s SupplierAccount without a supported exchange and local authority. |
| Target rename | Rename SupplierAccount·A01 after linking | The existing supplier_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No supplier_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### original_bill_id

The target is [SupplierBill](SupplierBill.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SupplierBill·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SupplierBill·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SupplierBill·MISSING | Queue the missing SupplierBill mapping or reject the command before linking. |
| Wrong scope | SupplierBill·B01 | Do not attach another church’s SupplierBill without a supported exchange and local authority. |
| Target rename | Rename SupplierBill·A01 after linking | The existing original_bill_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No original_bill_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### number

Use human-readable text for `SupplierCredit.number`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered number in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### credit_on

Use civil calendar date for `SupplierCredit.credit_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No credit_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount

Use exact monetary amount with currency for `SupplierCredit.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### line_allocations

Use typed value or bounded compound record for `SupplierCredit.line_allocations`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of line_allocations matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for line_allocations | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No line_allocations at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reason

Use human-readable text for `SupplierCredit.reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### posting_ref

Use scoped or external reference for `SupplierCredit.posting_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified posting_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped posting_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No posting_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PayableApplication](PayableApplication.md).`supplier_credit_id` | SupplierCredit identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
