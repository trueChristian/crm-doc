# CountSession

[Inventory and custody](../../commerce/inventory.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Record a reproducible cutoff and whether later movements were paused or tracked separately. Reviewer independent for material adjustments.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `location_id` | ref StockLocation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `scope_description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `snapshot_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `cutoff_movement_ref` | ref StockMovement? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `counter_id` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `reviewer_id` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `state` | prepared/counting/review/posted/cancelled | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### location_id

The target is [StockLocation](StockLocation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockLocation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockLocation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockLocation·MISSING | Queue the missing StockLocation mapping or reject the command before linking. |
| Wrong scope | StockLocation·B01 | Do not attach another church’s StockLocation without a supported exchange and local authority. |
| Target rename | Rename StockLocation·A01 after linking | The existing location_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No location_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scope_description

Use human-readable text for `CountSession.scope_description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered scope_description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No scope_description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### snapshot_at

Use unambiguous point in time for `CountSession.snapshot_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No snapshot_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cutoff_movement_ref

The target is [StockMovement](StockMovement.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | StockMovement·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | StockMovement·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | StockMovement·MISSING | Queue the missing StockMovement mapping or reject the command before linking. |
| Wrong scope | StockMovement·B01 | Do not attach another church’s StockMovement without a supported exchange and local authority. |
| Target rename | Rename StockMovement·A01 after linking | The existing cutoff_movement_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No cutoff_movement_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### counter_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing counter_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No counter_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reviewer_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewer_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reviewer_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `prepared`, `counting`, `review`, `posted`, `cancelled`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | prepared | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CountLine](CountLine.md).`session_id` | CountSession identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
