# AdmissionPaymentNotice

A registration reviewer uses this record to explain which external funding fact applied to a place. Keep the snapshot and its authenticated receipt immutable. A later provider revision can correct the fact. The [registration desk](../../handbook/ministry/admission.md) decides what the church can do with it.

## Field inventory

| Field | Logical declaration | Owner rule |
| --- | --- | --- |
| `place_id` | → RegistrationPlace | Resolve the registration occurrence, church and permitted external unit before accepting the notice. Transferring a permitted ticket preserves the original place identity. |
| `receipt_id` | → InboundReceipt | Must be an authenticated receipt for the approved issuing connection, recipient church and interface edition. A batch may authenticate multiple separately identified units. |
| `external_unit_key` | text | Opaque key from that provider, unique within its agreed namespace. Bind it to one local place at a time. Staff must resolve ambiguous mappings before applying a notice. |
| `external_operation_key` | text | Provider's stable reference for this funding or refund action. A split tender, whole booking and partial refund can have separate operation keys. |
| `provider_revision` | count | Monotonically ordered per provider unit, starting at the agreed initial revision. Unique connection, unit and revision. Preserve a conflicting duplicate for review. |
| `funding_state` | code | Normalize provider-defined states into pending, partial, funded, declined or reversed under the agreed edition. An unknown code needs review. A waived or free place uses the church's own admission policy. |
| `refund_state` | code | None, requested, pending, partial, completed or declined. Releasing a local seat never implies money was returned. |
| `reported_amount` | money? | Optional cumulative net amount received for this external unit as of the revision, with exact decimal amount and currency. Never sum successive snapshots. A provider that cannot supply this agreed measure omits it. Keep a payment dispute separate from a currency conversion. |
| `observed_at` | instant | Provider observation time. The receipt supplies the independent arrival time. Use the ordered revision when late notices have the same observation time. |

## Applying the notice

1. Match the issuer, purpose, subject unit, church and explicit allocation. Validate the whole snapshot and quarantine conflicting copies or cross-scope unit claims. A provider with no ordered per-unit revision must supply an authoritative snapshot through a compatible adapter before automatic action.
2. Store the snapshot, result and operation reference with the receipt. Compare with existing revisions. For a missing predecessor, hold for reconciliation or retrieve the current authoritative state using the agreed contract. A duplicate has one effect even if different carriers delivered it.
3. If this place becomes eligible for confirmation, recheck the current hold, all capacity pools and the family grouping policy in one local decision. A fully funded place can still require a remedy because the hold expired or another condition is unmet.
4. A later reversal or chargeback opens a review under the event terms. Preserve actual admissions and attendance. A cancellation or refund decision applies to the mapped unit alone. Protect amounts, payer identity and reference lookups from other households and door staff.

| Probe | Expected disposition |
| --- | --- |
| Two source systems use unit ID 123 | Match only in the issuing connection and recipient church. |
| Two callbacks carry the same unit revision and identical content | One snapshot and one effective admission action. Preserve delivery evidence. |
| The same unit revision identifies a different place or amount | Quarantine and assign to a reviewer. Never reassign a valid seat. |
| An older partial notice follows a newer funded snapshot | Keep the newer status and original ticket. |
| The current provider cannot settle an approved refund | Show local place released and remote refund pending. Retrying the refund uses the original operation key. |

[Registration and attendance](../../ministry/registration.md) · [Place](RegistrationPlace.md) · [Inbound receipt](../platform/InboundReceipt.md)
