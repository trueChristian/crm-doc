# IncidentReview

[Incidents, near misses and independent review](../../assurance/incidents-and-near-misses.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

A review can identify missing control evidence without attributing blame. Document dissent, alternative explanations, related findings and information still outstanding.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `report_id` | → IncidentReport | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `lead_id` | → UserAccount | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `review_method` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `enabling_conditions` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `evidence_refs` | ID set | Required when the record reaches its applicable state | [list](../value-conventions.md#list) |
| `conclusion` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `uncertainty` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `independence_review_ref` | ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `approved_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `actions_required` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `IncidentReview.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | IncidentReview·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
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
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | IncidentReport·MISSING | Queue the missing IncidentReport mapping or reject the command before linking. |
| Wrong scope | IncidentReport·B01 | Do not attach another church’s IncidentReport without a supported exchange and local authority. |
| Target rename | Rename IncidentReport·A01 after linking | The existing report_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No report_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### lead_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing lead_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No lead_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### review_method

Use versioned classification or status code for `IncidentReview.review_method`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active review_method code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped review_method code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No review_method at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### enabling_conditions

Use human-readable text for `IncidentReview.enabling_conditions`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered enabling_conditions in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No enabling_conditions at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### evidence_refs

Use ordered collection or mathematical set for `IncidentReview.evidence_refs`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Incomplete record | No evidence_refs at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### conclusion

Use human-readable text for `IncidentReview.conclusion`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered conclusion in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No conclusion at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### uncertainty

Use human-readable text for `IncidentReview.uncertainty`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered uncertainty in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No uncertainty provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### independence_review_ref

Use scoped or external reference for `IncidentReview.independence_review_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified independence_review_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped independence_review_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No independence_review_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### approved_at

Use unambiguous point in time for `IncidentReview.approved_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No approved_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### actions_required

Use explicit logical choice for `IncidentReview.actions_required`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No actions_required at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
