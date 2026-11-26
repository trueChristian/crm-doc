# AdmissionSeat

[Registration, tickets and attendance](../../ministry/registration.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Optional allocated seating. One active allocation per seat and occurrence. Reserve accessible stock according to stated policy and protect accessibility requests.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `option_id` | → AdmissionOption | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `seat_label` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `zone_label` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `accessible_features` | code_set? | Optional under owner conditions | [list](../value-conventions.md#list) |
| `place_id` | → RegistrationPlace? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### option_id

The target is [AdmissionOption](AdmissionOption.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AdmissionOption·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AdmissionOption·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AdmissionOption·MISSING | Queue the missing AdmissionOption mapping or reject the command before linking. |
| Wrong scope | AdmissionOption·B01 | Do not attach another church’s AdmissionOption without a supported exchange and local authority. |
| Target rename | Rename AdmissionOption·A01 after linking | The existing option_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No option_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### seat_label

Use human-readable text for `AdmissionSeat.seat_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered seat_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No seat_label at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### zone_label

Use human-readable text for `AdmissionSeat.zone_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered zone_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No zone_label provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### accessible_features

Use ordered collection or mathematical set for `AdmissionSeat.accessible_features`. Preserve ordering when meaningful; enforce uniqueness when the declaration is a set.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted members A and B | Preserve ordering when meaningful; enforce uniqueness when the declaration is a set. |
| Malformed or unmapped | an element outside the declared domain | Reject the affected collection or stage its invalid item under the import policy. |
| Same element appears twice | A, A, B | Apply declared sequence/set multiplicity without doubling financial or voting effects. |
| Empty collection versus unknown collection | empty collection and missing collection | Preserve the distinction where the rule requires evidence. |
| One element later becomes restricted | authorization for member B withdrawn before export | Recompute permitted projection before export or display. |
| Absent in intake | No accessible_features provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### place_id

The target is [RegistrationPlace](RegistrationPlace.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RegistrationPlace·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RegistrationPlace·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RegistrationPlace·MISSING | Queue the missing RegistrationPlace mapping or reject the command before linking. |
| Wrong scope | RegistrationPlace·B01 | Do not attach another church’s RegistrationPlace without a supported exchange and local authority. |
| Target rename | Rename RegistrationPlace·A01 after linking | The existing place_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No place_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
