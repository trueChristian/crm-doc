# LedgerAccount

[Books, dimensions and double entry](../../finance/ledger.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique book/code. Prevent cycles. A contra account may have the opposite normal side. Only active posting accounts accept lines. Subledger control accounts require a linked event or authorized opening/migration.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `book_id` | → FinanceBook | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `name` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `parent_id` | → LedgerAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `class` | {asset,liability,net_assets,income,expense} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `normal_side` | {debit,credit} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `posting_allowed` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `control_kind` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `cash_flow_class` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `valid_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `valid_to` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### book_id

The target is [FinanceBook](FinanceBook.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FinanceBook·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FinanceBook·MISSING | Queue the missing FinanceBook mapping or reject the command before linking. |
| Wrong scope | FinanceBook·B01 | Do not attach another church’s FinanceBook without a supported exchange and local authority. |
| Target rename | Rename FinanceBook·A01 after linking | The existing book_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No book_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### code

Use human-readable text for `LedgerAccount.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### name

Use human-readable text for `LedgerAccount.name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_id

The target is [LedgerAccount](LedgerAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | LedgerAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | LedgerAccount·MISSING | Queue the missing LedgerAccount mapping or reject the command before linking. |
| Wrong scope | LedgerAccount·B01 | Do not attach another church’s LedgerAccount without a supported exchange and local authority. |
| Target rename | Rename LedgerAccount·A01 after linking | The existing parent_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### class

Declared alternatives in owner order: `asset`, `liability`, `net_assets`, `income`, `expense`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | asset | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_class | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### normal_side

Declared alternatives in owner order: `debit`, `credit`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | debit | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_normal_side | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No normal_side at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### posting_allowed

Use explicit logical choice for `LedgerAccount.posting_allowed`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No posting_allowed at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### control_kind

Use versioned classification or status code for `LedgerAccount.control_kind`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active control_kind code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped control_kind code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No control_kind provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### cash_flow_class

Use versioned classification or status code for `LedgerAccount.cash_flow_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active cash_flow_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped cash_flow_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No cash_flow_class provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### valid_from

Use civil calendar date for `LedgerAccount.valid_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No valid_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### valid_to

Use civil calendar date for `LedgerAccount.valid_to`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No valid_to provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AllocationRule](AllocationRule.md).`offset_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssetClass](AssetClass.md).`accumulated_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssetClass](AssetClass.md).`cost_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssetClass](AssetClass.md).`depreciation_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssetClass](AssetClass.md).`disposal_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BorrowingAgreement](BorrowingAgreement.md).`liability_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BudgetLine](BudgetLine.md).`account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceTaxComponent](FinanceTaxComponent.md).`liability_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceTaxComponent](FinanceTaxComponent.md).`recovery_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FxValuationItem](FxValuationItem.md).`ledger_account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InventoryPolicy](InventoryPolicy.md).`cost_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InventoryPolicy](InventoryPolicy.md).`inventory_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [JournalLine](JournalLine.md).`account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LedgerAccount](LedgerAccount.md).`parent_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OpeningItem](OpeningItem.md).`ledger_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PayComponentRule](PayComponentRule.md).`expense_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PayComponentRule](PayComponentRule.md).`liability_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PurchaseOrderLine](PurchaseOrderLine.md).`account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PurchaseRequestLine](PurchaseRequestLine.md).`account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecognitionSchedule](RecognitionSchedule.md).`offset_account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecognitionSchedule](RecognitionSchedule.md).`recognition_account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RevenueObligation](RevenueObligation.md).`deferral_account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RevenueObligation](RevenueObligation.md).`income_account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SalesInvoiceLine](SalesInvoiceLine.md).`account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SpendingCommitment](SpendingCommitment.md).`account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StoreCredit](../commerce/StoreCredit.md).`liability_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StoredValueLiability](StoredValueLiability.md).`liability_account_ref` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupplierBillLine](SupplierBillLine.md).`account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TreasuryAccount](TreasuryAccount.md).`ledger_account_id` | LedgerAccount identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
