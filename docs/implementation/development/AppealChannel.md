# AppealChannel

[Appeals and attribution](../../development/appeals.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Each named channel has at least one traceable invitation, event, offer or approved offline source. Many messages can serve one appeal. Source codes do not identify a donor publicly.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `appeal_id` | ref FundraisingAppeal | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `communication_campaign_id` | ref Campaign? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `event_id` | ref EventOccurrence? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `shop_offer_id` | ref Offer? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `source_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `attribution_window_days` | integer | Required when the record reaches its applicable state | [integer](../value-conventions.md#integer) |
| `begins_at` | instant | Required when the record reaches its applicable state | [instant](../value-conventions.md#instant) |
| `ends_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `audience_ref` | ref AudienceSnapshot? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### appeal_id

The target is [FundraisingAppeal](FundraisingAppeal.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | FundraisingAppeal·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | FundraisingAppeal·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | FundraisingAppeal·MISSING | Queue the missing FundraisingAppeal mapping or reject the command before linking. |
| Wrong scope | FundraisingAppeal·B01 | Do not attach another church’s FundraisingAppeal without a supported exchange and local authority. |
| Target rename | Rename FundraisingAppeal·A01 after linking | The existing appeal_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No appeal_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### communication_campaign_id

The target is [Campaign](../communications/Campaign.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Campaign·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Campaign·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Campaign·MISSING | Queue the missing Campaign mapping or reject the command before linking. |
| Wrong scope | Campaign·B01 | Do not attach another church’s Campaign without a supported exchange and local authority. |
| Target rename | Rename Campaign·A01 after linking | The existing communication_campaign_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No communication_campaign_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### event_id

The target is [EventOccurrence](../ministry/EventOccurrence.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | EventOccurrence·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | EventOccurrence·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | EventOccurrence·MISSING | Queue the missing EventOccurrence mapping or reject the command before linking. |
| Wrong scope | EventOccurrence·B01 | Do not attach another church’s EventOccurrence without a supported exchange and local authority. |
| Target rename | Rename EventOccurrence·A01 after linking | The existing event_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No event_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### shop_offer_id

The target is [Offer](../commerce/Offer.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Offer·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | Offer·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | Offer·MISSING | Queue the missing Offer mapping or reject the command before linking. |
| Wrong scope | Offer·B01 | Do not attach another church’s Offer without a supported exchange and local authority. |
| Target rename | Rename Offer·A01 after linking | The existing shop_offer_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No shop_offer_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### source_code

Use versioned classification or status code for `AppealChannel.source_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active source_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped source_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No source_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### attribution_window_days

Use whole-number measure for `AppealChannel.attribution_window_days`. Preserve integer precision and enforce the specific field bounds.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2 subject to field bounds | Preserve integer precision and enforce the specific field bounds. |
| Malformed or unmapped | 2.5 | Reject fractional input without rounding it into a whole person, place or sequence. |
| Value equals the configured upper bound | value exactly equal to the applicable maximum | Apply its inclusive or exclusive rule explicitly. |
| Value exceeds the bound by one | applicable maximum plus one | Return a range error before changing dependent totals. |
| Missing count versus measured zero | observed 0 and omitted value | Keep absence distinct from an observed zero. |
| Incomplete record | No attribution_window_days at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### begins_at

Use unambiguous point in time for `AppealChannel.begins_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Incomplete record | No begins_at at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### ends_at

Use unambiguous point in time for `AppealChannel.ends_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No ends_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### audience_ref

The target is [AudienceSnapshot](../communications/AudienceSnapshot.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | AudienceSnapshot·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | AudienceSnapshot·MISSING | Return a type mismatch without changing the link. |
| Unresolved target | AudienceSnapshot·MISSING | Queue the missing AudienceSnapshot mapping or reject the command before linking. |
| Wrong scope | AudienceSnapshot·B01 | Do not attach another church’s AudienceSnapshot without a supported exchange and local authority. |
| Target rename | Rename AudienceSnapshot·A01 after linking | The existing audience_ref keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No audience_ref provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [AppealAllocationCredit](AppealAllocationCredit.md).`appeal_channel_id` | AppealChannel identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |
| [AppealResponse](AppealResponse.md).`channel_id` | AppealChannel identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
