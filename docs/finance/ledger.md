# Books, dimensions and double entry

## Set up the reporting entity

A congregation may share a legal entity and treasury with other congregations. Select the book by accountable entity and basis. Configure the fiscal calendar, base currency, chart, default fund and financial roles before opening balances. A ministry or a bank account can serve several funds. A fund can use several bank accounts. Keep these independent when entering or searching transactions.

| Logical table | Fields and relationships | Rules |
| --- | --- | --- |
| FinanceBook | organization_id → Organization, code text, title text, base_currency code, basis {accrual, cash}, calendar_name text, time_zone text, policy_version text, opened_on date, closed_on date? | Unique organization/code. One authoritative posting book per entity/basis/reporting scope. A secondary basis needs an explicit reconciliation bridge. Lock currency after first posting. |
| FiscalPeriod | book_id → FinanceBook, year_label text, period_number integer, starts_on date, ends_on date, state {future,open,restricted,closed}, allowed_batch_class code?, close_revision integer | Inclusive, contiguous non-overlapping accounting dates within book. A restricted period admits only designated closing entries with approval. |
| LedgerAccount | book_id → FinanceBook, code text, name text, parent_id → LedgerAccount?, class {asset,liability,net_assets,income,expense}, normal_side {debit,credit}, posting_allowed boolean, control_kind code?, cash_flow_class code?, valid_from date, valid_to date? | Unique book/code. Prevent cycles. A contra account may have the opposite normal side. Only active posting accounts accept lines. Subledger control accounts require a linked event or authorized opening/migration. |
| Fund | book_id → FinanceBook, code text, name text, category {general,designated,restricted,endowment,agency}, parent_id → Fund?, starts_on date, ends_on date?, purpose text, spending_policy code | Unique book/code. Closing a fund with balances requires approved disposition. An agency fund carries a third-party obligation under the selected policy. |
| FinanceDimension | book_id → FinanceBook, kind {campus,congregation,ministry,project,grant,function,custom}, code text, title text, parent_id → FinanceDimension?, source?, starts_on date, ends_on date? | Normalize Campus and Congregation references through source. Cost centers and projects can span funds. Store hierarchy versions for historical comparison. |
| JournalEntry | book_id → FinanceBook, period_id → FiscalPeriod, number text?, effective_on date, captured_at instant, posted_at instant?, description text, source, rule_version text, state {draft,submitted,approved,posted,rejected,withdrawn}, created_by → UserAccount, approved_by → UserAccount?, reversal_of → JournalEntry?, reversal_reason text? | Unique book/number once posted. Enforce unique book/source event/revision/posting purpose. A reversal is its own posted entry and period. |
| JournalLine | entry_id → JournalEntry, sequence integer, account_id → LedgerAccount, fund_id → Fund, debit_base decimal, credit_base decimal, transaction_currency code, transaction_amount decimal, fx_rate decimal, memo text?, due_on date?, counterparty_ref?, reconciliation_key text? | Unique entry/sequence. Exactly one positive base amount per line, other side zero. Express direction by debit/credit and use a positive transaction amount. Zero-original/base-only rounding or valuation lines require a dedicated posting purpose. |
| JournalLineDimension | line_id → JournalLine, dimension_id → FinanceDimension | Unique line/dimension kind where that kind is single-valued. Split lines for multi-ministry amounts. |
| PostingRuleVersion | book_id → FinanceBook, event_kind code, version integer, valid_from date, valid_until date?, debit_map configuration, credit_map configuration, dimension_rules configuration, approval_policy code, approved_by → UserAccount | One applicable published version per event/date/policy. Preserve the rule used. New versions require sample posting checks and approval. |
| RecurringJournal | book_id → FinanceBook, template_source, recurrence rule, next_due date, ends_on date?, owner_id → UserAccount, approval_mode code, state {active,paused,ended} | One generated draft per recurrence/date, including after a retry. Each occurrence passes normal period and approval checks. |

## Posting contract

1. A producing domain emits one approved business event with original line IDs, amounts, currency, dates, dimensions and original evidence reference. Record its source key before accounting. Return the same posting reference when identical input repeats. Quarantine a conflicting payload under the same key.
2. The preparer previews debits, credits, effective date, affected funds, budget availability and rule version. Missing mappings or a closed period produce a named blocking exception. A correction preserves the submitted failure and captures the approved changes.
3. Recheck permissions, period state, source state and available authorization at posting. Assign the permanent journal number and commit all lines and the source acknowledgement atomically, or expose a durable pending acknowledgement safe to replay. No financial report includes a partially posted entry.
4. Debits equal credits in base currency per entry. Enforce a balancing-by-fund policy when each fund must produce a complete balance sheet. For a genuine interfund cash movement or shared-bank allocation, use explicit reciprocal due-to/from or transfer lines as required. Where funds are analytical only, require a reconciliation of fund movements to book totals; label the reporting mode.
5. Approved lines are immutable when posted. Reverse the complete erroneous posting, then post a replacement, or post a linked incremental adjustment where policy permits. Keep the chain navigable from the source and from any report. Refused or withdrawn drafts remain outside balances.

Store balances as derived sums. Debit-balance account movement is debits less credits; use the reverse for a credit-balance display. Import opening balances by account, fund and dimension at a cutoff, with corresponding open subledger items and reconciliation differences. Block cutover until subledgers and signed opening trial balance agree, allowing clearly identified transitional accounts only with ownership and deadlines.

## Worked interfund event

In a separately balanced fund book a board designates 200 from general resources for youth. Where policy recognizes a fund transfer, debit transfers out 200 and credit pooled cash 200 in General; debit pooled cash 200 and credit transfers in 200 in Youth. The combined bank asset is unchanged and transfer presentation eliminates the internal pair. If only a spending label changes, apply the approved designation model instead. A donor restriction needs its own terms and release evidence.

## Acceptance

- Post a debit of 250 and credits of 200 and 50. A trial balance contains a single source-linked entry even after two simultaneous submissions. Changing a credit to 49.99 prevents all lines posting.
- A cashier can submit a collection and read its deposit status. Attempting to post a manual credit directly to donor receivables requires an authorized control-account workflow.
- A closed-period reversal dated in the next open period leaves the prior issued statement intact. The auditor can traverse both entries, their rule versions, dates and authorizations.
- An inactive account, another entity's fund or a child dimension from the wrong hierarchy is rejected before balances change.
