# Fund

[Books, dimensions and double entry](../../finance/ledger.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique book/code. Closing a fund with balances requires approved disposition. An agency fund carries a third-party obligation under the selected policy.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `book_id` | → FinanceBook | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `name` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `category` | {general,designated,restricted,endowment,agency} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `parent_id` | → Fund? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `starts_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `ends_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `purpose` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `spending_policy` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

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

### code

Use human-readable text for `Fund.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### name

Use human-readable text for `Fund.name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### category

Declared alternatives in owner order: `general`, `designated`, `restricted`, `endowment`, `agency`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | general | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_category | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No category at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_id

The target is [Fund](Fund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Fund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Fund·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Fund·MISSING | Queue the missing Fund mapping or reject the command before linking. |
| Wrong scope | Fund·B01 | Do not attach another church’s Fund without a supported exchange and local authority. |
| Target rename | Rename Fund·A01 after linking | The existing parent_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### starts_on

Use civil calendar date for `Fund.starts_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No starts_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ends_on

Use civil calendar date for `Fund.ends_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No ends_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### purpose

Use human-readable text for `Fund.purpose`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered purpose in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### spending_policy

Use versioned classification or status code for `Fund.spending_policy`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active spending_policy code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped spending_policy code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No spending_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AidAward](../people/AidAward.md).`fund_ref` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidProgram](../people/AidProgram.md).`fund_ref` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AllocationDriver](AllocationDriver.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssetFundingPart](AssetFundingPart.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BasisAdjustment](BasisAdjustment.md).`fund_ref` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BudgetLine](BudgetLine.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CashVoucher](CashVoucher.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CustomerCredit](CustomerCredit.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DepositPart](DepositPart.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EndowmentDraw](EndowmentDraw.md).`destination_fund_ref` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EndowmentSpendingRule](EndowmentSpendingRule.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExpenseItem](ExpenseItem.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Fund](Fund.md).`parent_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundRestriction](FundRestriction.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundraisingAppeal](../development/FundraisingAppeal.md).`finance_fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftAllocation](GiftAllocation.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GiftOfferAssessment](../development/GiftOfferAssessment.md).`intended_fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingCampaign](GivingCampaign.md).`default_fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GrantAward](GrantAward.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InventoryValuationEvent](InventoryValuationEvent.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InvestmentHolding](InvestmentHolding.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [JournalLine](JournalLine.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OpeningItem](OpeningItem.md).`fund_ref` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PaySlipLine](PaySlipLine.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Pledge](Pledge.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProjectSupply](../ministry/ProjectSupply.md).`fund_ref` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PurchaseOrderLine](PurchaseOrderLine.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PurchaseRequestLine](PurchaseRequestLine.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecognitionSchedule](RecognitionSchedule.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SalesInvoiceLine](SalesInvoiceLine.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SpendingCommitment](SpendingCommitment.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StaffAdvance](StaffAdvance.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StewardshipReview](StewardshipReview.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupplierBillLine](SupplierBillLine.md).`fund_id` | Fund identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
