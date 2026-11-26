# MissionProject

[Missions and community service](../../ministry/missions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Proposed, authorized, active, paused, completed, closed or cancelled. Projects can run multiple trips or distributions. Public summaries require publication approval.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `owner_group_id` | → MinistryGroup | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `lead_person_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `sponsoring_congregation_id` | → Congregation | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `start_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `end_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `purpose` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `location_scope` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `public_summary` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `finance_project_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### title

Use human-readable text for `MissionProject.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### owner_group_id

The target is [MinistryGroup](MinistryGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MinistryGroup·MISSING | Queue the missing MinistryGroup mapping or reject the command before linking. |
| Wrong scope | MinistryGroup·B01 | Do not attach another church’s MinistryGroup without a supported exchange and local authority. |
| Target rename | Rename MinistryGroup·A01 after linking | The existing owner_group_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No owner_group_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### lead_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing lead_person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No lead_person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sponsoring_congregation_id

The target is [Congregation](../foundation/Congregation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Congregation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Congregation·MISSING | Queue the missing Congregation mapping or reject the command before linking. |
| Wrong scope | Congregation·B01 | Do not attach another church’s Congregation without a supported exchange and local authority. |
| Target rename | Rename Congregation·A01 after linking | The existing sponsoring_congregation_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No sponsoring_congregation_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### start_on

Use civil calendar date for `MissionProject.start_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No start_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### end_on

Use civil calendar date for `MissionProject.end_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No end_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### purpose

Use human-readable text for `MissionProject.purpose`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered purpose in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### location_scope

Use human-readable text for `MissionProject.location_scope`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered location_scope in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No location_scope provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### public_summary

Use human-readable text for `MissionProject.public_summary`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered public_summary in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No public_summary provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### finance_project_ref

Use scoped or external reference for `MissionProject.finance_project_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified finance_project_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped finance_project_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No finance_project_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Use versioned classification or status code for `MissionProject.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CommunityDistribution](CommunityDistribution.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundraisingAppeal](../development/FundraisingAppeal.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GrantApplication](../development/GrantApplication.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MissionTrip](MissionTrip.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PartnershipAgreement](../development/PartnershipAgreement.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProgramServiceTerms](../administration/ProgramServiceTerms.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProjectMilestone](ProjectMilestone.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProjectPartnerRole](ProjectPartnerRole.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProjectSupply](ProjectSupply.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProposalBudgetLine](../development/ProposalBudgetLine.md).`project_id` | MissionProject identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
