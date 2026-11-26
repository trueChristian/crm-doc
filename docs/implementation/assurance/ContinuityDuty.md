# ContinuityDuty

[Continuity exercises, accountability and reunification](../../assurance/continuity-and-reunification.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Assign lead, participant accountability, family liaison, accessibility, communications and continuity duties. Flag missing qualified cover. Share only the duty information required by the recipient.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `plan_id` | → ContinuityPlan | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `responsibility` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `primary_account_id` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `deputy_account_id` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `coverage_interval` | interval? | Optional under owner conditions | [interval](../value-conventions.md#interval) |
| `resource_or_partner_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `instruction_ref` | protected ID | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `acknowledgment_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ContinuityDuty.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ContinuityDuty·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### plan_id

The target is [ContinuityPlan](ContinuityPlan.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ContinuityPlan·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ContinuityPlan·MISSING | Queue the missing ContinuityPlan mapping or reject the command before linking. |
| Wrong scope | ContinuityPlan·B01 | Do not attach another church’s ContinuityPlan without a supported exchange and local authority. |
| Target rename | Rename ContinuityPlan·A01 after linking | The existing plan_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No plan_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### responsibility

Use versioned classification or status code for `ContinuityDuty.responsibility`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active responsibility code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped responsibility code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No responsibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### primary_account_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing primary_account_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No primary_account_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### deputy_account_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing deputy_account_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No deputy_account_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### coverage_interval

Use effective interval or window for `ContinuityDuty.coverage_interval`. Use a date or instant consistently and record whether each endpoint is inclusive.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ordered boundaries in the declared temporal scale | Use a date or instant consistently and record whether each endpoint is inclusive. |
| Malformed or unmapped | end before start | Return an interval error before scheduling or applying a policy. |
| Adjacent windows | one window ends as the next begins | Select the applicable interval at the common boundary using its stated convention. |
| Open-ended validity | start known and end unspecified | Accept a missing end only if the owner allows open-ended status. |
| Time used falls in a gap | instant is between disjoint valid windows | Report no applicable interval; never silently select the nearest future edition. |
| Absent in intake | No coverage_interval provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### resource_or_partner_ref

Use scoped or external reference for `ContinuityDuty.resource_or_partner_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified resource_or_partner_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped resource_or_partner_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No resource_or_partner_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### instruction_ref

Use scoped or external reference for `ContinuityDuty.instruction_ref`. Resolve against the permitted kind, owning namespace and purpose.
Field access: enforce the declared protection on reads, search, previews, exports and audit evidence as well as the underlying resource value.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified instruction_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped instruction_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No instruction_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### acknowledgment_at

Use unambiguous point in time for `ContinuityDuty.acknowledgment_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No acknowledgment_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
