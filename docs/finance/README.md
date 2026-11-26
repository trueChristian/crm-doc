# Finance and stewardship

The treasurer must be able to follow a unit of money from the collection plate, online checkout or grant letter into the bank, a fund, the general ledger and a signed report. Someone reviewing that report must be able to travel the same path in reverse, within their permissions. This domain owns accounting recognition, posting, allocation, reconciliation and period close. Operational systems own their original documents.

## Find a task

| Task | Specification |
| --- | --- |
| Configure a book, balances, dimensions and journal rules | [Ledger and posting](ledger.md) |
| Count an offering, allocate a gift, settle a pledge, issue a statement | [Giving and collection](giving.md) |
| Administer a restricted award, release a restriction, steward investments | [Funds, grants and investments](stewardship.md) |
| Pay a supplier, reimburse a worker or recover an advance | [Purchasing and payables](payables.md) |
| Invoice, collect, refund, handle disputed payments or sell a sermon | [Receivables and commerce](receivables.md) |
| Handle cash, bank statements, settlements and foreign currencies | [Treasury and reconciliation](treasury.md) |
| Pay employees and third parties and correct a prior payroll | [Payroll](payroll.md) |
| Capitalize, maintain and dispose of assets, service loans and leases | [Assets and financing](assets.md) |
| Plan ministry spending, allocate overheads and forecast cash | [Budgets and allocations](planning.md) |
| Produce statements, close periods and consolidate churches | [Reporting and close](reporting.md) |
| Localize financial rules, control access and exchange auditable data | [Controls and interfaces](controls.md) |
| Verify a complete month and reconcile the control accounts | [Worked month](worked-month.md) |

## Reading the financial data dictionary

Names are logical records. Every record has an immutable unique `id` and an owning `organization_id → Organization`, directly or through its mandatory parent. An arrow denotes one required parent of the named type, a question mark an optional value, braces an enumerated set, and plural members live in child rows. Multiple child rows may refer to the same parent unless uniqueness is specified. IDs and codes are distinct. Document snapshots preserve what was issued after a contact or rule changes.

`money` means a fixed-precision decimal plus a currency code, explicit on the row or inherited from its header. The currency defines payable precision. Quantities, rates, prices and intermediate calculations may retain additional precision. Dates denote local accounting days. An instant is a time with an unambiguous offset. Amounts are nonnegative unless an item explicitly allows signed values. A reference called `evidence` identifies an access-controlled, versioned attachment. A `source` contains the owner domain, type, stable record identifier, business event and revision. These references must resolve even after an operational item is archived.

The entity that owns a ledger may encompass several congregations, campuses and ministries. Scope every reference to its permitted organization. Inter-entity business requires paired explicit counterparty references and separate books. Common actors include a preparer, independent approver, cashier, recorder, donor-services officer, payroll officer, auditor and report publisher. One user may hold several functions subject to transaction-level separation of duties. Examples are product acceptance fixtures with a stated accounting policy. Each church selects its own approved reporting, recognition, tax and payroll policy for its legal entities.
