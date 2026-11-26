# AssemblyPaperRequest

[Annual assemblies, policies and review](../../governance/annual-cycle-and-policy.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique cycle/code. Holds the assembly's request and pack status. Pin the certified return or approved document; the reporting domain owns figures, external filing and attestation.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `cycle_id` | GovernanceCycle ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `owner_term_id` | OfficeTerm ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `due_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `paper_class` | financial/membership/ministry/charter/other | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `certified_return_id` | ReturnInstance ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `supplied_version_ref` | text? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `disclosure_class` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `packet_state` | requested/received/approved_for_packet/circulated | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `meeting_attachment_id` | GovernanceAttachment ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### cycle_id

The target is [GovernanceCycle](GovernanceCycle.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernanceCycle·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GovernanceCycle·MISSING | Queue the missing GovernanceCycle mapping or reject the command before linking. |
| Wrong scope | GovernanceCycle·B01 | Do not attach another church’s GovernanceCycle without a supported exchange and local authority. |
| Target rename | Rename GovernanceCycle·A01 after linking | The existing cycle_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No cycle_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### code

Use human-readable text for `AssemblyPaperRequest.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `AssemblyPaperRequest.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### owner_term_id

The target is [OfficeTerm](OfficeTerm.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | OfficeTerm·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | OfficeTerm·MISSING | Queue the missing OfficeTerm mapping or reject the command before linking. |
| Wrong scope | OfficeTerm·B01 | Do not attach another church’s OfficeTerm without a supported exchange and local authority. |
| Target rename | Rename OfficeTerm·A01 after linking | The existing owner_term_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No owner_term_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### due_at

Use unambiguous point in time for `AssemblyPaperRequest.due_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No due_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### paper_class

Declared alternatives in owner order: `financial`, `membership`, `ministry`, `charter`, `other`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | financial | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_paper_class | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No paper_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### certified_return_id

The target is [ReturnInstance](../administration/ReturnInstance.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ReturnInstance·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | ReturnInstance·MISSING | Queue the missing ReturnInstance mapping or reject the command before linking. |
| Wrong scope | ReturnInstance·B01 | Do not attach another church’s ReturnInstance without a supported exchange and local authority. |
| Target rename | Rename ReturnInstance·A01 after linking | The existing certified_return_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No certified_return_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### supplied_version_ref

Use scoped or external reference for `AssemblyPaperRequest.supplied_version_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified supplied_version_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped supplied_version_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No supplied_version_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### disclosure_class

Use versioned classification or status code for `AssemblyPaperRequest.disclosure_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active disclosure_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped disclosure_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No disclosure_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### packet_state

Declared alternatives in owner order: `requested`, `received`, `approved_for_packet`, `circulated`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | requested | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_packet_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No packet_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### meeting_attachment_id

The target is [GovernanceAttachment](GovernanceAttachment.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernanceAttachment·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GovernanceAttachment·MISSING | Queue the missing GovernanceAttachment mapping or reject the command before linking. |
| Wrong scope | GovernanceAttachment·B01 | Do not attach another church’s GovernanceAttachment without a supported exchange and local authority. |
| Target rename | Rename GovernanceAttachment·A01 after linking | The existing meeting_attachment_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No meeting_attachment_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
