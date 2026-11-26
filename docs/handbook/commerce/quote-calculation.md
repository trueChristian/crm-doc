# Quote a bundle, coupon and mixed basket

## Counter fixture

A church bookstore sells a workbook and audio study as a bundle for 45.00. Their standalone prices are 40.00 and 20.00. A buyer adds a journal at 12.05, delivery at 3.00 and a voluntary gift of 8.00. A coupon gives exactly 5.00 off the eligible physical goods. The audio is excluded. All prices in this example are exclusive of tax and use one two-decimal currency. An approved rule calculates 10% on physical goods at document level with half-up rounding. Another charges 5% on the audio by line. Delivery and gift are untaxed under this fixture. Standalone weights determine bundle allocation. The coupon uses the post-bundle eligible price. Gift and delivery absorb neither discount.

The operator should be able to read the shop answer from the receipt, the tax answer from the quote and the original promise from each order line. The undiscounted standalone prices may appear in the audit explanation, but posting their amounts and the bundle price together would overstate revenue.

| Step | Basis and calculation | Expected records |
| --- | --- | --- |
| Allocate 45.00 bundle | Workbook 45 × 40/60 = 30.00. Audio 45 × 20/60 = 15.00. | One sellable bundle parent with component references. Either its children carry posting amounts or its parent does, according to a declared method. This case posts children. |
| Resolve coupon scope | Eligible post-bundle values are 30.00 and 12.05. Proportional shares of 5 are approximately 3.5672 and 1.4328. | Allocate 3.57 to workbook and 1.43 to journal. Store promotion identity, rule edition, sequence and pre-discount bases. |
| Find taxable bases | Workbook 26.43, audio 15.00, journal 10.62. | Three immutable sale-line bases and a separate delivery and gift. |
| Allocate rounded physical tax | Physical basis 37.05 × 0.10 = 3.705, rounding to 3.71. Unrounded line shares 2.643 and 1.062 floor to 2.64 and 1.06. Give the extra cent to the largest remainder, the workbook. | Physical tax rows 2.65 and 1.06. Explain the extra cent on the workbook by reference to the original document-level component. |
| Charge audio tax | 15.00 × 0.05 = 0.75. | Audio tax row 0.75, independently identifiable from the physical rule. |
| Confirm total | Goods net 52.05, delivery 3.00, taxes 4.46, gift 8.00. | Amount due 67.51. Customer-facing lines include workbook 29.08, audio 15.75, journal 11.68, delivery 3.00 and gift 8.00. |

## Data handed to each owner

| Producer → consumer | Minimum facts | Consumer decision and evidence |
| --- | --- | --- |
| Catalogue → pricing | Organization, channel, offer, variant SKU, bundle revision, selected components, currency, quantities, standalone price version and weights | Price each component once. Reject cycles, missing weights or a selected variant outside the approved bundle. |
| Purchasing session → pricing | Basket revision, eligibility evidence, coupon, shipping method and destination evidence required by policy | Select eligible lists and promotions at one instant. Reject an expired or already exhausted coupon. Show changed delivery terms before capture. |
| Pricing → finance rules | Supply type, transaction date, jurisdiction evidence, tax class, approved exemption if present, currency and rounding precision | Return applicable TaxRuleVersion and FinanceTaxComponent identities, charge order, bases, inclusive status, rounding level and outcome. Unresolved jurisdiction prevents a binding taxable quote. |
| Accepted quote → orders | Quote ID and revision, accepted and expiry instants, currency, terms, QuoteLine identifiers, net/tax/gross per component, gift purpose and full QuoteTax breakdown | Freeze accepted prices. Checkout references the exact quote and cannot silently reuse a superseded one. |
| Orders → returns and finance | Original OrderLine, QuoteTax and posted FinanceAppliedTaxComponent, dispatched quantity, prior remedies, original discount and residual assignment | Credit only the remaining returnable tax and amount. Replacing a coupon or changing today's rate has no effect on this original allocation. |

## Other calculation policies to exercise

| Configuration change | Example | Expected difference |
| --- | --- | --- |
| Tax amount compounds | Start with net 40.00. Component A charges 10% of 40 = 4.00. Component B charges 5% of net plus A = 2.20. | Gross 46.20. If B were an independent component on net it would be 2.00 and gross 46.00. Retain the component input bases, order and rule edition. |
| Price includes one tax | A separate product gross 22.00 includes one 10% charge. | Net 20.00 and tax 2.00. A full refund returns exactly 22.00. When multiple components are included, apply the approved order and included-tax decomposition. |
| Multiple quantities return separately | Three identical units at net 0.05 each, single document tax 10%, round half up. | Tax total 0.02. Allocate cents across units deterministically, e.g. units 1 and 2 get 0.01 and unit 3 gets zero. Every ordered subset has a traceable credit ceiling. |
| Rounded zero or small monetary units | Run a second market in a zero-decimal unit and a third in a three-decimal unit. | Currency scale determines minor-unit allocation. Cash tender rounding follows its separate policy and does not change product/tax bases without an authorized rounding posting. |
| Prices change during checkout | Accepted quote Q7 is superseded by Q8 before buyer acceptance, or Q7 was accepted before its deadline. | First case requires renewed acceptance. Second case keeps Q7's terms and records capture/stock exceptions separately. |

## Operations and acceptance

A cashier may request a discretionary concession but cannot edit a finance tax component. A reviewer approves an override with scope, former/new amounts, rationale and requester. Capped promotions use one reservation per accepted cart. Two requests for the last redemption can authorize only one discounted sale. When payment becomes uncertain, retain the reservation until the order has an explicit disposition. A second session cannot free it by guessing the coupon or receipt.

Return the workbook alone under a policy permitting component-level returns. The cash value is 26.43 and the tax credit is 2.65, totalling 29.08. The audio and journal stay paid, delivery stays 3.00, and the donor has still given 8.00. The refundable remainder and each tax bucket decrease by the exact reversal. If a new 12% tax rate takes effect tomorrow, returning the journal still credits its original 1.06. A final all-eligible-items return credits no more than 4.46 tax overall. Repeating a previously successful credit leaves every bucket unchanged.
