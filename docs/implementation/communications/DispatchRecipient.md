# DispatchRecipient

[Campaigns, audiences and content](../../communications/campaigns-and-content.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

One intended person or opted household copy per dispatch/entry. Store route attempts under Delivery. Exclusions do not create attempted deliveries.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `dispatch_id` | DispatchRequest ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `entry_id` | AudienceEntry ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `endpoint_id` | DeliveryEndpoint ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `template_edition_id` | TemplateEdition ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `evaluated_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `eligibility` | eligible/excluded/delayed | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `reason` | code? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `language` | locale? | Optional under owner conditions | [language](../value-conventions.md#language) |
| `render_digest` | text? | Optional under owner conditions | [digest](../value-conventions.md#digest) |
| `representation_id` | RepresentationAuthority ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### dispatch_id

The target is [DispatchRequest](DispatchRequest.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DispatchRequest·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DispatchRequest·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DispatchRequest·MISSING | Queue the missing DispatchRequest mapping or reject the command before linking. |
| Wrong scope | DispatchRequest·B01 | Do not attach another church’s DispatchRequest without a supported exchange and local authority. |
| Target rename | Rename DispatchRequest·A01 after linking | The existing dispatch_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No dispatch_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### entry_id

The target is [AudienceEntry](AudienceEntry.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AudienceEntry·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AudienceEntry·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AudienceEntry·MISSING | Queue the missing AudienceEntry mapping or reject the command before linking. |
| Wrong scope | AudienceEntry·B01 | Do not attach another church’s AudienceEntry without a supported exchange and local authority. |
| Target rename | Rename AudienceEntry·A01 after linking | The existing entry_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No entry_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### endpoint_id

The target is [DeliveryEndpoint](DeliveryEndpoint.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DeliveryEndpoint·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | DeliveryEndpoint·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | DeliveryEndpoint·MISSING | Queue the missing DeliveryEndpoint mapping or reject the command before linking. |
| Wrong scope | DeliveryEndpoint·B01 | Do not attach another church’s DeliveryEndpoint without a supported exchange and local authority. |
| Target rename | Rename DeliveryEndpoint·A01 after linking | The existing endpoint_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No endpoint_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### template_edition_id

The target is [TemplateEdition](TemplateEdition.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | TemplateEdition·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | TemplateEdition·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | TemplateEdition·MISSING | Queue the missing TemplateEdition mapping or reject the command before linking. |
| Wrong scope | TemplateEdition·B01 | Do not attach another church’s TemplateEdition without a supported exchange and local authority. |
| Target rename | Rename TemplateEdition·A01 after linking | The existing template_edition_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No template_edition_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### evaluated_at

Use unambiguous point in time for `DispatchRecipient.evaluated_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No evaluated_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### eligibility

Declared alternatives in owner order: `eligible`, `excluded`, `delayed`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | eligible | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_eligibility | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No eligibility at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### reason

Use versioned classification or status code for `DispatchRecipient.reason`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active reason code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped reason code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No reason provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### language

Use language or locale identifier for `DispatchRecipient.language`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Absent in intake | No language provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### render_digest

Use integrity fingerprint or opaque verifier for `DispatchRecipient.render_digest`. Bind the algorithm or verifier scheme and object revision to the evidence.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | verified fingerprint of edition A | Bind the algorithm or verifier scheme and object revision to the evidence. |
| Malformed or unmapped | different fingerprint for the same purported bytes | Quarantine the mismatch or deny the claim. |
| An identical copy is rechecked | compare original bytes with verified copy | Equality confirms the checked bytes or verifier under the same scheme only. |
| New revision has changed content | different bytes under a new edition | Compute new evidence; preserve the prior verified revision. |
| A user knows a digest | unprivileged user presents a publicly observed fingerprint | Knowledge alone grants no additional access outside the documented token protocol. |
| Absent in intake | No render_digest provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### representation_id

The target is [RepresentationAuthority](../people/RepresentationAuthority.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | RepresentationAuthority·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | RepresentationAuthority·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | RepresentationAuthority·MISSING | Queue the missing RepresentationAuthority mapping or reject the command before linking. |
| Wrong scope | RepresentationAuthority·B01 | Do not attach another church’s RepresentationAuthority without a supported exchange and local authority. |
| Target rename | Rename RepresentationAuthority·A01 after linking | The existing representation_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No representation_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [Delivery](Delivery.md).`recipient_id` | DispatchRecipient identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
