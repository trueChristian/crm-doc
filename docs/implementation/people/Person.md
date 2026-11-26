# Person

[Personal register and identity resolution](../../people/personal-register.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One durable identity per person within the organization's data boundary. Display name may be a single name. Only merged records point to a live canonical record. Archiving ends routine discovery. Death is distinct from archival and from ending membership.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | ID | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `organization_id` | → Organization | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `display_name` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `sort_name` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `birth_date` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `birth_year` | year? | Optional under owner conditions | [year](../value-conventions.md#year) |
| `birth_month` | integer? | Optional under owner conditions | [month](../value-conventions.md#month) |
| `birth_day` | integer? | Optional under owner conditions | [day](../value-conventions.md#day) |
| `birth_precision` | enum(exact, year, month_year, month_day, unknown) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `birth_estimated` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `deceased_on` | date? | Optional under owner conditions | [date](../value-conventions.md#date) |
| `deceased_on_precision` | enum(day, year, unknown)? | Optional under owner conditions | [enum](../value-conventions.md#enum) |
| `deceased_year` | year? | Optional under owner conditions | [year](../value-conventions.md#year) |
| `life_state` | enum(living, deceased, unknown) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `language_tag` | text? | Optional under owner conditions | [language](../value-conventions.md#language) |
| `time_zone` | text? | Optional under owner conditions | [zone](../value-conventions.md#zone) |
| `accessibility_contact_instructions` | private text? | Optional under owner conditions | [protected](../value-conventions.md#protected) |
| `record_state` | enum(active, merged, archived) | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `canonical_person_id` | → Person? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `revision` | integer | Required when the record reaches its applicable state | [version](../value-conventions.md#version) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `Person.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Independent overwrite | Attempt to replace id through an ordinary field edit | Use the identity or projection owner; reject an independent reassignment. |

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

### display_name

Use human-readable text for `Person.display_name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered display_name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No display_name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### sort_name

Use human-readable text for `Person.sort_name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered sort_name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No sort_name provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### birth_date

Use civil calendar date for `Person.birth_date`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No birth_date provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### birth_year

Use civil year for `Person.birth_year`. Preserve year precision separately from month/day.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024 | Preserve year precision separately from month/day. |
| Malformed or unmapped | 2024.5 | Reject a fractional calendar year. |
| Date reported only as a year | 2024 with no month or day | Do not store 1 January as the actual day. |
| Date used to determine age eligibility | possible ages either side of the eligibility cutoff | Return a range or request verification if the answer depends on the day. |
| Cross-year comparison | interval spanning the civil new year | Compare known intervals and disclose uncertainty. |
| Absent in intake | No birth_year provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### birth_month

Use civil month number for `Person.birth_month`. Accept month 1 through 12 and keep any unknown year separate.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 | Accept month 1 through 12 and keep any unknown year separate. |
| Malformed or unmapped | 13 | Reject out-of-range month. |
| 1 and 12 | January and December | Both are possible calendar months. |
| 0 or a fractional month | 0 and 1.5 | Reject. |
| Known month, unknown year | April, year unknown | Do not manufacture a date of birth. |
| Absent in intake | No birth_month provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### birth_day

Use day of the month for `Person.birth_day`. Validate against the known month and year, respecting precision.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 29 in February 2024 | Validate against the known month and year, respecting precision. |
| Malformed or unmapped | 31 in April | Reject impossible day. |
| 29 February, year unknown | 29 February without an exact year | Preserve a possible month/day without claiming a particular year. |
| 31 April | 31 April | Reject as an impossible date. |
| Month unknown | day observed, month withheld | Preserve declared precision; no invented January. |
| Absent in intake | No birth_day provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### birth_precision

Declared alternatives in owner order: `exact`, `year`, `month_year`, `month_day`, `unknown`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | exact | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_birth_precision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No birth_precision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### birth_estimated

Use explicit logical choice for `Person.birth_estimated`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No birth_estimated at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### deceased_on

Use civil calendar date for `Person.deceased_on`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Absent in intake | No deceased_on provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### deceased_on_precision

Declared alternatives in owner order: `day`, `year`, `unknown`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | day | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_deceased_on_precision | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Absent in intake | No deceased_on_precision provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### deceased_year

Use civil year for `Person.deceased_year`. Preserve year precision separately from month/day.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024 | Preserve year precision separately from month/day. |
| Malformed or unmapped | 2024.5 | Reject a fractional calendar year. |
| Date reported only as a year | 2024 with no month or day | Do not store 1 January as the actual day. |
| Date used to determine age eligibility | possible ages either side of the eligibility cutoff | Return a range or request verification if the answer depends on the day. |
| Cross-year comparison | interval spanning the civil new year | Compare known intervals and disclose uncertainty. |
| Absent in intake | No deceased_year provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### life_state

Declared alternatives in owner order: `living`, `deceased`, `unknown`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | living | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_life_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No life_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### language_tag

Use language or locale identifier for `Person.language_tag`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Absent in intake | No language_tag provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### time_zone

Use time zone with civil-time rules for `Person.time_zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Absent in intake | No time_zone provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### accessibility_contact_instructions

Use restricted value or protected content reference for `Person.accessibility_contact_instructions`. Keep value and purpose together; apply field-level authority to projections.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | permitted accessibility_contact_instructions supplied in a restricted context | Keep value and purpose together; apply field-level authority to projections. |
| Malformed or unmapped | public disclosure without authority | Withhold publication unless the specific disclosure rule permits it. |
| Search snippet or autocomplete | restricted fact returned in type-ahead search | Filter before returning any protected content or revealing its existence. |
| Authorized report excludes this field | otherwise permitted export excludes the restricted field | Omit it from hidden metadata and attachments as well. |
| Approval withdrawn after a preview | draft was previewed before authority was withdrawn | Recheck at release; keep only permitted audit evidence. |
| Absent in intake | No accessibility_contact_instructions provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### record_state

Declared alternatives in owner order: `active`, `merged`, `archived`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_record_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No record_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### canonical_person_id

The target is [Person](Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing canonical_person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No canonical_person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### revision

Use revision number or opaque revision token for `Person.revision`. Compare under the declared revision scheme. Require the expected version for conflicting work.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | the current revision returned by the owner | Compare under the declared revision scheme. Require the expected version for conflicting work. |
| Malformed or unmapped | superseded version presented for a new approval | Reject or reopen review against the current contents. |
| Two operators begin at revision seven | two edits both cite baseline 7 | Commit the first change once and re-evaluate the second; never overwrite an unreviewed difference. |
| Re-read an already approved revision | re-open issued revision 4 after revision 6 | Return the frozen value and evidence for that edition. |
| Replay of an earlier result | same business operation observed at two revisions | Correlate by the business operation identity; a newer version does not create a second effect. |
| Incomplete record | No revision at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AccessGrant](../commerce/AccessGrant.md).`beneficiary_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccessItemIssue](../ministry/AccessItemIssue.md).`recipient_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountInvitation](../platform/AccountInvitation.md).`intended_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountabilityCheck](../ministry/AccountabilityCheck.md).`responsible_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AccountabilityEntry](../assurance/AccountabilityEntry.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AgendaItem](../governance/AgendaItem.md).`presenter_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AgendaItem](../governance/AgendaItem.md).`requested_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AgreementParty](../development/AgreementParty.md).`assigned_contact_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AidApplication](AidApplication.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ArchiveDisposition](../governance/ArchiveDisposition.md).`approved_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssemblyCredential](../governance/AssemblyCredential.md).`certified_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssemblyCredential](../governance/AssemblyCredential.md).`delegate_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssistanceIssue](../ministry/AssistanceIssue.md).`recipient_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AssistedService](../platform/AssistedService.md).`subject_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceRecord](../ministry/AttendanceRecord.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceResponse](../governance/AttendanceResponse.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AttendanceResponse](../governance/AttendanceResponse.md).`substitute_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AudienceEntry](../communications/AudienceEntry.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AuditEvent](../platform/AuditEvent.md).`represented_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AvailabilityWindow](../ministry/AvailabilityWindow.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CallAssignment](../communications/CallAssignment.md).`backup_caller_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CallAssignment](../communications/CallAssignment.md).`caller_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CallAssignment](../communications/CallAssignment.md).`intended_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareDisclosure](CareDisclosure.md).`subject_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareParticipant](CareParticipant.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareRequest](CareRequest.md).`requester_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CareRequest](CareRequest.md).`subject_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CeremonyParty](../administration/CeremonyParty.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CeremonyRequest](../administration/CeremonyRequest.md).`coordinator_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CertificateIssue](CertificateIssue.md).`recipient_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChannelBindingChallenge](../communications/ChannelBindingChallenge.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CharterEdition](../governance/CharterEdition.md).`approving_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChildCheckIn](../ministry/ChildCheckIn.md).`child_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChildCheckIn](../ministry/ChildCheckIn.md).`dropped_by_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CollectionAttempt](../ministry/CollectionAttempt.md).`claimant_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CommunityDistribution](../ministry/CommunityDistribution.md).`steward_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ConcernSubmission](../assurance/ConcernSubmission.md).`reporter_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CongregationParticipation](CongregationParticipation.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ConsentDecision](../platform/ConsentDecision.md).`subject_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactDecision](../communications/ContactDecision.md).`actor_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactDecision](../communications/ContactDecision.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactRestriction](../communications/ContactRestriction.md).`authorized_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactRestriction](../communications/ContactRestriction.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactSubscription](../communications/ContactSubscription.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactWindow](../communications/ContactWindow.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CourseOffering](../ministry/CourseOffering.md).`instructor_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CourseSession](../ministry/CourseSession.md).`teacher_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CredentialRecord](../administration/CredentialRecord.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DecisionRuling](../governance/DecisionRuling.md).`deciding_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DeliveryEndpoint](../communications/DeliveryEndpoint.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DigestEdition](../communications/DigestEdition.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DirectoryDisclosure](DirectoryDisclosure.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DocketParty](../assurance/DocketParty.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DuplicateReview](DuplicateReview.md).`candidate_a_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DuplicateReview](DuplicateReview.md).`candidate_b_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DutyShift](../ministry/DutyShift.md).`lead_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EmploymentEngagement](../administration/EmploymentEngagement.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EquipmentHandoff](../ministry/EquipmentHandoff.md).`giver_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EquipmentHandoff](../ministry/EquipmentHandoff.md).`receiver_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EquipmentReservation](../ministry/EquipmentReservation.md).`custodian_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EventRegistration](../ministry/EventRegistration.md).`booked_by_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EventSeries](../ministry/EventSeries.md).`organizer_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FacilitySpace](../ministry/FacilitySpace.md).`steward_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FamilyContactAttempt](../assurance/FamilyContactAttempt.md).`authorized_contact_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FamilyContactAttempt](../assurance/FamilyContactAttempt.md).`subject_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FollowUpEnrollment](FollowUpEnrollment.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GivingParty](../finance/GivingParty.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceMeeting](../governance/GovernanceMeeting.md).`chair_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceMeeting](../governance/GovernanceMeeting.md).`secretary_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernancePetition](../governance/GovernancePetition.md).`principal_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GovernanceReview](../governance/GovernanceReview.md).`appellant_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupInvitation](../ministry/GroupInvitation.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GroupParticipation](../ministry/GroupParticipation.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [HospitalityAllocation](../ministry/HospitalityAllocation.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [HospitalityOffer](../ministry/HospitalityOffer.md).`steward_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [HouseholdPerson](HouseholdPerson.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IdentityReview](../platform/IdentityReview.md).`requested_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentParty](../assurance/IncidentParty.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentReport](../assurance/IncidentReport.md).`reporter_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InterestDeclaration](../governance/InterestDeclaration.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [InterestDeclaration](../governance/InterestDeclaration.md).`verified_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IntermentRecord](../administration/IntermentRecord.md).`deceased_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ItemRecusal](../governance/ItemRecusal.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ItemRecusal](../governance/ItemRecusal.md).`presiding_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LearningAward](../ministry/LearningAward.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LearningEnrolment](../ministry/LearningEnrolment.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaContributor](../commerce/MediaContributor.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MeetingNotice](../governance/MeetingNotice.md).`issue_authority_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MeetingRoll](../governance/MeetingRoll.md).`certified_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MeetingSessionEvent](../governance/MeetingSessionEvent.md).`actor_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Membership](Membership.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipApplication](MembershipApplication.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipDecision](MembershipDecision.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MembershipTransfer](MembershipTransfer.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryGroup](../ministry/MinistryGroup.md).`public_contact_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryPartner](../ministry/MinistryPartner.md).`contact_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryProgramme](../ministry/MinistryProgramme.md).`lead_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteAttestation](../governance/MinuteAttestation.md).`attestor_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteBook](../governance/MinuteBook.md).`custodian_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinuteEdition](../governance/MinuteEdition.md).`prepared_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MissionProject](../ministry/MissionProject.md).`lead_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MissionTrip](../ministry/MissionTrip.md).`lead_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Motion](../governance/Motion.md).`seconder_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Motion](../governance/Motion.md).`sponsor_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [NamedVote](../governance/NamedVote.md).`recorded_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Nomination](../governance/Nomination.md).`candidate_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Nomination](../governance/Nomination.md).`proposer_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Nomination](../governance/Nomination.md).`seconder_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Nomination](../governance/Nomination.md).`verified_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [NoticeService](../governance/NoticeService.md).`reviewed_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OfficeTerm](../governance/OfficeTerm.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OfficialExtract](../governance/OfficialExtract.md).`issued_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationalAction](../ministry/OperationalAction.md).`owner_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationalBriefing](../ministry/OperationalBriefing.md).`duty_lead_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationalReview](../ministry/OperationalReview.md).`reviewer_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationsIncident](../ministry/OperationsIncident.md).`controller_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Order](../commerce/Order.md).`buyer_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OutreachInterest](OutreachInterest.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OutreachReferral](OutreachReferral.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PassengerBooking](../ministry/PassengerBooking.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PathParticipation](../ministry/PathParticipation.md).`adviser_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PathParticipation](../ministry/PathParticipation.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PayrollEngagement](../finance/PayrollEngagement.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Person](Person.md).`canonical_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonContactPoint](PersonContactPoint.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonIdentifier](PersonIdentifier.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonMergeItem](PersonMergeItem.md).`prior_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonMergeItem](PersonMergeItem.md).`resulting_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonMilestone](PersonMilestone.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonName](PersonName.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonRelationship](PersonRelationship.md).`from_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonRelationship](PersonRelationship.md).`to_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonalGoal](PersonalGoal.md).`mentor_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PersonalGoal](PersonalGoal.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PetitionEndorsement](../governance/PetitionEndorsement.md).`signer_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PolicyAcknowledgement](../governance/PolicyAcknowledgement.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PresenceInterval](../governance/PresenceInterval.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PresenceInterval](../governance/PresenceInterval.md).`recorded_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [PrintBatch](../communications/PrintBatch.md).`received_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProfileChangeRequest](ProfileChangeRequest.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProfileLink](ProfileLink.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProgrammeSelection](../ministry/ProgrammeSelection.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProjectMilestone](../ministry/ProjectMilestone.md).`owner_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectionParty](ProtectionParty.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProtectiveMeasure](ProtectiveMeasure.md).`subject_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ProxyMandate](../governance/ProxyMandate.md).`verified_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [QuorumCheck](../governance/QuorumCheck.md).`certified_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReadinessCheck](../ministry/ReadinessCheck.md).`owner_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReadinessPlan](../ministry/ReadinessPlan.md).`owner_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RecruitmentCase](../administration/RecruitmentCase.md).`candidate_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RegistrationPlace](../ministry/RegistrationPlace.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReminderAcknowledgement](../communications/ReminderAcknowledgement.md).`responding_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReminderInstance](../communications/ReminderInstance.md).`subject_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReplyThread](../communications/ReplyThread.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RepresentationAuthority](RepresentationAuthority.md).`representative_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RepresentationAuthority](RepresentationAuthority.md).`subject_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RepresentationGrant](../platform/RepresentationGrant.md).`actor_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RepresentationGrant](../platform/RepresentationGrant.md).`subject_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResolutionAction](../governance/ResolutionAction.md).`owner_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResolutionAction](../governance/ResolutionAction.md).`reviewed_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResourceWorkOrder](../ministry/ResourceWorkOrder.md).`assigned_to` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResultCount](../governance/ResultCount.md).`certified_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ResultCount](../governance/ResultCount.md).`witnessed_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReunificationDecision](../assurance/ReunificationDecision.md).`requesting_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReviewConflict](../assurance/ReviewConflict.md).`candidate_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiteParticipant](RiteParticipant.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RollEntry](RollEntry.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RoomBooking](../ministry/RoomBooking.md).`requester_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServicePlan](../ministry/ServicePlan.md).`planner_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ServicePlanItem](../ministry/ServicePlanItem.md).`lead_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SharingRequest](../communications/SharingRequest.md).`subject_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SharingRequest](../communications/SharingRequest.md).`submitted_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ShiftExchange](../ministry/ShiftExchange.md).`candidate_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ShiftExchange](../ministry/ShiftExchange.md).`requester_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StaffAbsence](../administration/StaffAbsence.md).`cover_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SubjectRequest](../platform/SubjectRequest.md).`representative_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SubjectRequest](../platform/SubjectRequest.md).`subject_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SupervisedSession](../ministry/SupervisedSession.md).`duty_lead_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TransportJourney](../ministry/TransportJourney.md).`driver_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TripLeg](../ministry/TripLeg.md).`lead_person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [TripParticipant](../ministry/TripParticipant.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [UserAccount](../platform/UserAccount.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VisitorEncounter](VisitorEncounter.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerApplication](../ministry/VolunteerApplication.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerAssignment](../ministry/VolunteerAssignment.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerCredential](../ministry/VolunteerCredential.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerProfile](../ministry/VolunteerProfile.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerSkill](../ministry/VolunteerSkill.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VotingRollEntry](../governance/VotingRollEntry.md).`changed_by` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VotingRollEntry](../governance/VotingRollEntry.md).`person_id` | Person identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
