# DeliveryException

[Delivery and responses](../../communications/delivery-and-responses.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One open exception per delivery/category. A manual resend records actor, permission recheck, reason, scope and the possibility of duplication.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `delivery_id` | Delivery ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `category` | no_route/reassigned/ambiguous/invalid_target/outage/cost_cap | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `opened_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `owner_id` | UserAccount ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `reviewed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `resolution` | retry/change_destination/use_manual_service/accept_unknown/close | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `evidence_note` | restricted text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### delivery_id

The target is [Delivery](Delivery.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Delivery·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Delivery·MISSING | Queue the missing Delivery mapping or reject the command before linking. |
| Wrong scope | Delivery·B01 | Do not attach another church’s Delivery without a supported exchange and local authority. |
| Target rename | Rename Delivery·A01 after linking | The existing delivery_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No delivery_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### category

Declared alternatives in owner order: `no_route`, `reassigned`, `ambiguous`, `invalid_target`, `outage`, `cost_cap`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | no_route | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_category | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No category at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### opened_at

Use unambiguous point in time for `DeliveryException.opened_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No opened_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### owner_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing owner_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No owner_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reviewed_at

Use unambiguous point in time for `DeliveryException.reviewed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No reviewed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### resolution

Declared alternatives in owner order: `retry`, `change_destination`, `use_manual_service`, `accept_unknown`, `close`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | retry | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_resolution | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No resolution at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_note

Use restricted value or protected content reference for `DeliveryException.evidence_note`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted evidence_note supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No evidence_note provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
