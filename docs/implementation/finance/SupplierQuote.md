# SupplierQuote

[Purchasing, payables and reimbursements](../../finance/payables.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Retain competing bids or a documented single-source exception.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `request_id` | → PurchaseRequest | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `supplier_id` | → SupplierAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `quoted_total` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `valid_until` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `quote_evidence` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [structured](../value-conventions.md#structured) |
| `selection_reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `selected` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### request_id

The target is [PurchaseRequest](PurchaseRequest.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PurchaseRequest·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PurchaseRequest·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PurchaseRequest·MISSING | Queue the missing PurchaseRequest mapping or reject the command before linking. |
| Wrong scope | PurchaseRequest·B01 | Do not attach another church’s PurchaseRequest without a supported exchange and local authority. |
| Target rename | Rename PurchaseRequest·A01 after linking | The existing request_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No request_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### quoted_total

Use exact monetary amount with currency for `SupplierQuote.quoted_total`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No quoted_total at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_until

Use civil calendar date for `SupplierQuote.valid_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No valid_until at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### quote_evidence

Use typed value or bounded compound record for `SupplierQuote.quote_evidence`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of quote_evidence matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for quote_evidence | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Incomplete record | No quote_evidence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### selection_reason

Use human-readable text for `SupplierQuote.selection_reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered selection_reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No selection_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### selected

Use explicit logical choice for `SupplierQuote.selected`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No selected at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
