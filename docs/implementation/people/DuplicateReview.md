# DuplicateReview

[Personal register and identity resolution](../../people/personal-register.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Show the canonical candidate whose ordered references identify two people in the same organization. Attach minimized person-specific evidence to that candidate. Its one review decides distinct/merge; retain a distinct result until material evidence changes.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | = DuplicateCandidate.id | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `candidate_a_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `candidate_b_id` | → Person | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `evidence_summary` | private text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `reason_codes` | = match_signals | Assigned or projected by owner | [alias](../value-conventions.md#alias) |
| `state` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `reviewed_by` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `reviewed_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `decision_reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Authoritative source: `DuplicateCandidate.id`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DuplicateCandidate.id | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### candidate_a_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing candidate_a_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No candidate_a_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### candidate_b_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing candidate_b_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No candidate_b_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_summary

Use restricted value or protected content reference for `DuplicateReview.evidence_summary`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted evidence_summary supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No evidence_summary provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reason_codes

Authoritative source: `match_signals`. Record one change at that owner and re-evaluate derived access.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | match_signals | Rebuild the projection from its authorized source revision. |
| Malformed or unmapped | independent local value | Route the correction to the owning record. |
| Owner revokes or corrects the source | owner changes revision 7 to 8 | Invalidate the prior projection at the defined effective point. |
| Rebuild after missed update | projection is at revision 6, owner is at 8 | Use authoritative revision and reconcile lag. |
| User lacks access to the source field | grant for the original source expires | Projection does not reveal the value. |
| Independent overwrite | Attempt to replace reason_codes through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### state

Use versioned classification or status code for `DuplicateReview.state`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active state code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped state code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reviewed_by

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing reviewed_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reviewed_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### reviewed_at

Use unambiguous point in time for `DuplicateReview.reviewed_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No reviewed_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### decision_reason

Use human-readable text for `DuplicateReview.decision_reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered decision_reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No decision_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
