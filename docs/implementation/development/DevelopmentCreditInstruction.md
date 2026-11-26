# DevelopmentCreditInstruction

[Donor service and gift acceptance](../../development/donor-service.md) · [Department records](README.md) · [Value conventions](../value-conventions.md)

## Record invariant

Identity, audit fields, ownership and effective-date notation follow the [shared record envelope](../../foundation/record-conventions.md). A business key or parent-child uniqueness rule below remains enforceable even when an implementation also assigns an opaque identifier.

Credit is influence or acknowledgement. The giving desk controls the actual giving party and any GiftAttribution. Multiple advisers cannot increase gift value or receive an official donor receipt solely for advising.

## Field inventory

| Field | Logical declaration | Presence at the applicable step | Validation family |
| --- | --- | --- | --- |
| `source_gift_id` | ref Gift | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `credited_party_id` | ref GivingParty | Required when the record reaches its applicable state | [relation](../value-conventions.md#relation) |
| `role` | adviser/referrer/organizer/match_coordinator | Required when the record reaches its applicable state | [enum](../value-conventions.md#enum) |
| `finance_attribution_id` | ref GiftAttribution? | Optional under owner conditions | [relation](../value-conventions.md#relation) |
| `scope_code` | code | Required when the record reaches its applicable state | [vocab](../value-conventions.md#vocab) |
| `recognition_label` | text? | Optional under owner conditions | [text](../value-conventions.md#text) |
| `authorized_at` | instant? | Optional under owner conditions | [instant](../value-conventions.md#instant) |
| `superseded_by_id` | ref DevelopmentCreditInstruction? | Optional under owner conditions | [relation](../value-conventions.md#relation) |

## Input, storage and exchange cases

Each section targets one field on an otherwise admissible record. The first probe tests its declared representation, not permission to commit the transaction. The owner invariant above can reject an otherwise valid value. A change to a projection is tested at its source.

### source_gift_id

The target is [Gift](../finance/Gift.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | Gift·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | Gift·MISSING | Queue the missing Gift mapping or reject the command before linking. |
| Wrong scope | Gift·B01 | Do not attach another church’s Gift without a supported exchange and local authority. |
| Target rename | Rename Gift·A01 after linking | The existing source_gift_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No source_gift_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### credited_party_id

The target is [GivingParty](../finance/GivingParty.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GivingParty·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GivingParty·MISSING | Queue the missing GivingParty mapping or reject the command before linking. |
| Wrong scope | GivingParty·B01 | Do not attach another church’s GivingParty without a supported exchange and local authority. |
| Target rename | Rename GivingParty·A01 after linking | The existing credited_party_id keeps the same identity and historic documents retain their original wording. |
| Incomplete record | No credited_party_id at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### role

Declared alternatives in owner order: `adviser`, `referrer`, `organizer`, `match_coordinator`. Approval and lifecycle guards still apply to transitions.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | adviser | Preserve the stable code and resolve its localized label separately. |
| Malformed or unmapped | outside_role | Return a choice error or place unmapped historical input in review. |
| Translated label reused for two choices | localized display label shared by two codes | Require the underlying code. |
| Display label changes after issue | display wording changes after issue | Keep the original issued rendering and stored code. |
| Unknown historical source value | unmapped retired legacy code | Retain raw staging evidence; never silently choose the first option. |
| Incomplete record | No role at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### finance_attribution_id

The target is [GiftAttribution](../finance/GiftAttribution.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | GiftAttribution·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | GiftAttribution·MISSING | Queue the missing GiftAttribution mapping or reject the command before linking. |
| Wrong scope | GiftAttribution·B01 | Do not attach another church’s GiftAttribution without a supported exchange and local authority. |
| Target rename | Rename GiftAttribution·A01 after linking | The existing finance_attribution_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No finance_attribution_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### scope_code

Use versioned classification or status code for `DevelopmentCreditInstruction.scope_code`. Check the relevant vocabulary and permitted transition before applying.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | active scope_code code in the bound vocabulary | Check the relevant vocabulary and permitted transition before applying. |
| Malformed or unmapped | unmapped scope_code code | Request mapping to an authorized code. |
| Code retired before a new transaction | new operation after code retirement | Allow historic display; withhold new use unless policy permits. |
| Same label in two code lists | same display name in two vocabularies | Use record type and field to locate the correct list. |
| Bulk import requests a state transition | import requests the final approved state | Run ordinary transition guards and approval checks. |
| Incomplete record | No scope_code at the step where the rule requires it | Identify the missing business fact before considering the record complete. |

### recognition_label

Use human-readable text for `DevelopmentCreditInstruction.recognition_label`. Preserve the meaningful spelling, script and structure; derive separate search forms.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | entered recognition_label in the original script | Preserve the meaningful spelling, script and structure; derive separate search forms. |
| Malformed or unmapped | invalid text encoding | Return a field-level validation issue without silently changing meaning. |
| Accented and non-Latin characters | Zoë and ǂNū-khoen in the original script | Preserve and display their original spelling. |
| Label changes after formal issue | approved edition before a spelling correction | Keep the authorized original rendering in the issued edition. |
| Bidirectional or multiline input | mixed-direction or multiline entered text | Render in the field’s declared context and respect accessibility and disclosure rules. |
| Absent in intake | No recognition_label provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### authorized_at

Use unambiguous point in time for `DevelopmentCreditInstruction.authorized_at`. Compare as the same instant as 07:00:00Z on that date; retain needed display context.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | 2026-11-26T09:00:00+02:00 | Compare as the same instant as 07:00:00Z on that date; retain needed display context. |
| Malformed or unmapped | ambiguous local time in repeated hour | Request the offset, zone resolution or explicit policy decision. |
| Two observations with different offsets denoting one instant | 09:00+02:00 and 07:00Z on the same day | Temporal comparison treats them as equal; business identity still uses its own key. |
| Observation arrives after a later event | event at 09:00 reported after event at 09:05 | Retain occurrence and observation order separately. |
| Expiry coincides with current instant | observation exactly at expiry | Apply the documented validity interval at the decision point. |
| Absent in intake | No authorized_at provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

### superseded_by_id

The target is [DevelopmentCreditInstruction](DevelopmentCreditInstruction.md). Resolve the identifier in the approved scope before using its fields.

| Probe | Input or observation | Expected result |
| --- | --- | --- |
| Admissible representation | DevelopmentCreditInstruction·A01 | Resolve stable identity in the permitted scope. |
| Malformed or unmapped | existing object of a different type | Return a type mismatch without changing the link. |
| Unresolved target | DevelopmentCreditInstruction·MISSING | Queue the missing DevelopmentCreditInstruction mapping or reject the command before linking. |
| Wrong scope | DevelopmentCreditInstruction·B01 | Do not attach another church’s DevelopmentCreditInstruction without a supported exchange and local authority. |
| Target rename | Rename DevelopmentCreditInstruction·A01 after linking | The existing superseded_by_id keeps the same identity and historic documents retain their original wording. |
| Absent in intake | No superseded_by_id provided | Keep the value absent and apply any conditional requirement at the relevant lifecycle step. |

## Incoming references

| Referencing record and field | Join key | Review when identity changes |
| --- | --- | --- |
| [DevelopmentCreditInstruction](DevelopmentCreditInstruction.md).`superseded_by_id` | DevelopmentCreditInstruction identity | Inspect this reference in the source owner’s scope; preserve previous issue and correction history. |

## Acceptance evidence

Record the owner revision, evaluated values, actor and scope, result, effective time, and any downstream references needed to reproduce a disputed decision. Release only the evidence permitted to the reader. The originating domain page defines the business action and precise historical or transactional effect.
