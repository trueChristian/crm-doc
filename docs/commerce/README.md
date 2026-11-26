# Shop, inventory and media

A congregation may offer free recordings, sell study guides at a book table, fulfil online orders or charge for time-limited access to a series. A church can enable each activity independently. The shop can serve guests. Buying, donating, watching and attending leave distinct records and confer no membership status.

## Find a task

| If you need to… | Read |
| --- | --- |
| Publish a book, select its sizes or bundle it with other items | [Catalogue and offers](catalogue.md) |
| Receive stock, reserve the last copy or move boxes between campuses | [Inventory and custody](inventory.md) |
| Price an order, calculate delivery or apply a concession | [Prices, tax and delivery quotes](pricing.md) |
| Take an order with both merchandise and a gift | [Checkout, orders and collection](orders.md) |
| Run a book table, send parcels or issue an invoice | [Counter sales and fulfilment](fulfilment.md) |
| Return damaged stock, resolve a dispute or reconcile a payout | [After-sale service and accounting](settlement.md) |
| Preserve, describe, clear and publish a sermon recording | [Sermon library and publication](media.md) |
| Sell, lend or grant access and handle expiry | [Subscriptions, grants and playback](access.md) |

## Ownership

| Role | Typical duties | Required separation |
| --- | --- | --- |
| Catalogue editor | Describes products, groups offers and drafts price changes | A pricing approver accepts exceptional discounts and effective dates. |
| Stock steward | Receives items, counts stock, prepares transfers | A second authorized person approves material variances. |
| Cashier or fulfilment worker | Takes tenders, packs and hands over orders | Address, phone and pickup details are visible only for assigned work and a defined period. |
| Finance reviewer | Reconciles clearing balances, verifies tax mappings and controls posting | May reconcile without access to a customer's viewing history. |
| Media editor | Describes recordings, handles transcripts and schedules releases | A rights reviewer clears restricted uses. |
| Member, guest or purchaser | Browses eligible items, buys, requests returns and manages access | Purchasing for a recipient does not disclose that recipient's account or church membership. |

## Reading the logical dictionaries

Each row defines a logical table and its own fields. Every table has a stable opaque `id: ID` and belongs to one `Organization`, either directly through `organization_id: ref Organization` or exclusively through its named parent. A reference targets one record, and many children may point to the same parent unless uniqueness is stated. `?` permits absence. Lists of alternatives separated by slashes are enumerations. `code` is a controlled value, `text` is human-readable text, `instant` is an unambiguous point in time, and `date` is a local calendar date. `money` is an exact amount in the explicitly stated or inherited currency, `quantity` is exact in a declared unit, and `rate` is an exact decimal. `ref` identifies a logical record across domain boundaries. `evidence_ref` identifies an access-controlled evidence object. Every business action records actor or service identity, authorization scope, time, reason and correlation identifier. Every external reference is scoped by issuer and organization.

The directory supplies `Person`, `Household`, `UserAccount`, `Congregation` and `Campus`. A household link never authorizes an adult to spend another adult's funds or inspect their purchases. Finance owns the journal, donor record, official receipt, invoices and final tax reporting. Commerce supplies identifiable facts and records acknowledgement, error or reversal from finance. The ministry calendar supplies service and event references. Communications owns delivery and opt-outs. A purchase confirmation and a promotional mailing have different purposes.

## Outcomes and measures

Staff should be able to trace a deposit from bank settlement to tender, order lines and postings, and trace a product copy from receipt to shipment or counted loss. A media officer should be able to explain exactly which rights and grant allowed a particular playback at a given time. Reports distinguish units ordered, fulfilled, returned, currently available, funds collected, tax owed, gifts designated, rights expiring and access delivered. Each quantity and amount carries its as-of time and scope. Private titles, pastoral details and identifiable viewing history stay out of general shop, member-directory and public engagement reports.
