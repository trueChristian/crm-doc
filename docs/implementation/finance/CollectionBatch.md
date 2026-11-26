# CollectionBatch

[Offerings, gifts and donor service](../../finance/giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One custody record for every movement. Preserve original count and recount. Deposit batches may group several collections using the treasury allocation record.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `book_id` | → FinanceBook | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `service_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `campus_id` | → Campus? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `collected_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `seal_number` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `custodian_id` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `expected_total` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `counted_total` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `state` | {open,counted,verified,posted,deposited,exception} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `deposit_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### book_id

The target is [FinanceBook](FinanceBook.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceBook·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FinanceBook·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FinanceBook·MISSING | Queue the missing FinanceBook mapping or reject the command before linking. |
| Wrong scope | FinanceBook·B01 | Do not attach another church’s FinanceBook without a supported exchange and local authority. |
| Target rename | Rename FinanceBook·A01 after linking | The existing book_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No book_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### service_ref

Use scoped or external reference for `CollectionBatch.service_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified service_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped service_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No service_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### campus_id

The target is [Campus](../foundation/Campus.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Campus·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Campus·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Campus·MISSING | Queue the missing Campus mapping or reject the command before linking. |
| Wrong scope | Campus·B01 | Do not attach another church’s Campus without a supported exchange and local authority. |
| Target rename | Rename Campus·A01 after linking | The existing campus_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No campus_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### collected_on

Use civil calendar date for `CollectionBatch.collected_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No collected_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `CollectionBatch.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### seal_number

Use human-readable text for `CollectionBatch.seal_number`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered seal_number in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No seal_number provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### custodian_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing custodian_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No custodian_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expected_total

Use exact monetary amount with currency for `CollectionBatch.expected_total`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No expected_total provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### counted_total

Use exact monetary amount with currency for `CollectionBatch.counted_total`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No counted_total provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `open`, `counted`, `verified`, `posted`, `deposited`, `exception`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | open | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### deposit_ref

Use scoped or external reference for `CollectionBatch.deposit_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified deposit_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped deposit_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No deposit_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CollectionCount](CollectionCount.md).`batch_id` | CollectionBatch identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CustodyTransfer](CustodyTransfer.md).`batch_id` | CollectionBatch identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DepositPart](DepositPart.md).`collection_batch_id` | CollectionBatch identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Gift](Gift.md).`batch_id` | CollectionBatch identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
