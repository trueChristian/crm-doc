# CashVoucher

[Banking, cash and currencies](../../finance/treasury.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

A replenishment moves cash; avoid expensing the disbursement again. An imprest report reconciles retained notes plus vouchers to the agreed float.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `session_id` | → CashSession | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `voucher_number` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `paid_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `payee_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `purpose` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `fund_id` | → Fund | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `receipt_evidence` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `approved_by_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `topup_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### session_id

The target is [CashSession](CashSession.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CashSession·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | CashSession·MISSING | Queue the missing CashSession mapping or reject the command before linking. |
| Wrong scope | CashSession·B01 | Do not attach another church’s CashSession without a supported exchange and local authority. |
| Target rename | Rename CashSession·A01 after linking | The existing session_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No session_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### voucher_number

Use human-readable text for `CashVoucher.voucher_number`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered voucher_number in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No voucher_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### paid_on

Use civil calendar date for `CashVoucher.paid_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No paid_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### payee_ref

Use scoped or external reference for `CashVoucher.payee_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified payee_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped payee_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No payee_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose

Use human-readable text for `CashVoucher.purpose`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered purpose in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fund_id

The target is [Fund](Fund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Fund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Fund·MISSING | Queue the missing Fund mapping or reject the command before linking. |
| Wrong scope | Fund·B01 | Do not attach another church’s Fund without a supported exchange and local authority. |
| Target rename | Rename Fund·A01 after linking | The existing fund_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No fund_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount

Use exact monetary amount with currency for `CashVoucher.amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### receipt_evidence

Use scoped or external reference for `CashVoucher.receipt_evidence`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified receipt_evidence in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped receipt_evidence | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No receipt_evidence provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approved_by_ref

Use scoped or external reference for `CashVoucher.approved_by_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approved_by_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approved_by_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No approved_by_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### topup_ref

Use scoped or external reference for `CashVoucher.topup_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified topup_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped topup_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No topup_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
