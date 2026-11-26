# GoverningBody

[Governing bodies, office terms and delegated authority](../../governance/bodies-and-terms.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Unique organization/code. Parents form an acyclic hierarchy. The dates of a child body's mandate must fit the authority recorded in its charter. Group links offer nominees for review.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `organization_id` | Organization ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `congregation_id` | Congregation ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `campus_id` | Campus ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `parent_body_id` | GoverningBody ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `roster_group_id` | MinistryGroup ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `code` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `name` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `purpose` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `authority_summary` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `time_zone` | zone | Required when the record reaches its applicable state | [zone](../value-conventions.md#zone) |
| `active_from` | date | Required when the record reaches its applicable state | [date](../value-conventions.md#date) |
| `retired_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### organization_id

The target is [Organization](../foundation/Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### congregation_id

The target is [Congregation](../foundation/Congregation.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Congregation·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Congregation·MISSING | Queue the missing Congregation mapping or reject the command before linking. |
| Wrong scope | Congregation·B01 | Do not attach another church’s Congregation without a supported exchange and local authority. |
| Target rename | Rename Congregation·A01 after linking | The existing congregation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No congregation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### campus_id

The target is [Campus](../foundation/Campus.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Campus·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Campus·MISSING | Queue the missing Campus mapping or reject the command before linking. |
| Wrong scope | Campus·B01 | Do not attach another church’s Campus without a supported exchange and local authority. |
| Target rename | Rename Campus·A01 after linking | The existing campus_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No campus_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### parent_body_id

The target is [GoverningBody](GoverningBody.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GoverningBody·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GoverningBody·MISSING | Queue the missing GoverningBody mapping or reject the command before linking. |
| Wrong scope | GoverningBody·B01 | Do not attach another church’s GoverningBody without a supported exchange and local authority. |
| Target rename | Rename GoverningBody·A01 after linking | The existing parent_body_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No parent_body_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### roster_group_id

The target is [MinistryGroup](../ministry/MinistryGroup.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | MinistryGroup·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | MinistryGroup·MISSING | Queue the missing MinistryGroup mapping or reject the command before linking. |
| Wrong scope | MinistryGroup·B01 | Do not attach another church’s MinistryGroup without a supported exchange and local authority. |
| Target rename | Rename MinistryGroup·A01 after linking | The existing roster_group_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No roster_group_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### code

Use human-readable text for `GoverningBody.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### name

Use human-readable text for `GoverningBody.name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose

Use human-readable text for `GoverningBody.purpose`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered purpose in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No purpose at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### authority_summary

Use human-readable text for `GoverningBody.authority_summary`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered authority_summary in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No authority_summary at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### time_zone

Use time zone with civil-time rules for `GoverningBody.time_zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Incomplete record | No time_zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### active_from

Use civil calendar date for `GoverningBody.active_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No active_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### retired_on

Use civil calendar date for `GoverningBody.retired_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No retired_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AssemblyCredential](AssemblyCredential.md).`sending_body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AuthorityDelegation](AuthorityDelegation.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CharterEdition](CharterEdition.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceCycle](GovernanceCycle.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceMeeting](GovernanceMeeting.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernancePetition](GovernancePetition.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernancePolicy](GovernancePolicy.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceReview](GovernanceReview.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GoverningBody](GoverningBody.md).`parent_body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InterestDeclaration](InterestDeclaration.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteBook](MinuteBook.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Office](Office.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Resolution](Resolution.md).`body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResolutionAction](ResolutionAction.md).`owner_body_id` | GoverningBody identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
