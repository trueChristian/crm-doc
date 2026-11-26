# StockMovement

[Inventory and custody](../../commerce/inventory.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Immutable posted movement. Quantity positive, endpoints distinct, at least one named. Unique source action/line/leg prevents duplicated posting. Stock lot matches variant. Apply both endpoints as one action.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `variant_id` | ref ProductVariant | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `lot_id` | ref StockLot? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `quantity` | quantity | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `from_location_id` | ref StockLocation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `to_location_id` | ref StockLocation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `kind` | receive/transfer/issue/return/write_off/adjust | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `posted_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `business_date` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `origin_type` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `origin_id` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `origin_line_key` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `reversal_of_id` | ref StockMovement? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `approved_by` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `unit_cost_snapshot` | money? | Optional under owner conditions | [money](../value-conventions.md#money) |
| `currency` | code? | Optional under owner conditions | [currency](../value-conventions.md#currency) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### variant_id

The target is [ProductVariant](ProductVariant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ProductVariant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ProductVariant·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ProductVariant·MISSING | Queue the missing ProductVariant mapping or reject the command before linking. |
| Wrong scope | ProductVariant·B01 | Do not attach another church’s ProductVariant without a supported exchange and local authority. |
| Target rename | Rename ProductVariant·A01 after linking | The existing variant_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No variant_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### lot_id

The target is [StockLot](StockLot.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLot·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockLot·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockLot·MISSING | Queue the missing StockLot mapping or reject the command before linking. |
| Wrong scope | StockLot·B01 | Do not attach another church’s StockLot without a supported exchange and local authority. |
| Target rename | Rename StockLot·A01 after linking | The existing lot_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No lot_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### quantity

Use exact decimal measure for `StockMovement.quantity`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No quantity at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### from_location_id

The target is [StockLocation](StockLocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockLocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockLocation·MISSING | Queue the missing StockLocation mapping or reject the command before linking. |
| Wrong scope | StockLocation·B01 | Do not attach another church’s StockLocation without a supported exchange and local authority. |
| Target rename | Rename StockLocation·A01 after linking | The existing from_location_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No from_location_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### to_location_id

The target is [StockLocation](StockLocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockLocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockLocation·MISSING | Queue the missing StockLocation mapping or reject the command before linking. |
| Wrong scope | StockLocation·B01 | Do not attach another church’s StockLocation without a supported exchange and local authority. |
| Target rename | Rename StockLocation·A01 after linking | The existing to_location_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No to_location_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### kind

Declared alternatives in owner order: `receive`, `transfer`, `issue`, `return`, `write_off`, `adjust`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | receive | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### posted_at

Use unambiguous point in time for `StockMovement.posted_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No posted_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### business_date

Use civil calendar date for `StockMovement.business_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No business_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### origin_type

Use versioned classification or status code for `StockMovement.origin_type`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active origin_type code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped origin_type code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No origin_type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### origin_id

Use scoped or external reference for `StockMovement.origin_id`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified origin_id in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped origin_id | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No origin_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### origin_line_key

Use human-readable text for `StockMovement.origin_line_key`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered origin_line_key in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No origin_line_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reversal_of_id

The target is [StockMovement](StockMovement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockMovement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockMovement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockMovement·MISSING | Queue the missing StockMovement mapping or reject the command before linking. |
| Wrong scope | StockMovement·B01 | Do not attach another church’s StockMovement without a supported exchange and local authority. |
| Target rename | Rename StockMovement·A01 after linking | The existing reversal_of_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reversal_of_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approved_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing approved_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No approved_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### unit_cost_snapshot

Use exact monetary amount with currency for `StockMovement.unit_cost_snapshot`. Preserve amount and currency; apply the owner’s scale at the named rounding boundary.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD 24.50 | Preserve amount and currency; apply the owner’s scale at the named rounding boundary. |
| Malformed or unmapped | 24.50 with unresolvable currency | Keep separate or request an approved conversion. |
| Amounts of 0.10 and 0.20 in one currency | 0.10 + 0.20 in the same currency | Their exact sum is 0.30 at two decimals. |
| Value has extra fractional digits | 1.005 in a two-decimal settlement profile | Apply the documented calculation or settlement precision; retain relevant intermediate evidence. |
| Reversal or credit | credit of one partially refunded component | Use the original component currency and owner’s sign/direction convention. |
| Absent in intake | No unit_cost_snapshot provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### currency

Use monetary unit code for `StockMovement.currency`. Resolve the code and its precision as of the transaction.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | NAD | Resolve the code and its precision as of the transaction. |
| Malformed or unmapped | ambiguous $ | Request the unambiguous currency. |
| Two amounts have different currencies | 24.50 NAD and 24.50 USD | Report separate totals or translate using recorded rates. |
| Catalog changes after document issue | document issued before currency-profile revision | The stored document keeps its currency. |
| Unrecognized imported code | unmapped monetary unit in staged transaction | Stage unmapped currency; block financial posting. |
| Absent in intake | No currency provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AssistanceIssue](../ministry/AssistanceIssue.md).`stock_movement_ref` | StockMovement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CountLine](CountLine.md).`movement_id` | StockMovement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CountSession](CountSession.md).`cutoff_movement_ref` | StockMovement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [HospitalityAllocation](../ministry/HospitalityAllocation.md).`stock_movement_ref` | StockMovement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InventoryValuationEvent](../finance/InventoryValuationEvent.md).`stock_movement_ref` | StockMovement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReturnLine](ReturnLine.md).`movement_id` | StockMovement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ShipmentLine](ShipmentLine.md).`movement_id` | StockMovement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockMovement](StockMovement.md).`reversal_of_id` | StockMovement identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
