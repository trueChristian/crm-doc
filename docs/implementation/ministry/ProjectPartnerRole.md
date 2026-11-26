# ProjectPartnerRole

[Missions and community service](../../ministry/missions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Many-to-many with effective scope e.g. sponsor, host, beneficiary organization or delivery partner. Ended agreements stop further sharing; history keeps its original scope.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `project_id` | → MissionProject | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `partner_id` | → MinistryPartner | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `role` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `from_date` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `until_date` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `agreement_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `share_scope` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### project_id

The target is [MissionProject](MissionProject.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MissionProject·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MissionProject·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MissionProject·MISSING | Queue the missing MissionProject mapping or reject the command before linking. |
| Wrong scope | MissionProject·B01 | Do not attach another church’s MissionProject without a supported exchange and local authority. |
| Target rename | Rename MissionProject·A01 after linking | The existing project_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No project_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### partner_id

The target is [MinistryPartner](MinistryPartner.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryPartner·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | MinistryPartner·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | MinistryPartner·MISSING | Queue the missing MinistryPartner mapping or reject the command before linking. |
| Wrong scope | MinistryPartner·B01 | Do not attach another church’s MinistryPartner without a supported exchange and local authority. |
| Target rename | Rename MinistryPartner·A01 after linking | The existing partner_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No partner_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### role

Use versioned classification or status code for `ProjectPartnerRole.role`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active role code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped role code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### from_date

Use civil calendar date for `ProjectPartnerRole.from_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No from_date at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### until_date

Use civil calendar date for `ProjectPartnerRole.until_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No until_date provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### agreement_ref

Use scoped or external reference for `ProjectPartnerRole.agreement_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified agreement_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped agreement_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No agreement_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### share_scope

Use versioned classification or status code for `ProjectPartnerRole.share_scope`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active share_scope code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped share_scope code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No share_scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AgreementParty](../development/AgreementParty.md).`project_role_id` | ProjectPartnerRole identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
