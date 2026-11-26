# Campus

[Churches, congregations, campuses and governing networks](../../foundation/organization.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One campus can host many rooms or sessions. A sensitive meeting point has separate public and restricted location descriptions.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `id` | Owner-scoped business value; see the record rule | Assigned or projected by owner | [key](../value-conventions.md#key) |
| `organization_id` | → Organization | Required at applicable lifecycle step | [relation](../value-conventions.md#relation) |
| `code` | text | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `name` | text | Required at applicable lifecycle step | [text](../value-conventions.md#text) |
| `kind` | physical, online or itinerant | Required at applicable lifecycle step | [enum](../value-conventions.md#enum) |
| `location_description` | optional text | Optional under owner conditions | [text](../value-conventions.md#text) |
| `zone` | zone | Required at applicable lifecycle step | [zone](../value-conventions.md#zone) |
| `public_contact` | optional contact | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `accessibility_summary` | optional text | Optional under owner conditions | [text](../value-conventions.md#text) |
| `active_from` | dates | Required at applicable lifecycle step | [date](../value-conventions.md#date) |
| `active_until` | dates | Required at applicable lifecycle step | [date](../value-conventions.md#date) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### id

Use opaque identity or token for `Campus.id`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Campus·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
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
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Organization·MISSING | Queue the missing Organization mapping or reject the command before linking. |
| Wrong scope | Organization·B01 | Do not attach another church’s Organization without a supported exchange and local authority. |
| Target rename | Rename Organization·A01 after linking | The existing organization_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No organization_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### code

Use human-readable text for `Campus.code`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered code in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### name

Use human-readable text for `Campus.name`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered name in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No name at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### kind

Declared alternatives in owner order: `physical`, `online`, `itinerant`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | physical | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_kind | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No kind at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### location_description

Use human-readable text for `Campus.location_description`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered location_description in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No location_description provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### zone

Use time zone with civil-time rules for `Campus.zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Incomplete record | No zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### public_contact

Use scoped or external reference for `Campus.public_contact`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified public_contact in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped public_contact | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No public_contact provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### accessibility_summary

Use human-readable text for `Campus.accessibility_summary`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered accessibility_summary in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No accessibility_summary provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### active_from

Use civil calendar date for `Campus.active_from`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No active_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### active_until

Use civil calendar date for `Campus.active_until`. Keep the date without converting it into a time or shifting it across zones.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2024-02-29 | Keep the date without converting it into a time or shifting it across zones. |
| Malformed or unmapped | 2025-02-29 | Reject the impossible civil date. |
| 2026-04-31 | 31 April 2026 | Reject instead of advancing into May. |
| Midnight in a different time zone | 23:30 on previous UTC day at a separate site | A civil date remains the entered date. |
| Date lies on an effective-period boundary | effective date equals the stated interval endpoint | Apply the owning record’s explicit endpoint convention. |
| Incomplete record | No active_until at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [Campaign](../communications/Campaign.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CollectionBatch](../finance/CollectionBatch.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CongregationCampus](CongregationCampus.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CongregationParticipation](../people/CongregationParticipation.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContinuityPlan](../assurance/ContinuityPlan.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [CourseOffering](../ministry/CourseOffering.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [EventOccurrence](../ministry/EventOccurrence.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [FacilitySpace](../ministry/FacilitySpace.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [GoverningBody](../governance/GoverningBody.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [IncidentReport](../assurance/IncidentReport.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LoanCopy](../administration/LoanCopy.md).`home_campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LoanReservation](../administration/LoanReservation.md).`pickup_campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryCalendar](../ministry/MinistryCalendar.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryGroup](../ministry/MinistryGroup.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MinistryVehicle](../ministry/MinistryVehicle.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [OperationsIncident](../ministry/OperationsIncident.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Product](../commerce/Product.md).`owner_campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReadinessPlan](../ministry/ReadinessPlan.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [RiskEntry](../assurance/RiskEntry.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [SermonDelivery](../commerce/SermonDelivery.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ShopChannel](../commerce/ShopChannel.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StaffPosition](../administration/StaffPosition.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [StockLocation](../commerce/StockLocation.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VisitorEncounter](../people/VisitorEncounter.md).`campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [VolunteerProfile](../ministry/VolunteerProfile.md).`preferred_campus_id` | Campus identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
