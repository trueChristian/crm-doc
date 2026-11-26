# GovernanceReview

[Annual assemblies, policies and review](../../governance/annual-cycle-and-policy.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Preserve intake, jurisdiction, time limit, independent review and permitted disclosure. A review may suspend execution when the governing policy allows. Sensitive safeguarding intake routes directly to its restricted domain.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `body_id` | GoverningBody ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `subject_type` | eligibility/election/office/decision/policy | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `subject_ref` | opaque | Required when the record reaches its applicable state | [resource](../value-conventions.md#resource) |
| `appellant_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `lodged_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `grounds` | restricted text | Required when the record reaches its applicable state | [protected](../value-conventions.md#protected) |
| `reviewer_term_id` | OfficeTerm ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `recusal_reviewed` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `deadline_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `outcome` | pending/upheld/varied/rejected/referred/withdrawn | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `ruling_text` | restricted text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `effective_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `released_extract_id` | OfficialExtract ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### body_id

The target is [GoverningBody](GoverningBody.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GoverningBody·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GoverningBody·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GoverningBody·MISSING | Queue the missing GoverningBody mapping or reject the command before linking. |
| Wrong scope | GoverningBody·B01 | Do not attach another church’s GoverningBody without a supported exchange and local authority. |
| Target rename | Rename GoverningBody·A01 after linking | The existing body_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No body_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### subject_type

Declared alternatives in owner order: `eligibility`, `election`, `office`, `decision`, `policy`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | eligibility | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_subject_type | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No subject_type at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### subject_ref

Use scoped or external reference for `GovernanceReview.subject_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified subject_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped subject_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Incomplete record | No subject_ref at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### appellant_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing appellant_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No appellant_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### lodged_at

Use unambiguous point in time for `GovernanceReview.lodged_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No lodged_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### grounds

Use restricted value or protected content reference for `GovernanceReview.grounds`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted grounds supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Incomplete record | No grounds at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reviewer_term_id

The target is [OfficeTerm](OfficeTerm.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OfficeTerm·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OfficeTerm·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OfficeTerm·MISSING | Queue the missing OfficeTerm mapping or reject the command before linking. |
| Wrong scope | OfficeTerm·B01 | Do not attach another church’s OfficeTerm without a supported exchange and local authority. |
| Target rename | Rename OfficeTerm·A01 after linking | The existing reviewer_term_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No reviewer_term_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### recusal_reviewed

Use explicit logical choice for `GovernanceReview.recusal_reviewed`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No recusal_reviewed at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### deadline_at

Use unambiguous point in time for `GovernanceReview.deadline_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No deadline_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### outcome

Declared alternatives in owner order: `pending`, `upheld`, `varied`, `rejected`, `referred`, `withdrawn`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | pending | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_outcome | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No outcome at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ruling_text

Use restricted value or protected content reference for `GovernanceReview.ruling_text`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted ruling_text supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No ruling_text provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### effective_at

Use unambiguous point in time for `GovernanceReview.effective_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No effective_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### released_extract_id

The target is [OfficialExtract](OfficialExtract.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OfficialExtract·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | OfficialExtract·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OfficialExtract·MISSING | Queue the missing OfficialExtract mapping or reject the command before linking. |
| Wrong scope | OfficialExtract·B01 | Do not attach another church’s OfficialExtract without a supported exchange and local authority. |
| Target rename | Rename OfficialExtract·A01 after linking | The existing released_extract_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No released_extract_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
