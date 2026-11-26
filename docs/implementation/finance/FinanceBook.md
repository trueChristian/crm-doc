# FinanceBook

[Books, dimensions and double entry](../../finance/ledger.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique organization/code. One authoritative posting book per entity/basis/reporting scope. A secondary basis needs an explicit reconciliation bridge. Lock currency after first posting.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `organization_id` | → Organization | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `base_currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `basis` | {accrual, cash} | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `calendar_name` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `time_zone` | text | Required when the record reaches its applicable state | [zone](../value-conventions.md#zone) |
| `policy_version` | text | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |
| `opened_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `closed_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### code

Use human-readable text for `FinanceBook.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `FinanceBook.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### base_currency

Use monetary unit code for `FinanceBook.base_currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No base_currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### basis

Declared alternatives in owner order: `accrual`, `cash`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | accrual | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_basis | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No basis at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### calendar_name

Use human-readable text for `FinanceBook.calendar_name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered calendar_name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No calendar_name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### time_zone

Use time zone with civil-time rules for `FinanceBook.time_zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Incomplete record | No time_zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### policy_version

Use revision number or opaque revision token for `FinanceBook.policy_version`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No policy_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### opened_on

Use civil calendar date for `FinanceBook.opened_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No opened_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### closed_on

Use civil calendar date for `FinanceBook.closed_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No closed_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccountingBasisBridge](AccountingBasisBridge.md).`source_book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountingPolicyVersion](AccountingPolicyVersion.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AllocationRule](AllocationRule.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssetClass](AssetClass.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BorrowingAgreement](BorrowingAgreement.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BudgetPlan](BudgetPlan.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CashForecastVersion](CashForecastVersion.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CloseCycle](CloseCycle.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CollectionBatch](CollectionBatch.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ConsolidationMember](ConsolidationMember.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CurrencyRate](CurrencyRate.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CustomerAccount](CustomerAccount.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Deposit](Deposit.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DepreciationSchedule](DepreciationSchedule.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ExpenseClaim](ExpenseClaim.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceApproval](FinanceApproval.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceAuditEvent](FinanceAuditEvent.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceDelegation](FinanceDelegation.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceDimension](FinanceDimension.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceException](FinanceException.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceExchangeBatch](FinanceExchangeBatch.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceHandover](FinanceHandover.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FinanceMigration](FinanceMigration.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FiscalPeriod](FiscalPeriod.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Fund](Fund.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FxValuationRun](FxValuationRun.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Gift](Gift.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingCampaign](GivingCampaign.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GrantAward](GrantAward.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InventoryPolicy](InventoryPolicy.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InventoryValuationEvent](InventoryValuationEvent.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InvestmentHolding](InvestmentHolding.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [JournalEntry](JournalEntry.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LeaseAgreement](LeaseAgreement.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LedgerAccount](LedgerAccount.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PayComponentRule](PayComponentRule.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PayRemittance](PayRemittance.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PaymentRun](PaymentRun.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PayrollAccrual](PayrollAccrual.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PayrollEngagement](PayrollEngagement.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PayrollRun](PayrollRun.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PlannedGift](PlannedGift.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PostingRuleVersion](PostingRuleVersion.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProcessorSettlement](ProcessorSettlement.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PurchaseRequest](PurchaseRequest.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecognitionSchedule](RecognitionSchedule.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecurringJournal](RecurringJournal.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SalesInvoice](SalesInvoice.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SourcePostingAttempt](SourcePostingAttempt.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SpendingCommitment](SpendingCommitment.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StaffAdvance](StaffAdvance.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StoredValueLiability](StoredValueLiability.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupplierAccount](SupplierAccount.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TaxReturn](TaxReturn.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TaxRuleVersion](TaxRuleVersion.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TenderReceipt](TenderReceipt.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TreasuryAccount](TreasuryAccount.md).`book_id` | FinanceBook identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
