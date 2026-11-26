# AdmissionSaleUnit

[Registration, tickets and attendance](../../ministry/registration.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One seat-bearing unit has one active place. Unique order line, positive unit ordinal and admission component. An unnamed three-seat allocation creates three stable units before individual holders are known. A separately priced adult and child receive separate line identifiers. Historical allocations survive a transfer or cancellation.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `place_id` | → RegistrationPlace | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `order_line_id` | → OrderLine | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `unit_ordinal` | count | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `component_key` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `parent_bundle_line_id` | → OrderLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `handoff_id` | → OrderHandoff | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `list_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `discount_amount` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `allocated_net` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `allocated_tax` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `amount_due` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `financial_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `seat_outcome` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### place_id

The target is [RegistrationPlace](RegistrationPlace.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RegistrationPlace·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RegistrationPlace·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RegistrationPlace·MISSING | Queue the missing RegistrationPlace mapping or reject the command before linking. |
| Wrong scope | RegistrationPlace·B01 | Do not attach another church’s RegistrationPlace without a supported exchange and local authority. |
| Target rename | Rename RegistrationPlace·A01 after linking | The existing place_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No place_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### order_line_id

The target is [OrderLine](../commerce/OrderLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderLine·MISSING | Queue the missing OrderLine mapping or reject the command before linking. |
| Wrong scope | OrderLine·B01 | Do not attach another church’s OrderLine without a supported exchange and local authority. |
| Target rename | Rename OrderLine·A01 after linking | The existing order_line_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No order_line_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### unit_ordinal

Use whole-number measure for `AdmissionSaleUnit.unit_ordinal`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No unit_ordinal at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### component_key

Use versioned classification or status code for `AdmissionSaleUnit.component_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active component_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped component_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No component_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_bundle_line_id

The target is [OrderLine](../commerce/OrderLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderLine·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderLine·MISSING | Queue the missing OrderLine mapping or reject the command before linking. |
| Wrong scope | OrderLine·B01 | Do not attach another church’s OrderLine without a supported exchange and local authority. |
| Target rename | Rename OrderLine·A01 after linking | The existing parent_bundle_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_bundle_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### handoff_id

The target is [OrderHandoff](../commerce/OrderHandoff.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderHandoff·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OrderHandoff·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OrderHandoff·MISSING | Queue the missing OrderHandoff mapping or reject the command before linking. |
| Wrong scope | OrderHandoff·B01 | Do not attach another church’s OrderHandoff without a supported exchange and local authority. |
| Target rename | Rename OrderHandoff·A01 after linking | The existing handoff_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No handoff_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `AdmissionSaleUnit.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### list_amount

Use exact monetary amount with currency for `AdmissionSaleUnit.list_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No list_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### discount_amount

Use exact monetary amount with currency for `AdmissionSaleUnit.discount_amount`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No discount_amount at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allocated_net

Use exact monetary amount with currency for `AdmissionSaleUnit.allocated_net`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No allocated_net at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### allocated_tax

Use exact monetary amount with currency for `AdmissionSaleUnit.allocated_tax`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No allocated_tax at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount_due

Use exact monetary amount with currency for `AdmissionSaleUnit.amount_due`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount_due at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### financial_state

Use versioned classification or status code for `AdmissionSaleUnit.financial_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active financial_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped financial_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No financial_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### seat_outcome

Use versioned classification or status code for `AdmissionSaleUnit.seat_outcome`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active seat_outcome code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped seat_outcome code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No seat_outcome at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AdmissionSaleAdjustment](AdmissionSaleAdjustment.md).`unit_id` | AdmissionSaleUnit identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AdmissionSettlementPart](AdmissionSettlementPart.md).`unit_id` | AdmissionSaleUnit identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
