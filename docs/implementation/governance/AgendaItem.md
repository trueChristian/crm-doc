# AgendaItem

[Deliberation and voting](../../governance/deliberation-and-voting.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique code within meeting. Parent belongs to same meeting. Reordering cannot change the identity of a motion, notice or signed record. Restricted items have their own packet.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `meeting_id` | GovernanceMeeting ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `parent_item_id` | AgendaItem ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `sequence` | decimal | Required when the record reaches its applicable state | [decimal](../value-conventions.md#decimal) |
| `item_code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `title` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `description` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `kind` | information/discussion/motion/election | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `requested_by` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `presenter_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `allocated_minutes` | integer? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `access_class` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `state` | proposed/admitted/deferred/withdrawn/completed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### meeting_id

The target is [GovernanceMeeting](GovernanceMeeting.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GovernanceMeeting·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GovernanceMeeting·MISSING | Queue the missing GovernanceMeeting mapping or reject the command before linking. |
| Wrong scope | GovernanceMeeting·B01 | Do not attach another church’s GovernanceMeeting without a supported exchange and local authority. |
| Target rename | Rename GovernanceMeeting·A01 after linking | The existing meeting_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No meeting_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### parent_item_id

The target is [AgendaItem](AgendaItem.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AgendaItem·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | AgendaItem·MISSING | Queue the missing AgendaItem mapping or reject the command before linking. |
| Wrong scope | AgendaItem·B01 | Do not attach another church’s AgendaItem without a supported exchange and local authority. |
| Target rename | Rename AgendaItem·A01 after linking | The existing parent_item_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_item_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### sequence

Use exact decimal measure for `AgendaItem.sequence`. Retain decimal magnitude, unit and precision required by the record.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2.50 in the field unit | Retain decimal magnitude, unit and precision required by the record. |
| Malformed or unmapped | sum across incompatible units | Obtain a unit or verified conversion before aggregating. |
| 0.1 plus 0.2 with the same unit | 0.1 + 0.2 in identical units | Obtain 0.3 exactly before presentation rounding. |
| Negative adjustment | a linked negative adjustment | Require the owner’s allowed sign and adjustment reason. |
| Unit change after recording | two cases of twelve units versus two individual units | Use an effective conversion; preserve earlier observations. |
| Incomplete record | No sequence at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### item_code

Use human-readable text for `AgendaItem.item_code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered item_code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No item_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### title

Use human-readable text for `AgendaItem.title`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered title in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No title at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### description

Use human-readable text for `AgendaItem.description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No description at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `information`, `discussion`, `motion`, `election`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | information | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### requested_by

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing requested_by keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No requested_by provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### presenter_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing presenter_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No presenter_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### allocated_minutes

Use whole-number measure for `AgendaItem.allocated_minutes`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No allocated_minutes provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### access_class

Use versioned classification or status code for `AgendaItem.access_class`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active access_class code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped access_class code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No access_class at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### state

Declared alternatives in owner order: `proposed`, `admitted`, `deferred`, `withdrawn`, `completed`. Approval and lifecycle guards still apply to transitions.

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
| [AgendaItem](AgendaItem.md).`parent_item_id` | AgendaItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ElectionContest](ElectionContest.md).`item_id` | AgendaItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceAttachment](GovernanceAttachment.md).`agenda_item_id` | AgendaItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernancePetition](GovernancePetition.md).`resulting_item_id` | AgendaItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ItemRecusal](ItemRecusal.md).`item_id` | AgendaItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteItem](MinuteItem.md).`agenda_item_id` | AgendaItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Motion](Motion.md).`item_id` | AgendaItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProxyMandate](ProxyMandate.md).`agenda_item_id` | AgendaItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [QuorumCheck](QuorumCheck.md).`item_id` | AgendaItem identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
