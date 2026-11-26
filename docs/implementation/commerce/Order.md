# Order

[Checkout, orders and collection](../../commerce/orders.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique organization/number and accepted quote. Purchase identity and donor identity each require their own verification. Derived summary states reconcile to child records.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `organization_id` | ref Organization | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `channel_id` | ref ShopChannel | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `order_number` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `cart_id` | ref Cart? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `quote_id` | ref Quote | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `buyer_account_id` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `buyer_person_id` | ref Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `placed_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `currency` | code | Required when the record reaches its applicable state | [currency](../value-conventions.md#currency) |
| `amount_due` | money | Required when the record reaches its applicable state | [money](../value-conventions.md#money) |
| `terms_version` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `state` | pending/confirmed/part_cancelled/cancelled/completed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `payment_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `fulfilment_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Organization·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### channel_id

The target is [ShopChannel](ShopChannel.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ShopChannel·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ShopChannel·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ShopChannel·MISSING | Queue the missing ShopChannel mapping or reject the command before linking. |
| Wrong scope | ShopChannel·B01 | Do not attach another church’s ShopChannel without a supported exchange and local authority. |
| Target rename | Rename ShopChannel·A01 after linking | The existing channel_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No channel_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### order_number

Use human-readable text for `Order.order_number`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered order_number in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No order_number at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cart_id

The target is [Cart](Cart.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Cart·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Cart·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Cart·MISSING | Queue the missing Cart mapping or reject the command before linking. |
| Wrong scope | Cart·B01 | Do not attach another church’s Cart without a supported exchange and local authority. |
| Target rename | Rename Cart·A01 after linking | The existing cart_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No cart_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### quote_id

The target is [Quote](Quote.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Quote·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Quote·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Quote·MISSING | Queue the missing Quote mapping or reject the command before linking. |
| Wrong scope | Quote·B01 | Do not attach another church’s Quote without a supported exchange and local authority. |
| Target rename | Rename Quote·A01 after linking | The existing quote_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No quote_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### buyer_account_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing buyer_account_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No buyer_account_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### buyer_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing buyer_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No buyer_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### placed_at

Use unambiguous point in time for `Order.placed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No placed_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### currency

Use monetary unit code for `Order.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Incomplete record | No currency at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### amount_due

Use exact monetary amount with currency for `Order.amount_due`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Incomplete record | No amount_due at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### terms_version

Use human-readable text for `Order.terms_version`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered terms_version in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No terms_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `pending`, `confirmed`, `part_cancelled`, `cancelled`, `completed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | pending | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### payment_state

Use versioned classification or status code for `Order.payment_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active payment_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped payment_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No payment_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### fulfilment_state

Use versioned classification or status code for `Order.fulfilment_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active fulfilment_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped fulfilment_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No fulfilment_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CouponUse](CouponUse.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FulfilmentGroup](FulfilmentGroup.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderAmendment](OrderAmendment.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderContact](OrderContact.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderHandoff](OrderHandoff.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OrderLine](OrderLine.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PaymentAttempt](PaymentAttempt.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Refund](Refund.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReturnRequest](ReturnRequest.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SalesDocumentLink](SalesDocumentLink.md).`order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SubscriptionTerm](SubscriptionTerm.md).`renewal_order_id` | Order identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
