# StockLocation

[Inventory and custody](../../commerce/inventory.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One organization throughout a location tree. Quarantine and transfer-in-transit cannot promise stock.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `campus_id` | ref Campus? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `organization_id` | ref Organization | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `parent_id` | ref StockLocation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `name` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `kind` | warehouse/bin/counter/quarantine/transit | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `sellable` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `active` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### campus_id

The target is [Campus](../foundation/Campus.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Campus·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Campus·MISSING | Queue the missing Campus mapping or reject the command before linking. |
| Wrong scope | Campus·B01 | Do not attach another church’s Campus without a supported exchange and local authority. |
| Target rename | Rename Campus·A01 after linking | The existing campus_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No campus_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_id

The target is [StockLocation](StockLocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | StockLocation·MISSING | Queue the missing StockLocation mapping or reject the command before linking. |
| Wrong scope | StockLocation·B01 | Do not attach another church’s StockLocation without a supported exchange and local authority. |
| Target rename | Rename StockLocation·A01 after linking | The existing parent_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### code

Use versioned classification or status code for `StockLocation.code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### name

Use human-readable text for `StockLocation.name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `warehouse`, `bin`, `counter`, `quarantine`, `transit`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | warehouse | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sellable

Use explicit logical choice for `StockLocation.sellable`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No sellable at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### active

Use explicit logical choice for `StockLocation.active`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No active at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [Collection](Collection.md).`pickup_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CountSession](CountSession.md).`location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DeliveryMethod](DeliveryMethod.md).`pickup_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FulfilmentGroup](FulfilmentGroup.md).`assigned_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReplenishmentRule](ReplenishmentRule.md).`location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Shipment](Shipment.md).`packing_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockLocation](StockLocation.md).`parent_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockMovement](StockMovement.md).`from_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockMovement](StockMovement.md).`to_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockReceipt](StockReceipt.md).`receiving_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockReservation](StockReservation.md).`location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockTransfer](StockTransfer.md).`from_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockTransfer](StockTransfer.md).`to_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockTransfer](StockTransfer.md).`transit_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Till](Till.md).`stock_location_id` | StockLocation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
