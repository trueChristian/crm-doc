# ContactSubscription

[Recipients and channel policy](../../communications/recipients-and-channels.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Use only an owned or validly represented endpoint. At most one effective decision per person/purpose/channel/endpoint scope. Blank channel applies to all channels for that purpose.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `person_id` | Person ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `purpose_id` | CommunicationPurpose ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `endpoint_id` | DeliveryEndpoint ref? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `channel` | enum? | Optional under owner conditions | [vocab](../value-conventions.md#vocab) |
| `state` | allowed/declined/undecided | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `preference_rank` | positive integer? | Optional under owner conditions | [integer](../value-conventions.md#integer) |
| `locale` | locale? | Optional under owner conditions | [language](../value-conventions.md#language) |
| `applies_from` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `expires_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `decision_id` | ContactDecision ref | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### person_id

The target is [Person](../people/Person.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Person·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Person·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Person·MISSING | Queue the missing Person mapping or reject the command before linking. |
| Wrong scope | Person·B01 | Do not attach another church’s Person without a supported exchange and local authority. |
| Target rename | Rename Person·A01 after linking | The existing person_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No person_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### purpose_id

The target is [CommunicationPurpose](CommunicationPurpose.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | CommunicationPurpose·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | CommunicationPurpose·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | CommunicationPurpose·MISSING | Queue the missing CommunicationPurpose mapping or reject the command before linking. |
| Wrong scope | CommunicationPurpose·B01 | Do not attach another church’s CommunicationPurpose without a supported exchange and local authority. |
| Target rename | Rename CommunicationPurpose·A01 after linking | The existing purpose_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No purpose_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

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

### channel

Use versioned classification or status code for `ContactSubscription.channel`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active channel code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped channel code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Absent in intake | No channel provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### state

Declared alternatives in owner order: `allowed`, `declined`, `undecided`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | allowed | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_state | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No state at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### preference_rank

Use whole-number measure for `ContactSubscription.preference_rank`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Absent in intake | No preference_rank provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### locale

Use language or locale identifier for `ContactSubscription.locale`. Resolve the published language or locale without inferring a person’s nationality.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | en | Resolve the published language or locale without inferring a person’s nationality. |
| Malformed or unmapped | unmapped locale display label | Keep the source value for review. |
| Specific translation unavailable | specific translation missing at delivery time | Apply the declared fallback and identify which language is being displayed. |
| User changes preferred language | approved letter after preferred-language change | Future communications use the effective preference; issued wording is preserved. |
| Two regional variants exist | two permitted regional variants in catalogue | Apply the requested locale/version where available. |
| Absent in intake | No locale provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### applies_from

Use unambiguous point in time for `ContactSubscription.applies_from`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No applies_from at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### expires_at

Use unambiguous point in time for `ContactSubscription.expires_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No expires_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### decision_id

The target is [ContactDecision](ContactDecision.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | ContactDecision·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | ContactDecision·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | ContactDecision·MISSING | Queue the missing ContactDecision mapping or reject the command before linking. |
| Wrong scope | ContactDecision·B01 | Do not attach another church’s ContactDecision without a supported exchange and local authority. |
| Target rename | Rename ContactDecision·A01 after linking | The existing decision_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No decision_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
