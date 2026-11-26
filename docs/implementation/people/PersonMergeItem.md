# PersonMergeItem

[Personal register and identity resolution](../../people/personal-register.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One entry per affected reference and domain. Restricted domains return an opaque result without disclosing contents to the registrar.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `merge_id` | → PersonMerge | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `owning_domain` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `record_type` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `record_key` | ID | Required when the record reaches its applicable state | [key](../value-conventions.md#key) |
| `action` | enum(relink, alias, retain, review) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `prior_person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `resulting_person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `outcome` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `PersonMergeItem.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PersonMergeItem·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### merge_id

The target is [PersonMerge](PersonMerge.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PersonMerge·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | PersonMerge·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | PersonMerge·MISSING | Queue the missing PersonMerge mapping or reject the command before linking. |
| Wrong scope | PersonMerge·B01 | Do not attach another church’s PersonMerge without a supported exchange and local authority. |
| Target rename | Rename PersonMerge·A01 after linking | The existing merge_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No merge_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### owning_domain

Use versioned classification or status code for `PersonMergeItem.owning_domain`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active owning_domain code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped owning_domain code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No owning_domain at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### record_type

Use versioned classification or status code for `PersonMergeItem.record_type`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active record_type code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped record_type code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No record_type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### record_key

Use opaque identity or token for `PersonMergeItem.record_key`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PersonMergeItem·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Incomplete record | No record_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### action

Declared alternatives in owner order: `relink`, `alias`, `retain`, `review`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | relink | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_action | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No action at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### prior_person_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing prior_person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No prior_person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### resulting_person_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing resulting_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No resulting_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### outcome

Use versioned classification or status code for `PersonMergeItem.outcome`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active outcome code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped outcome code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No outcome at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
