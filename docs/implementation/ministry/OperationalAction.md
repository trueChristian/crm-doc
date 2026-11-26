# OperationalAction

[Operational readiness, interruptions and review](../../ministry/readiness.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

At least one source. An action can require an independent checker where policy calls for it. Retain transfers of responsibility.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `incident_id` | → OperationsIncident? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `briefing_id` | → OperationalBriefing? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `owner_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `assigned_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `due_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `action_text` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `completion_evidence_ref` | id? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `status` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `verified_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### incident_id

The target is [OperationsIncident](OperationsIncident.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OperationsIncident·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OperationsIncident·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OperationsIncident·MISSING | Queue the missing OperationsIncident mapping or reject the command before linking. |
| Wrong scope | OperationsIncident·B01 | Do not attach another church’s OperationsIncident without a supported exchange and local authority. |
| Target rename | Rename OperationsIncident·A01 after linking | The existing incident_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No incident_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### briefing_id

The target is [OperationalBriefing](OperationalBriefing.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OperationalBriefing·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OperationalBriefing·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OperationalBriefing·MISSING | Queue the missing OperationalBriefing mapping or reject the command before linking. |
| Wrong scope | OperationalBriefing·B01 | Do not attach another church’s OperationalBriefing without a supported exchange and local authority. |
| Target rename | Rename OperationalBriefing·A01 after linking | The existing briefing_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No briefing_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### owner_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing owner_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No owner_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### assigned_at

Use unambiguous point in time for `OperationalAction.assigned_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No assigned_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### due_at

Use unambiguous point in time for `OperationalAction.due_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No due_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### action_text

Use human-readable text for `OperationalAction.action_text`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered action_text in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No action_text at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### completion_evidence_ref

Use scoped or external reference for `OperationalAction.completion_evidence_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified completion_evidence_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped completion_evidence_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No completion_evidence_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### status

Use versioned classification or status code for `OperationalAction.status`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active status code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped status code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### verified_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing verified_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No verified_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
