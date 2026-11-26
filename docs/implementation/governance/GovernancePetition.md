# GovernancePetition

[Annual assemblies, policies and review](../../governance/annual-cycle-and-policy.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Apply the charter's eligibility and minimum-support policy. Limit signatory exposure. Provide a human intake route when online signing is unavailable.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `body_id` | GoverningBody ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `request_kind` | special_meeting/agenda_item/review | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `submitted_text` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `requested_action` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `principal_person_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `opened_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `cutoff_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `threshold_rule` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `verification_state` | lodged/validating/accepted/declined/withdrawn | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `ruling_reason` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `resulting_item_id` | AgendaItem ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

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

### request_kind

Declared alternatives in owner order: `special_meeting`, `agenda_item`, `review`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | special_meeting | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_request_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No request_kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `GovernancePetition.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### submitted_text

Use human-readable text for `GovernancePetition.submitted_text`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered submitted_text in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No submitted_text at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_action

Use human-readable text for `GovernancePetition.requested_action`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered requested_action in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No requested_action at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### principal_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing principal_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No principal_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### opened_at

Use unambiguous point in time for `GovernancePetition.opened_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No opened_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### cutoff_at

Use unambiguous point in time for `GovernancePetition.cutoff_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No cutoff_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### threshold_rule

Use human-readable text for `GovernancePetition.threshold_rule`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered threshold_rule in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No threshold_rule provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### verification_state

Declared alternatives in owner order: `lodged`, `validating`, `accepted`, `declined`, `withdrawn`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | lodged | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_verification_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No verification_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ruling_reason

Use human-readable text for `GovernancePetition.ruling_reason`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered ruling_reason in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No ruling_reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### resulting_item_id

The target is [AgendaItem](AgendaItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AgendaItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AgendaItem·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AgendaItem·MISSING | Queue the missing AgendaItem mapping or reject the command before linking. |
| Wrong scope | AgendaItem·B01 | Do not attach another church’s AgendaItem without a supported exchange and local authority. |
| Target rename | Rename AgendaItem·A01 after linking | The existing resulting_item_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No resulting_item_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [PetitionEndorsement](PetitionEndorsement.md).`petition_id` | GovernancePetition identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
