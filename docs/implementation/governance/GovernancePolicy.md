# GovernancePolicy

[Annual assemblies, policies and review](../../governance/annual-cycle-and-policy.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique body/code. Ordinary operating policies complement the body-specific procedural rule edition. Ownership transfer leaves prior editions intact.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `body_id` | GoverningBody ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `owner_term_id` | OfficeTerm ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `category` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `audience_scope` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `review_frequency` | duration? | Optional under owner conditions | [duration](../value-conventions.md#duration) |
| `state` | proposed/in_force/retired | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

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

### code

Use human-readable text for `GovernancePolicy.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `GovernancePolicy.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

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
| Malformed or unmapped | OfficeTerm·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | OfficeTerm·MISSING | Queue the missing OfficeTerm mapping or reject the command before linking. |
| Wrong scope | OfficeTerm·B01 | Do not attach another church’s OfficeTerm without a supported exchange and local authority. |
| Target rename | Rename OfficeTerm·A01 after linking | The existing owner_term_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No owner_term_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### category

Use versioned classification or status code for `GovernancePolicy.category`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active category code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped category code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No category at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### audience_scope

Use versioned classification or status code for `GovernancePolicy.audience_scope`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active audience_scope code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped audience_scope code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No audience_scope at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### review_frequency

Use elapsed interval or named calendar duration for `GovernancePolicy.review_frequency`. Preserve unit and distinguish elapsed minutes from a calendar day or working day.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 30 minutes in elapsed-time profile | Preserve unit and distinguish elapsed minutes from a calendar day or working day. |
| Malformed or unmapped | duration without resolvable unit | Request an interval unit. |
| A working-day deadline crosses a closure | a one-workday deadline starting on Friday | Use the named work-calendar edition. |
| A civil day crosses an offset change | a local civil day covers 23 or 25 elapsed hours | Do not assume 24 elapsed hours. |
| Zero-length interval | duration of zero units | Apply the owner’s validity or immediate-trigger rule. |
| Absent in intake | No review_frequency provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `proposed`, `in_force`, `retired`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | proposed | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [GovernancePolicyEdition](GovernancePolicyEdition.md).`policy_id` | GovernancePolicy identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
