# AccessScope

[Subscriptions, grants and playback](../../commerce/access.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Each scope points to one release or one series. Specify whether future additions and later removals belong to a purchase. Intersect with current rights at use time.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `plan_id` | ref AccessPlan | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `release_id` | ref MediaRelease? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `series_id` | ref SermonSeries? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `included_content_policy` | frozen_set/current_collection | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `use_kind` | stream/read/download | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `audience_policy_ref` | opaque_ref | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### plan_id

The target is [AccessPlan](AccessPlan.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AccessPlan·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AccessPlan·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AccessPlan·MISSING | Queue the missing AccessPlan mapping or reject the command before linking. |
| Wrong scope | AccessPlan·B01 | Do not attach another church’s AccessPlan without a supported exchange and local authority. |
| Target rename | Rename AccessPlan·A01 after linking | The existing plan_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No plan_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### release_id

The target is [MediaRelease](MediaRelease.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MediaRelease·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MediaRelease·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MediaRelease·MISSING | Queue the missing MediaRelease mapping or reject the command before linking. |
| Wrong scope | MediaRelease·B01 | Do not attach another church’s MediaRelease without a supported exchange and local authority. |
| Target rename | Rename MediaRelease·A01 after linking | The existing release_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No release_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### series_id

The target is [SermonSeries](SermonSeries.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | SermonSeries·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | SermonSeries·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | SermonSeries·MISSING | Queue the missing SermonSeries mapping or reject the command before linking. |
| Wrong scope | SermonSeries·B01 | Do not attach another church’s SermonSeries without a supported exchange and local authority. |
| Target rename | Rename SermonSeries·A01 after linking | The existing series_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No series_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### included_content_policy

Declared alternatives in owner order: `frozen_set`, `current_collection`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | frozen_set | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_included_content_policy | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No included_content_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### use_kind

Declared alternatives in owner order: `stream`, `read`, `download`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | stream | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_use_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No use_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### audience_policy_ref

Use scoped or external reference for `AccessScope.audience_policy_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified audience_policy_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped audience_policy_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No audience_policy_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
