# ReviewDocket

[Complaints, whistleblowing and grievances](../../assurance/complaints-and-grievances.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

A separate docket can be created for each track. Use the workforce PersonnelCase as master for employment decisions, and ProtectionCase for safeguarding. Keep unrelated dockets isolated from one another.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `primary_submission_id` | → ConcernSubmission | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `scope_ref` | ID | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `track` | enum(service, grievance, wrongdoing, retaliation) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `personnel_case_ref` | restricted ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `protection_handoff_ref` | opaque ID? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `owner_role` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `owner_id` | → UserAccount? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `independent_authority_ref` | ID | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `policy_version` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `priority` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `reply_due_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `next_review_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `status` | enum(triage, scoped, investigating, awaiting_response, decision_due, decided, appeal, closed, reopened) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `ReviewDocket.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReviewDocket·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### primary_submission_id

The target is [ConcernSubmission](ConcernSubmission.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ConcernSubmission·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ConcernSubmission·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ConcernSubmission·MISSING | Queue the missing ConcernSubmission mapping or reject the command before linking. |
| Wrong scope | ConcernSubmission·B01 | Do not attach another church’s ConcernSubmission without a supported exchange and local authority. |
| Target rename | Rename ConcernSubmission·A01 after linking | The existing primary_submission_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No primary_submission_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### scope_ref

Use scoped or external reference for `ReviewDocket.scope_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified scope_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped scope_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No scope_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### track

Declared alternatives in owner order: `service`, `grievance`, `wrongdoing`, `retaliation`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | service | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_track | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No track at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### personnel_case_ref

Use scoped or external reference for `ReviewDocket.personnel_case_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified personnel_case_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped personnel_case_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No personnel_case_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### protection_handoff_ref

Use scoped or external reference for `ReviewDocket.protection_handoff_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified protection_handoff_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped protection_handoff_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No protection_handoff_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### owner_role

Use versioned classification or status code for `ReviewDocket.owner_role`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active owner_role code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped owner_role code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No owner_role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### owner_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | UserAccount·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing owner_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No owner_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### independent_authority_ref

Use scoped or external reference for `ReviewDocket.independent_authority_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified independent_authority_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped independent_authority_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No independent_authority_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### policy_version

Use human-readable text for `ReviewDocket.policy_version`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered policy_version in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No policy_version at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### priority

Use versioned classification or status code for `ReviewDocket.priority`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active priority code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped priority code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No priority at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reply_due_at

Use unambiguous point in time for `ReviewDocket.reply_due_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No reply_due_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### next_review_at

Use unambiguous point in time for `ReviewDocket.next_review_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No next_review_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Declared alternatives in owner order: `triage`, `scoped`, `investigating`, `awaiting_response`, `decision_due`, `decided`, `appeal`, `closed`, `reopened`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | triage | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DocketExchange](DocketExchange.md).`docket_id` | ReviewDocket identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DocketParty](DocketParty.md).`docket_id` | ReviewDocket identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReviewConflict](ReviewConflict.md).`docket_id` | ReviewDocket identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReviewDecision](ReviewDecision.md).`docket_id` | ReviewDocket identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReviewIssue](ReviewIssue.md).`docket_id` | ReviewDocket identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
