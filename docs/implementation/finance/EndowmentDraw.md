# EndowmentDraw

[Campaigns and specialized gifts](../../finance/special-giving.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Apply the active instrument and spending rule, limits on principal, actual eligible resources and prior draws. Track distribution and subsequent grant or ministry expenditure separately.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `rule_id` | → EndowmentSpendingRule | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `period_id` | → FiscalPeriod | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `measured_value` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `authorized_max` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `approved_draw` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `destination_fund_ref` | → Fund | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `approval_ref` | Owner-scoped business value; see the record rule | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `actual_transfer_ref` | ? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### rule_id

The target is [EndowmentSpendingRule](EndowmentSpendingRule.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EndowmentSpendingRule·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | EndowmentSpendingRule·MISSING | Queue the missing EndowmentSpendingRule mapping or reject the command before linking. |
| Wrong scope | EndowmentSpendingRule·B01 | Do not attach another church’s EndowmentSpendingRule without a supported exchange and local authority. |
| Target rename | Rename EndowmentSpendingRule·A01 after linking | The existing rule_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No rule_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### period_id

The target is [FiscalPeriod](FiscalPeriod.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FiscalPeriod·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | FiscalPeriod·MISSING | Queue the missing FiscalPeriod mapping or reject the command before linking. |
| Wrong scope | FiscalPeriod·B01 | Do not attach another church’s FiscalPeriod without a supported exchange and local authority. |
| Target rename | Rename FiscalPeriod·A01 after linking | The existing period_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No period_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### measured_value

Use exact monetary amount with currency for `EndowmentDraw.measured_value`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No measured_value at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authorized_max

Use exact monetary amount with currency for `EndowmentDraw.authorized_max`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No authorized_max at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approved_draw

Use exact monetary amount with currency for `EndowmentDraw.approved_draw`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No approved_draw at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### destination_fund_ref

The target is [Fund](Fund.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Fund·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Fund·MISSING | Queue the missing Fund mapping or reject the command before linking. |
| Wrong scope | Fund·B01 | Do not attach another church’s Fund without a supported exchange and local authority. |
| Target rename | Rename Fund·A01 after linking | The existing destination_fund_ref keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No destination_fund_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### approval_ref

Use scoped or external reference for `EndowmentDraw.approval_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified approval_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped approval_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No approval_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### actual_transfer_ref

Use scoped or external reference for `EndowmentDraw.actual_transfer_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified actual_transfer_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped actual_transfer_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No actual_transfer_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Use versioned classification or status code for `EndowmentDraw.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
