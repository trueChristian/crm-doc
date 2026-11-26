# CommunityDistribution

[Missions and community service](../../ministry/missions.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One operating session, with named, pseudonymous or anonymous recipients as policy allows. Capture eligibility privately and provide a manual review route.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `project_id` | → MissionProject | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `occurrence_id` | → EventOccurrence | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `steward_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `site_label` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `eligibility_policy` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `identity_mode` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### project_id

The target is [MissionProject](MissionProject.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MissionProject·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MissionProject·MISSING | Queue the missing MissionProject mapping or reject the command before linking. |
| Wrong scope | MissionProject·B01 | Do not attach another church’s MissionProject without a supported exchange and local authority. |
| Target rename | Rename MissionProject·A01 after linking | The existing project_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No project_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### occurrence_id

The target is [EventOccurrence](EventOccurrence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EventOccurrence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | EventOccurrence·MISSING | Queue the missing EventOccurrence mapping or reject the command before linking. |
| Wrong scope | EventOccurrence·B01 | Do not attach another church’s EventOccurrence without a supported exchange and local authority. |
| Target rename | Rename EventOccurrence·A01 after linking | The existing occurrence_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No occurrence_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### steward_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing steward_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No steward_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### site_label

Use human-readable text for `CommunityDistribution.site_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered site_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No site_label at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligibility_policy

Use versioned classification or status code for `CommunityDistribution.eligibility_policy`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active eligibility_policy code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped eligibility_policy code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No eligibility_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### identity_mode

Use versioned classification or status code for `CommunityDistribution.identity_mode`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active identity_mode code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped identity_mode code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No identity_mode at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Use versioned classification or status code for `CommunityDistribution.state`. Check the relevant vocabulary and permitted transition before applying.

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
| [AssistanceIssue](AssistanceIssue.md).`distribution_id` | CommunityDistribution identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssistanceRound](../administration/AssistanceRound.md).`distribution_id` | CommunityDistribution identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Use the minimum evidence allowed by the selected anonymous, pseudonymous or identified mode. A permitted operator may be accountable for receiving or reviewing work without collecting the identity of a protected subject. Keep safe-channel, identity and case evidence apart from releasable totals and narratives; apply the original permissions to the verification evidence.
