# IncidentOccurrenceLink

[Incidents, near misses and independent review](../../assurance/incidents-and-near-misses.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One current occurrence per report. Relink by closing the prior link and recording the decision; earlier reports and published counts remain reconstructable.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `occurrence_id` | → IncidentOccurrence | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `report_id` | → IncidentReport | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `effective_from` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `effective_until` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `linked_by` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `justification` | restricted text | Required when the record reaches its applicable state | [protected](../value-conventions.md#protected) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `IncidentOccurrenceLink.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | IncidentOccurrenceLink·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### occurrence_id

The target is [IncidentOccurrence](IncidentOccurrence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | IncidentOccurrence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | IncidentOccurrence·MISSING | Queue the missing IncidentOccurrence mapping or reject the command before linking. |
| Wrong scope | IncidentOccurrence·B01 | Do not attach another church’s IncidentOccurrence without a supported exchange and local authority. |
| Target rename | Rename IncidentOccurrence·A01 after linking | The existing occurrence_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No occurrence_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### report_id

The target is [IncidentReport](IncidentReport.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | IncidentReport·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | IncidentReport·MISSING | Queue the missing IncidentReport mapping or reject the command before linking. |
| Wrong scope | IncidentReport·B01 | Do not attach another church’s IncidentReport without a supported exchange and local authority. |
| Target rename | Rename IncidentReport·A01 after linking | The existing report_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No report_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_from

Use unambiguous point in time for `IncidentOccurrenceLink.effective_from`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No effective_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### effective_until

Use unambiguous point in time for `IncidentOccurrenceLink.effective_until`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No effective_until provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### linked_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing linked_by keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No linked_by at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### justification

Use restricted value or protected content reference for `IncidentOccurrenceLink.justification`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted justification supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Incomplete record | No justification at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
