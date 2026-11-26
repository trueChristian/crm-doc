# DeliveryEndpoint

[Recipients and channel policy](../../communications/recipients-and-channels.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Require an entitled recipient or explicit representative. A print destination may pin a verified correspondence address. Push and inbox can be account-linked. Shared endpoints can be used by multiple people. Never infer identity by comparing addresses.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `organization_id` | Organization ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `person_id` | Person ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `person_contact_point_id` | PersonContactPoint ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `household_address_id` | HouseholdAddress ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `owner_account_id` | UserAccount ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `channel` | email/sms/telegram_dm/push/inbox/print/voice | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `protected_destination` | text | Required when the record reaches its applicable state | [text](../value-conventions.md#text) |
| `comparison_key` | opaque | Required when the record reaches its applicable state | [key](../value-conventions.md#key) |
| `locale` | locale? | Optional under owner conditions | [language](../value-conventions.md#language) |
| `zone` | zone? | Optional under owner conditions | [zone](../value-conventions.md#zone) |
| `shared` | boolean | Required when the record reaches its applicable state | [bool](../value-conventions.md#bool) |
| `verification_state` | pending/verified/expired/revoked | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `verified_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `retired_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |

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

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### person_contact_point_id

The target is [PersonContactPoint](../people/PersonContactPoint.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | PersonContactPoint·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | PersonContactPoint·MISSING | Queue the missing PersonContactPoint mapping or reject the command before linking. |
| Wrong scope | PersonContactPoint·B01 | Do not attach another church’s PersonContactPoint without a supported exchange and local authority. |
| Target rename | Rename PersonContactPoint·A01 after linking | The existing person_contact_point_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No person_contact_point_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### household_address_id

The target is [HouseholdAddress](../people/HouseholdAddress.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | HouseholdAddress·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | HouseholdAddress·MISSING | Queue the missing HouseholdAddress mapping or reject the command before linking. |
| Wrong scope | HouseholdAddress·B01 | Do not attach another church’s HouseholdAddress without a supported exchange and local authority. |
| Target rename | Rename HouseholdAddress·A01 after linking | The existing household_address_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No household_address_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### owner_account_id

The target is [UserAccount](../platform/UserAccount.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | UserAccount·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | UserAccount·MISSING | Queue the missing UserAccount mapping or reject the command before linking. |
| Wrong scope | UserAccount·B01 | Do not attach another church’s UserAccount without a supported exchange and local authority. |
| Target rename | Rename UserAccount·A01 after linking | The existing owner_account_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No owner_account_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### channel

Declared alternatives in owner order: `email`, `sms`, `telegram_dm`, `push`, `inbox`, `print`, `voice`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | email | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_channel | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No channel at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### protected_destination

Use human-readable text for `DeliveryEndpoint.protected_destination`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered protected_destination in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Incomplete record | No protected_destination at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### comparison_key

Use opaque identity or token for `DeliveryEndpoint.comparison_key`. Compare the opaque value under its issuer rules; preserve leading characters.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DeliveryEndpoint·0007 | Compare the opaque value under its issuer rules; preserve leading characters. |
| Malformed or unmapped | human-readable name passed as the identifier | Request a verified lookup or an explicit mapping. |
| Renamed display label | update display label; retain stable key | Identity comparisons still use the stable key. |
| Conflicting claim on an existing key | second owner claims the same issued key | Retain original binding; route conflict for review. |
| Retried creation with the original operation key | submit original creation receipt twice | Use the owning creation outcome and return the established identity. |
| Incomplete record | No comparison_key at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### locale

Use language or locale identifier for `DeliveryEndpoint.locale`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Absent in intake | No locale provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### zone

Use time zone with civil-time rules for `DeliveryEndpoint.zone`. Preserve zone identity; use the applicable local rules for the date.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Africa/Windhoek | Preserve zone identity; use the applicable local rules for the date. |
| Malformed or unmapped | ambiguous zone abbreviation | Require a named zone or explicitly supported fixed offset. |
| Future recurring appointment | fixed local Sunday service across offset change | Recompute local-time occurrences using its stored zone and change policy. |
| Staff view from a second zone | remote attendee opens the schedule abroad | Show the requested local display without moving the actual instant. |
| Zone changes for a campus | campus adopts a new effective zone | Re-evaluate future occurrences and retain historical issue evidence. |
| Absent in intake | No zone provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### shared

Use explicit logical choice for `DeliveryEndpoint.shared`. Preserve the supplied value; do not promote an unanswered choice to consent.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | true | Preserve the supplied value; do not promote an unanswered choice to consent. |
| Malformed or unmapped | unmapped input “perhaps” | Map only declared true/false representations. |
| False versus blank | false and absent | Retain the distinction if absence is allowed. |
| Historic default changes | historical edition had false as its default | Issued records keep the value used at decision time. |
| User has no authority to set the flag | valid true submitted outside authorized role | Reject the attempted change even when the value is well formed. |
| Incomplete record | No shared at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### verification_state

Declared alternatives in owner order: `pending`, `verified`, `expired`, `revoked`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | pending | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_verification_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No verification_state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### verified_at

Use unambiguous point in time for `DeliveryEndpoint.verified_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No verified_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### retired_at

Use unambiguous point in time for `DeliveryEndpoint.retired_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No retired_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [CallAssignment](CallAssignment.md).`endpoint_id` | DeliveryEndpoint identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ChannelBindingChallenge](ChannelBindingChallenge.md).`endpoint_id` | DeliveryEndpoint identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactDecision](ContactDecision.md).`endpoint_id` | DeliveryEndpoint identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactRestriction](ContactRestriction.md).`endpoint_id` | DeliveryEndpoint identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ContactSubscription](ContactSubscription.md).`endpoint_id` | DeliveryEndpoint identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [Delivery](Delivery.md).`endpoint_id` | DeliveryEndpoint identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [DispatchRecipient](DispatchRecipient.md).`endpoint_id` | DeliveryEndpoint identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [ReplyThread](ReplyThread.md).`endpoint_id` | DeliveryEndpoint identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
