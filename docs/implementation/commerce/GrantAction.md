# GrantAction

[Subscriptions, grants and playback](../../commerce/access.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Append-only, unique source transition. Reversal or reinstatement records fresh evidence. Grants from independent sources remain assessable separately.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `grant_id` | ref AccessGrant | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `kind` | issue/claim/activate/suspend/reinstate/extend/revoke/expire | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `cause_ref` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `effective_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `recorded_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `decision_by` | ref UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `reason` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `before_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `after_state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### grant_id

The target is [AccessGrant](AccessGrant.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessGrant·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AccessGrant·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AccessGrant·MISSING | Queue the missing AccessGrant mapping or reject the command before linking. |
| Wrong scope | AccessGrant·B01 | Do not attach another church’s AccessGrant without a supported exchange and local authority. |
| Target rename | Rename AccessGrant·A01 after linking | The existing grant_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No grant_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `issue`, `claim`, `activate`, `suspend`, `reinstate`, `extend`, `revoke`, `expire`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | issue | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cause_ref

Use scoped or external reference for `GrantAction.cause_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified cause_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped cause_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No cause_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_at

Use unambiguous point in time for `GrantAction.effective_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No effective_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recorded_at

Use unambiguous point in time for `GrantAction.recorded_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No recorded_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing decision_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No decision_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason

Use versioned classification or status code for `GrantAction.reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No reason at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### before_state

Use versioned classification or status code for `GrantAction.before_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active before_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped before_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No before_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### after_state

Use versioned classification or status code for `GrantAction.after_state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active after_state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped after_state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No after_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
