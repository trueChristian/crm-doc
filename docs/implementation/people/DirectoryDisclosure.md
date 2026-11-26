# DirectoryDisclosure

[Directory publication and member self-service](../../people/directory-and-self-service.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Field and audience specific. Record a named clerk for paper choices, the verified person or lawful delegate for self-service. An active restriction overrides an allow. When a person's status changes, recompute eligibility and any delegate authority.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `edition_id` | → DirectoryEdition | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `field_key` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `decision` | enum(show, hide) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `purpose` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `authority_id` | → RepresentationAuthority? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `decided_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `recorded_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `effective_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `withdrawn_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `evidence_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `DirectoryDisclosure.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DirectoryDisclosure·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### edition_id

The target is [DirectoryEdition](DirectoryEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DirectoryEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DirectoryEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DirectoryEdition·MISSING | Queue the missing DirectoryEdition mapping or reject the command before linking. |
| Wrong scope | DirectoryEdition·B01 | Do not attach another church’s DirectoryEdition without a supported exchange and local authority. |
| Target rename | Rename DirectoryEdition·A01 after linking | The existing edition_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No edition_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### person_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### field_key

Use versioned classification or status code for `DirectoryDisclosure.field_key`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active field_key code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped field_key code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No field_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### decision

Declared alternatives in owner order: `show`, `hide`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | show | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_decision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No decision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose

Use versioned classification or status code for `DirectoryDisclosure.purpose`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active purpose code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped purpose code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authority_id

The target is [RepresentationAuthority](RepresentationAuthority.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RepresentationAuthority·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RepresentationAuthority·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RepresentationAuthority·MISSING | Queue the missing RepresentationAuthority mapping or reject the command before linking. |
| Wrong scope | RepresentationAuthority·B01 | Do not attach another church’s RepresentationAuthority without a supported exchange and local authority. |
| Target rename | Rename RepresentationAuthority·A01 after linking | The existing authority_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No authority_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### decided_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing decided_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No decided_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recorded_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing recorded_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No recorded_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### effective_at

Use unambiguous point in time for `DirectoryDisclosure.effective_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No effective_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### withdrawn_at

Use unambiguous point in time for `DirectoryDisclosure.withdrawn_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No withdrawn_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### evidence_ref

Use scoped or external reference for `DirectoryDisclosure.evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
