# SermonDelivery

[Sermon library and publication](../../commerce/media.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One work can have multiple deliveries. Keep public venue labels separate from restricted location details.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `sermon_id` | ref Sermon | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `service_ref` | opaque_ref? | Optional under owner conditions | [resource](../value-conventions.md#resource) |
| `campus_id` | ref Campus? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `venue_label` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `spoken_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `local_zone` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `language` | code | Required when the record reaches its applicable state | [language](../value-conventions.md#language) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### sermon_id

The target is [Sermon](Sermon.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Sermon·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Sermon·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Sermon·MISSING | Queue the missing Sermon mapping or reject the command before linking. |
| Wrong scope | Sermon·B01 | Do not attach another church’s Sermon without a supported exchange and local authority. |
| Target rename | Rename Sermon·A01 after linking | The existing sermon_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No sermon_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### service_ref

Use scoped or external reference for `SermonDelivery.service_ref`. Resolve against the permitted kind, owning namespace and purpose.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified service_ref in the owner namespace | Resolve against the permitted kind, owning namespace and purpose. |
| Malformed or unmapped | unmapped service_ref | Request clarification or quarantine the mapping. |
| Same visible code from two sources | issuer A:007 and issuer B:007 | Retain distinct namespace/key pairs. |
| Referenced evidence is restricted | restricted attachment behind an otherwise visible request | Show a minimal permitted result and check document access independently. |
| Duplicate delivery of the same mapped reference | same namespace, key and accepted mapping twice | Resolve the same destination record once. |
| Absent in intake | No service_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

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

### venue_label

Use human-readable text for `SermonDelivery.venue_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered venue_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No venue_label provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### spoken_at

Use unambiguous point in time for `SermonDelivery.spoken_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No spoken_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### local_zone

Use human-readable text for `SermonDelivery.local_zone`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered local_zone in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No local_zone at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### language

Use language or locale identifier for `SermonDelivery.language`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Incomplete record | No language at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DeliveryCredit](DeliveryCredit.md).`delivery_id` | SermonDelivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [LiveSession](LiveSession.md).`delivery_id` | SermonDelivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaEdition](MediaEdition.md).`delivery_id` | SermonDelivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [MediaRights](MediaRights.md).`delivery_id` | SermonDelivery identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
