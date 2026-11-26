# Congregation

[Churches, congregations, campuses and governing networks](../../foundation/organization.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Code unique per organization. Closing ends current assignments through reviewed workflows and retains historic rolls.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `organization_id` | → Organization | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `code` | text | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `display_name` | text | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `language` | optional tag | Optional under owner conditions | [structured](../value-conventions.md#structured) |
| `started_on` | date | Required at applicable lifecycle step | [date](../value-conventions.md#date) |
| `ended_on` | optional date | Optional under owner conditions | [date](../value-conventions.md#date) |
| `status` | forming, active, merged or closed | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `Congregation.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Congregation·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

### organization_id

The target is [Organization](Organization.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Organization·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Organization·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### code

Use human-readable text for `Congregation.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### display_name

Use human-readable text for `Congregation.display_name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered display_name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No display_name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### language

Use typed value or bounded compound record for `Congregation.language`. Validate allowed keys, element types and cardinality; preserve its definition revision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | value of language matching its owner definition | Validate allowed keys, element types and cardinality; preserve its definition revision. |
| Malformed or unmapped | incompatible shape for language | Return a version or shape error. |
| One mandatory child missing | one mandatory child absent | Identify the child to an authorized operator before committing effects. |
| Unknown imported extension | a new unrecognized child from historic import | Isolate for mapping; do not discard data silently. |
| Historic re-render | display selection made under a retired form edition | Use the original definition and approved vocabulary. |
| Absent in intake | No language provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### started_on

Use civil calendar date for `Congregation.started_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No started_on at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ended_on

Use civil calendar date for `Congregation.ended_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No ended_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### status

Declared alternatives in owner order: `forming`, `active`, `merged`, `closed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | forming | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_status | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No status at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AidProgram](../people/AidProgram.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [BulletinEdition](../communications/BulletinEdition.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Campaign](../communications/Campaign.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareCase](../people/CareCase.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareRequest](../people/CareRequest.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CeremonyRequest](../administration/CeremonyRequest.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CongregationCampus](CongregationCampus.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CongregationParticipation](../people/CongregationParticipation.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactTree](../communications/ContactTree.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DirectoryEdition](../people/DirectoryEdition.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FollowUpEnrollment](../people/FollowUpEnrollment.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FundraisingAppeal](../development/FundraisingAppeal.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GoverningBody](../governance/GoverningBody.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Membership](../people/Membership.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipApplication](../people/MembershipApplication.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipDecision](../people/MembershipDecision.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipPolicy](../people/MembershipPolicy.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipTransfer](../people/MembershipTransfer.md).`destination_congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipTransfer](../people/MembershipTransfer.md).`source_congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryCalendar](../ministry/MinistryCalendar.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryGroup](../ministry/MinistryGroup.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MissionProject](../ministry/MissionProject.md).`sponsoring_congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OutreachInterest](../people/OutreachInterest.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonMilestone](../people/PersonMilestone.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectionCase](../people/ProtectionCase.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RegisterBook](../people/RegisterBook.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskEntry](../assurance/RiskEntry.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiteRecord](../people/RiteRecord.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RollSnapshot](../people/RollSnapshot.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Sermon](../commerce/Sermon.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VisitorEncounter](../people/VisitorEncounter.md).`congregation_id` | Congregation identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
