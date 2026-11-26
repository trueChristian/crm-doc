# IncidentParty

[Incidents, near misses and independent review](../../assurance/incidents-and-near-misses.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Permit external or unidentified people, including witnesses, contractors and guests. A party role does not admit liability or become a general profile tag.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `report_id` | → IncidentReport | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `role` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `supplied_identity` | restricted text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `safe_contact_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `contact_authority_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `IncidentParty.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | IncidentParty·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### report_id

The target is [IncidentReport](IncidentReport.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | IncidentReport·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | IncidentReport·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | IncidentReport·MISSING | Queue the missing IncidentReport mapping or reject the command before linking. |
| Wrong scope | IncidentReport·B01 | Do not attach another church’s IncidentReport without a supported exchange and local authority. |
| Target rename | Rename IncidentReport·A01 after linking | The existing report_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No report_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### role

Use versioned classification or status code for `IncidentParty.role`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active role code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped role code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### supplied_identity

Use restricted value or protected content reference for `IncidentParty.supplied_identity`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted supplied_identity supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No supplied_identity provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### safe_contact_ref

Use scoped or external reference for `IncidentParty.safe_contact_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified safe_contact_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped safe_contact_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No safe_contact_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### contact_authority_ref

Use scoped or external reference for `IncidentParty.contact_authority_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified contact_authority_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped contact_authority_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No contact_authority_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
