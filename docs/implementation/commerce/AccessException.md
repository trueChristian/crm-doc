# AccessException

[Subscriptions, grants and playback](../../commerce/access.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unavailable paid releases, failed assignment, chargebacks, outages and rights changes route to a recoverable support case with a customer-visible, discreet status.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `grant_id` | ref AccessGrant? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `order_line_id` | ref OrderLine? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `reason` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `opened_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `assigned_to` | ref UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `remedy` | extend/replace/refund/none? | Optional under owner conditions | [enum](../value-conventions.md#enum) |
| `requires_approval` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `resolved_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### grant_id

The target is [AccessGrant](AccessGrant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessGrant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AccessGrant·MISSING | Queue the missing AccessGrant mapping or reject the command before linking. |
| Wrong scope | AccessGrant·B01 | Do not attach another church’s AccessGrant without a supported exchange and local authority. |
| Target rename | Rename AccessGrant·A01 after linking | The existing grant_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No grant_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### order_line_id

The target is [OrderLine](OrderLine.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OrderLine·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OrderLine·MISSING | Queue the missing OrderLine mapping or reject the command before linking. |
| Wrong scope | OrderLine·B01 | Do not attach another church’s OrderLine without a supported exchange and local authority. |
| Target rename | Rename OrderLine·A01 after linking | The existing order_line_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No order_line_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason

Use versioned classification or status code for `AccessException.reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### opened_at

Use unambiguous point in time for `AccessException.opened_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No opened_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assigned_to

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing assigned_to keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No assigned_to at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### remedy

Declared alternatives in owner order: `extend`, `replace`, `refund`, `none`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | extend | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_remedy | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Absent in intake | No remedy provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### requires_approval

Use explicit logical choice for `AccessException.requires_approval`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No requires_approval at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### resolved_at

Use unambiguous point in time for `AccessException.resolved_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No resolved_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
