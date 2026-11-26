# CollectionAttempt

[Children and supervised handover](../../ministry/child-check-in.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Many attempts, one successful final handover. Check current active authority and restrictions at collection. Record refusal or escalation privately. Evidence copies are restricted and retained only under configured policy.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `check_in_id` | → ChildCheckIn | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `claimant_person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `verification_method` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `authority_ref` | → RepresentationAuthority? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `checked_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `operator_id` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `second_reviewer_id` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `result` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `reason_code` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### check_in_id

The target is [ChildCheckIn](ChildCheckIn.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ChildCheckIn·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ChildCheckIn·MISSING | Queue the missing ChildCheckIn mapping or reject the command before linking. |
| Wrong scope | ChildCheckIn·B01 | Do not attach another church’s ChildCheckIn without a supported exchange and local authority. |
| Target rename | Rename ChildCheckIn·A01 after linking | The existing check_in_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No check_in_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### claimant_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing claimant_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No claimant_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### verification_method

Use versioned classification or status code for `CollectionAttempt.verification_method`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active verification_method code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped verification_method code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No verification_method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authority_ref

The target is [RepresentationAuthority](../people/RepresentationAuthority.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RepresentationAuthority·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | RepresentationAuthority·MISSING | Queue the missing RepresentationAuthority mapping or reject the command before linking. |
| Wrong scope | RepresentationAuthority·B01 | Do not attach another church’s RepresentationAuthority without a supported exchange and local authority. |
| Target rename | Rename RepresentationAuthority·A01 after linking | The existing authority_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No authority_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### checked_at

Use unambiguous point in time for `CollectionAttempt.checked_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No checked_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### operator_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing operator_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No operator_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### second_reviewer_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing second_reviewer_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No second_reviewer_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### result

Use versioned classification or status code for `CollectionAttempt.result`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active result code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped result code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No result at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reason_code

Use versioned classification or status code for `CollectionAttempt.reason_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reason_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reason_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No reason_code provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
