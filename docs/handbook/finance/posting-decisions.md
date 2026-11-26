# Posting decisions and replay

## What the posting service must decide

A posted line answers five questions: which book owns the event, when the economic event qualifies for recognition, which party owns each amount, what entry records that change, and which subsequent event settles it. Determine those answers before selecting accounts. A checkout, bank notification or imported email may describe the same money as a separate notice. A business document can give rise to several genuinely different accounting events over its life.

The operational system assigns a stable event identity, a source revision and an economic transaction reference. A sale with a gift portion has one capture owner and multiple named allocations. A supplier can reuse an invoice number across legal entities. A processor can reuse a payout identifier across merchant accounts. Construct the idempotency scope using the book, issuing party or source namespace, source event and posting purpose. Compare a canonical fingerprint of the economic payload with the stored one. A harmless change in display description must not turn a retry into a second payment.

| Situation presented | Required decision | What the person handling it sees |
| --- | --- | --- |
| Authorization for 100, later captured for 95 | An authorization can reserve purchasing power. The 95 capture is the monetary event. Expired authority releases the reservation. | Authorized and actually captured figures, currency, timestamps and remaining permitted capture. |
| Duplicate event with identical economic fingerprint | Return the same journal and acknowledgement, including when the original acknowledgement was lost. | Original reference and completed status; no additional debit, credit or document number. |
| Same event key with amount 96 instead of 95 | Quarantine, retain both fingerprints and require issuer confirmation or new corrective event. | Conflict at the exact original line with differences, contact and permitted resolution. |
| Refund notice delivered before the original sale | Register receipt of the notice, reserve the referenced amount for investigation, wait for the capture or an independently authorized historical import. | Unmatched notice with expected original key, amount and age. |
| Missing bank, tax, clearing or restricted-fund mapping | Error on the specific mapping before creating a posted entry. If an actual bank movement has already occurred, reconcile it via approved temporary treatment with ownership and deadline. | Which book, date, account purpose and rule are missing; any controlled suspense item is visible separately. |
| Period closes after preview and before execution | Recheck the effective period and authority at commit. Return a decision request for next permissible date or controlled reopening. | Proposed and permitted dates, affected period, original evidence and reviewer. |
| Same approval twice, or concurrent entry on the same source | Exactly one transition posts and reserves its assigned number. The other request receives that outcome. | A single source balance, single approval trail and unchanged posted totals on retry. |
| Source canceled after legitimate recognition | Cancel remaining obligations and issue linked adjustments for recognized portions as warranted. | Original, adjustment, open financial consequences and owner. |

## Validate the proposed posting

Load the book's approved policy for the effective date and jurisdiction. Keep the policy edition and the facts that selected it. Compare transaction currency, source money precision, book currency, rate direction, earned/delivered amounts, parent legal entity, permitted fund and active dimensions. Verify that every control-account line points to an open item, treasury event, specialist schedule or authorized opening record. Verify balancing in book currency to the smallest unit and, when configured, for each fund. A conversion can introduce rounding; calculate and explicitly assign a permitted residual. Never distribute a shortage across donor restrictions merely to make a file post.

Preview should show the financial source total, tax/fee/gift subdivisions, date of the transaction, accounting date, date the request reached the system and actual time of posting. A backdated payment with today's timestamp is still a backdated payment. If a consolidation pack was already issued for the accounting date, put its downstream effect on the approval screen. For a period-spanning transaction, retain the source event once and generate separate date-specific recognized portions, each with its own completion key.

Verify whether there is authority for the exact financial payload. A delegation valid for up to 500 cannot approve two displayed 300 installments of a single 600 committed obligation if the configured limit applies to total exposure. A supplier destination change after approval invalidates the transfer authorization even if amounts stay fixed. For rotating approvers, resolve scope, validity dates, conflicts and the replacement actor; release requires the rule to hold at execution.

## Worked order of arrival

A retreat costs 120. In this fixture the church recognizes revenue on attendance, accrues an approved refund obligation immediately, and pays a provider fee of 3 on settlement. There is one booking and one payer. Opening balances for the booking are zero.

| Arrival | Posted debit | Posted credit | Expected resulting state |
| --- | --- | --- | --- |
| Booking and card authorization | None | None | One operational reservation, zero ledger cash and customer liability. |
| Provider confirms capture of 120 | Provider clearing 120 | Deferred retreat revenue 120 | Clearing 120 receivable and obligation 120. Customer sees paid. |
| Same capture arrives from the portal | None | None | Original journal returned. Available value remains 120. |
| Attendance accepted for the paid place | Deferred retreat revenue 120 | Retreat revenue 120 | Obligation zero; revenue 120. |
| Provider pays 117 and retains 3 | Bank 117 and fees 3 | Provider clearing 120 | Bank 117, clearing zero. |
| Staff approve a partial 30 refund for a service issue | Sales adjustments 30 | Refund payable 30 | Earned revenue net 90; cash still 117. |
| Provider confirms refund execution | Refund payable 30 | Provider clearing 30 | Refund payable zero; credit balance on clearing 30 until recovered. |
| Bank debited 30 | Provider clearing 30 | Bank 30 | Bank 87, clearing zero, revenue net 90 and fees 3. |

If the 30 claim is received but staff decline it, nothing in the last three rows occurs. If approval stands but the provider rejects the payout, leave refund payable 30 until a verified payment mechanism succeeds or a separately authorized resolution changes the obligation. An additional request for 100 after a confirmed 30 refund must fail the over-refund test: only 90 of the 120 original capture remains refundable before any stricter line allowance.

## Correction and release tests

A data-entry operator accidentally marks a June item as general giving instead of restricted youth giving. On an open June book the approved correction reallocates the precise source portion between fund and income lines; it changes neither receipt number nor church bank. If fund books must balance, reassign corresponding cash allocation or valid due-to/from positions. If June has been published, preserve as-issued, assess materiality and route an approved open-period correction or restatement. An operator cannot repair a financial misclassification by changing the text on the donation alone.

A rule edition is approved effective 1 July. A June event received on 2 July uses the June rule unless the church approves different accounting treatment for a new July adjustment. The approval record, both dates and the explanation must be exportable. Two books for different legal entities may each have a journal numbered 105; a lookup always includes the book. A cancelled or reserved serial number in a regulated sequence should remain explainable through a void/gap report. A sequence hole alone is insufficient evidence of a deleted entry.

Test a crash after successful journal storage but before receipt acknowledgement, a duplicate notice during close, a rule change during approval, a mismatching currency, a missing fund, a partial capture and a partially satisfied refund. Each case must end in exactly one of three visible conditions: a durable posted transaction, an explicit pending obligation/event with an owner, or an explained rejection. During replay the report reader can reconcile using a repeatable posting cutoff. See [ledger data and invariants](../../finance/ledger.md) and [financial control records](../../finance/controls.md).
