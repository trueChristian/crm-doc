# MinistryGroup

[Groups and participation](../../ministry/groups.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique short code per organization. Public, members-only, listed-by-invitation and confidential visibility govern discovery. A confidential group's existence and member counts are protected. A household's private address requires explicit release before appearing as a meeting place.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `kind_id` | → GroupKind | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `congregation_id` | → Congregation? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `campus_id` | → Campus? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `name` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `short_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `purpose` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `language` | code? | Optional under owner conditions | [language](../value-conventions.md#language) |
| `visibility` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `join_policy` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `status` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `opened_on` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `closed_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `capacity` | count? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `public_contact_person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### kind_id

The target is [GroupKind](GroupKind.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GroupKind·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | GroupKind·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | GroupKind·MISSING | Queue the missing GroupKind mapping or reject the command before linking. |
| Wrong scope | GroupKind·B01 | Do not attach another church’s GroupKind without a supported exchange and local authority. |
| Target rename | Rename GroupKind·A01 after linking | The existing kind_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No kind_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### congregation_id

The target is [Congregation](../foundation/Congregation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Congregation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Congregation·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Congregation·MISSING | Queue the missing Congregation mapping or reject the command before linking. |
| Wrong scope | Congregation·B01 | Do not attach another church’s Congregation without a supported exchange and local authority. |
| Target rename | Rename Congregation·A01 after linking | The existing congregation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No congregation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### campus_id

The target is [Campus](../foundation/Campus.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Campus·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Campus·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Campus·MISSING | Queue the missing Campus mapping or reject the command before linking. |
| Wrong scope | Campus·B01 | Do not attach another church’s Campus without a supported exchange and local authority. |
| Target rename | Rename Campus·A01 after linking | The existing campus_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No campus_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### name

Use human-readable text for `MinistryGroup.name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### short_code

Use versioned classification or status code for `MinistryGroup.short_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active short_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped short_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No short_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose

Use human-readable text for `MinistryGroup.purpose`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered purpose in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### language

Use language or locale identifier for `MinistryGroup.language`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Absent in intake | No language provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### visibility

Use versioned classification or status code for `MinistryGroup.visibility`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active visibility code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped visibility code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No visibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### join_policy

Use versioned classification or status code for `MinistryGroup.join_policy`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active join_policy code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped join_policy code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No join_policy at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### status

Use versioned classification or status code for `MinistryGroup.status`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active status code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped status code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### opened_on

Use civil calendar date for `MinistryGroup.opened_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No opened_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### closed_on

Use civil calendar date for `MinistryGroup.closed_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No closed_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### capacity

Use whole-number measure for `MinistryGroup.capacity`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No capacity provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### public_contact_person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing public_contact_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No public_contact_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccountabilityCheck](AccountabilityCheck.md).`group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceRecord](AttendanceRecord.md).`group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Curriculum](Curriculum.md).`owner_group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EventRegistration](EventRegistration.md).`group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EventSeries](EventSeries.md).`host_group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FormationPath](FormationPath.md).`owner_group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GoverningBody](../governance/GoverningBody.md).`roster_group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupLink](GroupLink.md).`child_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupLink](GroupLink.md).`parent_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupRole](GroupRole.md).`group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupTerm](GroupTerm.md).`group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryCalendar](MinistryCalendar.md).`owner_group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryProgramme](MinistryProgramme.md).`owner_group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MissionProject](MissionProject.md).`owner_group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RehearsalCall](RehearsalCall.md).`team_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServicePosition](ServicePosition.md).`group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupervisedSession](SupervisedSession.md).`group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [WorshipTemplate](WorshipTemplate.md).`group_id` | MinistryGroup identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
