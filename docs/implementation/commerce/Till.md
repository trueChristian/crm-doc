# Till

[Counter sales and fulfilment](../../commerce/fulfilment.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One configured currency per drawer. Organization and campus scope must agree.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `channel_id` | ref ShopChannel | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `stock_location_id` | ref StockLocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `cash_account_ref` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `active` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### channel_id

The target is [ShopChannel](ShopChannel.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ShopChannel·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ShopChannel·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ShopChannel·MISSING | Queue the missing ShopChannel mapping or reject the command before linking. |
| Wrong scope | ShopChannel·B01 | Do not attach another church’s ShopChannel without a supported exchange and local authority. |
| Target rename | Rename ShopChannel·A01 after linking | The existing channel_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No channel_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### stock_location_id

The target is [StockLocation](StockLocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockLocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockLocation·MISSING | Queue the missing StockLocation mapping or reject the command before linking. |
| Wrong scope | StockLocation·B01 | Do not attach another church’s StockLocation without a supported exchange and local authority. |
| Target rename | Rename StockLocation·A01 after linking | The existing stock_location_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No stock_location_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### code

Use versioned classification or status code for `Till.code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `Till.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cash_account_ref

Use scoped or external reference for `Till.cash_account_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified cash_account_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped cash_account_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No cash_account_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### active

Use explicit logical choice for `Till.active`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No active at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CashShift](CashShift.md).`till_id` | Till identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
